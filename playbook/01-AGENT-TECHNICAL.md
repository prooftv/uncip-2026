# AGENT 1: TECHNICAL STABILISATION
## Mission: Make UNCIP demo-ready on Supabase in 2 weeks

---

## AGENT IDENTITY
- **Role:** Full-stack technical lead
- **Objective:** Migrate from Firebase to Supabase, fix all critical bugs, prepare 3 working demo flows
- **Success Criteria:** A minister can watch a live demo without anything breaking

---

## PHASE 1: SUPABASE MIGRATION (Days 1-5)

### Why Supabase over Firebase
| Factor | Firebase | Supabase |
|---|---|---|
| Free tier | Spark plan (limited) | Generous free tier, 500MB DB, 1GB storage |
| Auth | Firebase Auth | Built-in auth with RLS (Row Level Security) |
| Database | Firestore (NoSQL) | PostgreSQL (relational — better for government data) |
| Real-time | Firestore listeners | Built-in real-time subscriptions |
| Storage | Firebase Storage | S3-compatible storage |
| Self-hosting | Not possible | Can self-host (government data sovereignty requirement) |
| SA data residency | Google Cloud (no SA region) | Can deploy to any region / self-host in SA |
| Cost at scale | Unpredictable billing | Predictable pricing |

### Database Schema (PostgreSQL)

```sql
-- Enable RLS on all tables
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
ALTER TABLE children ENABLE ROW LEVEL SECURITY;
ALTER TABLE alerts ENABLE ROW LEVEL SECURITY;

-- USERS
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT UNIQUE NOT NULL,
  display_name TEXT NOT NULL,
  photo_url TEXT,
  role TEXT NOT NULL CHECK (role IN ('parent', 'school', 'authority', 'community', 'admin')),
  phone_number TEXT,
  address TEXT,
  province TEXT,
  organization_id UUID REFERENCES organizations(id),
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- ORGANIZATIONS (schools, SAPS stations, NGOs)
CREATE TABLE organizations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  type TEXT NOT NULL CHECK (type IN ('school', 'saps_station', 'ngo', 'dsd_office', 'municipality')),
  province TEXT NOT NULL,
  district TEXT,
  address TEXT,
  contact_phone TEXT,
  contact_email TEXT,
  emis_number TEXT,  -- Education Management Information System number for schools
  station_code TEXT, -- SAPS station code
  created_at TIMESTAMPTZ DEFAULT now()
);

-- CHILDREN
CREATE TABLE children (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  first_name TEXT NOT NULL,
  last_name TEXT NOT NULL,
  date_of_birth DATE NOT NULL,
  gender TEXT CHECK (gender IN ('male', 'female', 'other')),
  id_number TEXT,  -- SA ID number (13 digits) or birth certificate number
  photo_url TEXT,
  school_id UUID REFERENCES organizations(id),
  grade TEXT,
  province TEXT,
  address_street TEXT,
  address_city TEXT,
  address_province TEXT,
  address_postal_code TEXT,
  blood_type TEXT,
  allergies TEXT[],
  medical_conditions TEXT[],
  emergency_contact_name TEXT,
  emergency_contact_phone TEXT,
  emergency_contact_relationship TEXT,
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- GUARDIANS (many-to-many: parents ↔ children)
CREATE TABLE guardians (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  child_id UUID REFERENCES children(id) ON DELETE CASCADE,
  relationship TEXT NOT NULL CHECK (relationship IN ('mother', 'father', 'guardian', 'grandparent', 'other')),
  is_primary BOOLEAN DEFAULT false,
  created_at TIMESTAMPTZ DEFAULT now(),
  UNIQUE(user_id, child_id)
);

-- ALERTS
CREATE TABLE alerts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  child_id UUID REFERENCES children(id) NOT NULL,
  alert_type TEXT NOT NULL CHECK (alert_type IN ('missing', 'endangered', 'medical', 'abduction', 'runaway')),
  status TEXT NOT NULL DEFAULT 'active' CHECK (status IN ('active', 'resolved', 'cancelled', 'false_alarm')),
  description TEXT NOT NULL,
  last_seen_location TEXT,
  last_seen_date TIMESTAMPTZ,
  last_seen_wearing TEXT,
  contact_phone TEXT NOT NULL,
  saps_case_number TEXT,  -- SAPS case reference
  saps_station_id UUID REFERENCES organizations(id),
  created_by UUID REFERENCES users(id),
  resolved_by UUID REFERENCES users(id),
  resolved_at TIMESTAMPTZ,
  resolution_notes TEXT,
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- ALERT UPDATES (timeline of actions taken)
CREATE TABLE alert_updates (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  alert_id UUID REFERENCES alerts(id) ON DELETE CASCADE,
  user_id UUID REFERENCES users(id),
  update_type TEXT NOT NULL CHECK (update_type IN ('sighting', 'status_change', 'info_added', 'assigned', 'note')),
  content TEXT NOT NULL,
  location TEXT,
  created_at TIMESTAMPTZ DEFAULT now()
);

-- AUDIT LOG
CREATE TABLE audit_log (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id),
  action TEXT NOT NULL,
  resource_type TEXT NOT NULL,
  resource_id UUID,
  details JSONB,
  ip_address INET,
  created_at TIMESTAMPTZ DEFAULT now()
);

-- NOTIFICATIONS
CREATE TABLE notifications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  alert_id UUID REFERENCES alerts(id),
  title TEXT NOT NULL,
  message TEXT NOT NULL,
  type TEXT NOT NULL CHECK (type IN ('alert', 'update', 'system', 'reminder')),
  is_read BOOLEAN DEFAULT false,
  created_at TIMESTAMPTZ DEFAULT now()
);
```

