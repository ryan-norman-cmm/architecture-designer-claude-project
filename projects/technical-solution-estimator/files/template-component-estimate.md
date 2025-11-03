# Component Estimate Template

Use this template for estimating each technical component from the Technical Requirements Specification.

---

## Component: [Component Name]

**Category**: Service / Integration Adapter / Workflow / UI Component / GraphQL Subgraph
**Type**: New / Enhancement / Existing
**Complexity**: Low / Medium / High / Critical

---

### Component Description

**Purpose**: [1-2 sentences describing what this component does]

**Source**: TRS Section [X.Y] - [Reference to technical requirements]

---

### Classification

#### For Services:

**Service Classification**: FHIR Service / Non-FHIR Service

**Rationale**: [Why this classification]
- FHIR Service: Uses FHIR resources as primary data model, benefits from Aidbox CRUD + GraphQL
- Non-FHIR Service: Custom data model, requires custom implementation

**Platform Capability Recognition**:
- [ ] Aidbox provides FHIR CRUD operations (0 weeks)
- [ ] Aidbox provides GraphQL auto-generation (0 weeks)
- [ ] Custom business logic needed ([X] weeks)

---

#### For Integration Adapters:

**Endpoint**: [Specific endpoint this adapter connects to]

**One Adapter Per Endpoint**: ✅ Yes / ❌ No

**Rationale**: [Why separate adapter or why grouped - NOTE: should always be separate]

**External System**: [Name of external system/vendor]

**Integration Pattern**: REST API / SOAP / HL7 v2 / FHIR / Custom

**Authentication**: OAuth 2.0 / API Key / Certificate / Custom

---

#### For Workflows:

**Orchestration Pattern**: FHIR Task + BPM + BAMOE UI / Custom

**Platform Capability Recognition**:
- [ ] FHIR Task resource for state management (provided by Aidbox)
- [ ] BPM workflow engine (BAMOE/custom)
- [ ] Workflow UI (BAMOE provides - 0 weeks)

**User Workflows**: [Number of user-facing workflows]

**System Workflows**: [Number of background/automated workflows]

---

#### For UI Components:

**UI Type**: Custom UI / BAMOE Workflow UI / Existing

**Platform Capability Recognition**:
- [ ] BAMOE provides workflow UI (0 weeks)
- [ ] Custom UI needed ([X] weeks)

**Rationale**: [Why custom UI is needed or why BAMOE UI is sufficient]

---

### Effort Estimate

#### Base Effort

**Base Estimate**: [X] weeks

**Base Calculation**:
- FHIR Service: 1 week base (Aidbox provides CRUD + GraphQL)
- Non-FHIR Service: 2 weeks base (custom implementation)
- Integration Adapter: 1 week base (per endpoint)
- Workflow (FHIR Task + BPM): 1 week base (BAMOE UI provided)
- Custom UI: 1 week base (per screen/component)

---

#### Complexity Adjustments

| Factor | Impact | Adjustment | Rationale |
|--------|--------|------------|-----------|
| [Factor 1] | +[X] weeks | [Percentage] | [Why this adds complexity] |
| [Factor 2] | -[X] weeks | [Percentage] | [Why this reduces complexity] |

**Common Complexity Factors**:
- **Unknown domain**: +50% (new business domain, unfamiliar requirements)
- **Complex business rules**: +25-50% (multiple validation rules, state machines)
- **External dependencies**: +25% (relies on external system behavior)
- **Novel integration**: +50% (new integration pattern, no existing examples)
- **High concurrency**: +25% (performance optimization needed)
- **Critical component**: +25% (high-risk, requires extra testing/validation)

**Complexity Reduction Factors**:
- **Similar existing component**: -25% (can copy pattern from existing)
- **Simple CRUD**: -25% (straightforward data operations)
- **Standard pattern**: -25% (well-known, documented approach)

---

#### Batching Adjustments

**Batching Applied**: ✅ Yes / ❌ No

**Batch Group**: [List of similar components in batch]

**Batching Rule**: 40% reduction after first component

**Adjusted Effort**:
- First component: [X] weeks (100%)
- This component: [X] weeks (60% of base)

**Rationale**: [Why batching is appropriate - same pattern, same complexity, similar implementation]

**Batching Validation**:
- [ ] All components in batch follow same pattern
- [ ] All components have same complexity level
- [ ] NOT batching across different endpoints
- [ ] NOT batching different UI component types

---

