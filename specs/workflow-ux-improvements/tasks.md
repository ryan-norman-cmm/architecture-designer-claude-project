# Implementation Tasks: Workflow UX Improvements

**Feature:** workflow-ux-improvements
**Target:** Architecture Exploration Workflow v1.7 → v1.8
**Type:** Conversational workflow refactoring (documentation enhancement)
**Estimated Total Time:** 16-24 hours (2-3 days at 8h/day)

---

## Task Breakdown

### Task 1: Create Knowledge Base Templates
- **Status:** [ ] Not Started
- **Estimated Time:** 3 hours
- **Dependencies:** None
- **Type:** Foundation - Template Creation

#### Acceptance Criteria
- [ ] **Validation Test Written**: Template format validation checklist created
  - Table column widths (mobile-friendly ≤80 chars)
  - Line count constraints (comparison table: 50-75 lines)
  - Markdown syntax validation
  - Checkpoint option count (2-3 options)
- [ ] **Template 1**: `kb/templates/comparison-table.md` created
  - [ ] Architecture comparison table structure (4 columns: Approach, Key Pattern, Best For, Main Tradeoff)
  - [ ] Technology decision table structure (5 columns: Category, Chosen, Why, Alternative, Trade-off)
  - [ ] Checkpoint format at end (3 contextual options)
  - [ ] Line count: 50-75 lines maximum
- [ ] **Template 2**: `kb/templates/progressive-questions.md` created
  - [ ] Single question format per exchange
  - [ ] "Why this matters" rationale section
  - [ ] Example answers/options
  - [ ] Plain language (8th grade reading level)
- [ ] **Template 3**: `kb/templates/learning-snippet.md` created
  - [ ] Blockquote format with emoji marker
  - [ ] 2-3 sentence explanation
  - [ ] Real-world analogy section
  - [ ] Technical term → plain English pattern
- [ ] **Template 4**: `kb/templates/checkpoint-format.md` created
  - [ ] Standard checkpoint structure
  - [ ] Contextual option patterns (continue/adjust/explain)
  - [ ] User input format guidance
  - [ ] Visual separator markers
- [ ] **Format Validation Tests**: Each template validated against constraints
  - [ ] Mobile rendering (80 char width test)
  - [ ] Line count verification
  - [ ] Reading level check (Flesch-Kincaid)
- [ ] **Refactored Code**: N/A (documentation only)

#### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/kb/templates/comparison-table.md`
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/kb/templates/progressive-questions.md`
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/kb/templates/learning-snippet.md`
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/kb/templates/checkpoint-format.md`
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/template-validation-checklist.md`

---

### Task 2: Refactor Phase 1 - Progressive Requirements Gathering
- **Status:** [ ] Not Started
- **Estimated Time:** 3 hours
- **Dependencies:** Task 1 (templates must exist)
- **Type:** Workflow Refactoring - Critical Path (Time to Value)

#### Acceptance Criteria
- [ ] **Test Cases Written**: Phase 1 conversation validation scenarios
  - [ ] Scenario 1: User with provided requirements (document review first)
  - [ ] Scenario 2: User with no requirements (progressive questions)
  - [ ] Scenario 3: Incomplete answers (skip inferrable questions)
  - [ ] Line count per question exchange: ≤20 lines
- [ ] **One Question Per Exchange**: Replace batched questions with sequential pattern
  - [ ] Remove multi-question blocks from lines 88-104 (current v1.7)
  - [ ] Insert progressive question template references
  - [ ] Add "Question N of ~5" progress indicator
  - [ ] Include "Why this matters" rationale for each question
- [ ] **Contextual Question Flow**: Add question routing logic
  - [ ] Document how to skip inferrable questions based on previous answers
  - [ ] Add example answer patterns per question type
  - [ ] Include platform context questions (auth, notifications, storage)
- [ ] **First Checkpoint**: Insert checkpoint after 3 questions (before proceeding to Phase 2)
  - [ ] Format: Reference checkpoint template
  - [ ] Options: "Continue questions" / "Skip to overview" / "Adjust answers"
