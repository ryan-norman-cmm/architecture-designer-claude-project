# Initiative Decomposition - Workflow State

## Initiative Information
**Initiative Name**: [To be filled]
**Initiative ID**: [To be filled]
**Requirements Source**: [To be filled]
**Product Manager**: [To be filled]
**Start Time**: [To be filled]

---

## Current Status

**Current Stage**: Not Started (Stage 0)
**Last Action**: None
**Next Step**: Provide product requirements to begin Stage 1

---

## Workflow Progress

### Stage 1: Initiative Decomposition (Requirements Analysis)
**Status**: ⏸️ Not Started
**Agent**: Initiative_Decomposition_Agent
**Input Required**: Product requirements document
**Output Format**: Release Review Summary

**Progress**:
- [ ] Requirements received
- [ ] Healthcare glossary referenced
- [ ] User type identified
- [ ] Decomposition patterns applied
- [ ] Requirements traceability validated
- [ ] Release Review Summary generated

**Output Location**: [To be filled]
**Iterations**: 0
**Time Spent**: 0 minutes

---

### Stage 2: User Decision Point
**Status**: ⏸️ Not Started
**Decision Required**: Update / Approve / Request Alternatives

**User Options**:
- [ ] **Option A**: Update requirements → Return to Stage 1
- [ ] **Option B**: Approve approach → Skip to Stage 5
- [ ] **Option C**: Request alternatives → Proceed to Stage 3

**Decision Made**: [To be filled]
**Rationale**: [To be filled]
**Timestamp**: [To be filled]

---

### Stage 3: Alternative Approaches (Optional)
**Status**: ⏸️ Not Started
**Agent**: Alternative_Release_Strategy_Agent
**Trigger**: User requested alternatives in Stage 2

**Constraints Specified**:
- Alternative 1: [Constraint description]
- Alternative 2: [Constraint description]

**Progress**:
- [ ] Baseline approach analyzed
- [ ] Alternative 1 generated (Tactical Variation)
- [ ] Alternative 2 generated (Radical Rethink)
- [ ] Comparison template completed
- [ ] All 3 approaches documented

**Output Locations**:
- Approach 1 (Original): [Stage 1 output]
- Approach 2 (Alternative 1): [To be filled]
- Approach 3 (Alternative 2): [To be filled]
- Comparison: [To be filled]

**Iterations**: 0
**Time Spent**: 0 minutes

---

### Stage 4: Consolidation & Selection (If Stage 3 Run)
**Status**: ⏸️ Not Started
**Trigger**: Stage 3 completed

**Available Approaches**:
1. **Approach 1** (Original from Stage 1)
   - Strength: [To be filled]
   - Trade-off: [To be filled]

2. **Approach 2** (Alternative 1)
   - Strength: [To be filled]
   - Trade-off: [To be filled]

3. **Approach 3** (Alternative 2)
   - Strength: [To be filled]
   - Trade-off: [To be filled]

**Selected Approach**: [1/2/3]
**Selection Rationale**: [To be filled]
**Timestamp**: [To be filled]

---

### Stage 5: Marty Cagan Validation
**Status**: ⏸️ Not Started
**Agent**: Marty_Cagan_Review_Agent
**Input**: Selected approach (from Stage 1 or Stage 4)
**Output Format**: Report Card

**Validation Results**:
- **Maturity Score**: [X/10]
- **Requirements Traceability Grade**: [A/B/C/D/F]
- **Hypothesis Rigor Grade**: [A/B/C/D/F]
- **Risk Prioritization Grade**: [A/B/C/D/F]
- **Learning Velocity Grade**: [A/B/C/D/F]
- **Outcome Focus Grade**: [A/B/C/D/F]

**Critical Issues**:
- Blocking Issues: [Count]
- High Priority Issues: [Count]
- Medium Priority Issues: [Count]

**Hallucinated Releases Detected**: [Count]
**Valid Releases Confirmed**: [Count]

**Progress**:
- [ ] Requirements traceability check complete
- [ ] Vertical slice quality assessed
- [ ] Risk mitigation sequencing validated
- [ ] Continuous discovery principles verified
- [ ] Healthcare standards applied
- [ ] Scope discipline assessed
- [ ] Report card generated

**Output Location**: [To be filled]
**Iterations**: 0
**Time Spent**: 0 minutes

