<!-- AI PROCESSING INSTRUCTIONS - DO NOT OUTPUT THIS SECTION
=================================================================

SECTION COMPLETION GUIDELINES:

Metadata Section:
- Initiative Name: Clear, outcome-focused name
- Initiative ID: Tracking identifier (INIT-XXX format)
- Total Releases: Count of all releases (MVP + CONDITIONAL + DEFER)
- Target Release: Overall initiative target (MVP Phase 1, MVP Phase 2, etc.)
- Dates: Use YYYY-MM-DD format

Release Overview - Summary Table:
- One row per release (REL-001, REL-002, etc.)
- Sequence: Delivery order (1 = first deployed)
- Priority: Composite score 0-10 (weighted by value, risk, dependency, learning)
- User Capability: One sentence - what users can NOW do
- Category: MVP (must have), CONDITIONAL (data-driven decision), DEFER (future)
- Dependencies: Brief summary (e.g., "REL-001", "None - Foundation")

Release Overview - Delivery Timeline:
- Create Mermaid Gantt chart showing release sequence
- Include decision gates after key releases
- Show critical path and parallel work
- Mark CONDITIONAL releases visually distinct
- Use realistic timeframes (not placeholder "1w")

Release Overview - Release Dependencies:
- Create Mermaid graph showing release relationships
- Use decision gates (diamonds) for proceed/skip decisions
- Show external blockers as separate nodes
- Color code: MVP (red), CONDITIONAL (orange), gates (orange), complete (blue)
- Include pivot/skip paths for conditional releases

Key Insights Section:
- Fastest Path: Describe quickest route to core value (specific REL IDs)
- Optional Enhancements: List CONDITIONAL/DEFER releases and what they add
- Critical Blockers: List external dependencies with owning teams
- Decision Gates: Describe proceed/skip criteria after key releases

Detailed Releases:
- One full section per release
- Category: Choose MVP, CONDITIONAL, or DEFER
- Priority Score: 0-10 with scoring breakdown
- Value Summary: One sentence max - specific user outcome
- User Capabilities: 3-5 bullet points of what users can DO (verbs, not features)
- Key Exclusions: What's NOT in this release and why
- Hypothesis: What assumption we're testing (testable, falsifiable)
- Success Criteria: Data that proves hypothesis valid
- Key Metrics: 2-4 metrics with targets and measurement frequency
- Technical Overview: Brief list of integrations, FHIR resources, workflows
- Biggest Risk: Primary technical/business risk with mitigation
- Dependencies: Prerequisites and blocking items
- Sequencing Rationale: One sentence why this release is sequenced here

Scoring Breakdown (calculate priority):
- User Value: 0-10 (business value and user impact)
- Dependency Minimal: 0-10 (fewer dependencies = higher score)
- Technical Risk Reduction: 0-10 (reduces uncertainty = higher score)
- Learning Potential: 0-10 (validates critical assumptions = higher score)
- Priority Score: Average of four dimensions

Category Assignment Rules:
- MVP: Must have for basic functionality; enables core user value
- CONDITIONAL: Build based on validation data; proceed/skip decision after prerequisite
- DEFER: Nice to have; explicitly postponed to future phase

Release Sequencing Logic:
- Foundation releases first (enable other work)
- High learning potential early (validate assumptions)
- Technical risk reduction prioritized (de-risk architecture)
- Dependency-light releases preferred (reduce coordination)
- User value balanced with technical necessity

Validation Metrics:
- Leading indicators: User behavior, feature adoption, engagement
- Lagging indicators: Business outcomes, satisfaction scores
- Frequency: daily (high urgency), weekly (normal), end_of_release (low urgency)
- Targets: Specific percentages or thresholds

Technical Surface:
- List major components for scope clarity (not detailed sizing)
- FHIR resources involved
- Key integrations required
- Workflows orchestrated
- Biggest risk with mitigation strategy

