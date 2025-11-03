# Technical Estimation Analysis Workflow

## Overview

Analyze technical requirements to produce accurate development estimates with component-level detail and justification.

**Duration:** 45-60 minutes per feature
**Output:** Complete technical estimation document with component breakdown, totals, critical path, and assumptions

---

## Workflow Steps

### Step 1: Document Analysis

1. **Read Technical Requirements** thoroughly
2. **Check CMM Service Features** for what's already built
3. **Map requirements** to estimation template sections
4. **Identify dependencies** and critical path items

**Validation Checklist**:
- [ ] Technical Requirements document reviewed completely
- [ ] Existing Platform Capabilities checked
- [ ] Requirements mapped to components
- [ ] Dependencies identified
- [ ] Critical path items noted

---

### Step 2: Component Classification

#### Service Classification

```
Can functionality use FHIR resources?
├─ YES → FHIR Service (1 week base)
│   └─ GraphQL automatic via Aidbox (0 additional weeks)
└─ NO → Non-FHIR Service (2 weeks base)
    └─ Needs GraphQL? → Add subgraph estimates
```

#### Type Classification

- **Existing**: Component fully operational, meets requirements → 0 weeks
- **Enhancement**: Component exists but needs modification → 50% of new effort
- **New**: Component doesn't exist → Full effort

#### Complexity Assessment

- **Low**: Simple, well-defined, minimal dependencies
- **Medium**: Some unknowns, moderate integration
- **High**: Complex dependencies, significant unknowns
- **Critical**: High-risk, major architectural impact

**Validation Checklist**:
- [ ] FHIR services identified (no GraphQL subgraphs)
- [ ] Non-FHIR services identified (with GraphQL if needed)
- [ ] Types classified (Existing/Enhancement/New)
- [ ] Complexity assessed with rationale
- [ ] Vendor-provided features marked as Existing

---

### Step 3: Integration Adapter Analysis

#### Endpoint-Level Evaluation

For EACH external endpoint, check:

```
existing_services.external_integrations.[vendor].endpoints.[endpoint_name]
├─ status: "integrated"
│   ├─ adapter_exists: true → Existing (0 weeks)
│   └─ adapter_exists: false → New adapter only (4 weeks)
└─ status: "not integrated"
    ├─ adapter_exists: true → Enhancement (2 weeks)
    └─ adapter_exists: false → New full (4 weeks)
```

**CRITICAL RULE**: ONE adapter per endpoint - never group multiple endpoints

**Validation Checklist**:
- [ ] Each endpoint has separate adapter estimate
- [ ] No grouped endpoints under single adapter
- [ ] Adapter types classified correctly
- [ ] Endpoint status verified in platform capabilities
- [ ] Webhook endpoints included separately

---

### Step 4: Workflow & Orchestration Pattern

All workflows MUST follow:

```
FHIR Task (state management)
    ↓
BPM Workflow (business logic)
    ↓
BAMOE UI (monitoring/forms)
```

**This means**:
- Include Task Service if ANY workflows exist
- Use BPM estimates for orchestration logic
- NO custom workflow UI (BAMOE provides it)
- NO custom workflow events (use FHIR Task events)

**Validation Checklist**:
- [ ] Task Service included (if workflows exist)
- [ ] BPM workflows estimated
- [ ] No custom workflow UI estimated
- [ ] BAMOE UI capabilities recognized
- [ ] FHIR Task events used

---

### Step 5: UI Component Selection

#### Component Type Decision

```
Is it a simple visual element?
├─ YES (badge, icon, indicator) → Don't include
└─ NO → Is it data-heavy or interactive?
    ├─ YES → Standard Component (0.7-4 weeks based on complexity)
    └─ NO → Is it a full page?
        └─ YES → Screen (1.5-6 weeks based on complexity)
```

#### Vendor UI Check

Before estimating ANY UI:
1. Does Aidbox provide it? → Existing
2. Does BAMOE provide it? → Existing
3. Does another vendor tool provide it? → Existing
4. Custom needed? → Estimate as New

**Validation Checklist**:
- [ ] Simple visual elements excluded
- [ ] Vendor-provided UI marked as Existing
- [ ] Aidbox UI capabilities checked
- [ ] BAMOE UI capabilities checked
- [ ] Custom UI complexity justified

