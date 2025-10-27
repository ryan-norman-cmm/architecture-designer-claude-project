# Deployment Guide - Staged Review Approval Workflow

## Overview
This guide provides step-by-step instructions for deploying the enhanced Architecture Exploration Workflow (v1.4) to your Claude Desktop "Architecture Designer" project.

## What You're Deploying

**Feature:** Staged Review & Approval Workflow with ADR-Ready Decisions
**File:** `output/workflow-architecture-exploration.md`
**Version:** v1.4
**File Size:** ~40KB

### New Capabilities

After deployment, the Architecture Designer agent will:

1. **Review Requirements First** (Phase 1 enhancement)
   - Agent reads provided requirements documents before asking questions
   - Summarizes understanding back to user
   - Asks only clarifying questions about gaps

2. **Generate Solution Overviews for Approval** (Phase 2.5 - NEW)
   - Minimal high-level overview (500 words max)
   - User approval required before detailed documentation
   - Supports approve/refine/reject workflow
   - Prevents wasted effort on wrong direction

3. **Research Technologies via Web Search** (Phase 2.75 - NEW)
   - Looks up current technology capabilities when mentioned
   - Uses web search for up-to-date information
   - Focuses on features relevant to system design
   - Optional, triggered when technologies specified

4. **Capture ADR-Ready Decisions** (Phase 3 enhancement)
   - Each architectural approach includes technology decisions
   - Decision context: rationale, alternatives, tradeoffs
   - Enables ADR generation without detailed component design

5. **Recommend ADR Generation** (Phase 5 update)
   - Default path: Generate 3-5 ADRs in 10-15 minutes
   - Optional path: Detailed component design (1-2 hours)
   - Phase 6 (detailed design) now optional for most teams

## Deployment Steps

### 1. Locate the Workflow File

**File Path:** `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md`

**Verify Version:**
```bash
head -20 /Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md | grep "Version:"
```

Expected output: `**Version:** v1.4`

### 2. Open Claude Desktop

1. Launch the Claude Desktop application
2. Navigate to your **"Architecture Designer"** project
3. If you don't have this project yet, create it:
   - Click "New Project"
   - Name: "Architecture Designer"
   - Add relevant knowledge base files

### 3. Upload Workflow File

1. In the Architecture Designer project, go to **Project Settings** or **Knowledge Base**
2. Locate the existing `workflow-architecture-exploration.md` file (if it exists)
3. **Replace or upload** the new version:
   - If replacing: Delete old file, then upload new version
   - If new: Upload `output/workflow-architecture-exploration.md`
4. Verify upload success:
   - File size should be ~40KB
   - No upload errors

### 4. Verify Deployment

Open a new conversation in the Architecture Designer project and ask:

```
What are all the phases in the architecture exploration workflow,
and what was added in version 1.4?
```

**Expected Response:**

The agent should mention:
- **Phase 1:** Requirements Intake (enhanced to review requirements first)
- **Phase 2:** Gap Identification
- **Phase 2.5:** Solution Overview & Approval Checkpoint (NEW in v1.2)
- **Phase 2.75:** Technology Research & Discovery (NEW in v1.3)
- **Phase 3:** Architecture Exploration (enhanced in v1.4 with ADR-ready decisions)
- **Phase 4:** Approach Selection & Refinement
- **Phase 5:** Documentation Generation (updated to emphasize ADR generation)
- **Phase 6:** Detailed Component Design (now optional)

If the agent correctly lists these phases and mentions the enhancements, deployment is successful.

### 5. Quick Functionality Test

Test the approval workflow with a simple example:

```
I want to build a task management app for a team of 3 engineers.
We have 100-500 users expected in the first year, and a 2-month timeline.
```

**Expected Behavior:**

1. Agent reviews your requirements (Phase 1)
2. Agent generates a solution overview (Phase 2.5) - should be < 500 words
3. Agent presents 3 options: **Approve / Refine / Reject**
4. If you select "Approve", agent proceeds to Phase 3 with 2-3 detailed approaches

## Testing

After deployment, use the comprehensive testing template to validate all scenarios:

**File:** `specs/staged-review-approval/testing-results.md`

### Test Scenarios

1. **Happy Path** (2 test cases)
   - Simple CRUD application
   - Complex microservices system

2. **Refinement Path** (3 test cases)
   - Budget constraint refinement
   - Timeline constraint refinement
   - Multiple refinements (up to 3)

3. **Rejection Path** (1 test case)
   - Misunderstood requirements

4. **Size Constraint Validation** (10 test cases)
   - Verify all overviews stay within 500 words

5. **Skip Override** (1 test case)
   - User requests skipping Phase 2.5

6. **Technology Research** (1 test case)
   - Phase 2.75 web search functionality

7. **ADR Generation** (1 test case)
   - Generate ADRs from Phase 3 without Phase 6

**Total:** 19 test cases across 7 scenarios

