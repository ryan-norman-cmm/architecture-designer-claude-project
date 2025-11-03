# Technical Estimation Analysis Workflow State

Use this template to track your technical estimation progress.

---

## Feature Information

**Feature Name**: [Name]
**Technical Requirements Version**: [Version]
**Start Date**: [Date]
**Target Estimate Delivery**: [Date]

---

## Current Status

**Current Step**: [1-9] - [Step Name]
**Last Action**: [What was just completed]
**Next Action**: [What to do next]

---

## Step Progress

| Step | Status | Completed | Notes |
|------|--------|-----------|-------|
| 1. Document Analysis | ⚫️ Pending / ✅ Complete | [Date] | [TRS analyzed] |
| 2. Classify Components | ⚫️ Pending / ✅ Complete | [Date] | [FHIR vs Non-FHIR] |
| 3. Analyze Integration Adapters | ⚫️ Pending / ✅ Complete | [Date] | [Endpoint separation] |
| 4. Workflow & Orchestration | ⚫️ Pending / ✅ Complete | [Date] | [FHIR Task + BPM pattern] |
| 5. UI Component Selection | ⚫️ Pending / ✅ Complete | [Date] | [Custom vs BAMOE] |
| 6. Apply Batching Rules | ⚫️ Pending / ✅ Complete | [Date] | [Batching applied] |
| 7. Calculate Totals | ⚫️ Pending / ✅ Complete | [Date] | [Critical path identified] |
| 8. Document Assumptions | ⚫️ Pending / ✅ Complete | [Date] | [Open questions tracked] |
| 9. Final Quality Check | ⚫️ Pending / ✅ Complete | [Date] | [Validation passed] |

---

## Component Breakdown

### Services

| Service Name | Type | Classification | Complexity | Effort (weeks) | Rationale |
|--------------|------|----------------|-----------|----------------|-----------|
| [Service 1] | New/Enhancement/Existing | FHIR/Non-FHIR | Low/Med/High/Critical | [X] | [Why] |
| [Service 2] | New/Enhancement/Existing | FHIR/Non-FHIR | Low/Med/High/Critical | [X] | [Why] |

**Total Services**: [X] (FHIR: [X], Non-FHIR: [X])

---

### Integration Adapters

| Adapter Name | Endpoint | Type | Complexity | Effort (weeks) | Rationale |
|--------------|----------|------|-----------|----------------|-----------|
| [Adapter 1] | [Endpoint 1] | New/Enhancement/Existing | Low/Med/High | [X] | [Why] |
| [Adapter 2] | [Endpoint 2] | New/Enhancement/Existing | Low/Med/High | [X] | [Why] |

**Total Adapters**: [X] (New: [X], Enhancement: [X], Existing: [X])
**One Adapter Per Endpoint**: ✅ Yes / ❌ No

---

### Workflows & Orchestration

| Workflow Name | FHIR Task | BPM Process | BAMOE UI | Effort (weeks) | Notes |
|---------------|-----------|-------------|----------|----------------|-------|
| [Workflow 1] | ✅ / ❌ | ✅ / ❌ | ✅ / ❌ | [X] | [Pattern applied] |
| [Workflow 2] | ✅ / ❌ | ✅ / ❌ | ✅ / ❌ | [X] | [Pattern applied] |

**Total Workflows**: [X]

---

### UI Components

| Component Name | Type | Provided By | Complexity | Effort (weeks) | Notes |
|----------------|------|-------------|-----------|----------------|-------|
| [UI 1] | Custom/BAMOE/Existing | [Vendor/Team] | Low/Med/High | [X] | [Why custom/existing] |
| [UI 2] | Custom/BAMOE/Existing | [Vendor/Team] | Low/Med/High | [X] | [Why custom/existing] |

**Total UI Components**: [X] (Custom: [X], BAMOE: [X], Existing: [X])

---

### GraphQL Federation

| Subgraph Name | Type | Rationale | Effort (weeks) |
|---------------|------|-----------|----------------|
| [Subgraph 1] | New/Enhancement/Existing | [Why needed / Aidbox provides] | [X] |
| [Subgraph 2] | New/Enhancement/Existing | [Why needed / Aidbox provides] | [X] |

**Total Subgraphs**: [X]
**Aidbox Auto-Generated**: [X] (marked as Existing)

---

## Batching Applied

| Component Group | Batch Size | Reduction Applied | Total Effort (weeks) | Rationale |
|-----------------|-----------|-------------------|----------------------|-----------|
| [Similar components 1, 2, 3] | 3 | 40% after first | [X] | [Same pattern] |
| [Similar components 4, 5] | 2 | 40% after first | [X] | [Same pattern] |

