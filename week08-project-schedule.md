# Project Schedule: RCHN Patient Intake and Scheduling System

**Consultant:** Adnan Latif  
**Role:** Associate Consultant, Project Manager, NovaTech Consulting  
**Engagement:** Riverside Community Health Network (RCHN)  
**Date:** October 27, 2026  

---

## Work Breakdown Structure

### Grouping 1: Requirements and Workflow Design

- **1.1** Confirm standardized patient intake requirements
- **1.2** Define appointment scheduling workflow
- **1.3** Review clinical workflow requirements and approvals

### Grouping 2: System Development and Configuration

- **2.1** Configure standardized intake fields
- **2.2** Configure appointment scheduling workflow
- **2.3** Configure clinic role permissions and validation rules

### Grouping 3: Testing and Training

- **3.1** Conduct workflow testing across the six clinics
- **3.2** Resolve critical workflow defects
- **3.3** Prepare and deliver staff training

### Grouping 4: Deployment and Support

- **4.1** Prepare go-live support checklist
- **4.2** Deploy the intake and scheduling system to the six clinics
- **4.3** Provide 90-day post-launch support

### WBS Rationale

My WBS reflects the Week 5 Phase One scope by including patient intake workflow standardization, appointment scheduling replacement, staff training, and post-launch support. I organized the work into requirements, development, testing and training, and deployment and support so each major scope area has manageable work packages. Items that were previously considered outside Phase One, such as the patient-facing scheduling portal, billing integration, executive dashboard, and mobile application, are intentionally excluded because they would require a separate scope decision.

---

## Task Dependencies

- Configure standardized intake fields → Test standardized intake workflow, **Finish-to-Start**
- Configure appointment scheduling workflow → Test appointment scheduling workflow, **Finish-to-Start**
- Complete workflow testing → Deploy system to clinics, **Finish-to-Start**

### Dependency Logic

The dependency between configuring the scheduling workflow and testing the scheduling workflow could significantly affect the schedule. If configuration is delayed by two weeks, testing cannot begin as planned. This could also delay workflow acceptance and the deployment milestone. Some preparation work could continue in parallel, but if there is little or no schedule float, the project finish date may need to move unless the team can recover time later.

---

## Activity Schedule

| ID | Activity | Duration (working days) | Predecessors | Start Week |
|---|---|---:|---|---:|
| A | Finalize clinic workflow requirements | 5 | None | 1 |
| B | Configure standardized intake workflow | 10 | A | 2 |
| C | Configure appointment scheduling workflow | 10 | A | 2 |
| D | Conduct integrated workflow testing | 5 | B,C | 4 |

### Scheduling Assumptions

I estimated five working days to finalize workflow requirements, ten working days each to configure the intake and scheduling workflows, and five working days for integrated testing. Activities B and C can begin after the requirements are finalized and can occur at the same time. Testing must wait until both configurations are complete. One uncertainty is how quickly representatives from all six clinics and executive clinical leadership will be available to review or approve workflow decisions. If approvals take longer than expected, the schedule may need to change.

---

## Milestones

### Milestone 1: Core Intake and Scheduling Workflow Configuration Completed

**Target:** End of Project Week 3  

**Exit Criteria:** The standardized intake workflow and appointment scheduling workflow are fully configured and ready for integrated testing.

### Milestone 2: Phase One Workflow Acceptance Completed

**Target:** End of Project Week 5  

**Exit Criteria:** Workflow testing has been completed across the required clinic locations, no critical blocking defects remain, and required clinical workflow approval has been documented.

### Critical Path Analysis

Path A → B → D takes **9 days** because 3 + 4 + 2 = 9 days.

Path A → C → D takes **11 days** because 3 + 6 + 2 = 11 days.

The critical path is **A → C → D**, with a total project duration of **11 days**. If an activity on the critical path slips by two days and there is no available float or schedule recovery, the total project duration could increase to 13 days. This calculation is separate from my preliminary RCHN activity schedule above.

---

## Schedule Reflection

### Scope Connection

The Testing and Training WBS grouping is informed by the Week 5 Phase One scope, which included staff training and standardized intake and scheduling workflows across all six clinics. The lower-level work includes workflow testing, resolving critical defects, and preparing and delivering staff training. These activities help make sure the system works as expected and staff are prepared to use the new process.

### Objective Connection

The Phase One workflow acceptance milestone supports my Week 5 objective of implementing standardized patient intake and appointment scheduling workflows across all six clinics. The milestone provides a clear checkpoint showing that testing has been completed and critical problems have been resolved. The detailed acceptance criteria still need final sponsor approval, and the schedule also assumes clinic staff will be available for testing and review.

---

*NovaTech Consulting | IT 3310 | Governors State University | Fall 2026*