## Troubleshooting

### Issue: Agent doesn't trigger Phase 2.5

**Symptoms:** Agent goes directly from Phase 2 to Phase 3 without generating overview

**Solutions:**
1. Verify workflow file version is v1.4 (check file header)
2. Ensure file was uploaded to correct project
3. Try asking: "Can you generate a solution overview before detailed approaches?"
4. Start a new conversation (agent may have cached old workflow)

### Issue: Solution overviews exceed 500 words

**Symptoms:** Generated overviews are 800-1000 words

**Solutions:**
1. Explicitly remind agent: "Keep the overview under 500 words"
2. Check that workflow file v1.4 is uploaded (has explicit 500-word limit)
3. Provide feedback: "This is too detailed, please make it more concise"

### Issue: Agent doesn't offer web search for technologies

**Symptoms:** Phase 2.75 doesn't trigger when technologies are mentioned

**Solutions:**
1. Explicitly request: "Can you research [Technology] latest features via web search?"
2. Verify workflow file includes Phase 2.75 (added in v1.3)
3. Phase 2.75 is optional - agent may skip if knowledge base is sufficient

### Issue: Agent doesn't include technology decisions in Phase 3

**Symptoms:** Approaches lack decision context for ADRs

**Solutions:**
1. Verify workflow file version is v1.4
2. Explicitly request: "Include technology decisions with rationale and tradeoffs"
3. Check Phase 3 output format in workflow file

### Issue: Agent still recommends Phase 6 over ADR generation

**Symptoms:** Agent suggests detailed component design instead of ADRs

**Solutions:**
1. Verify workflow file v1.4 (Phase 5 update)
2. Explicitly say: "Generate ADRs from Phase 3 decisions instead of Phase 6"
3. Check Phase 5 "What would you like next?" section in workflow file

## Rollback Plan

If the new workflow causes issues, you can rollback to a previous version:

### Option 1: Revert to v1.3 (Technology Research without ADR enhancements)
- Remove Phase 3 "Key Technology Decisions" section
- Remove Phase 5 ADR generation emphasis
- Keep Phase 2.5 and 2.75

### Option 2: Revert to v1.2 (Solution Overview only)
- Remove Phase 2.75 (Technology Research)
- Remove Phase 1 enhancements
- Remove Phase 3 and 5 enhancements
- Keep only Phase 2.5

### Option 3: Revert to v1.0 (Original workflow)
- Remove all enhancements
- Direct Phase 2 → Phase 3 flow
- No approval checkpoint
- No technology research
- No ADR-ready decisions

**To Rollback:**
1. Use git to retrieve previous version: `git show HEAD~N:output/workflow-architecture-exploration.md`
2. Upload previous version to Claude Desktop project
3. Test that agent follows old workflow

## Post-Deployment Checklist

- [ ] Workflow file v1.4 uploaded to Claude Desktop project
- [ ] Agent correctly lists all phases (including 2.5, 2.75)
- [ ] Quick functionality test passed (approval workflow works)
- [ ] Testing results template reviewed (`testing-results.md`)
- [ ] Team informed about new workflow capabilities
- [ ] Feedback channel established for workflow improvements

## Success Metrics

Track these metrics over the first 2 weeks:

1. **Reduction in Regeneration**
   - Target: 70% decrease in full documentation regeneration due to approach changes
   - Measure: Count of "Refine" vs "Approve" decisions in Phase 2.5

2. **Time to Validation**
   - Target: Average time from requirements to approved overview < 5 minutes
   - Measure: Timestamp from requirements input to approval

3. **User Satisfaction**
   - Target: 80% of users report improved confidence in final documentation
   - Measure: Post-session survey or feedback

4. **Iteration Efficiency**
   - Target: Average refinements per overview ≤ 1.5
   - Measure: Count of refinement iterations before approval

5. **ADR Generation Adoption**
   - Target: 70% of users choose ADR generation over Phase 6
   - Measure: Phase 5 decision tracking

## Support and Feedback

If you encounter issues or have suggestions for improving the workflow:

1. Document the issue in `specs/staged-review-approval/testing-results.md`
2. Include:
   - Date/time of issue
   - Test scenario being run
   - Expected vs actual behavior
   - Screenshots (optional)
3. Create a follow-up spec for workflow refinements if needed

## Version History

- **v1.0** (Initial): Original 6-phase workflow
- **v1.2** (Phase 2.5): Added Solution Overview & Approval Checkpoint
- **v1.3** (Phase 2.75): Added Technology Research via Web Search, enhanced Phase 1
- **v1.4** (ADR-ready): Enhanced Phase 3 with technology decisions, updated Phase 5 to emphasize ADR generation

**Current Deployment:** v1.4

---

**Deployment prepared by:** Architecture Designer Claude Desktop agent
**Last updated:** 2025-10-27
**Spec location:** `specs/staged-review-approval/`
