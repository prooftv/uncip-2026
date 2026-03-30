# AGENT 4: DATA & IMPACT MODEL
## Mission: Build the statistical case for funding with verified numbers

---

## AGENT IDENTITY
- **Role:** Research analyst & impact modeller
- **Objective:** Compile verified SA statistics and build a cost-of-inaction model
- **Success Criteria:** Every number in the presentation is sourced and defensible

---

## KEY STATISTICS TO VERIFY & SOURCE

### Missing Children
| Statistic | Source to verify | Notes |
|---|---|---|
| Children reported missing per year | SAPS Annual Crime Statistics | Check "missing persons" category, filter by age |
| Children reported missing per month | Derived from annual | ~700/month commonly cited |
| Recovery rate | SAPS / Missing Children SA | What % are found? How quickly? |
| Unresolved cases | SAPS | How many remain open after 12 months? |
| Child trafficking cases | SAPS / NPA | Subset of missing that become trafficking |

### Education
| Statistic | Source to verify |
|---|---|
| Total learners in SA public schools | DBE Annual Report / LURITS |
| Learner dropout rate | DBE Statistics |
| Schools in pilot townships | Provincial education departments |
| Average school size in townships | DBE / EMIS data |

### Cost of Current System
| Cost element | How to estimate |
|---|---|
| SAPS person-hours per missing child case | SAPS operational data or estimate |
| Social worker hours per case | DSD data |
| Court/legal costs for unresolved cases | NPA / Legal Aid SA |
| Economic cost to families (lost work, transport) | Estimate based on minimum wage |

---

## COST-OF-INACTION MODEL

### Framework
```
Annual cost of missing children in SA =
  (Cases per year × Average SAPS hours per case × SAPS hourly cost)
+ (Cases per year × Average social worker hours × DSD hourly cost)
+ (Cases per year × Average family economic loss)
+ (Unresolved cases × Ongoing investigation cost)
+ (Trafficking cases × Long-term social cost)
```

### Estimated Calculation (to be verified)
```
Assumptions (conservative):
- 8,400 children reported missing per year (700/month)
- Average 40 SAPS person-hours per case
- SAPS cost: R250/hour (fully loaded)
- Average 20 social worker hours per case
- Social worker cost: R200/hour
- Family economic loss: R5,000 per case (transport, lost wages, phone costs)
- 10% cases unresolved after 12 months (840 cases)
- Ongoing investigation: R50,000 per unresolved case per year

SAPS cost:        8,400 × 40 × R250     = R  84,000,000
Social work cost: 8,400 × 20 × R200     = R  33,600,000
Family cost:      8,400 × R5,000         = R  42,000,000
Unresolved:       840 × R50,000          = R  42,000,000
                                    TOTAL = R 201,600,000/year

Conservative estimate: R200M+ per year in direct costs
```

### UNCIP Impact Projection
```
If UNCIP reduces average response time from 24hrs to 1hr:
- Estimated 30% reduction in SAPS hours per case (faster resolution)
- Estimated 40% reduction in unresolved cases (better coordination)
- Estimated 50% reduction in family economic loss (faster resolution)

Annual savings:
SAPS:       R84M × 30%  = R 25,200,000
Unresolved: R42M × 40%  = R 16,800,000
Family:     R42M × 50%  = R 21,000,000
                   TOTAL = R 63,000,000/year potential savings

Pilot cost: R2.4M
ROI if scaled nationally: 26:1
```

---

## RESEARCH TASKS

```
Task 4.1: SAPS Crime Statistics
  - Download latest SAPS Annual Crime Statistics
  - Extract missing persons data (filter by under-18)
  - Get 5-year trend data
  - Source: https://www.saps.gov.za/services/crimestats.php

Task 4.2: Missing Children SA Data
  - Contact Missing Children SA for annual report
  - Get recovery rate statistics
  - Get average time-to-recovery data
  - Source: https://missingchildren.org.za

Task 4.3: DBE Education Statistics
  - Total learner enrolment by province
  - Number of schools in pilot townships
  - LURITS coverage statistics
  - Source: DBE Annual Report, education.gov.za

Task 4.4: International Benchmarks
  - AMBER Alert (USA): Impact statistics since implementation
  - UK Child Rescue Alert: Response time improvements
  - Australia: National Missing Persons Coordination Centre stats
  - Use these as "what's possible" benchmarks

Task 4.5: Township-Specific Data
  - Khayelitsha: Population, schools, SAPS stations, crime stats
  - Soweto: Same
  - Umlazi: Same
  - Source: Stats SA Census, municipal IDPs

Task 4.6: Build Impact Dashboard
  - Create a simple spreadsheet model
  - Input: number of children registered, alerts created, response times
  - Output: projected cost savings, lives impacted
  - This becomes the M&E framework for the pilot
```

---

## DATA PRESENTATION FORMATS

### For the Slide Deck (Slide 9)
Use 4 large numbers:
```
700+     children reported missing per month
24-72hrs average response time today
<1hr     target response time with UNCIP
R200M+   annual cost of current system
```

### For the Policy Brief (1-pager)
Use a comparison table:
```
                    Without UNCIP    With UNCIP (projected)
Response time       24-72 hours      <1 hour
Stakeholders        Sequential       Simultaneous
Records             Paper-based      Digital + auditable
Recovery rate       [X]%             [X+15]% (projected)
Annual cost         R200M+           R140M (30% reduction)
```

### For the Budget Document
Use the ROI calculation:
```
Pilot investment:           R 2,400,000
Projected annual savings
  if scaled nationally:     R63,000,000
Return on investment:       26:1
Payback period:             <1 month at national scale
```
