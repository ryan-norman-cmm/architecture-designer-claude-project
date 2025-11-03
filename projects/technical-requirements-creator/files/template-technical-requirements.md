<!-- AI PROCESSING INSTRUCTIONS - DO NOT OUTPUT THIS SECTION
=================================================================

SECTION COMPLETION GUIDELINES:

Problem & Solution Context:
- Provide technical interpretation of business problem
- Define high-level technical approach
- Identify key technical challenges
- Outline solution architecture

Assumptions:
- Include verbatim from product requirements
- Add 1-2 technical assumptions max
- Focus on what is NOT included
- Examples: data migration scope, integration boundaries

OAuth2 Scopes:
- Only specify roles from product requirements
- Use SMART on FHIR scope patterns
- Context prefixes: patient/, user/, system/
- Action suffixes: .read, .write, .rs, .cruds, .*
- One row per unique scope
- EXCLUDE audit scopes unless critical

Role-based Access Controls:
- One row per control per user role
- User Role from product requirements only
- Data Resource: single resource per control
- Access Level: Read/Write/Full
- Context Restrictions: own patients, organization-scoped, system-wide
- Required Scope: OAuth2 scope for this control
- EXCLUDE audit resources unless critical

Internal Service Dependencies:
- One row per FHIR endpoint to be called
- Use actual FHIR REST API syntax (GET/POST/PUT/DELETE)
- Include search parameters when relevant
- Terminology Server operations for all coding systems
- EXCLUDE audit endpoints unless critical

External System Integrations:
- One row per endpoint called or received
- Outgoing: endpoints we call/send
- Incoming: webhooks/events we receive
- Endpoint Name: descriptive of operation
- Coding systems are NEVER external integrations

GraphQL Requirements:
- List specific operations for frontend
- Map to underlying FHIR/non-FHIR resources
- Queries: data retrieval
- Mutations: data modification
- Use FHIR operation types when directly manipulating FHIR in Aidbox
- Use Non-FHIR for custom business operations

FHIR Resource Mapping:
- Select FHIR resources comprehensively
- Map to appropriate profiles
- Use Task to model workflow states
- Assume US Core unless IG or custom needed
- EXCLUDE audit resources unless critical

Workflow Definitions:
- One row per workflow from product requirements
- Include workflow type, BPM elements, DMN tables
- Count external calls, human tasks, error paths
- Expand user steps into technical orchestration
- Include system-to-system interactions

Decision Tables:
- Every decision point in workflows
- Business rules mentioned or implied
- Label Input: {attribute} and Output: {attribute}
- Always include logical default action

Entity Lifecycle Events - FHIR:
- FHIR-First Approach always
- Use Task for workflow events
- Standard FHIR Interactions: Create, Update, Delete
- Domain-based naming: [domain].[resource].[action]
- Da Vinci ePA: use Task, Claim, ClaimResponse

Entity Lifecycle Events - Non-FHIR:
- Use sparingly - rare exceptions only
- Consider FHIR alternatives first
- Valid cases: system metrics, integration health
- Last resort when FHIR doesn't fit

Event Consumption:
- Focus on FHIR resource lifecycle events
- Include business context
- Cross-service coordination
- Workflow triggers

UI Screen Specifications:
- Only list components in Component Technical Specifications
- List primary data elements (comma separated)
- List user actions (comma separated)
- Assume simplest approach
- DO NOT list components completable in <1 day

Performance Targets:
- Set P50/P99 based on expectations
- Project load based on user volumes
- If volumes not specified, mark "Not specified"

Data Retention:
- DO NOT make assumptions requiring product decision
- Mark as "Not specified" if product decision needed
- PAs: 24 months
- Audit records: 10 years
- Patient data: 5 years
- Make recommendations for other data based on product requirements

Growth Projections:
- Use retention period and growth rate for hot storage
- Use retention + archival rate for cold storage
- Use KB, MB, GB, TB units
- DO NOT list audit, log, infrastructure data

Test Scenarios:
- Create for ALL workflows
- Include happy path for each
- Add failure scenarios for critical paths
- Use Gherkin format

Production Smoke Tests:
- Only most critical workflows (patient/user significantly impacted)
- Capture 1-2 workflows max, never more than 3
- Key checks: comma separated list

Monitoring and Alerting:
- Only metrics unique to this feature
- System monitors (disk, memory, CPU) handled by Platform

Technical Risks:
- Address product-identified risks technically
- Add technical risks discovered (high & critical only)
- Define feasible mitigation strategies

Open Questions:
- Capture questions critical to architecture
- Must result in significant impact to sizing
- Don't capture disaster recovery, auditing, compliance unless unique
- Assume infrastructure handles cross-cutting concerns

================================================================= -->