### Total Effort: [X] weeks

**Calculation**: Base ([X]) + Complexity ([+/-X]) + Batching ([+/-X]) = **[X] weeks**

---

### Dependencies

**Depends On**:
- [Component 1]: [Why this must complete first]
- [Component 2]: [Why this must complete first]

**Blocks**:
- [Component 3]: [What can't start until this completes]
- [Component 4]: [What can't start until this completes]

**Critical Path**: ✅ Yes / ❌ No

---

### Assumptions

| Assumption | Impact on Estimate | Risk Level | Validation Needed |
|------------|-------------------|------------|-------------------|
| [Assumption 1] | [+/- X weeks if wrong] | High/Med/Low | [How to validate] |
| [Assumption 2] | [+/- X weeks if wrong] | High/Med/Low | [How to validate] |

**Common Assumptions**:
- API documentation is accurate (+1 week if wrong)
- External system has < 2 second response time (+1 week if wrong)
- Business rules are fully specified (+2 weeks if wrong)
- Authentication mechanism is standard OAuth (+1 week if wrong)

---

### Open Questions

| Question | Context | Impact on Estimate | Priority | Resolution |
|----------|---------|-------------------|----------|------------|
| [Question 1] | [Why it matters] | [+/- X weeks] | High/Med/Low | [Answer / TBD] |
| [Question 2] | [Why it matters] | [+/- X weeks] | High/Med/Low | [Answer / TBD] |

---

## Estimation Rules Reference

### Services

#### FHIR Service (1 week base)
- Uses FHIR resources as primary data model
- Aidbox provides CRUD operations (0 weeks)
- Aidbox provides GraphQL auto-generation (0 weeks)
- Estimate only custom business logic

**Example**: Patient Service
- Base: 1 week
- Custom validation rules: +0.25 weeks
- **Total: 1.25 weeks**

#### Non-FHIR Service (2 weeks base)
- Custom data model (not FHIR resources)
- Custom CRUD operations needed
- Custom GraphQL subgraph needed
- Full implementation required

**Example**: Billing Service
- Base: 2 weeks
- Complex pricing rules: +0.5 weeks
- **Total: 2.5 weeks**

---

### Integration Adapters (1 week per endpoint)

**One Adapter Per Endpoint Rule**: Each external endpoint gets separate adapter and estimate

**Bad** ❌:
- "Payer Integration Adapter" covering Submit PA, Get Status, Webhook (3 endpoints) = 1 week

**Good** ✅:
- Payer Submit PA Adapter = 1 week
- Payer Get Status Adapter = 1 week
- Payer Webhook Adapter = 1 week
- **Total: 3 weeks**

**Enhancement = 50% of New Effort**:
- New adapter: 1 week
- Enhancement to existing adapter: 0.5 weeks

---

### Workflows (1 week base - FHIR Task + BPM)

**Standard Pattern**: FHIR Task + BPM + BAMOE UI
- FHIR Task resource: 0 weeks (Aidbox provides)
- BPM workflow: 1 week (orchestration logic)
- BAMOE UI: 0 weeks (vendor provides)

**Custom Pattern**: Non-standard workflow
- Custom state management: +1 week
- Custom UI: +1 week per screen

---

### UI Components

**BAMOE Workflow UI**: 0 weeks (vendor provides)
- Task lists
- Task details
- Task actions (approve, reject, reassign)

**Custom UI**: 1 week per screen/component
- Complex forms: +0.5 weeks
- Data visualization: +0.5 weeks
- Real-time updates: +0.5 weeks

---

### GraphQL Subgraphs

**FHIR Resources**: 0 weeks (Aidbox auto-generates)
- Patient, Task, Observation, etc.

**Custom Entities**: 1 week per subgraph
- Custom data models
- Custom resolvers
- Custom federation logic

---

### Batching Rules

**When to Apply Batching**:
- ✅ Multiple similar components with same pattern
- ✅ Same complexity level
- ✅ Same implementation approach

**When NOT to Apply Batching**:
- ❌ Different endpoints (even if same external system)
- ❌ Different complexity levels
- ❌ Different implementation patterns
- ❌ Different types (Service vs Adapter vs UI)

**Batching Reduction**: 40% after first
- Component 1: 1.0 weeks (100%)
- Component 2: 0.6 weeks (60%)
- Component 3: 0.6 weeks (60%)
- **Total: 2.2 weeks** (vs 3.0 weeks without batching)

---

## Estimation Checklist

Use this checklist when estimating each component:

### Classification
- [ ] Component category identified (Service/Adapter/Workflow/UI/Subgraph)
- [ ] Type determined (New/Enhancement/Existing)
- [ ] Complexity level assessed (Low/Med/High/Critical)
- [ ] For Services: FHIR vs Non-FHIR classified
- [ ] For Adapters: One adapter per endpoint verified

### Platform Capabilities
- [ ] Aidbox capabilities recognized (FHIR CRUD + GraphQL)
- [ ] BAMOE capabilities recognized (Workflow UI + Task Management)
- [ ] Vendor-provided features marked as Existing (0 weeks)
- [ ] No duplication of vendor-provided capabilities

### Effort Calculation
- [ ] Base effort applied correctly (FHIR=1w, Non-FHIR=2w, Adapter=1w)
- [ ] Complexity factors identified with rationale
- [ ] Batching applied only to similar components
- [ ] Batching validated (same pattern, same complexity)
- [ ] Enhancement = 50% of new effort rule applied

### Dependencies & Risks
- [ ] Dependencies identified (blocking relationships)
- [ ] Critical path components flagged
- [ ] Assumptions documented with impact
- [ ] Open questions captured with priority
- [ ] Risk level assessed for each assumption

---

## Common Estimation Mistakes

### ❌ Grouping Multiple Endpoints

**Bad**: "FastAuth Integration Adapter" (3 endpoints: Login, Refresh, Validate) = 1 week

**Good**:
- FastAuth Login Adapter = 1 week
- FastAuth Refresh Adapter = 1 week
- FastAuth Validate Adapter = 1 week

**Impact**: Underestimate by 2 weeks

---

### ❌ Estimating Aidbox-Provided Features

**Bad**: "Patient Service GraphQL subgraph" = 1 week (Aidbox auto-generates this)

**Good**: "Patient Service GraphQL subgraph" = 0 weeks (Existing - Aidbox provides)

**Impact**: Overestimate by 1 week

---

### ❌ Estimating BAMOE-Provided UI

**Bad**: "Prior Authorization Task UI" = 1 week (BAMOE provides task UI)

**Good**: "Prior Authorization Task UI" = 0 weeks (Existing - BAMOE provides)

**Impact**: Overestimate by 1 week per workflow

---

### ❌ Batching Different Endpoints

**Bad**: Batching "Payer Submit PA", "Payer Get Status", "Payer Webhook" because they're same payer

**Good**: Separate estimates (different endpoints = different adapters)

**Impact**: Underestimate complexity and risk

---

### ❌ Not Adjusting for Complexity

**Bad**: All services estimated at base (1 week FHIR, 2 weeks Non-FHIR) regardless of complexity

**Good**: Adjust for:
- Unknown domain (+50%)
- Complex business rules (+25-50%)
- Novel integration (+50%)
- Critical component (+25%)

**Impact**: Significant underestimation for complex components

---

### ❌ Ignoring Enhancements

**Bad**: Enhancing existing adapter = 1 week (same as new)

**Good**: Enhancing existing adapter = 0.5 weeks (50% of new effort)

**Impact**: Overestimate by 0.5 weeks per enhancement

---

## Template Usage Guide

### When to Use This Template

Use for **every component** identified in the Technical Requirements Specification:
- Backend services (FHIR and Non-FHIR)
- Integration adapters (one per endpoint)
- Workflows and orchestration
- UI components (custom only, not vendor-provided)
- GraphQL subgraphs (custom only, not Aidbox-generated)

### Filling Out the Template

1. **Start with Classification**: Determine category, type, complexity before estimating

2. **Recognize Platform Capabilities**: Check if Aidbox/BAMOE provides this (0 weeks if yes)

3. **Apply Base Effort**: Use correct base for component type (FHIR=1w, Non-FHIR=2w, etc.)

4. **Adjust for Complexity**: Add/subtract based on complexity factors with rationale

5. **Consider Batching**: Only if similar components, same pattern, same complexity

6. **Document Assumptions**: Every assumption has impact estimate and validation approach

### Validation Before Finalizing

- [ ] Platform capabilities checked (Aidbox, BAMOE)
- [ ] One adapter per endpoint rule followed
- [ ] Batching only applied to similar components
- [ ] Complexity adjustments have clear rationale
- [ ] Dependencies and critical path identified
- [ ] Assumptions documented with risk level
