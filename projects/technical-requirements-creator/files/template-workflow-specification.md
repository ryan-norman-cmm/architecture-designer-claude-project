# Workflow Specification Template

Use this template for documenting each workflow extracted from the Product Requirements Document.

---

## Workflow ID: W-XXX - [Workflow Name]

**Type**: Main Workflow / Additional Workflow / Workflow Variation
**Source**: PRD Section [X.Y]
**Priority**: High / Medium / Low
**MVP**: Yes / No / TBD

---

### Overview

**Purpose**: [1-2 sentences describing what this workflow accomplishes]

**Trigger**: [What initiates this workflow - user action, system event, scheduled task, etc.]

**Outcome**: [What state/result exists when this workflow completes successfully]

---

### Actors

| Actor | Role | Responsibilities |
|-------|------|------------------|
| [Actor 1] | [User/System/External] | [What they do in this workflow] |
| [Actor 2] | [User/System/External] | [What they do in this workflow] |

---

### Workflow Steps

#### Step 1: [Step Name]

**Actor**: [Who performs this step]

**Action**: [What happens in this step]

**Inputs**:
- [Input 1]: [Description, source]
- [Input 2]: [Description, source]

**Outputs**:
- [Output 1]: [Description, destination]
- [Output 2]: [Description, destination]

**Business Rules**:
- [Rule 1]: [Condition or constraint]
- [Rule 2]: [Condition or constraint]