**User Decision Required**:
- [ ] Approve recommendations → Proceed to Stage 6
- [ ] Ignore recommendations → Proceed to Stage 6 (not recommended if score < 7)
- [ ] Iterate based on feedback → Return to Stage 1 or Stage 3

**Decision Made**: [To be filled]
**Timestamp**: [To be filled]

---

### Stage 6: Final Release Plan Generation
**Status**: ⏸️ Not Started
**Trigger**: Stage 5 approved
**Output Format**: Detailed Initiative Release Plan

**Deliverables**:
- [ ] Complete metadata and overview
- [ ] Release summary table
- [ ] Delivery timeline (Gantt chart)
- [ ] Dependency graph with decision gates
- [ ] Detailed release sections
- [ ] Key insights and fastest path
- [ ] Critical blockers documented
- [ ] JSON validation passed

**Additional Visualizations Requested**:
- [ ] Gantt chart
- [ ] Dependency flowchart
- [ ] Decision logic diagram

**Output Location**: [To be filled]
**Final Validation**: [Pass/Fail]
**Time Spent**: 0 minutes

---

## Workflow Metrics

### Timing
- **Start Time**: [Timestamp]
- **Current Stage Duration**: 0 minutes
- **Total Workflow Duration**: 0 minutes
- **Estimated Completion**: [Timestamp]

### Iterations
- **Requirements Updates**: 0
- **Alternative Approaches Generated**: 0
- **Validation Iterations**: 0
- **Stage Reversals**: 0

### Quality Indicators
- **First-Time Stage Approvals**: 0/6
- **Hallucinations Caught**: 0
- **Requirements Gaps Found**: 0
- **Final Maturity Score**: [X/10]

---

## Decision Log

### Decision 1: [Stage] - [Date]
**Context**: [What was the situation]
**Options Considered**: [List]
**Decision**: [What was decided]
**Rationale**: [Why this choice]
**Outcome**: [Result if known]

---

## Key Learnings

### What Worked Well
- [Learning 1]
- [Learning 2]

### What Could Improve
- [Challenge 1]
- [Challenge 2]

### For Next Initiative
- [Lesson 1]
- [Lesson 2]

---

## Quick Status Check

**Where am I?**: [Current stage name and number]

**What did I just complete?**: [Last completed action]

**What's next?**: [Next required action]

**Can I skip ahead?**: [Yes/No with reasoning]

**Should I iterate?**: [Yes/No with reasoning]

**Blockers**: [Any current blockers]

---

## Valid Commands at Current Stage

### Navigation
- "What stage am I at?" → Check workflow state
- "Go back to Stage [X]" → Return to previous stage
- "Skip to Stage [X]" → Jump ahead (not recommended)
- "Start over" → Restart workflow from Stage 1

### Actions (Stage-Specific)
**Stage 1**:
- "Run decomposition agent"
- "Analyze these requirements"

**Stage 2**:
- "Approve this approach"
- "Generate alternatives: [constraints]"
- "Update requirements: [changes]"

**Stage 3**:
- "Show comparison"
- "I select approach [1/2/3]"

**Stage 5**:
- "Approve recommendations"
- "Ignore recommendations and proceed"
- "Go back to Stage 1 with these changes: [changes]"

**Stage 6**:
- "Add visualizations"
- "Generate Gantt chart"
- "Export final plan"

### Help
- "Show me the workflow overview"
- "What are my options?"
- "What happens next?"
- "Why did validation fail?"

---

## Output Artifacts

### Stage 1 Output
**Type**: Release Review Summary
**Location**: [To be filled]
**Created**: [Timestamp]
**Format**: Markdown

### Stage 3 Outputs (If Generated)
**Type**: 2 Alternative Approaches + Comparison
**Locations**:
- Alternative 1: [To be filled]
- Alternative 2: [To be filled]
- Comparison: [To be filled]
**Created**: [Timestamp]
**Format**: Markdown

### Stage 5 Output
**Type**: Marty Cagan Report Card
**Location**: [To be filled]
**Created**: [Timestamp]
**Maturity Score**: [X/10]

### Stage 6 Output
**Type**: Final Initiative Release Plan
**Location**: [To be filled]
**Created**: [Timestamp]
**Format**: Markdown with Mermaid diagrams
**Release Count**: [X MVP + Y Conditional]

---

## Notes & Context

[Free-form notes for important context, observations, or reminders]
