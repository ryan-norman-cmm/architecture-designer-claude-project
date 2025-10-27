# Architecture Design Document

## Overview
**Feature:** Staged Review Approval Workflow
**Purpose:** Add Phase 2.5 checkpoint to Architecture Exploration Workflow that generates minimal solution overviews for validation before comprehensive documentation generation
**Type:** Conversational workflow enhancement (not code implementation)

## Design Approach

### Conversational Workflow Pattern

This enhancement follows Claude Desktop's **conversational workflow** paradigm:
- No custom code or components to build
- No APIs, databases, or state management systems
- Works through instructions in knowledge base files
- Agent reads workflow file and follows conversation patterns
- State tracked implicitly through conversation context

### Integration Point

Adds **Phase 2.5: Solution Overview & Approval Checkpoint** between:
- **Phase 2**: Gap Identification (requirements complete)
- **Phase 3**: Architecture Exploration (generate 2-3 approaches)

### Design File Modified

**File:** `output/workflow-architecture-exploration.md`
**Location:** Line 97-246 (Phase 2.5 section)
**Version:** v1.2

## Workflow Design

### Phase 2.5 Flow

```
Phase 1-2: Requirements Intake & Gap Identification
    ↓
Phase 2.5: Solution Overview & Approval (NEW)
    ↓
    Generate Minimal Overview (500 words max)
    ↓
    Present to User with 3 Options:
    - ✅ Approve → Continue to Phase 3
    - 🔄 Refine → Regenerate overview with feedback
    - ❌ Reject → Return to Phase 1
    ↓
Phase 3: Architecture Exploration (blocked until approval)
    ↓
    Generate 2-3 Approaches with Diagrams
```

### Solution Overview Template

**Structure** (500 words maximum):

1. **Problem Understanding** (2-3 sentences)
   - Confirms what problem we're solving

2. **Proposed Architectural Direction** (1 paragraph)
   - High-level approach (NOT implementation details)
   - Examples: "Modular monolith", "Event-driven microservices", "Serverless"

3. **Key Assumptions** (bulleted list)
   - Team constraints
   - Scale targets
   - Timeline
   - Budget
   - Critical requirements

4. **Architectural Principles** (3-5 principles)
   - Guiding decisions for this specific solution
   - Examples: "Optimize for velocity over scale", "Minimize operational complexity"

5. **What This Enables** (2-3 sentences)
   - User capabilities from this architecture

6. **What This Defers** (2-3 items)
   - Intentionally not solving in initial design
   - Examples: "Multi-region deployment", "Real-time collaboration"

### Conversation Patterns

#### After Phase 2 Complete

```
Agent: "Before I generate 2-3 detailed architectural approaches with diagrams
and tradeoff analysis, let me confirm we're aligned on the high-level direction.

Here's my solution overview for your [project]:

[Generate overview using template - max 500 words]

---

**Review Questions:**
- Does this match your understanding of the problem?
- Is the proposed direction reasonable given your constraints?
- Any critical assumptions I got wrong?

**Your Options:**
1. ✅ **Approve** - Proceed to generate 2-3 detailed architectural approaches
2. 🔄 **Refine** - Adjust assumptions/direction and regenerate overview
3. ❌ **Reject** - We misunderstood the problem, restart requirements gathering

What would you like to do?"
```

#### User Approves

```
User: "Looks good, proceed"

Agent: "Perfect! I'll now generate 2-3 distinct architectural approaches with:
- System context diagrams
- Component structure diagrams
- Detailed tradeoff analysis
- Technology recommendations
- Fit scores

This will take a moment as I reference the knowledge base..."

[Proceed to Phase 3]
```

#### User Refines

```
User: "Actually, budget is more constrained"

Agent: "Got it! Let me update the solution overview with tighter budget constraints.

Here's the revised overview:

[Regenerate with updated assumptions]

Does this better match your needs?"

[Allow up to 3 refinement iterations]
```

#### User Rejects

```
User: "No, this isn't what I need"

Agent: "I apologize for the misunderstanding. Let's step back and clarify
the requirements.

What specifically did I get wrong?
- Problem understanding?
- Constraints?
- Priorities?

Let's restart from Phase 1 with better clarity."

[Return to Phase 1]
```

## Design Decisions

### 1. Conversational vs Code Implementation

**Decision:** Implement as conversational workflow instructions
**Rationale:**
- Claude Desktop projects work through knowledge base files, not code
- Existing workflow pattern already conversational (Phases 1-6)
- No infrastructure needed - agent reads instructions and follows them
- Faster to deploy - just update knowledge base file