- [ ] **Line Count Validation**: Each question exchange stays under 20 lines
- [ ] **Refactored Code**: Phase 1 section (lines 21-106) updated with progressive pattern

#### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md` (Phase 1: lines 21-106)

#### Files to Create (Test Documentation)
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/test-scenarios-phase1.md`

---

### Task 3: Insert Phase 2.5 Enhancement - Comparison Table First
- **Status:** [ ] Not Started
- **Estimated Time:** 4 hours
- **Dependencies:** Task 1 (comparison table template)
- **Type:** New Feature - Summary-First Pattern

#### Acceptance Criteria
- [ ] **Test Cases Written**: Comparison table validation scenarios
  - [ ] Table renders correctly (50-75 lines)
  - [ ] Mobile-friendly width (≤80 chars per row)
  - [ ] 3-5 approaches maximum
  - [ ] Checkpoint after table with clear options
- [ ] **Phase 2.5 Section Created**: Insert after Phase 2 (after line 142)
  - [ ] Instructions: Generate comparison table BEFORE detailed approaches
  - [ ] Format: Reference comparison-table.md template
  - [ ] Constraint: 50-75 lines maximum
  - [ ] Content: High-level summary only (no implementation details)
- [ ] **Comparison Table Structure**: Define required columns
  - [ ] Approach name (20 char max)
  - [ ] Key pattern (30 char max)
  - [ ] Best for (50 char max)
  - [ ] Main tradeoff (50 char max)
- [ ] **Checkpoint After Table**: User selection gates detailed generation
  - [ ] Options: "See Approach N details" / "Compare technologies" / "Adjust requirements"
  - [ ] Only generate full Phase 3 details after user selection
- [ ] **Time to Value**: Instructions ensure table appears within 2 minutes of starting
  - [ ] Maximum 3 progressive questions before table
  - [ ] No detailed approaches until user requests
- [ ] **Refactored Code**: Phase 2.5 inserted (new section ~100 lines)

#### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md` (Insert Phase 2.5 after line 142)

#### Files to Create (Test Documentation)
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/test-scenarios-phase25.md`

---

### Task 4: Refactor Phase 3 - Chunking and Checkpoints
- **Status:** [ ] Not Started
- **Estimated Time:** 5 hours
- **Dependencies:** Task 1 (checkpoint template), Task 3 (comparison table as entry point)
- **Type:** Core Refactoring - Cognitive Load Reduction

#### Acceptance Criteria
- [ ] **Test Cases Written**: Chunking behavior validation
  - [ ] Output segment stays within 50-100 lines
  - [ ] Checkpoint appears at natural break points (section boundaries)
  - [ ] Context preserved across chunks
  - [ ] Tables/code blocks not broken mid-content
- [ ] **Chunking Engine Instructions**: Add line-counting guidance to Phase 3
  - [ ] Monitor output generation (target: 75 lines ±25)
  - [ ] Insert checkpoint at natural break (section boundary or paragraph end)
  - [ ] Never break: tables mid-row, code blocks mid-function, bullet lists mid-item
  - [ ] Store continuation context for next chunk
- [ ] **Checkpoint Placement**: Identify 4-6 checkpoint locations in Phase 3
  - [ ] After comparison table (already in Task 3)
  - [ ] After first approach overview (before detailed component breakdown)
  - [ ] Mid-approach (after component diagrams, before technology decisions)
  - [ ] After approach complete (before next approach or final recommendation)
  - [ ] Each checkpoint references checkpoint-format.md template
- [ ] **Content Restructuring**: Break monolithic approach sections into chunks
  - [ ] Chunk 1: System context diagram + high-level pros/cons (50-75 lines)
  - [ ] Checkpoint: "Continue with component details?"
  - [ ] Chunk 2: Component structure + technology decisions (50-100 lines)
  - [ ] Checkpoint: "See tradeoff analysis?"
  - [ ] Chunk 3: Fit score + detailed tradeoffs (50-75 lines)
- [ ] **Context Preservation**: Add brief recap at each checkpoint
  - [ ] "So far we've covered: [2-3 bullet summary]"
  - [ ] "Next up: [what user will see if they continue]"
- [ ] **Line Count Validation**: Average segment size 50-100 lines (measure in testing)
- [ ] **Refactored Code**: Phase 3 section (lines 389-644) restructured with chunking

#### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md` (Phase 3: lines 389-644)

