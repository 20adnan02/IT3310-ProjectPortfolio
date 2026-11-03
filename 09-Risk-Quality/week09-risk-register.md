# Risk Register: RCHN Patient Intake and Scheduling System

**Consultant:** Adnan Latif  
**Role:** Associate Consultant, NovaTech Consulting  
**Engagement:** Regional Care Health Network (RCHN)  
**Date:** November 3, 2026  

---

## Risk Entries

### Risk 1

**Description:** If clinic staff are not available for scheduled testing and training, then training and rollout activities may be delayed.

**Probability:** Medium  
**Impact:** High  
**Score:** 6  
**Priority:** High  

**Response Strategy:** Mitigate. The team will schedule training early, provide multiple training opportunities when possible, and monitor clinic readiness.

**Trigger or Monitoring Condition:** A clinic misses a scheduled training or readiness checkpoint.

**Owner:** Project Manager, because this role coordinates the schedule, training activities, and clinic readiness.

---

### Risk 2

**Description:** If RCHN's technical environment cannot support the new system without additional upgrades, then project cost, technical work, and schedule may increase.

**Probability:** Medium  
**Impact:** High  
**Score:** 6  
**Priority:** High  

**Response Strategy:** Mitigate. The technical team will review system requirements and RCHN's current environment early to identify compatibility or infrastructure problems.

**Trigger or Monitoring Condition:** The technical assessment identifies an unmet infrastructure or compatibility requirement.

**Owner:** Developer, because this role can evaluate system compatibility and technical infrastructure requirements with RCHN IT.

---

### Risk 3

**Description:** If patient or appointment data is migrated incorrectly or errors remain undetected, then data accuracy, testing, clinic operations, and go-live readiness could be affected.

**Probability:** Medium  
**Impact:** High  
**Score:** 6  
**Priority:** High  

**Response Strategy:** Mitigate. The team will validate migrated patient and appointment data, perform testing, and correct discrepancies before go-live.

**Trigger or Monitoring Condition:** Data validation identifies missing, incorrect, duplicated, or inconsistent records.

**Owner:** Developer, because this role can monitor data migration, validation, and technical data-quality problems.

---

### Risk 4

**Description:** If required clinical workflow approvals are delayed, then configuration and deployment activities may not begin as scheduled.

**Probability:** Medium  
**Impact:** Medium  
**Score:** 4  
**Priority:** Medium  

**Response Strategy:** Mitigate. The Project Manager will schedule clinical approval checkpoints early and follow up with executive stakeholders.

**Trigger or Monitoring Condition:** Required approval has not been received by the planned decision date.

**Owner:** Project Manager, because this role coordinates approvals, schedule dependencies, and executive escalation.

---

### Risk 5

**Description:** If major defects are identified during the Week 8 Conduct Integrated Workflow Testing activity, then additional rework and retesting may be required and the planned go-live date could be delayed.

**Probability:** Medium  
**Impact:** High  
**Score:** 6  
**Priority:** High  

**Response Strategy:** Mitigate. The team will conduct acceptance testing early, correct critical defects, and retest affected workflows before deployment.

**Trigger or Monitoring Condition:** A critical defect is identified or acceptance testing falls behind the planned readiness checkpoint.

**Owner:** Product Manager, working with Developers, because the Product Manager can confirm acceptance requirements while Developers investigate and correct technical defects.

---

## Bring Forward

### Week 5 Assumptions

- Staff from all six clinics will be available to participate in workflow review, testing, and training during the planned implementation period.
- RCHN's current technical environment can support the replacement intake and scheduling system without a major infrastructure upgrade.

### Week 7 Product Backlog

**Backlog Item:** As a front desk staff member, I want to use the same required patient intake fields at all six RCHN clinics so that I can collect complete and consistent patient information.

### Week 8 Project Schedule

**Activity:** Conduct integrated workflow testing  
**Predecessors:** Configure standardized intake workflow and configure appointment scheduling workflow  
**Planned Week:** Week 4  

---

## Assumption Connection

Risk 1 connects to my Week 5 assumption that staff from all six clinics will be available for testing and training. This became a risk because staff availability has not been guaranteed. If staff are unavailable, it could affect my Week 5 objective that staff at all six clinics complete training by the approved Phase One go-live milestone.

Risk 2 connects to my Week 5 assumption that RCHN's current technical environment can support the new system without a major infrastructure upgrade. This became a risk because the technical environment still needs to be confirmed. If the assumption is wrong, it could affect my Week 5 objective to implement the standardized patient intake and appointment scheduling workflow across all six clinics by the approved Phase One go-live milestone.

---

## Score Justification

For Risk 3, I rated the probability as Medium because moving patient and appointment data creates a possibility of errors that must be validated. I rated the impact as High because inaccurate data could affect testing, clinic operations, patient service, and go-live readiness.

For Risk 5, I rated the probability as Medium because acceptance testing may identify problems that were not found earlier. I rated the impact as High because major defects could require rework, retesting, and could delay the planned deployment.

---

## Risk Reflection

### Highest Priority Risk and Project Impact

My highest-priority threat is **Risk 3** with a course score of **6**. It deserves the most attention because data migration errors could directly affect the accuracy and reliability of the new system. If it occurred, it could affect **quality** by creating incorrect patient or appointment data, **schedule** by requiring additional testing and rework, and **cost** by requiring extra staff time to investigate and correct problems. It could also reduce stakeholder confidence and affect go-live readiness.

### Risk vs. Issue Distinction

After reviewing my five risks, I confirmed that each one is a future uncertainty. Staff may become unavailable, technical upgrades may be required, migration errors may occur, approvals may be delayed, and integrated workflow testing may identify major defects. I verified each entry by checking that it describes an uncertain future event using the If/then format and that the project information does not confirm that the event has already occurred.

The distinction matters because a **risk** is something that may happen and should be monitored and planned for, while an **issue** has already happened and requires immediate action and resolution.

---

*NovaTech Consulting | IT 3310 | Governors State University | Fall 2026*
