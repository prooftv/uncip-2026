# AGENT 5: PILOT PROGRAMME DESIGN
## Mission: Design a 6-month pilot in 2-3 townships

---

## AGENT IDENTITY
- **Role:** Programme designer & implementation planner
- **Objective:** Create a credible, executable pilot plan that government can approve
- **Success Criteria:** Pilot design answers every "how would this actually work?" question

---

## PILOT OVERVIEW

| Parameter | Detail |
|---|---|
| Duration | 6 months |
| Locations | 3 townships across 2-3 provinces |
| Schools | 10 per township (30 total) |
| SAPS stations | 1 per township (3 total) |
| Children registered | ~2,000 (target) |
| Parents onboarded | ~1,500 (target) |
| Budget | R2.4 million |

---

## PROPOSED PILOT SITES

### Site 1: Khayelitsha, Western Cape
- **Why:** Large township, high crime rate, active community structures, proximity to UCT/UWC for evaluation
- **Schools:** 10 primary schools (to be selected with WCED)
- **SAPS:** Khayelitsha Community Service Centre
- **Community partner:** Khayelitsha Community Policing Forum

### Site 2: Soweto, Gauteng
- **Why:** Iconic township, large population, GDE infrastructure, media visibility
- **Schools:** 10 primary schools (to be selected with GDE)
- **SAPS:** Soweto SAPS cluster
- **Community partner:** Soweto Community Policing Forum

### Site 3: Umlazi, KwaZulu-Natal
- **Why:** Large township, different provincial context, tests cross-provincial model
- **Schools:** 10 primary schools (to be selected with KZN DoE)
- **SAPS:** Umlazi SAPS
- **Community partner:** Local ward councillor network

---

## IMPLEMENTATION PHASES

### Month 1: Setup & Partnerships
```
Week 1-2:
  - Sign MOU with DBE (or provincial education department)
  - Sign MOU with SAPS provincial office
  - Appoint pilot coordinator per site
  - Finalise school selection with provincial department

Week 3-4:
  - Deploy Supabase infrastructure
  - Create school admin accounts
  - Create SAPS user accounts
  - Prepare training materials (in English, isiXhosa, isiZulu, Sesotho)
  - Print registration consent forms (POPIA compliant)
```

### Month 2: Training & Registration
```
Week 5-6:
  - Train school principals and admin staff (2-hour session per school)
  - Train SAPS designated officers (half-day session per station)
  - Train community champions (1 per school — could be SGB member)

Week 7-8:
  - Parent registration drives at each school
  - Community champions assist parents with smartphone registration
  - USSD/SMS fallback for parents without smartphones
  - Target: 60-70 children registered per school
```

### Month 3-4: Active Operation
```
  - System goes live
  - Weekly check-ins with school coordinators
  - Monthly review meetings with SAPS liaison
  - Real alerts processed through the system
  - Simulated drills (1 per site per month) to test response times
  - Data collection for M&E
```

### Month 5: Evaluation
```
  - Independent evaluator conducts assessment
  - Parent satisfaction surveys
  - School staff feedback sessions
  - SAPS officer interviews
  - Response time analysis
  - System usage analytics
```

### Month 6: Report & Recommendation
```
  - Final evaluation report
  - Presentation to DBE
  - Recommendation for scale or iteration
  - Handover documentation
```

---

## ROLES & RESPONSIBILITIES

### UNCIP Team (Unami Foundation)
| Role | Responsibility | FTE |
|---|---|---|
| Project Manager | Overall coordination, reporting to DBE | 1.0 |
| Technical Lead | Platform maintenance, bug fixes, data | 1.0 |
| Field Coordinator (×3) | One per site, manages local operations | 3 × 0.5 |
| Training Facilitator | Develops and delivers training | 0.5 |

### Government Partners
| Partner | Responsibility |
|---|---|
| DBE / Provincial DoE | School selection, principal buy-in, LURITS data access |
| SAPS | Designated officer per station, case number integration |
| DSD (optional) | Social worker linkage for welfare cases |
| Ward Councillor | Community mobilisation, registration drives |

### Evaluation Partner
| Partner | Responsibility |
|---|---|
| University / CSIR | Independent M&E, baseline study, endline study, report |

---

## MONITORING & EVALUATION FRAMEWORK

### Key Performance Indicators

| KPI | Baseline | Target | Measurement |
|---|---|---|---|
| Children registered | 0 | 2,000 | System count |
| Parents onboarded | 0 | 1,500 | System count |
| Schools active | 0 | 30 | System count |
| Alerts created | N/A | Track all | System count |
| Average response time | 24-72hrs (estimated) | <2hrs | System timestamp analysis |
| Alert resolution rate | Unknown | >80% within 24hrs | System data |
| Parent satisfaction | N/A | >70% positive | Survey |
| School staff satisfaction | N/A | >70% positive | Survey |
| SAPS officer satisfaction | N/A | >60% positive | Interview |
| System uptime | N/A | >99% | Server monitoring |

### Data Collection Methods
```
Quantitative:
  - System analytics (automatic — registrations, alerts, response times)
  - Pre/post surveys (parents, school staff)
  - SAPS case data comparison (with/without UNCIP)

Qualitative:
  - Focus groups with parents (2 per site)
  - Interviews with school principals (all 30)
  - Interviews with SAPS officers (all 3 stations)
  - Case studies of actual alerts (anonymised)
```

---

## RISK REGISTER

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Low smartphone penetration | Medium | High | USSD/SMS fallback, community champions |
| Poor connectivity | High | Medium | PWA offline mode, SMS alerts |
| School staff resistance | Medium | Medium | Principal buy-in first, training, incentives |
| SAPS non-cooperation | Medium | High | MOU at provincial level, designated liaison |
| False alerts | Low | High | Verification step, consequences for misuse |
| Data breach | Low | Critical | Encryption, RLS, POPIA compliance, audit logs |
| Political change | Low | Medium | Cross-party framing (child safety is non-partisan) |
| Funding delay | Medium | High | Phased budget release, lean operations |

---

## TRAINING CURRICULUM

### For Parents (30 minutes, at school registration drive)
```
1. What is UNCIP? (5 min)
2. How to register your child (10 min — hands-on)
3. How to create an alert (10 min — hands-on)
4. Your rights under POPIA (5 min)
```

### For School Staff (2 hours)
```
1. Overview of UNCIP and the pilot (15 min)
2. Your role as a school user (15 min)
3. Hands-on: Viewing enrolled children (20 min)
4. Hands-on: Responding to an alert (20 min)
5. Hands-on: Adding "last seen" information (20 min)
6. Q&A and scenarios (30 min)
```

### For SAPS Officers (half day)
```
1. Overview of UNCIP and government mandate (30 min)
2. How alerts flow from parent → school → SAPS (30 min)
3. Hands-on: Authority dashboard walkthrough (45 min)
4. Hands-on: Assigning case numbers (30 min)
5. Hands-on: Resolving alerts (30 min)
6. Integration with existing CAS workflow (30 min)
7. Q&A (30 min)
```

---

## TASKS

```
Task 5.1: Draft MOU template for DBE partnership
Task 5.2: Draft MOU template for SAPS partnership
Task 5.3: Create school selection criteria
Task 5.4: Design parent consent form (POPIA compliant, multilingual)
Task 5.5: Create training slide decks (parent, school, SAPS)
Task 5.6: Design M&E data collection instruments (surveys, interview guides)
Task 5.7: Create pilot operations manual
Task 5.8: Design simulated drill protocol
Task 5.9: Create weekly/monthly reporting templates
Task 5.10: Identify potential evaluation partners (UCT, Wits, CSIR)
```
