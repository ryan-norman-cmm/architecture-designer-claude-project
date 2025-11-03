# Guide: Recognizing Platform Capabilities

This guide helps you identify vendor-provided capabilities (Aidbox, BAMOE) to avoid estimating work that's already done.

---

## The Problem

Technical estimation often overestimates effort by including vendor-provided capabilities:

**Bad Estimate** ❌:
- Patient Service = 2 weeks (includes CRUD + GraphQL + REST API)
- Task UI = 1 week (includes workflow task list, details, actions)
- **Total: 3 weeks**

**Good Estimate** ✅:
- Patient Service = 0.5 weeks (only custom business logic - Aidbox provides CRUD + GraphQL)
- Task UI = 0 weeks (BAMOE provides workflow UI)
- **Total: 0.5 weeks**

**Savings: 2.5 weeks** (83% reduction!)

---

## Platform Capabilities Overview

### Aidbox (FHIR Server)

Aidbox provides these capabilities **out of the box** (0 weeks estimate):

#### FHIR CRUD Operations
- **Create**: POST /Patient
- **Read**: GET /Patient/{id}
- **Update**: PUT /Patient/{id}
- **Delete**: DELETE /Patient/{id}
- **Search**: GET /Patient?name=Smith&birthdate=1990-01-01

**Estimate**: 0 weeks (Aidbox provides)

---

#### GraphQL Auto-Generation
- Auto-generates GraphQL schema from FHIR resources
- Queries: `PatientList`, `PatientRead`
- Mutations: `PatientCreate`, `PatientUpdate`, `PatientDelete`

**Estimate**: 0 weeks (Aidbox provides)

---

#### FHIR Validation
- Validates resources against FHIR specification
- Validates against profiles (US Core, Da Vinci)
- Custom validation rules via Aidbox constraints

**Estimate**: 0 weeks for standard validation (Aidbox provides)

---

#### Search Parameters
- Standard FHIR search parameters (name, birthdate, identifier, etc.)
- Chained parameters (Patient?general-practitioner.name=Smith)
- Reverse chaining (_has)
- Includes and revIncludes

**Estimate**: 0 weeks for standard searches (Aidbox provides)

---

#### Batch/Transaction Operations
- FHIR Batch (multiple independent operations)
- FHIR Transaction (atomic operations with rollback)

**Estimate**: 0 weeks (Aidbox provides)

---

### BAMOE (Business Automation Manager Open Edition)

BAMOE provides these capabilities **out of the box** (0 weeks estimate):

#### Workflow Task UI
- Task list view (assigned tasks, available tasks)
- Task detail view (task data, forms, history)
- Task actions (claim, start, complete, release, skip)
- Task filtering and sorting
- Task assignment and reassignment

**Estimate**: 0 weeks (BAMOE provides)

---

#### BPM Workflow Engine
- BPMN 2.0 process execution
- Human task management
- Service task orchestration
- Event handling (timers, signals, messages)
- Subprocess support

**Estimate**: 1 week per workflow (orchestration logic only - UI provided)

---

#### Process Monitoring
- Process instance tracking
- Task instance tracking
- Process variables visibility
- Audit logs

**Estimate**: 0 weeks (BAMOE provides)

---

## Recognition Checklist

Use this checklist when estimating components:

### FHIR Services

**Question**: Does this service use FHIR resources as its primary data model?

**If YES → Aidbox provides**:
- [ ] CRUD operations (0 weeks)
- [ ] GraphQL schema auto-generation (0 weeks)
- [ ] Standard FHIR search parameters (0 weeks)
- [ ] FHIR validation (0 weeks)

**Estimate only**:
- Custom business logic not provided by FHIR (weeks vary)
- Custom search parameters not in FHIR spec (0.25 weeks each)
- Custom validation rules beyond FHIR profiles (0.25 weeks each)

**Example**:
```
Patient Service:
- FHIR CRUD: 0 weeks (Aidbox ✓)
- GraphQL: 0 weeks (Aidbox ✓)
- Custom validation (insurance required): 0.25 weeks
- Custom business logic (eligibility check): 0.5 weeks
TOTAL: 0.75 weeks
```

---

### Non-FHIR Services

**Question**: Does this service use custom data models (not FHIR resources)?