Deployment Approach:
- feature_flag: Gradual rollout with toggle control
- beta_practices: Limited user group testing
- gradual_rollout: Percentage-based deployment
- full_release: All users immediately

================================================================= -->
|                     |        |
|---------------------|--------|
| **Initiative Name** | [Name] |
| **Initiative ID** | [ID] |
| **Total Releases** | [Number] |
| **Target Release** | [MVP Phase] |
| **Created** | [YYYY-MM-DD] |
| **Last Updated** | [YYYY-MM-DD] |

---

## Release Overview

### Summary Table

| ID | Name | Sequence | Priority | User Capability | Category | Dependencies |
|---|---|---|---|---|---|---|
| REL-001 | [Name] | 1 | 10.0 | [What users can now do] | MVP | None - Foundation |
| REL-002 | [Name] | 2 | 9.0 | [What users can now do] | MVP | REL-001 |
| REL-003 | [Name] | 3 | 8.0 | [What users can now do] | CONDITIONAL | REL-002 |
| REL-004 | [Name] | 4 | 7.0 | [What users can now do] | MVP | REL-002 |
| REL-005 | [Name] | 5 | 6.0 | [What users can now do] | MVP | REL-004 |

### Delivery Timeline

```mermaid
gantt
    title Release Delivery Sequence
    dateFormat X
    axisFormat %s

    section Foundation
    REL-001 Foundation Release    :done, rel1, 0, 1w

    section Core Workflow
    REL-002 Core Capability          :active, rel2, after rel1, 3w

    section Conditional
    REL-003 Optional Enhancement (CONDITIONAL)   :crit, rel3, after rel2, 2w

    section Enhancements
    REL-004 Enhancement A                  :rel4, after rel2, 2w
    REL-005 Enhancement B              :rel5, after rel4, 1w

    section Decision Gates
    Gate 1 Foundation Validation               :milestone, gate1, after rel1, 0d
    Gate 2 Core Workflow Validation       :milestone, gate2, after rel2, 0d
    Gate 3 Enhancement A Validation               :milestone, gate3, after rel4, 0d
    Gate 4 Conditional Decision              :milestone, gate4, after rel5, 0d
```

### Release Dependencies

