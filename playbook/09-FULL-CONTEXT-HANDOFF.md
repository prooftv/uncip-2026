# UNCIP — COMPLETE PROJECT CONTEXT & HANDOFF
## Everything you need to continue this conversation anywhere

---

## WHAT IS UNCIP

UNCIP (Unami National Child Identification Programme) is a digital platform for child safety in South African townships. It connects parents, schools, and authorities (SAPS) in real-time when a child is missing or at risk.

Built by the Unami Foundation. This is a first vibe-coding project — prototype exists, cloned repo, needs strategic direction more than code right now.

**Live repo:** https://github.com/prooftv/uncip-2026
**Upstream:** https://github.com/unamiapp/app.git

---

## CORE PHILOSOPHY: SELF-DETERMINATION

This is non-negotiable. Everything flows from this.

UNCIP is not charity tech. It is **infrastructure that communities own and operate themselves.** Parents register their own children. Schools confirm attendance. Communities mobilise. Authorities coordinate. Government funds the platform, not the dependency.

Traditional model: Government designs → deploys to communities → communities are "beneficiaries"
UNCIP model: Communities identify need → UNCIP provides tools → communities run it → government funds infrastructure

This matters because:
- It scales without proportional cost (communities do the work)
- It survives political cycles (community ownership, not political appointee ownership)
- It aligns with constitutional values (Section 28 children's rights + Section 195 public participation)
- A minister doesn't want another dependency programme — they want a platform

---

## THE GOAL

Present UNCIP as a prototype to the **Minister of Education** (contact of a close contact) to secure funding for a 6-month pilot programme in 3 South African townships.

**The ask:** R2.4 million for a 6-month pilot across 30 schools, 3 SAPS stations, ~2,000 children.

**The angle:** UNCIP fills the gap between existing government systems (LURITS, NCPR, SAPS CAS) — it's the real-time, community-facing coordination layer that doesn't exist yet.

---

## CURRENT TECH STATE (Honest)

### Stack
- Next.js 13 (App Router) + React 18 + TypeScript
- Firebase (Auth + Firestore + Storage) — **billing issues, considering Supabase**
- NextAuth.js for session management
- Tailwind CSS, react-hook-form, react-hot-toast, framer-motion
- Deployed architecture: Vercel-ready, GitHub Actions CI/CD

### What works
- Multi-role auth (parent, school, authority, admin, community)
- Child profile creation with photo upload
- Alert system for missing/endangered children
- Role-based dashboards with real-time data
- User management (admin CRUD)
- Responsive mobile-first design
- Role switching (admin)

### What doesn't work
- Firebase backend (billing/subscription issues)
- No email/SMS notifications
- School and Authority dashboards are placeholders
- No test suite
- Security vulnerabilities (plaintext passwords, debug endpoints exposed, demo123 backdoor)
- No offline capability
- zod imported but not in package.json (will crash)
- Firebase Admin SDK initialized in 4 different places (conflict risk)
- 3 duplicate hooks for children data
- Production code depends on /api/debug/* endpoints

### Key decision: Supabase vs Firebase
For the presentation, don't mention either by name. Say:
> "PostgreSQL-based, open-source, self-hostable architecture. Children's data never leaves South African jurisdiction."

Why Supabase wins for government context:
- Self-hostable (data sovereignty — government requirement)
- PostgreSQL (standard, auditable, government-trusted)
- No vendor lock-in (open source)
- Predictable pricing (no surprise billing)
- Can deploy on SITA-approved infrastructure
- Firebase has no SA data region

Practical reality: Don't migrate now. Migrate when funded. The current app produces screenshots, which is all you need for the first meeting.

---

## SDG 16 ALIGNMENT

SDG 16: Peace, Justice and Strong Institutions

| Target | UNCIP Contribution |
|---|---|
| 16.1 Reduce violence | Real-time alerts reduce time children are at risk |
| 16.2 End violence against children | Early detection through coordinated parent-school-authority response |
| 16.3 Rule of law / equal access to justice | Digital case tracking ensures every alert gets a response |
| 16.6 Effective, accountable institutions | Audit trails, response time tracking |
| 16.7 Participatory decision-making | Parents and communities are active agents, not passive recipients |
| 16.9 Legal identity for all | Child registration with ID numbers, photos |
| 16.a Strengthen national institutions | Builds capacity of schools and SAPS to coordinate |

The founder has a **DG Primer (Development Gateway) certificate** — signals understanding of the development data ecosystem. Mention it in presentations.

SA's Voluntary National Review to the UN consistently highlights: high violence against children, gaps in child protection, need for digital transformation, need for community participation. UNCIP addresses all four.

---

## GOVERNMENT ALIGNMENT

### Key legislation
1. **Children's Act 38 of 2005** — Section 110 (National Child Protection Register). UNCIP is the real-time front-end to the NCPR.
2. **SA Schools Act 84 of 1996** — Section 3 (compulsory attendance). UNCIP automates the link between "child absent" and "alert raised."
3. **POPIA 2013** — Section 26-27 (children's data). UNCIP is POPIA-compliant by design.
4. **NDP 2030** — Chapter 11 (social protection).
5. **4IR Strategy** — Digital transformation of government services.

### Existing government systems UNCIP connects
| System | Owner | What it does | UNCIP integration |
|---|---|---|---|
| LURITS | DBE | Learner tracking by enrolment | UNCIP uses school enrolment as baseline |
| NCPR | DSD | Child protection register | UNCIP feeds real-time incidents into NCPR |
| SAPS CAS | SAPS | Case administration | UNCIP generates case references for SAPS |
| EMIS | DBE | School management info | UNCIP maps children to EMIS school codes |

### Why target Department of Basic Education (DBE)
- Schools see every child every day — they know first when something is wrong
- DBE has existing budget lines UNCIP fits into (CSTL, LURITS operational, conditional grants)
- Not asking for new money — asking them to spend existing money more effectively
- DBE entry point: Chief Directorate: Care and Support in Schools
- SAPS is operationally overwhelmed, slow procurement. DSD is underfunded. DBE has reach and infrastructure.

### Stakeholder map
- **Primary:** Minister of Basic Education, DG of Basic Education, Provincial Education Departments
- **Secondary:** Minister of Social Development, SAPS Provincial Commissioner, SITA, CSIR
- **Community:** School Governing Bodies, Ward Councillors, Community Policing Forums, NGOs (Missing Children SA)

### Government language guide
| Don't say | Say instead |
|---|---|
| App | Digital platform / Integrated system |
| Users | Stakeholders / Beneficiaries |
| Demo | Proof of concept / Working prototype |
| Startup | Social enterprise / Public-private partnership |
| Funding | Investment / Resource allocation |
| MVP | Phase 1 deliverable |
| Cloud | Government-approved hosting infrastructure |

---

## THE PRESENTATION (15 slides, 15 minutes)

No live demo needed for first meeting. Screenshots + story + numbers.

### Slide structure
1. **Title** — UNCIP, presented to Minister, date, Unami Foundation
2. **The Problem** — 23 children reported missing per day, no coordination system. Emotional hook.
3. **The Gap** — LURITS tracks enrolment, NCPR records after the fact, SAPS takes reports at station. No real-time layer.
4. **Introducing UNCIP** — Screenshot of parent dashboard on mobile.
5. **How It Works** — Register → Alert → Respond (3-step visual)
6. **"Thandi's Story"** — The demo narrative (see below). Screenshots or screen recording.
7. **Policy Alignment** — Children's Act, Schools Act, NDP, 4IR, POPIA
8. **Integration** — LURITS ↔ UNCIP ↔ SAPS CAS diagram
9. **The Numbers** — 700+/month missing, 24-72hr response time, R200M+ annual cost
10. **Pilot Proposal** — 3 townships, 30 schools, 6 months, map visual
11. **Budget** — R2.4M summary
12. **Expected Outcomes** — Before/after comparison
13. **Sustainability** — Phase 1 pilot → Phase 2 provincial → Phase 3 national → integrated into DBE budget
14. **The Team** — Founder, any advisors
15. **The Ask** — R2.4M, 30 schools, SAPS liaison, independent evaluation. Closing line: "Every child registered on UNCIP is a child the system can find."

### "Thandi's Story" (memorise this — 2 minutes, no slides)

> Thandi is 9 years old. She goes to Masiphumelele Primary in Khayelitsha. One afternoon, she doesn't come home.
>
> Her mother Nomsa opens UNCIP on her phone. She sees Thandi's profile — photo, school, medical info. She taps "Report Missing Child." She fills in: last seen at school at 14:30, wearing blue uniform.
>
> Instantly, the school principal gets a notification. He confirms Thandi left at 14:15 with two classmates heading toward the taxi rank.
>
> The local SAPS station sees the alert — Thandi's photo, description, last known location. A case reference is auto-generated.
>
> 45 minutes later, a community member spots Thandi at a neighbour's house. The alert is resolved. Total time: 47 minutes.
>
> Without UNCIP, that same process takes 24 to 72 hours of phone calls, station visits, and hoping someone has seen your child.

### Q&A talking points
- **"Why not WhatsApp?"** — Unstructured, unaccountable, not POPIA-compliant. UNCIP has audit trails, verified identities, role-based access.
- **"Data privacy?"** — POPIA-compliant by design. Parental consent. Encrypted. Self-hostable for full data sovereignty.
- **"Different from Missing Children SA?"** — They operate after the fact (flyers, social media). UNCIP operates in the critical first hour.
- **"No smartphones?"** — Works on any browser. USSD/SMS fallback planned. Community champions at schools assist parents.
- **"Who owns the data?"** — Government. UNCIP provides technology. Public-private partnership model.
- **"After the pilot?"** — Integration into DBE's LURITS infrastructure. Platform becomes part of government digital ecosystem.

---

## THE NUMBERS

### Key statistics (verify with SAPS Annual Crime Statistics)
- ~700 children reported missing per month in SA
- ~8,400 per year
- Average response time without coordination: 24-72 hours
- Target with UNCIP: <1 hour

### Cost-of-inaction model (conservative estimate)
```
SAPS cost:        8,400 cases × 40hrs × R250/hr  = R 84,000,000
Social work:      8,400 cases × 20hrs × R200/hr  = R 33,600,000
Family cost:      8,400 cases × R5,000            = R 42,000,000
Unresolved (10%): 840 cases × R50,000/yr          = R 42,000,000
TOTAL annual cost:                                 = R201,600,000+
```

### UNCIP impact projection
```
30% reduction in SAPS hours (faster resolution)    = R25.2M saved
40% reduction in unresolved cases                   = R16.8M saved
50% reduction in family economic loss               = R21.0M saved
TOTAL potential annual savings:                     = R63M
Pilot cost: R2.4M → ROI at national scale: 26:1
```

### Cost per child
```
Pilot: R2.4M ÷ 2,000 children = R1,200/child for 6 months
National scale: R25M ÷ 12M learners = R2.08/child/year
Compare: School nutrition programme = R1,200/child/year
```

---

## PILOT PROGRAMME DESIGN

### Overview
- 6 months, 3 townships, 30 schools, 3 SAPS stations, ~2,000 children
- Sites: Khayelitsha (Western Cape), Soweto (Gauteng), Umlazi (KwaZulu-Natal)
- Independent evaluation by university or CSIR

### Phases
1. **Month 1:** Setup — MOUs signed, schools selected, accounts created, training materials prepared
2. **Month 2:** Training & registration — principals trained, parent registration drives, community champions recruited
3. **Months 3-4:** Active operation — system live, weekly check-ins, monthly drills, data collection
4. **Month 5:** Evaluation — independent assessment, surveys, interviews
5. **Month 6:** Report — final evaluation, presentation to DBE, recommendation for scale

### KPIs
| KPI | Target |
|---|---|
| Children registered | 2,000 |
| Parents onboarded | 1,500 |
| Schools active | 30 |
| Average response time | <2 hours |
| Alert resolution rate | >80% within 24hrs |
| Parent satisfaction | >70% positive |

---

## BUDGET: R2,400,000

| Category | Amount | % |
|---|---|---|
| Technology & Infrastructure | R 480,000 | 20% |
| Personnel | R1,080,000 | 45% |
| Field Operations | R 360,000 | 15% |
| Training | R 120,000 | 5% |
| Monitoring & Evaluation | R 240,000 | 10% |
| Project Management & Overheads | R 120,000 | 5% |
| **TOTAL** | **R2,400,000** | **100%** |

### Funding sources
- **Primary:** DBE conditional grant or direct allocation
- **Alternatives:** DSD, National Lotteries Commission, UNICEF SA, MTN/Vodacom Foundation, Google.org
- **Sustainability:** Year 1 grant-funded → Year 2 70/30 govt/donor → Year 3+ integrated into DBE operational budget

---

## LEGAL & COMPLIANCE

### POPIA
- Parental consent required for child registration
- Children's data encrypted at rest and in transit
- Row Level Security on all database tables
- Parents can view, correct, delete their data
- Information Officer to be appointed
- Privacy Impact Assessment required

### Entity structure
- Unami Foundation — needs NPO registration with DSD
- Structure funding as grant to NPO (avoids SITA procurement delays)
- BBBEE: if turnover <R10M, automatic Level 4 exemption

### IP model
- Open-source the platform code (builds government trust, no vendor lock-in)
- Data owned by government (DBE)
- UNCIP provides technology under license

### MOU key terms
- 6-month pilot, option to extend
- Data ownership: DBE
- Quarterly financial reporting
- Independent evaluation
- Either party can terminate with 30 days notice

---

## WHAT TO DO RIGHT NOW (No coding)

```
1. Take screenshots from the current app for the presentation deck
2. Verify 3-4 SAPS missing children statistics (saps.gov.za/services/crimestats.php)
3. Memorise "Thandi's Story" — 2 minutes, no slides needed
4. Write the 1-page policy brief (template in playbook/02-AGENT-GOVERNMENT.md)
5. Print 1-page budget summary
6. Prepare leave-behind documents (policy brief + budget on good paper)
```

The vibe coding happens after they say "yes, show us more."

---

## PLAYBOOK FILES (in repo at /playbook/)

| File | Contents |
|---|---|
| 00-MASTER-PLAYBOOK.md | Overview, narrative, demo flow, timeline |
| 01-AGENT-TECHNICAL.md | Full Supabase migration plan, PostgreSQL schema, RLS policies, file-by-file migration |
| 02-AGENT-GOVERNMENT.md | Legislation mapping, stakeholder map, policy brief template, government language guide |
| 03-AGENT-PRESENTATION.md | 15-slide deck with exact content, Q&A talking points, demo prep checklist |
| 04-AGENT-IMPACT.md | Statistics sources, cost-of-inaction model, ROI calculation, data presentation formats |
| 05-AGENT-PILOT.md | 3 sites, 6-month phases, roles, M&E framework, KPIs, risk register, training curricula |
| 06-AGENT-BUDGET.md | R2.4M line-item budget, funding sources, sustainability model, cost-per-child |
| 07-AGENT-LEGAL.md | POPIA matrix, Children's Act, SITA strategy, MOU template, IP model, compliance checklist |
| 08-CORE-PHILOSOPHY.md | Self-determination principle, SDG 16 mapping, Supabase vs Firebase, DBE targeting strategy |

---

## REPO STRUCTURE (key files only)

```
/src
  /app
    /api
      /admin-sdk/users/route.ts      — User CRUD (primary API)
      /admin-sdk/children/route.ts    — Children CRUD (primary API)
      /admin-sdk/alerts/route.ts      — Alerts (primary API)
      /alerts/route.ts                — Alerts (duplicate)
      /alerts/[id]/route.ts           — Single alert ops
      /children/route.ts              — Children (duplicate)
      /users/route.ts                 — Users (duplicate)
      /parent/create-child/route.ts   — Parent child creation
      /parent/alerts/route.ts         — Parent alerts
      /auth/[...nextauth]/route.ts    — NextAuth handler
      /auth/reset-password/route.ts   — Password reset
      /debug/*                        — Debug endpoints (should be removed)
    /auth/login/page.tsx              — Login page with role selector
    /auth/register/page.tsx           — Registration page
    /dashboard/layout.tsx             — Dashboard shell with sidebar
    /dashboard/admin/page.tsx         — Admin dashboard (functional)
    /dashboard/parent/page.tsx        — Parent dashboard (functional)
    /dashboard/school/page.tsx        — School dashboard (placeholder)
    /dashboard/authority/page.tsx      — Authority dashboard (placeholder)
    /dashboard/community/page.tsx      — Community dashboard (placeholder)
  /components
    /auth/LoginForm.tsx, RegisterForm.tsx
    /dashboard/DashboardOverview.tsx, DashboardStats.tsx, QuickActions.tsx, RecentActivity.tsx
    /emergency/MissingChildForm.tsx
    /forms/ChildProfileForm.tsx
    /ui/* (Button, Card, Input, PhotoUpload, etc.)
    RoleSwitcher.tsx
  /hooks
    useAuth.ts                        — Auth context (NextAuth + Firebase Auth)
    useChildren.ts                    — Children CRUD via /api/admin-sdk/children
    useChildProfiles.ts               — Children CRUD via client Firestore (DUPLICATE)
    useAdminSdk.ts                    — Users + Children via API (DUPLICATE)
    useUsers.ts                       — User CRUD via /api/admin-sdk/users
    useFirestore.ts                   — Generic Firestore wrapper
    useNotifications.ts               — Real-time notifications
    useActivity.ts                    — Activity logging
    useStorage.ts                     — File upload
    useResources.ts                   — Resources CRUD
  /lib
    auth.ts                           — NextAuth config (credentials + Google)
    /firebase/config.ts               — Client Firebase (lazy-loaded)
    /firebase/admin-singleton.ts      — Server Firebase Admin SDK
    /firebase/childrenApi.ts          — Direct Firestore children queries
    /utils/sessionUtils.ts            — Session helpers
    /utils/alertUtils.ts              — Alert data normalisation
    /utils/validation.ts              — Zod schemas (zod NOT in package.json)
  /types
    user.ts                           — UserProfile, UserRole, UserSession
    child.ts                          — ChildProfile, ChildAlert
  middleware.ts                       — Route protection, role-based redirects

/playbook                             — All strategy documents (8 files)
/firestore.rules                      — Firestore security rules
/storage.rules                        — Storage security rules
/firebase.json                        — Firebase config
/vercel.json                          — Vercel config
/.github/workflows/deploy.yml         — CI/CD to Vercel
```

---

## CONTINUATION PROMPT FOR CHATGPT

Copy-paste this to start the conversation:

> I'm building UNCIP — a child safety platform for South African townships. I have a complete playbook and need help executing specific parts. Here's my full context:
>
> [Paste this entire document]
>
> My immediate priority is: [state what you need — e.g., "help me write the 1-page policy brief" or "help me verify the SAPS statistics" or "help me refine the presentation talking points"]
>
> Key constraints:
> - No coding right now — first meeting is story + numbers + screenshots
> - Core philosophy is self-determination (communities as agents, not beneficiaries)
> - Targeting Department of Basic Education specifically
> - I have a DG Primer certificate (Development Gateway)
> - SDG 16 alignment is important
> - Budget is R2.4M for 6-month pilot
> - Supabase migration planned but not urgent (say "PostgreSQL, self-hostable" in presentations)