### Row Level Security Policies

```sql
-- Users: everyone can read, only self or admin can update
CREATE POLICY "Users are viewable by authenticated users"
  ON users FOR SELECT USING (auth.role() = 'authenticated');

CREATE POLICY "Users can update own profile"
  ON users FOR UPDATE USING (auth.uid() = id);

CREATE POLICY "Admins can manage all users"
  ON users FOR ALL USING (
    EXISTS (SELECT 1 FROM users WHERE id = auth.uid() AND role = 'admin')
  );

-- Children: parents see own, schools see enrolled, admin/authority see all
CREATE POLICY "Parents see own children"
  ON children FOR SELECT USING (
    EXISTS (SELECT 1 FROM guardians WHERE user_id = auth.uid() AND child_id = children.id)
  );

CREATE POLICY "Schools see enrolled children"
  ON children FOR SELECT USING (
    EXISTS (
      SELECT 1 FROM users u
      WHERE u.id = auth.uid()
      AND u.role = 'school'
      AND u.organization_id = children.school_id
    )
  );

CREATE POLICY "Admin and authority see all children"
  ON children FOR SELECT USING (
    EXISTS (SELECT 1 FROM users WHERE id = auth.uid() AND role IN ('admin', 'authority'))
  );

-- Alerts: all authenticated users can read active alerts
CREATE POLICY "Authenticated users can read alerts"
  ON alerts FOR SELECT USING (auth.role() = 'authenticated');

CREATE POLICY "Parents and admin can create alerts"
  ON alerts FOR INSERT WITH CHECK (
    EXISTS (SELECT 1 FROM users WHERE id = auth.uid() AND role IN ('parent', 'admin', 'authority'))
  );
```

### Migration Tasks

```
Task 1.1: Set up Supabase project
  - Create project on supabase.com
  - Run schema SQL above
  - Configure RLS policies
  - Set up storage buckets (child-photos, profile-photos, alert-attachments)

Task 1.2: Replace Firebase client SDK
  - Install @supabase/supabase-js
  - Create src/lib/supabase/client.ts (browser client)
  - Create src/lib/supabase/server.ts (server client for API routes)
  - Remove firebase and firebase-admin from package.json

Task 1.3: Replace authentication
  - Replace NextAuth credentials provider with Supabase Auth
  - Keep NextAuth as session wrapper OR replace entirely with Supabase Auth helpers
  - Migrate useAuth hook to use Supabase auth
  - Update middleware.ts to use Supabase session

Task 1.4: Replace API routes
  - Consolidate /api/admin-sdk/* and /api/* into single /api/* layer
  - Remove all /api/debug/* routes
  - Each route uses Supabase server client
  - Remove duplicate Firebase Admin SDK initializations

Task 1.5: Replace hooks
  - Consolidate useChildren + useChildProfiles + useAdminSdk into single useChildren
  - Replace useFirestore with useSupabase (or use Supabase client directly)
  - Update useNotifications to use Supabase real-time
  - Update useStorage to use Supabase Storage

Task 1.6: Seed demo data
  - 3 parent accounts (with SA names)
  - 2 school accounts (real township school names)
  - 1 authority account (SAPS station)
  - 1 admin account
  - 6 child profiles
  - 2 active alerts (for demo)
```