---

### Step 6: Apply Batching Rules

**Batching only applies to technically similar components:**
- Same type (e.g., all FHIR publishers)
- Same complexity level
- Same integration pattern
- Sequential implementation possible

**Batching NEVER applies to:**
- Different endpoints to same vendor
- Different complexity levels
- Parallel implementation requirements

**Validation Checklist**:
- [ ] Batching applied only to similar components
- [ ] Same type verified
- [ ] Same complexity verified
- [ ] Sequential implementation possible
- [ ] No endpoint grouping
- [ ] No different complexity batching

---

### Step 7: Calculate Totals and Critical Path

1. **Sum estimates by category**:
   - Backend Services
   - Frontend Components
   - Integration Adapters
   - Workflows
   - Platform Setup

2. **Identify critical path**:
   - Components with blocking dependencies
   - High-risk items
   - Must-complete-first items

3. **Add risk buffer**:
   - Critical items: +25% buffer
   - High complexity: +15% buffer

**Validation Checklist**:
- [ ] All components summed by category
- [ ] Critical path identified
- [ ] Risk buffer added to critical items
- [ ] Dependencies documented
- [ ] Parallel work opportunities noted

---

### Step 8: Document Assumptions and Open Questions

**Assumptions**:
- Technology choices
- Platform capabilities
- Team skills
- Implementation approach

**Open Questions**:
- Unclear requirements
- Missing specifications
- Technical unknowns

**Validation Checklist**:
- [ ] All assumptions documented
- [ ] Technology assumptions clear
- [ ] Platform assumptions clear
- [ ] Open questions flagged
- [ ] Impact of unknowns estimated

---

### Step 9: Final Quality Check

Before finalizing:
- All requirements mapped to components
- Types (New/Enhancement/Existing) verified
- Complexity justified with rationale
- Critical path items identified
- Risk buffer added to critical items
- Total weeks calculated correctly

**Final Validation Checklist**:
- [ ] All requirements have components
- [ ] Each endpoint has separate adapter
- [ ] FHIR services marked (no GraphQL subgraphs)
- [ ] Vendor-provided features marked as Existing
- [ ] Workflows include Task Service
- [ ] BAMOE UI capabilities recognized
- [ ] Batching applied only to similar components
- [ ] Totals calculated correctly
- [ ] Critical path documented
- [ ] Assumptions and open questions listed

---

## Clean Output Protocol

**DO NOT include in output:**
- Estimation methodology explanations or decision frameworks
- Complexity assessment guides showing multiplier criteria
- Batching calculation notes explaining reduction percentages
- "Guidelines:" sections after each table
- Template instructions or usage examples
- AI reasoning about why estimates were chosen
- Detailed notes in table cells explaining calculations
- Platform capability assessment methodology

**DO include in output:**
- Component estimation tables with calculations
- Summary totals by category
- Critical path analysis
- Assumptions and dependencies sections
- Open questions impacting estimates
- Clean, executive-ready estimation document

**Notes field usage rules:**
- Use notes ONLY for business-relevant context
- Keep to 1 sentence maximum per note
- Focus on WHAT, not HOW
- Example of good note: "First OAuth scope - full base effort" âœ…
- Example of bad note: "Okta OAuth configuration-based work - aggressive batching applied after first scope following estimation framework" âŒ
- When in doubt, leave notes field empty

**Verification before output:**
- âœ… Estimation tables with data
- âœ… Totals calculated correctly
- âœ… Critical path identified
- âœ… Assumptions documented
- âŒ No "Guidelines:" sections visible
- âŒ No complexity multiplier explanations
- âŒ No batching methodology text
- âŒ No estimation framework descriptions
- âŒ No verbose notes explaining calculations

---

## Common Pitfalls to Avoid

âŒ Grouping endpoints under single adapter
âŒ Estimating GraphQL for FHIR services
âŒ Missing vendor capabilities (marking as New when Existing)
âŒ Duplicating workflow UI that BAMOE provides
âŒ Over-batching dissimilar components
âŒ Ignoring enhancement option (defaulting to New)
âŒ Missing platform setup requirements
âŒ Including methodology explanations in final output
âŒ Verbose notes in component tables