**FHIR Resources**:
- [Resource 1]: [How it's used - create, read, update, search]
- [Resource 2]: [How it's used - create, read, update, search]

**Error Conditions**:
- [Error 1]: [What happens, how it's handled]
- [Error 2]: [What happens, how it's handled]

---

#### Step 2: [Step Name]

[Repeat structure from Step 1]

---

### Decision Points

| Decision Point | Options | Criteria | Next Step(s) |
|----------------|---------|----------|--------------|
| [Decision 1] | [Option A / Option B] | [What determines the choice] | [Step X / Step Y] |
| [Decision 2] | [Option A / Option B / Option C] | [What determines the choice] | [Step X / Step Y / Step Z] |

---

### Alternative Paths

#### Happy Path (Primary Flow)

Step 1 → Step 2 → Step 3 → Step 4 → Complete

#### Alternative Path 1: [Scenario Name]

**Trigger**: [What causes this alternative path]

**Flow**: Step 1 → Step 2 → Step 3A → Step 5 → Complete

**Rationale**: [Why this path exists]

---

### Error Handling

| Error Scenario | Detection | Response | Recovery |
|----------------|-----------|----------|----------|
| [Error 1] | [How it's detected] | [What the system does] | [How to recover] |
| [Error 2] | [How it's detected] | [What the system does] | [How to recover] |

---

### FHIR Resource Mapping

| Entity | FHIR Resource | Implementation Guide | Profile | Operations |
|--------|---------------|----------------------|---------|------------|
| [Entity 1] | [Resource] | [US Core / Da Vinci / etc] | [Profile name] | Create, Read, Update, Search |
| [Entity 2] | [Resource] | [US Core / Da Vinci / etc] | [Profile name] | Read, Search |

---

### Events Generated

| Event Name | Type | Trigger | Payload | Subscribers |
|------------|------|---------|---------|-------------|
| [Event 1] | [Lifecycle/Business-Critical/Document] | [When it fires] | [What data it carries] | [Who listens] |
| [Event 2] | [Lifecycle/Business-Critical/Document] | [When it fires] | [What data it carries] | [Who listens] |

**Event Derivation Rules**:
- **Lifecycle Events**: Entity created, updated, deleted (only if PRD mentions these)
- **Business-Critical Events**: State changes mentioned in PRD (status changed, submitted, approved, rejected)
- **Document Events**: Uploaded, downloaded, archived (only if PRD specifies document operations)
- **Avoid Routine CRUD**: Don't derive events for every entity update

---

### Technical Requirements

#### Backend Services Needed

| Service | Purpose | Type | Dependencies |
|---------|---------|------|--------------|
| [Service 1] | [What it does] | FHIR / Non-FHIR | [Other services] |
| [Service 2] | [What it does] | FHIR / Non-FHIR | [Other services] |

#### Integration Adapters Needed

| Adapter | Endpoint | Purpose | Protocol | Auth |
|---------|----------|---------|----------|------|
| [Adapter 1] | [External endpoint] | [What it does] | REST / SOAP / HL7 | OAuth / API Key / etc |
| [Adapter 2] | [External endpoint] | [What it does] | REST / SOAP / HL7 | OAuth / API Key / etc |

#### BPM Orchestration

**Workflow Pattern**: [FHIR Task + BPM + BAMOE UI / Custom / etc]

**Orchestration Steps**:
1. [Step 1]: [What BPM orchestrates]
2. [Step 2]: [What BPM orchestrates]
3. [Step 3]: [What BPM orchestrates]

**Human Tasks**:
- [Task 1]: [Who performs it, BAMOE UI or custom]
- [Task 2]: [Who performs it, BAMOE UI or custom]

---

### UI Requirements

| Screen/Component | Purpose | Type | Complexity |
|------------------|---------|------|-----------|
| [Screen 1] | [What it does] | BAMOE / Custom | Low / Med / High |
| [Screen 2] | [What it does] | BAMOE / Custom | Low / Med / High |

---

### Performance Requirements

**Volume**: [Expected transactions per hour/day/month]

**Response Time**: [Target response time for key operations]

**Concurrency**: [Number of simultaneous users/operations]

**Data Volume**: [Expected data growth over time]

---

### Security Requirements

**Authentication**: [How users/systems authenticate]

**Authorization**: [Who can do what]

**Data Privacy**: [PHI/PII handling, HIPAA compliance]

**Audit Logging**: [What gets logged, retention period]

---

### Test Scenarios

#### Scenario 1: Happy Path

**Given**:
- [Precondition 1]
- [Precondition 2]

**When**:
- [Action/trigger]

**Then**:
- [Expected outcome 1]
- [Expected outcome 2]

**And**:
- [Additional verification 1]
- [Additional verification 2]

---

#### Scenario 2: [Failure Path - Error Condition]

**Given**:
- [Precondition leading to failure]

**When**:
- [Action that triggers failure]

**Then**:
- [Expected error response]
- [Expected error handling]

**And**:
- [System state verification]
- [Recovery verification]

---

### Open Questions

| Question | Context | Priority | Resolution |
|----------|---------|----------|------------|
| [Question 1] | [Why it matters] | High/Med/Low | [Answer / TBD] |
| [Question 2] | [Why it matters] | High/Med/Low | [Answer / TBD] |

---

## Workflow Extraction Checklist

Use this checklist when extracting workflows from the PRD:

### Completeness
- [ ] All actors identified and documented
- [ ] All workflow steps captured from PRD
- [ ] All decision points documented with criteria
- [ ] All error/exception paths included
- [ ] All alternative paths captured

### FHIR Mapping
- [ ] Every entity mapped to FHIR resource
- [ ] Implementation guides selected
- [ ] Profiles identified
- [ ] Operations specified (CRUD)

### Event Derivation
- [ ] Lifecycle events derived (if mentioned in PRD)
- [ ] Business-critical state changes captured
- [ ] Document operation events included (if applicable)
- [ ] Routine CRUD events avoided

### Technical Coverage
- [ ] Backend services identified
- [ ] Integration adapters specified
- [ ] BPM orchestration pattern defined
- [ ] UI requirements documented

### Test Coverage
- [ ] Happy path test scenario created
- [ ] Critical failure paths included
- [ ] Given/When/Then/And format used
- [ ] Scenarios are testable and specific

---

## Common Mistakes to Avoid

### ❌ Consolidating Multiple Workflows

**Bad**: "User Management Workflow" (combining create user, update user, delete user into one workflow)

**Good**: Three separate workflows:
- W-001: Create New User Account
- W-002: Update User Profile
- W-003: Deactivate User Account

**Why**: Each has different triggers, actors, steps, and outcomes

---

### ❌ Missing Error Paths

**Bad**: Only documenting the happy path

**Good**: Including error scenarios like:
- API timeout
- Validation failure
- Duplicate submission
- Authorization denial
- External system unavailable

---

### ❌ Vague FHIR Mapping

**Bad**: "Patient resource is used"

**Good**: "Patient resource (US Core profile) - Create new patient record, Search by MRN/name, Update demographics"

---

### ❌ Deriving Too Many Events

**Bad**: Deriving events for every entity update (Patient.Updated, Task.Updated, Observation.Updated, etc.)

**Good**: Only deriving business-critical events mentioned in PRD:
- PriorAuthorization.StatusChanged (approved/denied)
- Document.Uploaded (attestation submitted)
- Notification.Sent (care coordinator alerted)

---

### ❌ Not Specifying Test Scenarios

**Bad**: "Test that the workflow works"

**Good**:
```
Given:
- Care coordinator is authenticated
- Patient has active coverage with Aetna
- Service requires prior authorization

When:
- Care coordinator submits prior authorization request

Then:
- FHIR Task resource created with status "requested"
- BPM workflow initiated
- Request sent to Aetna API

And:
- Care coordinator receives confirmation notification
- Task appears in care coordinator's worklist
```

---

## Template Usage Guide

### When to Use This Template

Use for **every workflow** extracted from the Product Requirements Document:
- Main workflows (core user journeys)
- Additional workflows (supporting processes)
- Workflow variations (different paths through similar flows)

### Filling Out the Template

1. **Start with Overview**: Understand purpose, trigger, outcome before diving into steps

2. **Document Steps**: Capture steps exactly as described in PRD, don't consolidate or simplify yet

3. **Map FHIR Resources**: For healthcare projects, every entity must map to FHIR resource

4. **Derive Events Strategically**: Only derive events mentioned in PRD or critical to business logic

5. **Technical Requirements**: Translate workflow needs into services, adapters, orchestration

6. **Test Scenarios**: Create testable Given/When/Then scenarios for happy path + critical failures

### Validation Before Finalizing

- [ ] Workflow extracted directly from PRD (no consolidation)
- [ ] All steps have FHIR resource mappings (healthcare projects)
- [ ] Events are business-critical (not routine CRUD)
- [ ] Test scenarios cover happy path + critical failures
- [ ] Technical requirements are specific (not vague "needs API")
