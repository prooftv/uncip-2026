# AGENT 7: LEGAL & COMPLIANCE
## Mission: Ensure UNCIP is legally defensible and procurement-ready

---

## AGENT IDENTITY
- **Role:** Legal & compliance advisor
- **Objective:** Pre-empt every legal question the Minister's legal team will ask
- **Success Criteria:** No legal blocker can derail the pilot approval

---

## POPIA COMPLIANCE

### Data Processed by UNCIP

| Data Category | POPIA Classification | Consent Required | Retention |
|---|---|---|---|
| Parent name, email, phone | Personal information (s1) | Yes — at registration | Duration of account |
| Child name, DOB, gender | Children's personal info (s34) | Parental consent required | Duration of registration |
| Child photo | Biometric information (s1) | Explicit parental consent | Duration of registration |
| Child ID number | Identity number (s1) | Parental consent | Duration of registration |
| Medical information | Special personal info (s26) | Explicit consent | Duration of registration |
| Location data (last seen) | Personal information | Implied consent (alert creation) | Duration of alert + 5 years |
| Alert details | Personal information | Implied consent | 5 years (legal requirement) |
| Audit logs | Operational data | No consent needed | 7 years |

### POPIA Principles Applied

| Principle | UNCIP Implementation |
|---|---|
| **Accountability (s8)** | Designated Information Officer, privacy policy published |
| **Processing limitation (s9-12)** | Only collect data necessary for child safety |
| **Purpose specification (s13-14)** | Data used only for child identification and safety alerts |
| **Further processing (s15)** | No data sold or shared outside stated purpose |
| **Information quality (s16)** | Parents can update/correct their data |
| **Openness (s17-18)** | Privacy policy in plain language, multilingual |
| **Security safeguards (s19-22)** | Encryption at rest and in transit, RLS, audit logs |
| **Data subject participation (s23-25)** | Parents can view, correct, delete their data |
| **Children's data (s34-35)** | Parental consent required, competent person processes |

### Required Documents
```
Task 7.1: Draft Privacy Policy (public-facing, multilingual)
Task 7.2: Draft PAIA Manual (Promotion of Access to Information Act)
Task 7.3: Draft Parental Consent Form (for child registration)
Task 7.4: Draft Data Processing Agreement (between UNCIP and DBE)
Task 7.5: Register with Information Regulator (if not already)
Task 7.6: Appoint Information Officer
Task 7.7: Conduct Privacy Impact Assessment (PIA)
```

---

## CHILDREN'S ACT COMPLIANCE

### Relevant Sections

| Section | Requirement | UNCIP Compliance |
|---|---|---|
| s7 | Best interests of the child paramount | All design decisions prioritise child safety |
| s9 | Child participation rights | Age-appropriate: children not direct users |
| s13 | Parental responsibilities | Parents are primary users, maintain control |
| s110 | National Child Protection Register | UNCIP data can feed into NCPR |
| s150 | Child in need of care | Alert system identifies children at risk |
| s305 | Regulations for child protection | UNCIP operates within regulatory framework |

### Key Legal Position
> UNCIP does not replace any statutory obligation. It is a technology tool that assists parents, schools, and authorities in fulfilling their existing legal duties under the Children's Act. The platform does not make decisions about child welfare — it facilitates communication between mandated stakeholders.

---

## GOVERNMENT PROCUREMENT

### If Funded by Government (SITA Act Considerations)

The State Information Technology Agency Act requires that government IT procurement goes through SITA. However, there are exceptions:

| Scenario | SITA Requirement | Notes |
|---|---|---|
| Direct government procurement | Must go through SITA | Full tender process |
| Grant to NGO/NPO | SITA not required | NGO procures own technology |
| Public-private partnership | Depends on structure | Legal advice needed |
| Pilot/proof of concept | Often exempt | Below threshold, innovation category |

**Recommended approach:** Structure as a grant to Unami Foundation (NPO) for a pilot programme. This avoids SITA procurement delays while maintaining accountability through MOU and M&E.