**If YES → Full implementation needed**:
- [ ] CRUD operations (2 weeks base)
- [ ] GraphQL subgraph (included in base)
- [ ] Custom search/filters (included in base)
- [ ] Data validation (included in base)

**Example**:
```
Billing Service (non-FHIR):
- CRUD + GraphQL + Validation: 2 weeks base
- Complex pricing rules: +0.5 weeks
TOTAL: 2.5 weeks
```

---

### Integration Adapters

**Question**: Does this adapter connect to an external system?

**Platform does NOT provide external adapters → Full implementation needed**:
- [ ] API client implementation (1 week per endpoint)
- [ ] Authentication (OAuth, API Key, etc.) (included)
- [ ] Error handling and retries (included)
- [ ] Data transformation (included)

**One Adapter Per Endpoint Rule**: Each external endpoint = separate adapter = separate estimate

**Example**:
```
Payer Integration (3 endpoints):
- Submit PA Adapter: 1 week
- Get Status Adapter: 1 week
- Webhook Adapter: 1 week
TOTAL: 3 weeks (NOT 1 week for all)
```

---

### Workflows & Orchestration

**Question**: Does this workflow follow the FHIR Task + BPM + BAMOE UI pattern?

**If YES → BAMOE provides**:
- [ ] Workflow task UI (0 weeks - BAMOE provides)
- [ ] Task management (claim, start, complete) (0 weeks - BAMOE provides)
- [ ] Task list and detail views (0 weeks - BAMOE provides)

**Estimate only**:
- BPM orchestration logic (1 week per workflow)
- FHIR Task state management (0 weeks - Aidbox provides)
- Custom UI for non-workflow screens (1 week per screen)

**Example**:
```
Prior Authorization Workflow:
- FHIR Task resource: 0 weeks (Aidbox ✓)
- BPM orchestration: 1 week
- BAMOE workflow UI: 0 weeks (BAMOE ✓)
TOTAL: 1 week
```

---

### UI Components

**Question**: Is this a workflow task UI (task list, task details, task actions)?

**If YES → BAMOE provides**:
- [ ] Task list view (0 weeks)
- [ ] Task detail view (0 weeks)
- [ ] Task actions (claim, start, complete, etc.) (0 weeks)

**If NO → Custom UI needed**:
- [ ] Custom screen/component (1 week per screen)
- [ ] Complex forms (+0.5 weeks)
- [ ] Data visualization (+0.5 weeks)

**Example**:
```
Prior Authorization UI:
- Task list (care coordinator worklist): 0 weeks (BAMOE ✓)
- Task details (view PA request): 0 weeks (BAMOE ✓)
- Task actions (approve, reject): 0 weeks (BAMOE ✓)
TOTAL: 0 weeks

Custom Dashboard UI:
- Dashboard layout: 1 week
- Charts and graphs: +0.5 weeks
TOTAL: 1.5 weeks
```

---

### GraphQL Subgraphs

**Question**: Is this subgraph for FHIR resources or custom entities?

**If FHIR → Aidbox provides**:
- [ ] GraphQL schema (0 weeks)
- [ ] Queries (0 weeks)
- [ ] Mutations (0 weeks)

**If Custom → Full implementation needed**:
- [ ] GraphQL schema (1 week)
- [ ] Resolvers (included)
- [ ] Federation (included)

**Example**:
```
Patient Subgraph (FHIR):
- Schema + Queries + Mutations: 0 weeks (Aidbox ✓)
TOTAL: 0 weeks

Billing Subgraph (custom):
- Schema + Resolvers + Federation: 1 week
TOTAL: 1 week
```

---

## Real-World Recognition Examples

### Example 1: Patient Service (FHIR)

**Technical Requirements**:
- CRUD operations for Patient resource
- Search patients by name, birthdate, MRN
- GraphQL API for patient queries
- Validate patient data (demographics required)
- Custom rule: Insurance information required

**Platform Capability Analysis**:

| Capability | Provided By | Estimate |
|------------|-------------|----------|
| CRUD operations | Aidbox | 0 weeks |
| Standard search (name, birthdate) | Aidbox | 0 weeks |
| Custom search (MRN) | Aidbox (identifier search) | 0 weeks |
| GraphQL auto-generation | Aidbox | 0 weeks |
| FHIR validation | Aidbox | 0 weeks |
| Custom rule (insurance required) | Custom logic | 0.25 weeks |