#### Files to Create (Test Documentation)
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/test-scenarios-phase3-chunking.md`

---

### Task 5: Add Learning Snippet Pattern Throughout
- **Status:** [ ] Not Started
- **Estimated Time:** 2 hours
- **Dependencies:** Task 1 (learning snippet template)
- **Type:** Enhancement - Inline Education

#### Acceptance Criteria
- [ ] **Test Cases Written**: Learning snippet validation
  - [ ] Technical term first use triggers snippet
  - [ ] Snippet format: blockquote with 2-3 sentences
  - [ ] Includes real-world analogy
  - [ ] Reading level: 8th grade or below
- [ ] **Phase 1 Snippets**: Add learning snippets for key requirements concepts
  - [ ] "Platform services" (auth, notifications, storage)
  - [ ] "Open standards" (REST, FHIR, OpenAPI)
  - [ ] "MVP scope" (minimal viable vs future features)
- [ ] **Phase 2.5 Snippets**: Add snippets for architecture pattern types
  - [ ] "Monolithic Architecture" (restaurant kitchen analogy)
  - [ ] "Microservices" (specialized stations analogy)
  - [ ] "Event-Driven" (message queue analogy)
- [ ] **Phase 3 Snippets**: Add snippets for technology terms
  - [ ] First use of technical terms: JSONB, Redis, Lambda, etc.
  - [ ] Format: Reference learning-snippet.md template
  - [ ] Placement: Immediately after first mention, before usage details
- [ ] **Snippet Density**: Maximum 1 snippet per 50 lines (avoid overwhelming)
- [ ] **Refactored Code**: 8-12 learning snippets inserted across all phases

#### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md` (All phases: scattered insertions)

#### Files to Create (Test Documentation)
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/learning-snippets-glossary.md` (tracks all snippets added)

---

### Task 6: Update Conversation Patterns Across All Phases
- **Status:** [ ] Not Started
- **Estimated Time:** 3 hours
- **Dependencies:** Tasks 2-5 (all phase refactorings complete)
- **Type:** Integration - Consistency Pass

#### Acceptance Criteria
- [ ] **Test Cases Written**: End-to-end conversation flow validation
  - [ ] Happy path: Start → 3 questions → comparison table → approach details → selection
  - [ ] Early exit: Comparison table → immediate selection (skip details)
  - [ ] Course correction: Mid-workflow "adjust requirements"
  - [ ] Learning mode: Multiple "explain" requests at checkpoints
- [ ] **Phase Transitions**: Add checkpoints at all phase boundaries
  - [ ] Phase 1 → Phase 2: After requirements complete
  - [ ] Phase 2 → Phase 2.5: Before generating comparison table
  - [ ] Phase 2.5 → Phase 3: After table, user selects approach to explore
  - [ ] Phase 3 → Phase 4: After approach exploration complete
  - [ ] Phase 4 → Phase 5: After clarification questions
- [ ] **Checkpoint Consistency**: Standardize all checkpoint formats
  - [ ] All use checkpoint-format.md template structure
  - [ ] Contextual options (2-3 max per checkpoint)
  - [ ] Always include: "continue" / "adjust" / "explain" variants
  - [ ] Visual consistency: separator lines, emoji markers
- [ ] **Response Constraint**: Update all conversation examples to show chunked responses
  - [ ] Example responses limited to 50-100 lines
  - [ ] Include continuation context for multi-chunk examples
  - [ ] Show checkpoint after each example chunk
- [ ] **Meta-Instructions**: Add workflow execution guidance
  - [ ] "Count lines as you generate output"
  - [ ] "Insert checkpoint at 75 lines (±25 for natural break)"
  - [ ] "Wait for user input at each checkpoint"
  - [ ] "Never generate more than 100 lines without checkpoint"
- [ ] **Refactored Code**: All conversation pattern examples updated throughout workflow

#### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md` (Entire file: consistency pass)

