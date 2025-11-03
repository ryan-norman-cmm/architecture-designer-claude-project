# Technical Requirements Analysis Stage Prompts

## User Prompts for Each Step

### Step 1: Complete Document Review

**User provides**: Product Requirements Document (PRD), Platform Capabilities, FHIR Resources
**User says**:
- "Create technical requirements from PRD"
- "Transform product requirements to technical specs"
- "Analyze Product Discovery Worksheet"
- "Generate technical requirements specification"

**What happens**: Agent reads all documents thoroughly before starting analysis

---

### Step 2-4: Extract & Map (Automatically Executes)

These steps happen automatically:
- Step 2: Extract workflows
- Step 3: Map healthcare standards
- Step 4: Derive entity events

**User can request mid-process**:
- "List all workflows found"
- "Show FHIR resource mappings"
- "Review entity events"

---

### Step 5: Design Technical Solution

**Automatically triggered**

**User can refine**:
- "Expand [workflow name] orchestration"
- "Add more detail to [section]"
- "Recommend [technology] for [component]"

---

### Step 6-7: Test Scenarios & Documentation

**Automatically executes**

**User can request**:
- "Add test scenarios for [workflow]"
- "Include failure path for [scenario]"

---

### Step 8: Final Quality Check

**User confirms completion**:
- "Generate clean output"
- "Finalize technical requirements"
- "Complete TRS document"

---

## Section-Specific Commands

### During Workflow Extraction
- "Add [workflow name]" → Include additional workflow
- "Mark [workflow] as Future/TBD" → Exclude from MVP
- "Separate [workflow variation] as distinct workflow"

### During FHIR Mapping
- "Update FHIR resource for [entity]" → Change resource selection
- "Use [implementation guide]" → Apply specific IG
- "Map [field] to [coding system]" → Specify code mapping

### During Event Derivation
- "Derive events for [entity]" → Generate lifecycle events
- "Add event: [event name]" → Include specific event
- "Skip routine CRUD for [entity]" → Exclude standard operations

### During Solution Design
- "Mark [section] as Not Applicable" → Document non-applicable
- "Recommend [approach]" → Add technical recommendation
- "Add [integration pattern]" → Include integration approach

---

## Refinement Commands

**Workflow Refinement**:
- "Expand [workflow] with more steps"
- "Add error handling for [scenario]"
- "Include [edge case] workflow"

**FHIR Refinement**:
- "Change [entity] from [Resource A] to [Resource B]"
- "Add [extension] for [field]"
- "Include [profile] requirement"

**Test Refinement**:
- "Add Given/When/Then for [workflow]"
- "Include negative test for [scenario]"

---

## Validation Commands

- "Check completeness" → Run through quality checklist
- "Verify all workflows extracted" → Validate workflow coverage
- "Review event catalog" → Ensure comprehensive events
- "Confirm FHIR mappings" → Validate resource selections

---

## Navigation Commands

- "What step am I at?" → Check current workflow step
- "Show extracted workflows" → List all workflows found
- "Display FHIR mappings" → Show resource assignments
- "Review events" → Show derived event catalog

---

## Common Scenarios

### Scenario 1: "Standard flow"
```
User: "Create technical requirements from PRD"
Agent: [Executes Steps 1-8 automatically]
User: "Finalize technical requirements"
```

### Scenario 2: "Add missing workflow"
```
User: "Generate technical requirements"
Agent: [Completes analysis]
User: "Add notification workflow for status updates"
Agent: [Adds workflow and derives events]
User: "Finalize"
```

### Scenario 3: "Change FHIR mapping"
```
User: "Create TRS"
Agent: [Completes draft]
User: "Change Medication from MedicationRequest to MedicationStatement"
Agent: [Updates mapping throughout document]
User: "Add US Core profile requirement"
Agent: [Adds profile constraints]
User: "Finalize"
```

---

## Error Recovery

### If Workflow Missed
- "Add [workflow name] from PRD section [X]"
- "You missed [functionality] - add as workflow"

### If Event Missing
- "Derive events for [entity]"
- "Add [event type] event for [entity]"

### If FHIR Mapping Wrong
- "Update FHIR resource for [entity]"
- "Use [different resource]"

### If Section Not Applicable
- "Mark [section] as Not Applicable - [reason]"

---

## Best Practices

**Good Prompts** ✅:
- "Add prior authorization submission workflow"
- "Update Patient resource to use US Core profile"
- "Derive events for Notification entity"
- "Mark Data Migration as Not Applicable - no legacy data"

**Vague Prompts** ⚠️:
- "Add more" (more what?)
- "Fix FHIR" (which resource, what issue?)
- "Include that" (include what?)

**Be Specific**:
- âœ… "Add error handling workflow for API timeout"
- âŒ "Add error workflow"