**Trade-offs:**
- ✅ Simple, no code to maintain
- ✅ Works within Claude Desktop paradigm
- ✅ Easy to iterate based on user feedback
- ❌ No programmatic enforcement (relies on agent following instructions)
- ❌ Manual testing only (no automated tests)

### 2. 500-Word Limit (not 250)

**Decision:** Set overview limit to 500 words (2 pages)
**Rationale:**
- Need enough space for complete overview template sections
- 250 words too restrictive for meaningful architectural direction
- 500 words readable in < 2 minutes (meets usability goal)
- Matches "1-2 pages" mentioned in requirements

### 3. Phase Placement (2.5 vs New Phase)

**Decision:** Insert as Phase 2.5 between Gap Identification and Architecture Exploration
**Rationale:**
- Logical checkpoint after requirements complete
- Blocks expensive Phase 3 work until validated
- Doesn't disrupt existing phase numbering significantly
- Clear trigger point (requirements complete)

### 4. Maximum 3 Refinements

**Decision:** Limit refinement iterations to 3
**Rationale:**
- Prevents endless refinement loops
- If not aligned after 3 tries, requirements need deeper work
- Keeps workflow moving forward
- Agent suggests requirements clarification after limit hit

### 5. Skip Override Capability

**Decision:** Allow users to skip Phase 2.5 with explicit request
**Rationale:**
- Some users may want full exploration immediately
- Experienced architects may not need validation checkpoint
- Maintains flexibility
- Example trigger: "skip overview, give me approaches"

## Testing Strategy

### Manual Testing in Claude Desktop

1. **Upload updated workflow file** to project knowledge base
2. **Test happy path:** Requirements → Overview → Approve → Full docs
3. **Test refinement:** Requirements → Overview → Refine → Approve
4. **Test rejection:** Requirements → Overview → Reject → Restart
5. **Verify 500-word limit** on generated overviews
6. **Test skip override:** Explicit request to skip Phase 2.5

### Test Scenarios

- Simple requirements (CRUD app)
- Complex requirements (microservices system)
- Ambiguous requirements (should trigger clarification)
- Budget-constrained project
- Timeline-constrained project

### Success Criteria

- ✅ Agent consistently triggers Phase 2.5 after Phase 2
- ✅ Overviews stay within 500-word limit
- ✅ Approval blocks Phase 3 until explicit user decision
- ✅ Refinements incorporate user feedback
- ✅ Rejections return to Phase 1
- ✅ Skip requests bypass Phase 2.5

## Deployment

### Files Modified

1. ✅ `output/workflow-architecture-exploration.md` - Added Phase 2.5 (lines 97-246)
2. ✅ Updated version history to v1.2

### Deployment Steps

1. ✅ Update workflow file (completed)
2. Upload updated file to Claude Desktop project knowledge base
3. Test with sample conversations
4. Iterate based on agent behavior
5. Document any adjustments needed

### Rollback Plan

If Phase 2.5 doesn't work as expected:
- Revert to workflow v1.1 (remove Phase 2.5 section)
- Re-upload to knowledge base
- Agent returns to direct Phase 2 → Phase 3 flow

## Future Enhancements

### Not in Current Scope

1. **Comparison tools:** Side-by-side comparison of multiple refined overviews
2. **Collaborative review:** Multiple stakeholders approving overview
3. **Version control integration:** Git-based approval workflows
4. **Partial documentation generation:** Generate single approach from overview
5. **Cost estimation in overview:** Infrastructure cost projections
6. **Automated approval:** Based on confidence scores or constraints

### Possible Future Iterations

- Add Phase 5.5: Approval checkpoint before detailed component design (Phase 6)
- Template variations for different project types (greenfield, migration, scaling)
- Learning from refinement patterns to improve initial overviews
- Integration with external requirements management systems

## Validation Checklist

Before considering this design complete:

- [x] Phase 2.5 added to workflow file
- [x] Solution overview template defined (500 words max)
- [x] Conversation patterns documented (approve/refine/reject)
- [x] Critical rules specified (5 rules in workflow)
- [x] Version history updated (v1.2)
- [x] Integration with existing phases clear
- [ ] Manual testing in Claude Desktop (pending deployment)
- [ ] User feedback incorporated (pending usage)

## Documentation References

- **Workflow File:** `output/workflow-architecture-exploration.md` (Phase 2.5, lines 97-246)
- **Requirements:** `specs/staged-review-approval/requirements.md`
- **Tasks:** `specs/staged-review-approval/tasks.md`

---

**Design Status:** Complete - Ready for deployment and testing
**Implementation Type:** Conversational workflow (no code)
**Deployment Method:** Upload updated knowledge base file to Claude Desktop project