|                   |                                          |
|-------------------|------------------------------------------|
| **Feature** | [Feature Name] |
| **Purpose** | Convert Product Requirements to Technical Specifications |
| **Target Release** | [Target Release] |
| **Business Rules Document** | |
| **Product Requirements** | |
| **Status** | Draft |
| **Created** | [Date] |
| **Approved** | |
| **Technical Lead** | [Technical Lead] |
| **Product Manager** | [Product Manager] |

## Problem & Solution Context

### Technical Problem Interpretation

|                      |                                                |
|----------------------|------------------------------------------------|
| **Business Problem** | [Technical interpretation of business problem] |
| **High-Level Technical Approach** | [Define high-level technical approach] |
| **Key Technical Challenges** | [Identify key technical challenges] |
| **Solution Architecture** | [Outline solution architecture] |

### Assumptions

- [High-impact product requirement assumption 1 - scope limitation or architectural constraint]
- [High-impact product requirement assumption 2 - scope limitation or architectural constraint]
- [High-impact technical assumption 1 - integration or data boundary]
- [High-impact technical assumption 2 - integration or data boundary]
- [Optional third technical assumption if absolutely critical]

---

## Security & Authentication

### OAuth2 Scopes

| **Scope** | **Purpose** | **User Roles** |
|-----------|-------------|---------------|
| [patient/Patient.read] | [Access patient demographic data] | [Provider, Office Staff] |
| [user/PriorAuth.write] | [Submit prior authorization requests] | [Provider] |
| [system/Benefits.*] | [Full benefits verification access] | [System Admin] |

### Role-based Access Controls

| **User Role** | **Control Name** | **Data Resource** | **Access Level** | **Context Restrictions** | **Required Scope** |
|---------------|------------------|-------------------|------------------|--------------------------|-------------------|
| [Provider] | [View patient data] | [Patient] | [Read] | [Own patients only] | [patient/Patient.read] |
| [Provider] | [Submit PA requests] | [PriorAuth] | [Write] | [Own patients only] | [user/PriorAuth.write] |
| [Care Coordinator] | [View patient data] | [Patient] | [Read] | [Organization-scoped] | [user/Patient.read] |

---

## Service Dependencies & APIs

### Internal Service Dependencies

| **Service** | **FHIR Endpoint** | **Purpose** |
|-------------|-------------------|-------------|
| [Service Name] | [GET /fhir/Patient?name=Smith] | [Purpose] |
| [Service Name] | [POST /fhir/Task] | [Purpose] |
| [Service Name] | [PUT /fhir/Patient/123] | [Purpose] |

### External System Integrations

#### Outgoing Endpoints

| **System** | **Endpoint** | **Type** | **API Type** | **Authentication** | **Purpose** |
|------------|--------------|----------|--------------|--------------------|-------------|
| [System Name] | [Endpoint Name] | [External/Acquisition/Legacy] | [REST/Kafka] | [Auth Type] | [Purpose] |

#### Incoming Endpoints

| **System** | **Endpoint** | **Type** | **API Type** | **Authentication** | **Purpose** |
|------------|--------------|----------|--------------|--------------------|-------------|
| [System Name] | [Endpoint Name] | [External/Acquisition/Legacy] | [Webhook/Kafka] | [Auth Type] | [Purpose] |

### GraphQL Requirements

#### Required Queries

| **Query Name** | **Purpose** | **Data Resources** | **Operation Type** |
|----------------|-------------|-------------------|------------------|
| [Query Name] | [Purpose] | [Data Resources] | [FHIR Read/FHIR Search/Non-FHIR] |

#### Required Mutations

| **Mutation Name** | **Purpose** | **Operation** | **Operation Type** |
|-------------------|-------------|-------------------|------------------|
| [Mutation Name] | [Purpose] | [Operation Name] | [FHIR Create/FHIR Update/FHIR Delete/Non-FHIR] |

---

## Healthcare Standards

### FHIR Resource Mapping

| **Use Case** | **FHIR Resource** | **Profile** | **Customization** |
|--------------|-------------------|-------------|-------------------|
| [Use Case]   | [Resource]        | [Profile]   | [Customization description] |

---

## Workflow & Orchestration

### Workflow Definitions

| **Workflow Name** | **Workflow Type** | **BPM Elements** | **DMN Tables** | **External Calls** | **Human Tasks** | **Error Paths** |
|------------------|------------------|----------------|------------------|----------------|--------------------|-----------------|
| [Workflow Name] | [Type] | [Count/description] | [Count/description] | [Count/description] | [Count/description] | [Count/description] |

### Workflow Details

#### [Workflow Name]

| **Action** | **Actor** | **Error Handling** |
|----------|-------------|--------------------|
| [Action] | [User Role/System] | [Error Action] |
| [Action] | [User Role/System] | [Error Action] |

### Decision Management (DMN Tables)