```mermaid
graph TD
    START([Initiative<br/>Initiative ID])
    style START fill:#E9F4FB,stroke:#00426A,stroke-width:3px,color:#00426A

    REL1[REL-001<br/>Foundation Release<br/>Core Capability]
    style REL1 fill:#FFE5EF,stroke:#E70665,stroke-width:2px,color:#00426A

    GATE1{Success Criteria<br/>Met?}
    style GATE1 fill:#FFF4E9,stroke:#FF8F1D,stroke-width:3px,color:#00426A

    REL2[REL-002<br/>Core Workflow<br/>Primary Value]
    style REL2 fill:#FFE5EF,stroke:#E70665,stroke-width:2px,color:#00426A

    GATE2{Adoption Target<br/>Met?<br/>Error Rate<br/>Acceptable?}
    style GATE2 fill:#FFF4E9,stroke:#FF8F1D,stroke-width:3px,color:#00426A

    REL4[REL-004<br/>Enhancement A<br/>Supporting Capability]
    style REL4 fill:#FFE5EF,stroke:#E70665,stroke-width:2px,color:#00426A

    GATE3{Usage Target<br/>Met?}
    style GATE3 fill:#FFF4E9,stroke:#FF8F1D,stroke-width:3px,color:#00426A

    REL5[REL-005<br/>Enhancement B<br/>Additional Value]
    style REL5 fill:#FFE5EF,stroke:#E70665,stroke-width:2px,color:#00426A

    GATE4{Conditional Criteria<br/>Validated?<br/>OR User Requests?}
    style GATE4 fill:#FFF4E9,stroke:#FF8F1D,stroke-width:3px,color:#00426A

    REL3[REL-003<br/>Conditional Feature<br/>CONDITIONAL]
    style REL3 fill:#FFF4E9,stroke:#FF8F1D,stroke-width:2px,color:#00426A

    COMPLETE([MVP Complete])
    style COMPLETE fill:#E9F4FB,stroke:#1E91D6,stroke-width:3px,color:#00426A

    PIVOT1([Pivot:<br/>Alternative Approach])
    style PIVOT1 fill:#FEE6F0,stroke:#E70665,stroke-width:2px,color:#E70665

    PIVOT2([Investigate:<br/>Root Cause Analysis])
    style PIVOT2 fill:#FEE6F0,stroke:#E70665,stroke-width:2px,color:#E70665

    PIVOT3([Simplify:<br/>Reduce Scope])
    style PIVOT3 fill:#FEE6F0,stroke:#E70665,stroke-width:2px,color:#E70665

    SKIP3([Skip Conditional:<br/>Not Needed])
    style SKIP3 fill:#E9F4FB,stroke:#1E91D6,stroke-width:2px,color:#00426A

    START --> REL1
    REL1 --> GATE1
    GATE1 -->|YES| REL2
    GATE1 -->|NO| PIVOT1

    REL2 --> GATE2
    GATE2 -->|YES| REL4
    GATE2 -->|NO| PIVOT2

    REL4 --> GATE3
    GATE3 -->|YES| REL5
    GATE3 -->|NO| PIVOT3

    REL5 --> GATE4
    GATE4 -->|YES| REL3
    GATE4 -->|NO| SKIP3

    REL3 --> COMPLETE
    SKIP3 --> COMPLETE

    BLOCK1[External Dependency 1<br/>Required Service]
    style BLOCK1 fill:#F5F5F5,stroke:#666,stroke-width:2px,color:#333

    BLOCK2[External Dependency 2<br/>Integration Requirement]
    style BLOCK2 fill:#F5F5F5,stroke:#666,stroke-width:2px,color:#333

    BLOCK3[External Dependency 3<br/>Configuration Needed]
    style BLOCK3 fill:#F5F5F5,stroke:#666,stroke-width:2px,color:#333

    BLOCK4[External Dependency 4<br/>Approval Required]
    style BLOCK4 fill:#F5F5F5,stroke:#666,stroke-width:2px,color:#333

    BLOCK1 -.->|Blocks| REL1
    BLOCK1 -.->|Blocks| REL2
    BLOCK2 -.->|Blocks| REL2
    BLOCK3 -.->|Blocks| REL4
    BLOCK3 -.->|Blocks| REL5
    BLOCK4 -.->|Blocks| REL3
```

### Key Insights

**Fastest Path to Value**:
[Description of quickest route to core value - typically REL-001 → REL-002 → REL-004 → REL-005]

**Optional Enhancements**:
- **REL-003**: [What this adds and when to consider it]

**Critical Blockers**:
- **[Blocker name]**: [Description] - Blocks [REL-XXX] - Owner: [Team]

**Decision Gates**:
- **After REL-001**: [Decision criteria for proceeding]
- **After REL-002**: [Decision criteria for proceeding]

---

## Detailed Releases

---

### REL-001: [Release Name]

**Category**: MVP | CONDITIONAL | DEFER
**Priority**: 10.0 / 10.0

#### Value Summary
[One sentence: what user value is delivered]

#### User Capabilities
**What users can now do**:
1. [Capability]
2. [Capability]
3. [Capability]
4. [Capability]
5. [Capability]

#### Key Exclusions
- **[Excluded capability]** → Deferred to REL-XXX because [reason]
- **[Excluded capability]** → Not planned because [reason]

#### Hypothesis & Validation