**Total Batching Savings**: [X] weeks

---

## Effort Summary

| Category | Count | Total Effort (weeks) | % of Total |
|----------|-------|---------------------|------------|
| FHIR Services | [X] | [X] | [X]% |
| Non-FHIR Services | [X] | [X] | [X]% |
| Integration Adapters | [X] | [X] | [X]% |
| Workflows & Orchestration | [X] | [X] | [X]% |
| UI Components (Custom) | [X] | [X] | [X]% |
| GraphQL Subgraphs | [X] | [X] | [X]% |
| **TOTAL** | **[X]** | **[X]** | **100%** |

**Critical Path**: [Component 1] → [Component 2] → [Component 3] ([X] weeks)

---

## Platform Capabilities Recognized

| Capability | Provided By | Components Affected | Effort Saved |
|------------|-------------|---------------------|--------------|
| FHIR CRUD + GraphQL | Aidbox | [Services 1, 2, 3] | [X] weeks |
| Workflow UI | BAMOE | [UI 1, 2] | [X] weeks |
| Task Management | FHIR Task + BPM | [Workflows 1, 2] | [X] weeks |

**Total Effort Saved**: [X] weeks

---

## Complexity Adjustments

| Component | Original | Adjusted To | Reason | Impact (weeks) |
|-----------|----------|-------------|--------|----------------|
| [Component 1] | Medium | High | [Unknown integrations] | +[X] |
| [Component 2] | High | Critical | [New domain, high risk] | +[X] |
| [Component 3] | Medium | Low | [Simple display] | -[X] |

---

## Assumptions Made

| Assumption | Impact on Estimate | Risk Level | Validation Needed |
|------------|-------------------|------------|-------------------|
| [Assumption 1] | [+/- X weeks] | High/Med/Low | [How to validate] |
| [Assumption 2] | [+/- X weeks] | High/Med/Low | [How to validate] |

---

## Open Questions

| Question | Context | Impact on Estimate | Priority | Resolution |
|----------|---------|-------------------|----------|------------|
| [Question 1] | [Why it matters] | [+/- X weeks] | High/Med/Low | [Answer / TBD] |
| [Question 2] | [Why it matters] | [+/- X weeks] | High/Med/Low | [Answer / TBD] |

---

## Type Changes Made

| Component | Original Type | Changed To | Reason | Date |
|-----------|--------------|------------|--------|------|
| [Component 1] | New | Enhancement | [Already partially built] | [Date] |
| [Component 2] | New | Existing | [Vendor provides] | [Date] |

---

## Refinements Made

| Date | Component | Change | Reason |
|------|-----------|--------|--------|
| [Date] | [Adapter 1] | Split by endpoint | [Violated one-per-endpoint rule] |
| [Date] | [Service 1] | Changed to FHIR | [Uses FHIR resources] |
| [Date] | [UI 1] | Marked as BAMOE | [Workflow UI provided] |

---

## Quality Checklist

### Component Classification
- [ ] All services classified as FHIR or Non-FHIR
- [ ] FHIR services estimated at 1 week base
- [ ] Non-FHIR services estimated at 2 week base
- [ ] Aidbox capabilities recognized (CRUD + GraphQL)

### Integration Adapters
- [ ] One adapter per endpoint (no grouping)
- [ ] Each endpoint has separate estimate
- [ ] Enhancement = 50% of new effort
- [ ] External API adapters identified

### Workflows & Orchestration
- [ ] FHIR Task + BPM + BAMOE UI pattern applied
- [ ] User workflows converted to BPM
- [ ] BAMOE workflow UI recognized as Existing
- [ ] No custom workflow UI estimated

### UI Components
- [ ] BAMOE-provided UI marked as Existing
- [ ] Custom UI only for non-workflow screens
- [ ] Complexity aligned with requirements

### Batching Rules
- [ ] Similar components grouped (same pattern)
- [ ] 40% reduction applied after first
- [ ] No batching across different endpoints
- [ ] No batching across different complexity levels

### Vendor Capabilities
- [ ] Aidbox: FHIR CRUD + GraphQL recognized
- [ ] BAMOE: Workflow UI + Task Management recognized
- [ ] No duplication of vendor-provided features

---

## Completion Status

**Document Status**: ⚫️ Draft / ✅ Complete
**Clean Output Generated**: ⚫️ No / ✅ Yes (template instructions removed)
**Final Review Date**: [Date]
**Approved By**: [Name]
**Version**: [X.Y]

---

## Notes

[Additional notes, context, or observations about the estimation analysis]