#### Files to Create (Test Documentation)
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/checkpoint-inventory.md` (lists all checkpoints and their contexts)

---

### Task 7: Manual Conversational Testing and Validation
- **Status:** [ ] Not Started
- **Estimated Time:** 4-6 hours
- **Dependencies:** Tasks 1-6 (all refactoring complete)
- **Type:** Quality Assurance - Manual Testing

#### Acceptance Criteria
- [ ] **Test Plan Created**: Reference staged-review-approval pattern (19 test cases model)
  - [ ] 8-10 conversational test scenarios documented
  - [ ] Each scenario includes: user input sequence, expected checkpoints, line counts
  - [ ] Success criteria per scenario (time to value, checkpoint count, cognitive load)
- [ ] **Test Scenario 1: Happy Path Flow** (Simple CRUD app)
  - [ ] Run conversation: requirements → comparison table → approach selection → ADR generation
  - [ ] Validate: 8-10 checkpoints encountered
  - [ ] Validate: Average segment size 50-100 lines
  - [ ] Validate: Time to comparison table < 2 minutes
  - [ ] Document: Actual vs expected checkpoint placements
- [ ] **Test Scenario 2: Early Value Extraction** (Startup MVP)
  - [ ] Run conversation: minimal questions → comparison table → immediate selection
  - [ ] Validate: Skip detailed exploration (user gets value from table only)
  - [ ] Validate: Total time < 5 minutes
- [ ] **Test Scenario 3: Learning Mode** (Complex microservices)
  - [ ] Run conversation: trigger 3+ "explain" requests at checkpoints
  - [ ] Validate: Learning snippets appear (2-3 sentences + analogy)
  - [ ] Validate: Return to previous context after explanation
- [ ] **Test Scenario 4: Course Correction** (Legacy modernization)
  - [ ] Run conversation: provide requirements → see comparison → adjust requirements → regenerate
  - [ ] Validate: Refinement workflow (max 3 iterations)
  - [ ] Validate: Context preserved across adjustments
- [ ] **Test Scenario 5: Deep Dive Exploration** (Healthcare FHIR platform)
  - [ ] Run conversation: full Phase 3 exploration with all approach details
  - [ ] Validate: 15-20 total checkpoints (chunked output)
  - [ ] Validate: No single output exceeds 100 lines
- [ ] **Metrics Validation**: Measure against success criteria
  - [ ] Cognitive Load: Average segment 50-100 lines (target met)
  - [ ] Time to Value: First insight < 2 min (target met)
  - [ ] User Control: 8-10 checkpoints minimum (target met)
  - [ ] Conversation Length: 8-12 exchanges typical (target met)
- [ ] **Regression Testing**: Ensure core workflow functionality preserved
  - [ ] Pattern selection still works (2-3 diverse approaches)
  - [ ] Fit scoring still accurate (platform cohesion, vendor leverage)
  - [ ] Diagrams still generated (Mermaid context + component)
  - [ ] Tradeoff analysis still honest (pros AND cons)
- [ ] **Bug Fixes**: Document and fix issues found during testing
  - [ ] Checkpoint placement issues (breaking mid-table, etc.)
  - [ ] Line count inaccuracies (segments too long/short)
  - [ ] Context loss between chunks
  - [ ] Missing learning snippets for key terms
- [ ] **Test Results Documented**: Test report with pass/fail per scenario
  - [ ] Screenshots or conversation logs per scenario
  - [ ] Metrics collected (line counts, time measurements, checkpoint counts)
  - [ ] Issues found and resolution status

#### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/test-plan.md`
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/test-results.md`
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/test-scenarios-full.md` (8-10 scenarios with expected outputs)
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/workflow-ux-improvements/conversation-logs/` (directory for test conversation exports)

#### Files to Modify (if bugs found)
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md` (bug fixes)

