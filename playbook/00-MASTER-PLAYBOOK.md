# UNCIP MASTER PLAYBOOK
## From Prototype to Government-Funded National Programme

---

## EXECUTIVE CONTEXT

**What this is:** A complete operational playbook to take the UNCIP prototype — a child identification and safety platform built for South African townships — from its current state to a fundable, demonstrable product suitable for presentation to the Minister of Education.

**The ask:** Government funding to pilot UNCIP as a national child safety infrastructure programme, integrated with the Department of Basic Education (DBE) and the South African Police Service (SAPS).

**The angle:** South Africa loses thousands of children annually. The government already runs programmes like LURITS (Learner Unit Record Information and Tracking System) and the National Child Protection Register. UNCIP fills the gap between these systems — it's the real-time, community-facing layer that connects parents, schools, and authorities when a child goes missing or is at risk.

---

## PLAYBOOK STRUCTURE

This playbook is divided into **7 workstreams**, each with a dedicated agent brief:

| # | Workstream | Document | Purpose |
|---|---|---|---|
| 0 | Core Philosophy | [08-CORE-PHILOSOPHY.md](./08-CORE-PHILOSOPHY.md) | Self-determination, SDG 16, Supabase vs Firebase, DBE targeting strategy |
| 1 | Technical Stabilisation | [01-AGENT-TECHNICAL.md](./01-AGENT-TECHNICAL.md) | Fix the prototype, migrate to Supabase, make it demo-ready |
| 2 | Government Alignment | [02-AGENT-GOVERNMENT.md](./02-AGENT-GOVERNMENT.md) | Map UNCIP to SA government policy, legislation, and existing systems |
| 3 | Presentation & Pitch | [03-AGENT-PRESENTATION.md](./03-AGENT-PRESENTATION.md) | Build the ministerial presentation deck and talking points |
| 4 | Data & Impact Model | [04-AGENT-IMPACT.md](./04-AGENT-IMPACT.md) | Compile statistics, build the case for funding with numbers |
| 5 | Pilot Programme Design | [05-AGENT-PILOT.md](./05-AGENT-PILOT.md) | Design a 6-month pilot in 2-3 townships |
| 6 | Budget & Funding | [06-AGENT-BUDGET.md](./06-AGENT-BUDGET.md) | Cost model, funding request, sustainability plan |
| 7 | Legal & Compliance | [07-AGENT-LEGAL.md](./07-AGENT-LEGAL.md) | POPIA, Children's Act, data sovereignty, government procurement |

---

## CURRENT STATE (Honest Assessment)

### What Works
- ✅ Multi-role authentication (parent, school, authority, admin)
- ✅ Child profile creation with photo upload
- ✅ Alert system for missing/endangered children
- ✅ Role-based dashboards with real-time data
- ✅ User management (admin CRUD)
- ✅ Responsive mobile-first design
- ✅ Deployed architecture (Next.js + Vercel ready)

### What Doesn't Work
- ❌ Firebase backend (billing/subscription issues)
- ❌ No email/SMS notifications
- ❌ School and Authority dashboards are placeholders
- ❌ No test suite
- ❌ Security vulnerabilities (plaintext passwords, debug endpoints exposed)
- ❌ No offline capability (critical for townships with poor connectivity)

### What's Needed for Demo Day
- Supabase migration (free tier, no billing issues)
- 3 working demo flows (parent reports missing child → authority receives alert → school confirms last seen)
- Clean, professional UI with government branding context
- Offline-first capability (PWA)
- Real SA data (province names, school names, SAPS station names)

---

## THE GOVERNMENT NARRATIVE

### Problem Statement (for the Minister)
> "South Africa has approximately 700 children reported missing every month. The current system relies on fragmented communication between parents, schools, and SAPS. There is no unified digital platform that enables real-time coordination when a child goes missing. UNCIP bridges this gap."