---

## PHASE 2: SECURITY FIXES (Days 3-5, parallel)

```
Task 2.1: Remove all hardcoded credentials
  - Remove admin password from auth.ts and README
  - Remove demo123 backdoor
  - Remove isRegistration bypass

Task 2.2: Remove debug endpoints
  - Delete entire /api/debug/ directory
  - Update components that depend on debug APIs to use production APIs

Task 2.3: Fix authentication
  - Use Supabase Auth (bcrypt password hashing built-in)
  - Remove plaintext password storage
  - Implement proper password reset flow with email

Task 2.4: Add missing dependency
  - Add zod to package.json OR remove the import

Task 2.5: Environment security
  - Create proper .env.local template
  - Ensure no secrets in client-side code
  - Remove console.log of private key info
```

---

## PHASE 3: DEMO PREPARATION (Days 6-10)

### Demo Flow 1: Parent Reports Missing Child
```
Pages needed:
  /dashboard/parent → shows children list
  /dashboard/parent/children → child profiles with photos
  /dashboard/parent/report → missing child form (MissingChildForm component)
  /dashboard/parent/alerts → shows created alert with status

Tasks:
  3.1: Ensure ChildProfileForm works end-to-end with Supabase
  3.2: Ensure MissingChildForm creates alert in Supabase
  3.3: Add SA-specific fields (province selector, SAPS station selector)
  3.4: Add photo display on alert (child's registered photo)
```

### Demo Flow 2: School Confirms Last Seen
```
Pages needed:
  /dashboard/school → shows incoming alert notification
  /dashboard/school/alerts → alert detail with "Add Information" button
  /dashboard/school/students → shows enrolled children

Tasks:
  3.5: Build real school alerts page (replace placeholder)
  3.6: Add "Confirm Last Seen" action on alert
  3.7: Show alert timeline (parent reported → school confirmed → authority notified)
```

### Demo Flow 3: Authority Responds
```
Pages needed:
  /dashboard/authority → shows active alerts with map context
  /dashboard/authority/alerts → alert management with status updates
  /dashboard/authority/cases → case file view

Tasks:
  3.8: Build real authority alerts page (replace placeholder)
  3.9: Add "Assign Case Number" action
  3.10: Add alert timeline view showing all stakeholder actions
  3.11: Add resolution flow (mark as found/resolved)
```

### Demo Data (SA Context)
```
Task 3.12: Seed realistic demo data

Parents:
  - Nomsa Dlamini (Khayelitsha, Western Cape)
  - Sipho Mthembu (Soweto, Gauteng)
  - Zanele Nkosi (Umlazi, KwaZulu-Natal)

Schools:
  - Masiphumelele Primary School (Khayelitsha)
  - Soweto Combined School (Soweto)

Authority:
  - Khayelitsha SAPS Community Service Centre

Children:
  - Thandi Dlamini (9, Grade 4, Masiphumelele Primary)
  - Bongani Dlamini (6, Grade 1, Masiphumelele Primary)
  - Lerato Mthembu (11, Grade 6, Soweto Combined)
  - Siyanda Mthembu (8, Grade 3, Soweto Combined)
  - Ayanda Nkosi (10, Grade 5, Umlazi Primary)
  - Nhlanhla Nkosi (7, Grade 2, Umlazi Primary)

Active Alerts:
  - Thandi Dlamini: Missing since 14:30, last seen at school gate
  - Lerato Mthembu: Medical emergency, not at school today
```

---

## PHASE 4: POLISH (Days 11-14)