### BBBEE Considerations
- If government-funded, BBBEE compliance may be required
- Unami Foundation should have BBBEE certificate or exemption (if turnover <R10M, automatic Level 4)
- Subcontractors should be BBBEE compliant where possible

---

## ENTITY STRUCTURE

### Current: Unami Foundation
- **Type:** Needs to be registered as NPO (Non-Profit Organisation) with DSD
- **Registration:** NPO Act 71 of 1997
- **Tax:** Section 18A status for tax-deductible donations (if applicable)

### Required Registrations
```
Task 7.8: Verify NPO registration status
Task 7.9: Verify tax exemption status (IT12EI)
Task 7.10: Obtain BBBEE certificate or exemption letter
Task 7.11: Register with CIPC if not already
Task 7.12: Open dedicated bank account for pilot funds
```

---

## INTELLECTUAL PROPERTY

### IP Ownership Model

| Component | Owner | License |
|---|---|---|
| UNCIP source code | Unami Foundation | Open-source (recommended) or licensed to government |
| Platform design & UX | Unami Foundation | Licensed to government for pilot |
| Data collected during pilot | Government (DBE) | UNCIP processes on behalf of DBE |
| Evaluation report | Evaluation partner | Published, open access |
| Training materials | Unami Foundation | Creative Commons for government use |

**Recommended approach:** Open-source the platform code. This:
1. Builds trust with government (no vendor lock-in)
2. Allows independent security audit
3. Enables other countries to adopt
4. Aligns with government open-source policy

---

## LIABILITY & INDEMNITY

### Key Risks to Address in MOU

| Risk | Mitigation |
|---|---|
| False alert causes harm | Terms of use prohibit false reports; criminal liability under existing law |
| Data breach exposes children's info | Encryption, RLS, security audit, cyber insurance |
| System downtime during real emergency | SLA with 99.9% uptime; SMS fallback; SAPS still operates independently |
| Incorrect information on alert | Parents responsible for accuracy; school verification step |
| Child harmed despite alert | UNCIP is a communication tool, not a guarantee of safety; existing SAPS/DSD responsibilities unchanged |

### Insurance Requirements
```
Task 7.13: Obtain professional indemnity insurance
Task 7.14: Obtain cyber liability insurance
Task 7.15: Obtain public liability insurance
```

---

## MOU KEY TERMS

### Between Unami Foundation and DBE

```
1. PURPOSE
   Pilot deployment of UNCIP platform in [X] schools across [Y] provinces

2. DURATION
   6 months from date of signature, with option to extend

3. RESPONSIBILITIES
   Unami Foundation: Technology, training, field operations, reporting
   DBE: School access, principal cooperation, LURITS data (anonymised), funding

4. DATA OWNERSHIP
   All data collected belongs to DBE
   Unami Foundation processes data on behalf of DBE
   Data Processing Agreement (Annexure A) governs processing

5. INTELLECTUAL PROPERTY
   Platform code: Unami Foundation (licensed to DBE)
   Data: DBE
   Reports: Joint ownership

6. FUNDING
   DBE allocates R[X] to Unami Foundation
   Quarterly financial reporting required
   Unaudited management accounts monthly
   Audited financial statements at project end

7. REPORTING
   Monthly progress reports to DBE project manager
   Quarterly review meetings
   Final evaluation report at month 6

8. TERMINATION
   Either party may terminate with 30 days written notice
   Data returned/deleted within 60 days of termination

9. CONFIDENTIALITY
   Both parties bound by confidentiality
   POPIA compliance mandatory

10. DISPUTE RESOLUTION
    Mediation first, then arbitration under Arbitration Act
```

---

## COMPLIANCE CHECKLIST

```
□ NPO registration current
□ Tax exemption status verified
□ BBBEE certificate/exemption obtained
□ Information Officer appointed
□ Privacy Policy drafted and published
□ PAIA Manual drafted
□ Parental Consent Form drafted (multilingual)
□ Data Processing Agreement drafted
□ Privacy Impact Assessment completed
□ Professional indemnity insurance obtained
□ Cyber liability insurance obtained
□ MOU template drafted
□ Terms of Use drafted
□ Information Regulator registration
□ CIPC registration verified
□ Dedicated bank account opened
```