#### Decision Table: [Decision Name]

| **Input: [Input 1]** | **Input: [Input 2]** | **Output: [Output 1]** | **Output: [Output 2]** | **Action** |
|---------|---------|----------|----------|--------|
| [Value] | [Value] | [Result] | [Result] | [Action] |
| [Value] | [Value] | [Result] | [Result] | [Action] |
| Default | Default | [Default] | [Default] | [Default Action] |

---

## Events

### Entity Lifecycle Events - FHIR

| Event Name | Primary Resource | Trigger Condition | Event Payload | Interaction | FHIRPath Expression |
|------------|------------------|-------------------|---------------|-------------|-------------------|
| task.created | Task | PA workflow initiated | Task resource with status | Create | Task.status = 'requested' |
| task.completed | Task | PA workflow finished | Task resource with outcome | Update | Task.status = 'completed' |
| patient.updated | Patient | Demographics changed | Patient resource | Update | Patient.meta.lastUpdated |

### Entity Lifecycle Events - Non-FHIR

| Event Name | Primary Resource | Trigger Condition | Event Payload | Interaction |
|------------|------------------|-------------------|---------------|-------------|
| [analytics.metric.calculated] | [Analytics Data] | [Performance metric computed] | [Metric results] | [Create] |

### Event Consumption Requirements

#### FHIR Event Consumers

| Consumer Name | Source Event | FHIR Resource | Trigger Condition | Our Response | Business Impact |
|---------------|--------------|---------------|-------------------|--------------|-----------------|
| [PA Status Tracker] | [task.updated] | [Task] | [Task.status changed] | [Update UI status display] | [Providers see real-time PA progress] |

---

## UI Technical Requirements

### Screen Technical Specifications

| **Name** | **Purpose** | **Screen Components** | **Performance Target** |
|----------|-------------|-----------------------|------------------------|
| [Screen Name] | [Purpose] | [Components needed] | [Performance targets] |

### Component Technical Specifications

| **Name** | **Purpose** | **Screen** | **Data Elements** | **User Actions** |
|----------|-------------|------------|-------------------|------------------|
| [Component Name] | [Purpose] | [Screen] | [Data elements] | [User actions] |

---

## Performance & Scale

### Performance Targets

| **User Action** | **P50 Target** | **P99 Target** |
|-------------|------------|------------|
| [Action] | [Target] | [Target] |

### Load Projections

| **Metric** | **Projected Volume** | **Peak** |
|--------|------------------|------|
| [Metric] | [Projection/Not specified] | [Peak/Not specified] |

### Data Retention and Archival

| **Data Type** | **Retention Period** | **Archival Strategy** |
|---------------|----------------------|-----------------------|
| [Data Type] | [Period/Not specified] | [Strategy/Not specified] |

### Growth Projections

| **Data**   | **Storage Growth Rate** | **Hot Storage Requirement** | **Annual Cold Storage Requirement** |
|------------|-------------------------|-----------------------------|-------------------------------------|
| [Data Entity] | [Growth Per Month ]   | [Storage requirement]       | [Annual Storage requirement] |

---

## Testing & Quality

### Test Scenarios

```gherkin
Feature: [Workflow 1 Name]
  Scenario: Happy path for [workflow 1]
    Given [preconditions]
    When [trigger action]
    Then [expected outcome]
    And [verification steps]

  Scenario: Failure scenario for [workflow 1] - [specific failure]
    Given [preconditions]
    When [trigger action]
    And [failure condition occurs]
    Then [expected error handling]
    And [compensation actions]
```

### Production Smoke Tests

| **Workflow**    | **Reason** | **Key Checks** |
|-----------------|------------|----------------|
| [Workflow name] | [Reason for smoke test] | [Key checks] |

### Monitoring and Alerting

| **Metric** | **Alert Threshold** | **Action** |
|------------|---------------------|------------|
| [Metric] | [Threshold] | [Response action] |

---

## Risks & Mitigations

### Technical Risks

| **Risk** | **Identified By** | **Impact** | **Probability** | **Mitigation Strategy** |
|----------|-------------------|------------|-----------------|-------------------------|
| [Product-identified risk]    | [Product/Technology/Other]   | [Impact level] | [Probability] | [Feasible mitigation] |
| [Technical risk discovered]  | [Product/Technology/Other]   | [Impact level] | [Probability] | [Feasible mitigation] |

---

## Open Questions & Requirements Validation

### Critical Architecture Questions

| **Question** | **Impact on Architecture** | **Sizing Impact** | **Need By When** | **Answer** | **Answered By** | **Answered On**|
|--------------|----------------------------|-------------------|------------------|------------|-----------------|----------------|
| [Question]   | [Architecture impact]      | [Sizing impact]   | [Timeline]       |            |                 |                |