```
Task 4.1: PWA setup
  - Update manifest.json with UNCIP branding
  - Add service worker for offline capability
  - Add "Add to Home Screen" prompt

Task 4.2: Government branding context
  - Add SA coat of arms context (as "in partnership with" framing)
  - Use government colour palette (green, gold, black, white)
  - Add "Prototype — Not an official government system" disclaimer

Task 4.3: Mobile optimisation
  - Test all 3 demo flows on mobile
  - Ensure touch targets are 44px minimum
  - Test on slow 3G connection

Task 4.4: Loading states
  - Add skeleton screens for all dashboard pages
  - Add optimistic updates for alert creation
  - Add offline indicator

Task 4.5: Error handling
  - Add user-friendly error messages
  - Add retry logic for failed API calls
  - Add fallback UI for network errors
```

---

## TECHNICAL ARCHITECTURE (Post-Migration)

```
┌─────────────────────────────────────────────┐
│                 FRONTEND                     │
│          Next.js 13 (App Router)            │
│          Deployed on Vercel                  │
│                                              │
│  ┌─────────┐ ┌──────────┐ ┌──────────────┐ │
│  │ Parent  │ │ School   │ │  Authority   │ │
│  │Dashboard│ │Dashboard │ │  Dashboard   │ │
│  └────┬────┘ └────┬─────┘ └──────┬───────┘ │
│       │           │               │          │
│  ┌────┴───────────┴───────────────┴────┐    │
│  │     Supabase Client SDK             │    │
│  │     (Auth + DB + Storage + Realtime)│    │
│  └─────────────────┬───────────────────┘    │
└────────────────────┼────────────────────────┘
                     │
                     ▼
┌────────────────────────────────────────────┐
│              SUPABASE                       │
│                                             │
│  ┌──────────┐ ┌──────────┐ ┌────────────┐ │
│  │   Auth   │ │ Postgres │ │  Storage   │ │
│  │(built-in)│ │  + RLS   │ │ (S3-compat)│ │
│  └──────────┘ └──────────┘ └────────────┘ │
│                                             │
│  ┌──────────────────────────────────────┐  │
│  │         Real-time Engine             │  │
│  │   (WebSocket subscriptions)          │  │
│  └──────────────────────────────────────┘  │
│                                             │
│  ┌──────────────────────────────────────┐  │
│  │         Edge Functions               │  │
│  │   (SMS/email notifications)          │  │
│  └──────────────────────────────────────┘  │
└────────────────────────────────────────────┘
```

---

## FILES TO CREATE/MODIFY

### New Files
```
src/lib/supabase/client.ts          — Browser Supabase client
src/lib/supabase/server.ts          — Server Supabase client
src/lib/supabase/middleware.ts       — Auth middleware helper
supabase/migrations/001_schema.sql   — Database schema
supabase/seed.sql                    — Demo data
```

### Files to Delete
```
src/lib/firebase/                    — Entire directory
src/app/api/debug/                   — Entire directory
src/app/api/admin-sdk/check/         — Health check (no auth)
src/hooks/useAdminSdk.ts             — Duplicate
src/hooks/useChildProfiles.ts        — Duplicate (keep useChildren)
src/hooks/useTestAuth.ts             — Hardcoded creds
scripts/                             — Firebase-specific scripts
public/test-*.html                   — Test pages
public/test-*.js                     — Test scripts
reference/                           — Legacy reference files
```

### Files to Modify
```
src/lib/auth.ts                      — Replace Firebase with Supabase auth
src/middleware.ts                     — Use Supabase session
src/hooks/useAuth.ts                 — Supabase auth methods
src/hooks/useChildren.ts             — Supabase queries
src/hooks/useFirestore.ts            — Replace with useSupabase or remove
src/hooks/useNotifications.ts        — Supabase real-time
src/hooks/useStorage.ts              — Supabase storage
src/hooks/useUsers.ts                — Supabase queries
src/app/api/alerts/route.ts          — Supabase server client
src/app/api/children/route.ts        — Supabase server client
src/app/api/users/route.ts           — Supabase server client
src/app/dashboard/school/page.tsx    — Real functionality
src/app/dashboard/authority/page.tsx  — Real functionality
package.json                         — Remove firebase, add supabase
```
