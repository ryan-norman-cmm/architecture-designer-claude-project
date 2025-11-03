# Stage Transition Prompts

## User Prompts for Each Stage

### Stage 1: Initiative Decomposition (Requirements Analysis)
**User provides**: Product requirements document
**User says**:
- "Please decompose these requirements"
- "Run decomposition agent"
- "Analyze these product requirements"
- "Create initiative release breakdown"

**What happens**: Initiative_Decomposition_Agent runs first-pass decomposition

---

### Stage 2a: Request Update
**User says**:
- "I need to update the requirements"
- "Update requirements: [changes]"
- "Let me revise the requirements"
- "Go back to Stage 1 with these changes: [changes]"

**What happens**: Return to Stage 1 with updated requirements

---

### Stage 2b: Request Alternatives
**User says**:
- "Show me alternative approaches"
- "Generate alternatives"
- "Request alternative strategies"
- "I want to see other options"

**With constraints** (recommended):
- "Show alternatives optimized for: [your criteria]"
- "Create alternatives with these constraints: [constraints]"

**What happens**: Proceed to Stage 3 (Alternative approaches)

---

### Stage 3: Generate Alternatives
**What happens**: ALT_AGENT generates 2 additional approaches

---

### Stage 4: Select Alternative
**User says**:
- "I select approach 1" (original from Stage 1)
- "I select approach 2" (first alternative)
- "I select approach 3" (second alternative)
- "Go with option 2"
- "Proceed with the risk-minimized approach"

**What happens**: Selected approach confirmed, automatically proceeds to Stage 5

---

### Stage 5a: Approve Validation
**After Marty Cagan review**, user says:
- "Approve recommendations"
- "Proceed to final plan"
- "Accept validation, generate detailed breakdown"
- "Looks good, create the full release plan"

**What happens**: Proceed to Stage 6 (Final detailed release plan)

---

### Stage 5b: Ignore Recommendations
**After Marty Cagan review**, user says:
- "Ignore recommendations and proceed"
- "Accept current approach despite issues"
- "Generate final plan anyway"
- "I acknowledge the issues but want to continue"

**When to use**:
- Maturity score 7+ with minor issues
- User has strategic reasons to accept lower score
- Issues are understood and acceptable

**What happens**: Proceed to Stage 6 with current approach (not recommended if maturity < 7)

---

### Stage 5c: Iterate Based on Recommendations
**After Marty Cagan review**, user says:
- "Go back to Stage 1 and fix the issues"
- "Update requirements based on recommendations"
- "Re-run decomposition with these changes: [changes]"
- "Generate alternatives addressing the validation concerns"

**What happens**: Return to Stage 1 or Stage 3 based on user request

---

### Stage 6: Final Output
**Automatically triggered after Stage 5 approval**

**User can request additions**:
- "Add visualizations" (Gantt chart, dependency graph)
- "Generate Gantt chart"
- "Create dependency flowchart"
- "Include decision logic diagram"

**What happens**: Complete detailed Initiative Release plan generated

---

## Quick Reference Commands

### Navigation Commands
- "What stage am I at?" -> Check workflow state
- "Go back to Stage [X]" -> Return to previous stage
- "Skip to Stage [X]" -> Jump ahead (not recommended)
- "Start over" -> Restart workflow from Stage 1

### Help Commands
- "Show me the workflow overview" -> Display workflow stages
- "What are my options?" -> List available actions
- "What happens next?" -> Explain next step
- "Why did validation fail?" -> Review Marty Cagan report

### Output Commands
- "Show me the Release Review Summary" -> Display Stage 1 output
- "Compare all 3 approaches" -> Side-by-side comparison (Stage 4)
- "Show validation report" -> Display Marty Cagan report (Stage 5)
- "Export final plan" -> Save detailed JSON (Stage 6)

---

## Stage-Specific Clarifications

### Stage 1: First-Pass Decomposition
**Initiative_Decomposition_Agent focuses on**:
- Requirements traceability (quote requirements)
- Bulk operations validation (frequency â‰  bulk)
- User type identification (physician/administrator/internal)
- "Considered But Excluded" documentation

**Output format**: Release Review Summary (5-minute read)

---

### Stage 3: Alternative Approaches
**Alternative_Release_Strategy_Agent runs 2 times** with different constraints:

**Example request**:
"Generate alternatives:
1. Risk-minimized: prioritize de-risking integrations
2. Value-maximized: prioritize fastest user value delivery"

**What you get**: 3 total approaches to choose from
- Approach 1: Original (from Stage 1)
- Approach 2: Risk-minimized
- Approach 3: Value-maximized

---

### Stage 5: Validation Deep Dive
**Marty_Cagan_Review_Agent checks**:
- Requirements traceability (are releases hallucinated?)
- Scope discipline (exclusions documented?)
- Vertical slice quality (complete user value?)
- Minimum testable scope (smallest possible?)

**Output includes**:
- Maturity score (1-10)
- Requirements traceability report
- Hallucinated releases flagged
- Specific recommendations

**Decision criteria**:
- Maturity 9-10: Excellent -> Approve
- Maturity 7-8: Good -> Approve with minor tweaks
- Maturity 4-6: Moderate issues -> Consider iteration
- Maturity 1-3: Fundamental issues -> Restart recommended

---

## Common Workflow Scenarios

### Scenario 1: "I trust the first decomposition"
```
Stage 1: Run decomposition
Stage 2: "Approve this approach"
Stage 5: Validation runs
Stage 5: "Approve recommendations"
Stage 6: Final plan generated
```

### Scenario 2: "I want to see alternatives first"
```
Stage 1: Run decomposition
Stage 2: "Generate alternatives: risk-minimized and value-maximized"
Stage 3: Review 3 approaches
Stage 4: "I select approach 2"
Stage 5: Validation runs
Stage 5: "Approve recommendations"
Stage 6: Final plan generated
```

### Scenario 3: "Validation found issues, need to iterate"
```
Stage 1: Run decomposition
Stage 2: "Approve this approach"
Stage 5: Validation finds hallucinated releases
Stage 5: "Go back to Stage 1 and fix issues"
Stage 1: Re-run with corrected understanding
Stage 2: "Approve"
Stage 5: Validation passes
Stage 6: Final plan generated
```

### Scenario 4: "I want alternatives AFTER seeing validation"
```
Stage 1: Run decomposition
Stage 2: "Approve this approach"
Stage 5: Validation shows maturity score 6/10
Stage 5: "Generate alternatives addressing validation concerns"
Stage 3: 2 new approaches generated
Stage 4: "Select approach 2"
Stage 5: Re-validate selected approach
Stage 6: Final plan generated
```
