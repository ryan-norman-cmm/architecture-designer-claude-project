# Technical Estimation Analysis Stage Prompts

## User Prompts for Each Step

### Step 1: Document Analysis

**User provides**: Technical Requirements Specification (TRS), Platform Capabilities
**User says**:
- "Estimate technical requirements"
- "Create development estimates from technical specs"
- "Analyze components for sizing"
- "Generate technical estimation"

**What happens**: Agent analyzes TRS and checks platform capabilities

---

### Step 2-6: Classification & Analysis (Automatically Executes)

These steps happen automatically:
- Step 2: Component classification
- Step 3: Integration adapter analysis
- Step 4: Workflow & orchestration
- Step 5: UI component selection
- Step 6: Apply batching rules

**User can refine mid-process**:
- "Check existing capabilities"
- "List all adapters needed"
- "Show service classifications"
- "Identify UI components"

---

### Step 7-8: Calculate & Document

**Automatically executes**:
- Step 7: Calculate totals and critical path
- Step 8: Document assumptions and open questions

**User can request**:
- "Show critical path"
- "Calculate totals"
- "Identify risks"

---

### Step 9: Final Quality Check

**User confirms completion**:
- "Generate clean estimate"
- "Finalize technical estimates"
- "Complete estimation document"

---

## Component-Specific Commands

### Service Classification
- "Change [service] to FHIR service" → Reclassify with 1 week base
- "Change [service] to Non-FHIR service" → Reclassify with 2 week base
- "Mark [service] as Existing" → 0 weeks estimate

### Adapter Management
- "Split [adapter] by endpoint" → Separate combined adapter
- "Create separate adapter for [endpoint]" → One adapter per endpoint
- "Mark [adapter] as Enhancement" → 50% of new effort

### Type Changes
- "Change [component] to New" → Full effort estimate
- "Change [component] to Enhancement" → 50% of new effort
- "Change [component] to Existing" → 0 weeks

### Complexity Updates
- "Update [component] complexity to High" → Increase estimate
- "Change [component] to Low complexity" → Decrease estimate
- "Mark [component] as Critical" → Add risk buffer

### Batching
- "Apply batching to [component1, component2, component3]"
- "Remove batching from [components]"
- "Group similar [component type]"

---

## Validation Commands

- "Check endpoint separation" → Verify one adapter per endpoint
- "Verify vendor capabilities" → Ensure Aidbox/BAMOE recognized
- "Review batching rules" → Validate similar component grouping
- "Confirm workflow pattern" → Check FHIR Task + BPM + BAMOE

---

## Analysis Commands

- "Show critical path" → Display blocking dependencies
- "Calculate totals" → Sum effort estimates by category
- "Identify risks" → Flag high-complexity items
- "List assumptions" → Show all assumptions made
- "Show open questions" → Display unknowns

---

## Navigation Commands

- "What step am I at?" → Check current workflow step
- "Show service breakdown" → Display FHIR vs Non-FHIR
- "List all adapters" → Show endpoint-level adapters
- "Display UI components" → Show custom UI estimates
- "Show totals" → Display category summaries

---

## Common Scenarios

### Scenario 1: "Trust the estimates"
```
User: "Estimate technical requirements"
Agent: [Executes Steps 1-9 automatically]
User: "Finalize technical estimates"
```

### Scenario 2: "Fix endpoint grouping"
```
User: "Create development estimates"
Agent: [Completes analysis]
User: "Split FastAuth adapter by endpoint"
Agent: [Creates separate adapters for each endpoint]
User: "Finalize"
```

### Scenario 3: "Adjust complexity"
```
User: "Generate estimates"
Agent: [Completes draft]
User: "Update Patient Service complexity to High - unknown integrations"
Agent: [Increases estimate, adds rationale]
User: "Change Notification UI to Low - simple display"
Agent: [Decreases estimate]
User: "Finalize"
```

### Scenario 4: "Apply batching"
```
User: "Estimate components"
Agent: [Completes initial estimates]
User: "Apply batching to FHIR Publisher 1, 2, 3 - all same pattern"
Agent: [Applies 40% reduction after first]
User: "Finalize"
```

---

## Error Recovery

### If Endpoints Grouped
- "Split [adapter name] by endpoint"
- "Create separate adapter for [endpoint 1], [endpoint 2], [endpoint 3]"

### If GraphQL Estimated for FHIR
- "Remove GraphQL subgraph for [FHIR service] - Aidbox provides it"
- "Mark GraphQL as Existing for [FHIR service]"

### If Vendor Capability Missed
- "Mark [component] as Existing - Aidbox provides it"
- "Change [UI] to Existing - BAMOE provides it"

### If Wrong Type
- "Change [component] from New to Enhancement"
- "Mark [component] as Existing - already built"

### If Batching Applied Incorrectly
- "Remove batching from [components] - different complexity"
- "Don't batch [adapters] - different endpoints"

---

## Best Practices

**Good Prompts** ✅:
- "Split Payer Integration adapter into separate adapters for Submit PA, Get Status, and Webhook endpoints"
- "Change Prior Authorization Service complexity to Critical - new domain, high risk"
- "Apply batching to Notification Publisher 1, 2, 3 - all same FHIR pattern"
- "Mark Task UI as Existing - BAMOE provides workflow UI"

**Vague Prompts** ⚠️:
- "Fix adapters" (which adapter, what issue?)
- "Change complexity" (which component, to what level?)
- "Apply batching" (to which components?)

**Be Specific with Rationale**:
- âœ… "Update Auth Service to High complexity - OAuth integration with unknown IDP"
- âŒ "Change to High"

**Reference Specific Components**:
- âœ… "Split FastAuth Integration adapter by endpoint"
- âŒ "Split that adapter"