### Alignment with Government Priorities
1. **National Development Plan (NDP) 2030** — Chapter 11: Social Protection
2. **Children's Act 38 of 2005** — Section 110: National Child Protection Register
3. **SAPS Missing Persons Policy** — Currently paper-based in most stations
4. **DBE LURITS System** — Tracks learner enrolment but not real-time safety
5. **National Integrated Early Childhood Development Policy** — Community-based child protection
6. **4IR Strategy** — Digital transformation of government services

### What UNCIP Adds to the Ecosystem
```
┌─────────────────────────────────────────────────────┐
│                  GOVERNMENT SYSTEMS                  │
│                                                      │
│  LURITS ──── tracks enrolment                       │
│  NCPR ────── tracks abuse/neglect records           │
│  SAPS ────── takes missing persons reports          │
│  DSD ─────── manages social workers                 │
│                                                      │
│         ↕ GAP: No real-time coordination ↕          │
│                                                      │
│  ┌──────────────────────────────────────────────┐   │
│  │              UNCIP PLATFORM                   │   │
│  │                                               │   │
│  │  Parent reports → Instant alert to:           │   │
│  │    • School (confirm last attendance)         │   │
│  │    • SAPS station (case number generated)     │   │
│  │    • Community network (eyes on the ground)   │   │
│  │    • Social worker (welfare check)            │   │
│  │                                               │   │
│  │  All within minutes, not hours/days           │   │
│  └──────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

---

## DEMO FLOW (What the Minister Sees)

### Scenario: "Thandi's Story"
A 9-year-old girl in Khayelitsha doesn't come home from school.

**Screen 1 — Parent Dashboard**
> Thandi's mother, Nomsa, opens UNCIP on her phone. She sees Thandi's profile with photo, school info, and medical details. She taps "Report Missing Child."

**Screen 2 — Alert Creation**
> Nomsa fills in: last seen at Masiphumelele Primary at 14:30, wearing blue uniform. The alert goes live.

**Screen 3 — School Dashboard**
> The school principal receives an instant notification. They confirm Thandi left school at 14:15. They add: "She was with two classmates heading toward the taxi rank."

**Screen 4 — Authority Dashboard**
> The local SAPS Community Service Centre and the ward councillor both see the alert. The system shows Thandi's photo, description, and last known location on a map. A case reference is auto-generated.

**Screen 5 — Resolution**
> 45 minutes later, a community member spots Thandi at a neighbour's house. The alert is resolved. Total time from report to found: 47 minutes. Current average without UNCIP: 24-72 hours.

---

## TIMELINE TO PRESENTATION

| Week | Milestone | Owner |
|---|---|---|
| 1-2 | Technical stabilisation + Supabase migration | Agent 1 |
| 1-2 | Government policy research + alignment doc | Agent 2 |
| 2-3 | Impact data compilation + statistics | Agent 4 |
| 3 | Pilot programme design | Agent 5 |
| 3 | Budget model | Agent 6 |
| 3-4 | Legal compliance review | Agent 7 |
| 4 | Presentation deck build | Agent 3 |
| 4 | Demo rehearsal with "Thandi's Story" flow | All |
| 5 | **Presentation to Minister** | You + team |

---

## FILES IN THIS PLAYBOOK

```
/playbook
├── 00-MASTER-PLAYBOOK.md          ← You are here
├── 01-AGENT-TECHNICAL.md          ← Supabase migration, demo prep, security fixes
├── 02-AGENT-GOVERNMENT.md         ← Policy alignment, stakeholder mapping
├── 03-AGENT-PRESENTATION.md       ← Slide deck structure, talking points
├── 04-AGENT-IMPACT.md             ← Statistics, cost-of-inaction model
├── 05-AGENT-PILOT.md              ← Township pilot design
├── 06-AGENT-BUDGET.md             ← Funding request, cost model
├── 07-AGENT-LEGAL.md              ← POPIA, Children's Act, procurement
└── 08-CORE-PHILOSOPHY.md          ← Self-determination, SDG 16, sovereignty, DBE strategy
```