**Hypothesis**: [What we're testing - specific, testable, falsifiable]

**Success Criteria**: [What proves this worked]

**Key Metrics**:
- [Metric]: Target [X%] measured [frequency]
- [Metric]: Target [X%] measured [frequency]
- [Metric]: Target [X%] measured [frequency]

#### Technical Overview

**Integrations**: [System 1], [System 2], [System 3]

**FHIR Resources**: [Resource 1], [Resource 2], [Resource 3]

**Workflows**: [Workflow 1], [Workflow 2]

**Biggest Risk**: [Primary risk] → Mitigation: [How we'll address it]

#### Scoring Breakdown
- **User Value**: [0-10]
- **Dependency Minimal**: [0-10]
- **Technical Risk Reduction**: [0-10]
- **Learning Potential**: [0-10]

#### Dependencies

**Prerequisite Releases**: [REL-XXX] or None - Foundation

**Blocking Items**:
- [External dependency] - Impact: [Description] - Owner: [Team]

**Parallel Releases**: [REL-XXX, REL-XXX] (can be developed concurrently)

**Sequencing Rationale**: [One sentence: why this release is sequenced here]

#### Deployment

**Approach**: feature_flag | beta_practices | gradual_rollout | full_release

**Rollback Criteria**:
- [Criterion for rollback decision]
- [Criterion for rollback decision]

---

### REL-002: [Release Name]

**Category**: MVP | CONDITIONAL | DEFER
**Priority**: 9.0 / 10.0

#### Value Summary
[One sentence: what user value is delivered]

#### User Capabilities
**What users can now do**:
1. [Capability]
2. [Capability]
3. [Capability]
4. [Capability]

#### Key Exclusions
- **[Excluded capability]** → Deferred to REL-XXX because [reason]
- **[Excluded capability]** → Not planned because [reason]

#### Hypothesis & Validation

**Hypothesis**: [What we're testing - specific, testable, falsifiable]

**Success Criteria**: [What proves this worked]

**Key Metrics**:
- [Metric]: Target [X%] measured [frequency]
- [Metric]: Target [X%] measured [frequency]

#### Technical Overview

**Integrations**: [System 1], [System 2]

**FHIR Resources**: [Resource 1], [Resource 2]

**Workflows**: [Workflow 1]

**Biggest Risk**: [Primary risk] → Mitigation: [How we'll address it]

#### Scoring Breakdown
- **User Value**: [0-10]
- **Dependency Minimal**: [0-10]
- **Technical Risk Reduction**: [0-10]
- **Learning Potential**: [0-10]

#### Dependencies

**Prerequisite Releases**: REL-XXX

**Blocking Items**:
- [External dependency] - Impact: [Description] - Owner: [Team]

**Parallel Releases**: [REL-XXX, REL-XXX] (can be developed concurrently)

**Sequencing Rationale**: [One sentence: why this release is sequenced here]

#### Deployment

**Approach**: feature_flag | beta_practices | gradual_rollout | full_release

**Rollback Criteria**:
- [Criterion for rollback decision]
- [Criterion for rollback decision]

---

### REL-003: [Release Name]

**Category**: MVP | CONDITIONAL | DEFER
**Priority**: 8.0 / 10.0

#### Value Summary
[One sentence: what user value is delivered]

#### User Capabilities
**What users can now do**:
1. [Capability]
2. [Capability]
3. [Capability]

#### Key Exclusions
- **[Excluded capability]** → Deferred to REL-XXX because [reason]
- **[Excluded capability]** → Not planned because [reason]

#### Hypothesis & Validation

**Hypothesis**: [What we're testing - specific, testable, falsifiable]

**Success Criteria**: [What proves this worked]

**Key Metrics**:
- [Metric]: Target [X%] measured [frequency]
- [Metric]: Target [X%] measured [frequency]

**Failure Action**: [What happens if hypothesis proves wrong]

#### Technical Overview

**Integrations**: [System 1], [System 2]

**FHIR Resources**: [Resource 1], [Resource 2]

**Workflows**: [Workflow 1]

**Biggest Risk**: [Primary risk] → Mitigation: [How we'll address it]

#### Scoring Breakdown
- **User Value**: [0-10]
- **Dependency Minimal**: [0-10]
- **Technical Risk Reduction**: [0-10]
- **Learning Potential**: [0-10]

#### Dependencies

**Prerequisite Releases**: REL-XXX

**Blocking Items**:
- [External dependency] - Impact: [Description] - Owner: [Team]

**Parallel Releases**: [REL-XXX, REL-XXX] (can be developed concurrently)

**Sequencing Rationale**: [One sentence: why this release is sequenced here]

#### Deployment

**Approach**: feature_flag | beta_practices | gradual_rollout | full_release

**Rollback Criteria**:
- [Criterion for rollback decision]
- [Criterion for rollback decision]

---

### REL-004: [Release Name]

**Category**: MVP | CONDITIONAL | DEFER
**Priority**: 7.0 / 10.0

#### Value Summary
[One sentence: what user value is delivered]

#### User Capabilities
**What users can now do**:
1. [Capability]
2. [Capability]
3. [Capability]

#### Key Exclusions
- **[Excluded capability]** → Deferred to REL-XXX because [reason]
- **[Excluded capability]** → Not planned because [reason]

#### Hypothesis & Validation

**Hypothesis**: [What we're testing - specific, testable, falsifiable]

**Success Criteria**: [What proves this worked]

**Key Metrics**:
- [Metric]: Target [X%] measured [frequency]
- [Metric]: Target [X%] measured [frequency]

#### Technical Overview

**Integrations**: [System 1], [System 2]

**FHIR Resources**: [Resource 1], [Resource 2]

**Workflows**: [Workflow 1]

**Biggest Risk**: [Primary risk] → Mitigation: [How we'll address it]

#### Scoring Breakdown
- **User Value**: [0-10]
- **Dependency Minimal**: [0-10]
- **Technical Risk Reduction**: [0-10]
- **Learning Potential**: [0-10]

#### Dependencies

**Prerequisite Releases**: REL-XXX

**Blocking Items**:
- [External dependency] - Impact: [Description] - Owner: [Team]

**Parallel Releases**: [REL-XXX, REL-XXX] (can be developed concurrently)

**Sequencing Rationale**: [One sentence: why this release is sequenced here]

#### Deployment

**Approach**: feature_flag | beta_practices | gradual_rollout | full_release

**Rollback Criteria**:
- [Criterion for rollback decision]
- [Criterion for rollback decision]

---

### REL-005: [Release Name]

**Category**: MVP | CONDITIONAL | DEFER
**Priority**: 6.0 / 10.0

#### Value Summary
[One sentence: what user value is delivered]

#### User Capabilities
**What users can now do**:
1. [Capability]
2. [Capability]
3. [Capability]

#### Key Exclusions
- **[Excluded capability]** → Deferred to REL-XXX because [reason]
- **[Excluded capability]** → Not planned because [reason]

#### Hypothesis & Validation

**Hypothesis**: [What we're testing - specific, testable, falsifiable]

**Success Criteria**: [What proves this worked]

**Key Metrics**:
- [Metric]: Target [X%] measured [frequency]
- [Metric]: Target [X%] measured [frequency]

#### Technical Overview

**Integrations**: [System 1], [System 2]

**FHIR Resources**: [Resource 1], [Resource 2]

**Workflows**: [Workflow 1]

**Biggest Risk**: [Primary risk] → Mitigation: [How we'll address it]

#### Scoring Breakdown
- **User Value**: [0-10]
- **Dependency Minimal**: [0-10]
- **Technical Risk Reduction**: [0-10]
- **Learning Potential**: [0-10]

#### Dependencies

**Prerequisite Releases**: REL-XXX

**Blocking Items**:
- [External dependency] - Impact: [Description] - Owner: [Team]

**Parallel Releases**: [REL-XXX, REL-XXX] (can be developed concurrently)

**Sequencing Rationale**: [One sentence: why this release is sequenced here]

#### Deployment

**Approach**: feature_flag | beta_practices | gradual_rollout | full_release

**Rollback Criteria**:
- [Criterion for rollback decision]
- [Criterion for rollback decision]
