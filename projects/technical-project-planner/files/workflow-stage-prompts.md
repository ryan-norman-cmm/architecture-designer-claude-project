# Epic Decomposition Stage Prompts

## User Prompts for Each Step

### Step 1: Retrieve Existing Diagrams

**User provides**: Product Requirements Document (PRD)
**User says**:
- "Create epic breakdown for [initiative name]"
- "Decompose Product Requirements into epics"
- "Generate technology epics from PRD"
- "Break down [feature name] into technology epics"

**What happens**: Agent searches arch-diagrammer for existing diagrams, then begins decomposition

---

### Step 2: Create Overview & Summary Table

**Automatically triggered** after Step 1 completes

**User can request**:
- "Show epic summary table"
- "List all epics by iteration"
- "What's the team size breakdown?"

---

### Step 3: Create Timeline Gantt Chart

**Automatically triggered** after Step 2 completes

**User can request**:
- "Generate Gantt chart"
- "Show delivery timeline"
- "Create timeline visualization"

---

### Step 4-6: Analyze & Create Epics

**Automatically executes** through iterations

**User can interrupt with**:
- "Add more detail to [TECH-EPIC-XXX]"
- "Revise [TECH-EPIC-XXX] diagram"
- "Change [TECH-EPIC-XXX] to [S/M/L size]"
- "Split [TECH-EPIC-XXX] into two epics"

---

### Step 7: Create Appendix

**Automatically triggered** after all epics created

**User can request**:
- "Include diagram repository appendix"
- "Add architecture diagram reference"
- "Link to detailed diagrams"

---

### Step 8: Final Validation

**User confirms completion**:
- "Finalize epic breakdown"
- "Complete document"
- "Export epic breakdown"

---

## Refinement Commands

### During Any Step

**Diagram Refinements**:
- "Simplify diagram for [TECH-EPIC-XXX]" → Reduce to 3-6 components
- "Make diagram more business-friendly" → Remove technical jargon
- "Show [component] connections" → Focus on specific integrations
- "Use more plain language" → Simplify technical terms

**Epic Changes**:
- "Change [TECH-EPIC-XXX] to [size]" → Adjust t-shirt sizing
- "Move [TECH-EPIC-XXX] to [iteration]" → Reassign iteration
- "Combine [TECH-EPIC-1] and [TECH-EPIC-2]" → Merge related epics
- "Add dependency: [TECH-EPIC-XXX] depends on [TECH-EPIC-YYY]"

**Content Additions**:
- "Add [epic name] to [iteration]" → Insert new epic
- "Include [component] in diagram" → Expand specific diagram
- "Document [risk/concern]" → Add to epic description

---

## Navigation Commands

- "What step am I at?" → Check current workflow step
- "Go back to Step [N]" → Return to earlier step
- "Skip to Step [N]" → Jump ahead (not recommended)
- "Show overview" → Display summary table
- "Show timeline" → Display Gantt chart
- "List all epics" → Show all TECH-EPIC-XXX identifiers

---

## Quick Reference Commands

### Status Checks
- "What's the status?" → Show current step and progress
- "How many epics?" → Count by iteration
- "What's next?" → Explain next step

### Output Requests
- "Show me epic summary" → Display summary table
- "Generate Gantt chart" → Create timeline
- "List diagrams found" → Show arch-diagrammer search results

---

## Common Workflow Scenarios

### Scenario 1: "Trust the agent, minimal interaction"
```
User: "Create epic breakdown for Enrollment Forms initiative"
Agent: [Executes Steps 1-8 automatically]
User: "Finalize epic breakdown"
```

### Scenario 2: "Review and refine each epic"
```
User: "Create epic breakdown for Medication Sync"
Agent: [Executes Steps 1-3]
Agent: [Presents first epic]
User: "Simplify diagram - too technical"
Agent: [Revises diagram]
User: "Good, continue"
Agent: [Continues through remaining epics]
User: "Finalize epic breakdown"
```

### Scenario 3: "Adjust sizing after seeing all epics"
```
User: "Generate technology epics"
Agent: [Completes all steps]
User: "Change TECH-EPIC-003 to Large"
Agent: [Updates sizing]
User: "Split TECH-EPIC-005 into two Medium epics"
Agent: [Creates TECH-EPIC-005A and TECH-EPIC-005B]
User: "Finalize"
```

### Scenario 4: "Reorganize iterations"
```
User: "Create epic breakdown"
Agent: [Completes breakdown]
User: "Move TECH-EPIC-004 from ITR-002 to ITR-001"
Agent: [Updates iteration assignment]
User: "Move TECH-EPIC-006 to ITR-003"
Agent: [Updates and validates dependencies]
User: "Finalize"
```

---

## Error Recovery Commands

### If Agent Skips Diagram Retrieval
- "Go back to Step 1 and search for diagrams"
- "Search arch-diagrammer for this initiative"

### If Diagram Too Complex
- "Simplify to 3-6 components only"
- "Remove implementation details"
- "Focus on business value"

### If Epic Missing
- "Add [epic name] to [iteration]"
- "Did you miss [functionality]?"

### If Dependencies Unclear
- "Show all dependencies for [iteration]"
- "What does [TECH-EPIC-XXX] depend on?"

---

## Best Practices for Prompts

**Good Prompts** ✅:
- "Create epic breakdown for Patient Portal initiative"
- "Simplify diagram for TECH-EPIC-002"
- "Change TECH-EPIC-005 to Medium"
- "Add prior authorization workflow epic to ITR-001"

**Vague Prompts** ⚠️:
- "Make it better" (specify what to improve)
- "Fix the epics" (which epic, what issue?)
- "Update" (update what, how?)

**Use Specific IDs**:
- âœ… "Revise TECH-EPIC-003 diagram"
- âŒ "Revise that epic"
