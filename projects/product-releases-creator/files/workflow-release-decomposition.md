# Initiative Release Workflow v2.0

## Getting Started

Transform product initiatives into smallest-testable releases optimized for learning and user value.

**Provide**: Product requirements document
**Time**: 40-60 minutes (alternatives exploration mandatory)

---

## Checkpoint Pattern

After each stage output, present status and await user decision:

```markdown
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 WORKFLOW PROGRESS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Current Stage: [X of 6] - [Stage Name]
Completed: [List of completed stages]
Last Output: [What was generated]
Next Step: [What to do next]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**What would you like to do?**

Options:
[Stage-specific options based on current stage]
```

**Stage-Specific Checkpoints:**

**Stage 1 (Requirements Analysis):**
- "Approve this approach" → Skip to Stage 5 (Validation)
- "Generate alternatives" → Proceed to Stage 3
- "Update requirements: [changes]" → Re-run Stage 1

**Stage 3 (Alternative Strategies):**
- "I select approach [1/2/3]" → Proceed to Stage 5
- "Show comparison" → Display side-by-side comparison
- "Go back to Stage 1" → Revise requirements

**Stage 5 (Validation):**
- "Approve recommendations" → Proceed to Stage 6
- "Ignore recommendations and proceed" → Proceed to Stage 6 (maturity score noted)
- "Go back to Stage [1/3] with changes" → Iterate based on feedback

**Validation Rules:**
- [ ] Requirements traceability confirmed (no hallucinated features)
- [ ] Maturity score ≥7 recommended before Stage 6
- [ ] User explicitly approved decision before proceeding
- [ ] Workflow state updated in workflow-state.md

---

## The 6-Stage Workflow

### Stage 1: Requirements Analysis
**Output**: Initial release breakdown
**Details**: See `agent-decomposition.md`
**Time**: 5-10 min

**Validation Checklist**:
- [ ] Requirements document provided
- [ ] Release Review Summary generated
- [ ] All releases traced to requirements (no hallucinations)
- [ ] User types identified (Physician/Administrator/Internal)
- [ ] Bulk operations validated (frequency ≠ bulk)
- [ ] "Considered But Excluded" section documented
- [ ] User reviewed initial breakdown

### Stage 2: Review & Request Alternatives
**Required Action**: Request alternative approaches
**Note**: Alternatives are **mandatory** for exploring strategic trade-offs
**Time**: 1 min

### Stage 3: Alternative Strategies (MANDATORY)
**Output**: 3 total approaches (original + 2 alternatives)
**Constraints**: Specify risk-minimized, value-maximized, or custom
**Details**: See `agent-option-explorer.md`
**Time**: 10-15 min

**Validation Checklist**:
- [ ] User requested alternative approaches
- [ ] Constraints specified for alternatives (risk/value/custom)
- [ ] 2 alternative approaches generated
- [ ] All 3 approaches documented (original + 2 alternatives)
- [ ] Comparison table provided
- [ ] Each approach shows different strategic trade-offs

### Stage 4: Selection
**Action**: Choose best approach from 3 options
**Time**: 5 min

**Validation Checklist**:
- [ ] User reviewed all 3 approaches
- [ ] User explicitly selected one approach
- [ ] Selection rationale understood
- [ ] Selected approach confirmed before validation

### Stage 5: Validation
**Output**: Maturity score and critical issues
**Details**: See `agent-validation.md`
**Decision criteria**: See `workflow-stage-prompts.md` lines 202-206
**Time**: 5-10 min

**Validation Checklist**:
- [ ] Marty Cagan validation complete
- [ ] Maturity score calculated (1-10 scale)
- [ ] Requirements traceability verified
- [ ] Hallucinated releases flagged (if any)
- [ ] Scope discipline assessed
- [ ] Vertical slice quality validated
- [ ] User decision made (approve/iterate/ignore)
- [ ] Maturity score ≥7 recommended for proceeding

### Stage 6: Final Release Plan
**Output**: Complete release breakdown with visualizations
**Template**: `template-releases-complete.md`
**Visuals**: See `diagram-visualization-guide.md`
**Time**: 5-10 min

**Validation Checklist**:
- [ ] Complete release plan generated
- [ ] All metadata and overview included
- [ ] Release summary table complete
- [ ] Detailed release sections documented
- [ ] Dependency graph included
- [ ] Key insights and fastest path identified
- [ ] Critical blockers documented
- [ ] JSON validation passed (if applicable)
- [ ] Visualizations added (Gantt, dependencies)
- [ ] User confirmed plan is complete

---

## State Tracking

**All workflow state tracked in**: `workflow-state.md`

Maintains: current stage, decisions, outputs, metrics, timing

**Check status**: "What stage am I at?"

---

## Commands & Scenarios

**For complete command reference**: See `workflow-stage-prompts.md`
**For workflow examples**: See `workflow-stage-prompts.md` lines 210-253

---

## Knowledge Base

**Agents read these automatically**:
- `kb-health-glossary.md` - Healthcare terminology
- `kb-user-standards.md` - User type requirements (Physician/Administrator/Internal)
- `kb-best-practices.md` - Decomposition patterns and anti-patterns

**You don't need to reference these** - agents use them automatically.

---

## Templates Used

| Stage | Template |
|-------|----------|
| 1, 3 | `template-release-review.md` |
| 3 | `template-option-comparison.md` |
| 5 | `template-report-card.md` |
| 6 | `template-releases-complete.md` |

---

## Mandatory Workflow Path

**Stage 3 alternatives are required** to ensure strategic thinking:

```
Stage 1: Initial decomposition (10 min)
    ↓
Stage 2: Must request alternatives (1 min)
    ↓
Stage 3: Generate 2 alternatives (15 min)
    ↓
Stage 4: Select best approach (5 min)
    ↓
Stage 5: Validation (5 min)
    ↓
Stage 6: Final plan (5 min)

Total: ~40 minutes
```

**Why alternatives are mandatory**:
- Prevents anchoring on first solution
- Explores risk vs value trade-offs
- Identifies fastest learning paths
- Surfaces better strategic options

---

## Quality Gates

**Before Stage 5**: See `workflow-stage-prompts.md` validation criteria
**Before Stage 6**: Maturity score ≥7 or documented acceptance

---

## File Integration

**Agent details**: See individual agent files (`agent-decomposition.md`, `agent-option-explorer.md`, `agent-validation.md`)

---

## Ready to Start

Say: **"Run decomposition agent"** and provide requirements

The system will guide you through all 6 stages with alternatives exploration.