---

## Task Dependencies Diagram

```
Task 1 (Templates)
    ├─→ Task 2 (Phase 1 - Progressive Questions)
    ├─→ Task 3 (Phase 2.5 - Comparison Table)
    │       └─→ Task 4 (Phase 3 - Chunking)
    └─→ Task 5 (Learning Snippets)

Tasks 2-5 → Task 6 (Consistency Pass) → Task 7 (Testing)
```

---

## Implementation Notes

### TDD Approach for Documentation Workflow

Since this is a conversational workflow (not code), the TDD approach adapts as follows:

1. **Red (Test First)**: Write conversation scenarios with expected behavior (line counts, checkpoint placements, user interactions)
2. **Green (Implement)**: Refactor workflow instructions to produce expected conversation patterns
3. **Refactor**: Optimize wording, consolidate patterns, reference templates for consistency

### Testing Strategy

- **Manual Conversational Testing**: No automated E2E (conversational agents don't support Playwright)
- **Reference Model**: staged-review-approval feature's 19 test cases approach
- **Validation Metrics**: Line counts, time measurements, checkpoint counts (manual observation)
- **Test Documentation**: Conversation logs exported as markdown for review

### File Organization

```
specs/workflow-ux-improvements/
├── requirements.md (existing)
├── design.md (existing)
├── tasks.md (this file)
├── .spec-meta.json (update phase to "implementation")
├── template-validation-checklist.md (Task 1)
├── test-plan.md (Task 7)
├── test-results.md (Task 7)
├── test-scenarios-phase1.md (Task 2)
├── test-scenarios-phase25.md (Task 3)
├── test-scenarios-phase3-chunking.md (Task 4)
├── test-scenarios-full.md (Task 7)
├── learning-snippets-glossary.md (Task 5)
├── checkpoint-inventory.md (Task 6)
└── conversation-logs/ (Task 7)
    ├── test1-happy-path.md
    ├── test2-early-exit.md
    ├── test3-learning-mode.md
    └── ...

kb/templates/ (new directory)
├── comparison-table.md (Task 1)
├── progressive-questions.md (Task 1)
├── learning-snippet.md (Task 1)
└── checkpoint-format.md (Task 1)

output/
└── workflow-architecture-exploration.md (v1.7 → v1.8)
```

---

## Success Criteria Summary

### Per-Task Validation
- **Task 1**: All 4 templates created, format validated (line counts, mobile width)
- **Task 2**: Phase 1 uses progressive questions (1 per exchange, <20 lines each)
- **Task 3**: Comparison table appears as first value (50-75 lines, <2 min from start)
- **Task 4**: Phase 3 chunked (50-100 line segments, checkpoints at breaks)
- **Task 5**: Learning snippets inserted (8-12 total, 8th grade reading level)
- **Task 6**: All checkpoints consistent (checkpoint-format.md template used)
- **Task 7**: 5 test scenarios pass (metrics validate targets from requirements.md)

### Overall Feature Success (from requirements.md)
- Cognitive Load: Average lines per segment 50-100 (vs current 500-1000)
- Time to Value: First insight < 2 minutes (comparison table)
- User Control: 8-10 checkpoints per session (vs current 3)
- Conversation Length: 8-12 exchanges typical (vs current 15-20)
- Understanding: Clear explanations with analogies (learning snippets)

---

## Version History

**v1.0** - 2025-10-27
- Initial task breakdown for workflow-ux-improvements
- 7 tasks: Templates → Phase refactoring → Testing
- Estimated 16-24 hours total
- Manual conversational testing approach
- TDD adapted for documentation workflow
