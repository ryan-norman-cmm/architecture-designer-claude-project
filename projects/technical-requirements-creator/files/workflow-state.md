# Technical Requirements Analysis Workflow State

Use this template to track your technical requirements analysis progress.

---

## Feature Information

**Feature Name**: [Name]
**Product Requirements Version**: [Version]
**Start Date**: [Date]
**Target MVP Date**: [Date]

---

## Current Status

**Current Step**: [1-8] - [Step Name]
**Last Action**: [What was just completed]
**Next Action**: [What to do next]

---

## Step Progress

| Step | Status | Completed | Notes |
|------|--------|-----------|-------|
| 1. Complete Document Review | âš«ï¸ Pending / âœ… Complete | [Date] | [Documents read] |
| 2. Extract Workflows | âš«ï¸ Pending / âœ… Complete | [Date] | [Workflow count] |
| 3. Map Healthcare Standards | âš«ï¸ Pending / âœ… Complete | [Date] | [FHIR resources mapped] |
| 4. Derive Entity Events | âš«ï¸ Pending / âœ… Complete | [Date] | [Events derived] |
| 5. Design Technical Solution | âš«ï¸ Pending / âœ… Complete | [Date] | [Solution designed] |
| 6. Create Test Scenarios | âš«ï¸ Pending / âœ… Complete | [Date] | [Scenarios created] |
| 7. Document Technical Decisions | âš«ï¸ Pending / âœ… Complete | [Date] | [Decisions tagged] |
| 8. Final Quality Check | âš«ï¸ Pending / âœ… Complete | [Date] | [Validation passed] |

---

## Workflows Extracted

| ID | Workflow Name | Type | Source Section | Status |
|----|---------------|------|----------------|--------|
| W001 | [Name] | Main/Additional/Variation | PRD Section X | âœ… Extracted |
| W002 | [Name] | Main/Additional/Variation | PRD Section Y | âœ… Extracted |
| W003 | [Name] | Main/Additional/Variation | PRD Section Z | âœ… Extracted |

**Total Workflows**: [X] (Main: [X], Additional: [X], Variations: [X])

---

## FHIR Resource Mappings

| Entity | FHIR Resource | Implementation Guide | Coding System | Status |
|--------|---------------|----------------------|---------------|--------|
| [Entity 1] | [Resource] | [US Core / Da Vinci / etc] | [ICD-10 / CPT / etc] | âœ… Mapped |
| [Entity 2] | [Resource] | [US Core / Da Vinci / etc] | [ICD-10 / CPT / etc] | âœ… Mapped |
| [Entity 3] | [Resource] | [US Core / Da Vinci / etc] | [ICD-10 / CPT / etc] | âœ… Mapped |

---

## Entity Events Derived

| Entity | Events | Type | Status |
|--------|--------|------|--------|
| [Entity 1] | Created, Updated, Deleted | Lifecycle | âœ… Derived |
| [Entity 2] | Status Changed, Submitted | Business-Critical | âœ… Derived |
| [Entity 3] | Uploaded, Downloaded | Document Ops | âœ… Derived |

**Total Events**: [X] (Lifecycle: [X], Business-Critical: [X], Document: [X])

---

## Technical Decisions

| Decision | Tag | Choice | Rationale | Date |
|----------|-----|--------|-----------|------|
| [Decision 1] | [Recommended] | [Choice] | [Why] | [Date] |
| [Decision 2] | [Inferred] | [Choice] | [Why] | [Date] |
| [Decision 3] | [Standard] | [Choice] | [Why] | [Date] |

---

## Services & APIs

| Service Type | Count | Examples |
|--------------|-------|----------|
| Backend Services | [X] | [Service 1, Service 2] |
| Integration Adapters | [X] | [Adapter 1, Adapter 2] |
| FHIR Endpoints | [X] | [Endpoint 1, Endpoint 2] |
| BPM Workflows | [X] | [Workflow 1, Workflow 2] |

---

## Test Scenarios Created

| Workflow | Scenarios | Coverage | Status |
|----------|-----------|----------|--------|
| [Workflow 1] | [X] Given/When/Then | Happy path + [X] failures | âœ… Complete |
| [Workflow 2] | [X] Given/When/Then | Happy path + [X] failures | âœ… Complete |

**Total Scenarios**: [X] (Happy path: [X], Failure paths: [X])

---

## Sections Marked N/A

| Section | Reason | Date |
|---------|--------|------|
| Data Migration | No legacy data to migrate | [Date] |
| External Integrations | Fully internal system | [Date] |

---

## Refinements Made

| Date | Section | Change | Reason |
|------|---------|--------|--------|
| [Date] | Workflow W003 | Added error handling steps | Missed in PRD, inferred from requirements |
| [Date] | Patient Entity | Changed from Patient to Person | Broader scope needed |
| [Date] | Event Catalog | Added Notification.Sent event | Business-critical lifecycle |

---

## Open Questions

| Question | Context | Priority | Resolution |
|----------|---------|----------|------------|
| [Question 1] | [Which workflow/entity] | High/Med/Low | [Answer / TBD] |
| [Question 2] | [Technical detail needed] | High/Med/Low | [Answer / TBD] |

---

## Quality Checklist

### Document Review
- [ ] Read entire product requirements document
- [ ] Read entire Platform Capabilities document
- [ ] Read entire FHIR Resources document
- [ ] Listed ALL workflows (main, additional, variations)
- [ ] Identified every entity needing CRUD operations

### Workflow Extraction
- [ ] Every process in "Main Workflow" captured
- [ ] Every process in "Additional Workflow" captured
- [ ] Every variation captured as separate workflow
- [ ] Every decision path documented
- [ ] Every error/exception path captured

### Standards Mapping
- [ ] All entities mapped to FHIR resources
- [ ] Implementation guides selected
- [ ] Coding systems mapped
- [ ] Integration patterns defined

### Event Derivation
- [ ] Notification events from PRD captured
- [ ] Key entity lifecycle events derived
- [ ] Business-critical state changes documented
- [ ] Routine CRUD events avoided

### Technical Solution
- [ ] User workflows converted to BPM orchestration
- [ ] Data needs mapped to services/APIs
- [ ] Performance SLAs defined
- [ ] Security boundaries defined
- [ ] Only specified technologies included

### Test Scenarios
- [ ] Test scenarios cover all workflows
- [ ] Critical failure paths included
- [ ] Acceptance criteria testable
- [ ] Error handling specified

### Documentation
- [ ] [Recommended] tags on suggestions
- [ ] [Inferred] tags on derived requirements
- [ ] [Derived] tags on implicit events
- [ ] "Not specified" used appropriately
- [ ] "Not Applicable" with reasons

---

## Completion Status

**Document Status**: âš«ï¸ Draft / âœ… Complete
**Clean Output Generated**: âš«ï¸ No / âœ… Yes (template instructions removed)
**Final Review Date**: [Date]
**Approved By**: [Name]
**Version**: [X.Y]

---

## Notes

[Additional notes, context, or observations about the technical requirements analysis]
