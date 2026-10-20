# Product Backlog: RCHN Patient Intake and Scheduling System

**Consultant:** Adnan Latif  
**Role:** Associate Consultant, NovaTech Consulting  
**Engagement:** Riverside Community Health Network (RCHN)  
**Date:** October 20, 2026  

---

## User Story 1

**User Story:**  
As a front desk staff member, I want to use the same required patient intake fields at all six RCHN clinics, so that I can collect complete and consistent patient information regardless of the clinic location.

**Acceptance Criteria:**
- Given a staff member opens a new patient intake form, when the form loads, then the same required core fields are displayed at all six clinics.
- Given a required field is empty, when the staff member attempts to submit the form, then the system identifies the missing field.

**Story Points:** 5  
**MoSCoW Priority:** Must Have

---

## User Story 2

**User Story:**  
As a scheduling staff member, I want to see available appointment times for the selected clinic, so that I can schedule patients accurately without choosing an unavailable time.

**Acceptance Criteria:**
- Given a clinic and date are selected, when the staff member views appointment availability, then the system displays the available appointment times.
- Given an appointment slot is already booked, when availability is displayed, then that time is not shown as available.

**Story Points:** 8  
**MoSCoW Priority:** Must Have

---

## User Story 3

**User Story:**  
As a front desk staff member, I want the system to identify missing required intake information, so that I can correct incomplete information before submitting the patient intake.

**Acceptance Criteria:**
- Given one or more required fields are incomplete, when the staff member attempts to submit the intake form, then the system identifies each missing field.
- Given all required fields are complete, when the staff member submits the form, then the system allows the intake process to continue.

**Story Points:** 3  
**MoSCoW Priority:** Should Have

---

## User Story 4

**User Story:**  
As a front desk staff member, I want to confirm the correct patient record before making changes, so that I can avoid updating information on the wrong patient.

**Acceptance Criteria:**
- Given a staff member searches for a patient, when matching records are displayed, then enough identifying information is shown to confirm the correct patient.
- Given the patient has not been confirmed, when the staff member attempts to change patient information, then the system requires confirmation first.

**Story Points:** 5  
**MoSCoW Priority:** Must Have

---

## User Story 5

**User Story:**  
As a patient, I want to schedule my own appointment through an online portal, so that I can choose an appointment time without calling the clinic.

**Acceptance Criteria:**
- Given a patient is using the online portal, when available appointments are displayed, then the patient can select an available time.
- Given an appointment is successfully scheduled, when the booking is completed, then the patient receives confirmation.

**Story Points:** 13  
**MoSCoW Priority:** Won't Have This Time

---

## Prioritization Rationale

### Must Have Justification

I marked the standardized patient intake fields story as Must Have because RCHN needs a consistent intake process across all six clinics. Earlier user research showed that different clinic processes create confusion and make daily work less efficient. Standardizing the required intake fields supports the Phase One scope and gives staff a consistent process to follow. This does not automatically mean the story must be completed in Sprint 1, but it is essential to the current product direction because the new system is intended to improve consistency and reliability across RCHN.

### Won't Have Rationale

I marked the patient-facing online scheduling portal as Won't Have This Time because it was excluded from the recommended Phase One scope. The current priority is improving RCHN's internal patient intake and scheduling workflows before adding a new patient-facing system. The portal would introduce additional design, privacy, security, testing, and support requirements. It could be reconsidered after the core system is stable or if the project sponsor approves a scope change and the team confirms the additional resources and requirements needed.

---

## Backlog Reflection

### Persona Connection

User Story 1, which standardizes the required intake fields across all six clinics, is supported by the Week 3 front desk persona. Maya Rodriguez needs a consistent workflow because different clinic processes, unnecessary steps, and workarounds make patient intake and scheduling more difficult. This story addresses that need by giving staff a common set of required intake fields across RCHN while creating a more predictable workflow.

### Scope Connection

User Story 2, which allows scheduling staff to see available appointment times, connects directly to the Week 5 Phase One scope because appointment scheduling system replacement was identified as in scope. The scope established the overall need to replace scheduling, while this backlog story gives the Developers a more specific capability to build and test. It explains who needs the feature, what information should be displayed, and how the team can verify that unavailable appointment times are not presented as available.

---

*NovaTech Consulting | IT 3310 | Governors State University | Fall 2026*