**Estimate: 0.25 weeks** (NOT 2 weeks!)

---

### Example 2: Prior Authorization Workflow

**Technical Requirements**:
- Care coordinator submits PA request
- Task assigned to care coordinator
- Care coordinator reviews and approves/rejects
- Task list showing all assigned tasks
- Task detail view with PA information

**Platform Capability Analysis**:

| Capability | Provided By | Estimate |
|------------|-------------|----------|
| FHIR Task resource | Aidbox | 0 weeks |
| BPM orchestration (submit → review → decision) | BAMOE engine | 1 week |
| Task list UI | BAMOE | 0 weeks |
| Task detail UI | BAMOE | 0 weeks |
| Task actions (approve, reject) | BAMOE | 0 weeks |

**Estimate: 1 week** (NOT 3 weeks!)

---

### Example 3: Payer Integration

**Technical Requirements**:
- Submit PA request to payer API
- Get PA status from payer API
- Receive webhook notifications from payer
- OAuth 2.0 authentication
- Error handling and retries

**Platform Capability Analysis**:

| Capability | Provided By | Estimate |
|------------|-------------|----------|
| Submit PA adapter | Custom | 1 week |
| Get Status adapter | Custom | 1 week |
| Webhook adapter | Custom | 1 week |
| OAuth client | Included in adapter | 0 weeks (included) |
| Error handling | Included in adapter | 0 weeks (included) |

**Estimate: 3 weeks** (one adapter per endpoint rule)

**Common Mistake**: Grouping all 3 endpoints into "Payer Integration Adapter" = 1 week ❌

---

### Example 4: Document Management

**Technical Requirements**:
- Upload documents (PDF, images)
- Store documents securely
- Search documents by patient
- Download documents
- Document metadata (type, date, author)

**Platform Capability Analysis**:

| Capability | Provided By | Estimate |
|------------|-------------|----------|
| DocumentReference CRUD | Aidbox | 0 weeks |
| Search by patient | Aidbox | 0 weeks |
| GraphQL API | Aidbox | 0 weeks |
| File storage (S3) | Custom adapter | 1 week |
| Upload/download UI | Custom | 1 week |

**Estimate: 2 weeks** (storage adapter + UI, NOT 4 weeks)

---

## Common Recognition Mistakes

### Mistake 1: Estimating FHIR CRUD ❌

**Bad**:
```
Patient Service:
- Create patient: 0.5 weeks
- Read patient: 0.25 weeks
- Update patient: 0.5 weeks
- Delete patient: 0.25 weeks
TOTAL: 1.5 weeks
```

**Good**:
```
Patient Service:
- FHIR CRUD: 0 weeks (Aidbox ✓)
- Custom validation rule: 0.25 weeks
TOTAL: 0.25 weeks
```

**Impact**: Overestimate by 1.25 weeks

---

### Mistake 2: Estimating GraphQL for FHIR ❌

**Bad**:
```
Patient GraphQL Subgraph:
- Schema design: 0.25 weeks
- Resolvers: 0.5 weeks
- Federation: 0.25 weeks
TOTAL: 1 week
```

**Good**:
```
Patient GraphQL Subgraph:
- Auto-generated by Aidbox: 0 weeks (Aidbox ✓)
TOTAL: 0 weeks
```

**Impact**: Overestimate by 1 week

---

### Mistake 3: Estimating BAMOE Workflow UI ❌

**Bad**:
```
Prior Auth Task UI:
- Task list view: 0.5 weeks
- Task detail view: 0.5 weeks
- Task actions: 0.25 weeks
TOTAL: 1.25 weeks
```

**Good**:
```
Prior Auth Task UI:
- BAMOE provides workflow UI: 0 weeks (BAMOE ✓)
TOTAL: 0 weeks
```

**Impact**: Overestimate by 1.25 weeks per workflow

---

### Mistake 4: Grouping Multiple Endpoints ❌

**Bad**:
```
Payer Integration Adapter (3 endpoints):
- Submit PA, Get Status, Webhook: 1 week
TOTAL: 1 week
```

**Good**:
```
Payer Integration Adapters:
- Submit PA Adapter: 1 week
- Get Status Adapter: 1 week
- Webhook Adapter: 1 week
TOTAL: 3 weeks
```

**Impact**: Underestimate by 2 weeks

---

## Validation Questions

Before finalizing estimates, ask these questions:

### For Services

**Q1**: Is this a FHIR resource?
- YES → Estimate only custom logic (Aidbox provides CRUD + GraphQL)
- NO → Estimate full implementation (2 weeks base)

**Q2**: What custom logic is needed?
- Custom validation rules: 0.25 weeks each
- Custom business logic: 0.5-1 week
- Complex workflows: 1-2 weeks

**Q3**: Are there custom search parameters not in FHIR spec?
- Standard FHIR searches: 0 weeks (Aidbox provides)
- Custom searches: 0.25 weeks each

---

### For Workflows

**Q1**: Does this follow FHIR Task + BPM + BAMOE UI pattern?
- YES → Estimate BPM orchestration only (1 week), UI = 0 weeks
- NO → Estimate custom state management + UI (2+ weeks)

**Q2**: Is the UI workflow-related (task list, task details)?
- YES → 0 weeks (BAMOE provides)
- NO → 1 week per custom screen

**Q3**: Are there human tasks?
- YES → BAMOE provides task management (0 weeks)
- NO → Automated workflow (BPM orchestration only)

---

### For Integration Adapters

**Q1**: How many external endpoints?
- One adapter per endpoint (1 week each)
- Do NOT group multiple endpoints into one adapter

**Q2**: Is this enhancing an existing adapter?
- YES → 0.5 weeks (50% of new effort)
- NO → 1 week (new adapter)

**Q3**: Is authentication standard (OAuth, API Key)?
- YES → Included in adapter estimate (0 weeks)
- NO → +0.5 weeks for custom auth

---

### For UI Components

**Q1**: Is this a workflow task UI?
- YES → 0 weeks (BAMOE provides)
- NO → Continue to Q2

**Q2**: What type of custom UI?
- Simple form/display: 1 week
- Complex form: 1.5 weeks
- Data visualization (charts, graphs): 1.5 weeks
- Dashboard: 1.5-2 weeks

---

### For GraphQL Subgraphs

**Q1**: Is this for FHIR resources?
- YES → 0 weeks (Aidbox auto-generates)
- NO → 1 week (custom subgraph)

**Q2**: Are there custom resolvers beyond basic CRUD?
- YES → +0.25 weeks per complex resolver
- NO → Use base estimate

---

## Quick Reference

### Platform Capability Checklist

**Aidbox Provides (0 weeks)**:
- ✅ FHIR CRUD operations
- ✅ FHIR validation
- ✅ Standard FHIR search parameters
- ✅ GraphQL auto-generation for FHIR resources
- ✅ Batch/transaction operations
- ✅ FHIR Task resource

**BAMOE Provides (0 weeks)**:
- ✅ BPM workflow engine
- ✅ Workflow task UI (task list, details, actions)
- ✅ Task management (claim, start, complete, release)
- ✅ Process monitoring and tracking

**You Must Estimate (weeks vary)**:
- ❌ Custom business logic
- ❌ Custom validation rules (beyond FHIR)
- ❌ BPM orchestration logic (BAMOE engine runs it, you write it)
- ❌ Integration adapters (one per endpoint)
- ❌ Custom UI (non-workflow screens)
- ❌ Non-FHIR services (full implementation)
- ❌ Custom GraphQL subgraphs (non-FHIR)

---

## Summary

**The Goal**: Recognize vendor-provided capabilities to avoid over-estimating effort.

**The Rule**: If Aidbox or BAMOE provides it, estimate = 0 weeks.

**The Test**: Before estimating any component, ask:
1. Does Aidbox provide this? (FHIR CRUD, GraphQL, validation)
2. Does BAMOE provide this? (Workflow UI, task management)
3. Is this one adapter per endpoint? (NOT grouped)

If you can answer these questions → you'll avoid 90% of estimation mistakes ✅

**Common Savings**:
- FHIR Service: 1.5-2 weeks saved per service
- Workflow UI: 1-1.5 weeks saved per workflow
- GraphQL: 1 week saved per FHIR subgraph

**Total Potential Savings**: 30-50% of initial estimate by recognizing platform capabilities!
