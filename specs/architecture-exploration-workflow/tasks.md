# Implementation Tasks: Architecture Exploration Workflow

**Feature:** Architecture Exploration Workflow (REL-002)
**Status:** Ready for Implementation
**Estimated Total Time:** 22-31 hours (3-4 days)
**Dependencies:** REL-001 (Complete Project Setup with 230K token knowledge base)

---

## Task Overview

This feature implements a conversational agent workflow for exploring multiple architectural approaches. Implementation focuses on custom instructions, prompt templates, and validation scenarios rather than traditional code, as this is a Claude Desktop Project-based agent.

**Critical Success Factors:**
- Pattern diversity algorithm ensures genuinely different approaches (not variations)
- Tradeoff analysis includes disadvantages for every approach (no silver bullets)
- Context-driven recommendations based on stated constraints
- Structured consistency despite conversational interface

---

## Task 1: Custom Instructions & Conversation State Management

**Status:** [✅] COMPLETE (2025-10-27)
**Estimated Time:** 4-5 hours
**Actual Time:** ~3 hours
**Dependencies:** None (requires REL-001 complete)

### Description
Create custom instructions file that defines the agent's conversational behavior, state tracking, and workflow orchestration. This establishes the foundation for consistent multi-approach exploration across sessions.

### Acceptance Criteria
- [✅] Tests written and failing (Red)
  - [✅] Test scenario document created with expected conversation flows
  - [✅] State transition validation checklist created
- [✅] Implementation passes tests (Green)
  - [✅] Custom instructions file defines conversation phases (requirements, exploration, clarification, selection)
  - [✅] State machine logic embedded in instructions for tracking completeness
  - [✅] Gap identification prompts trigger when critical constraints missing (team size, timeline, budget)
  - [✅] Requirements confirmation summary generated before exploration begins
  - [✅] Agent maintains context across multi-turn conversations
- [✅] Code refactored (Refactor)
  - [✅] Instructions optimized for token efficiency
  - [✅] Clear separation between system behavior and user-facing language
- [✅] Manual validation with simple CRUD test scenario completes requirements gathering

### Files Created
- [✅] `/Users/rnorman/Projects/architecture-designer-claude-project/custom-instructions.md` - General architecture agent instructions (15KB)
- [✅] `/Users/rnorman/Projects/architecture-designer-claude-project/output/workflow-architecture-exploration.md` - Architecture exploration workflow (17KB)
- [✅] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/architecture-exploration-workflow/task1-test-scenarios.md` - Test scenarios and validation checklist
- [✅] `/Users/rnorman/Projects/architecture-designer-claude-project/specs/architecture-exploration-workflow/task1-completion.md` - Task completion report

### Files to Modify
- None (new agent setup)

### Test Data
- Simple CRUD requirement: "User management system, 2-person team, 3-month timeline"
- Expected: Agent asks about scale, performance targets, expertise level
- Validation: Agent summarizes requirements before proceeding to exploration

---

## Task 2: Pattern Selection Engine & Diversity Algorithm

**Status:** [✅] COMPLETE (2025-10-27)
**Estimated Time:** 4-5 hours
**Actual Time:** ~4 hours
**Dependencies:** Task 1 (conversation framework)

### Description
Implement pattern selection logic as prompt templates that query the knowledge base and ensure genuinely different architectural approaches. This is the core intelligence of the feature, preventing variations of the same pattern.

### Acceptance Criteria
- [ ] Tests written and failing (Red)
  - [ ] Pattern diversity validation checklist created
  - [ ] Test scenarios for different constraint combinations documented
- [ ] Implementation passes tests (Green)
  - [ ] Pattern selection prompts reference architecture-patterns-library.md from REL-001
  - [ ] Diversity algorithm ensures categories differ (e.g., monolithic vs microservices vs serverless)
  - [ ] Constraint mapping logic filters patterns by team size, timeline, budget, scale
  - [ ] Exactly 2-3 approaches generated per session (not configurable)
  - [ ] Simpler approaches recommended when constraints favor simplicity
- [ ] Code refactored (Refactor)
  - [ ] Selection logic consolidated into reusable prompt components
  - [ ] Clear documentation of pattern selection rules
- [ ] High-scale e-commerce test generates microservices and event-driven (not 3 microservice variations)

### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/pattern-selection-prompts.md` - Pattern query and selection logic
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/diversity-algorithm.md` - Rules ensuring different pattern categories
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/constraint-mapping-rules.md` - Requirements to pattern suitability mapping

### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/custom-instructions.md` - Integrate pattern selection logic

### Test Data
- High-scale input: "1M+ users, 100 TPS, 10-person team, 6-month timeline"
- Expected: Microservices, Event-driven, and potentially Modular Monolith (3 different categories)
- Validation: No two approaches from same pattern category (e.g., no "microservices with API gateway" and "microservices with service mesh")

---

## Task 3: Mermaid Diagram Generation Templates

**Status:** [ ] Not Started
**Estimated Time:** 3-4 hours
**Dependencies:** Task 2 (pattern selection determines components)

### Description
Create Mermaid diagram templates for system context and component structure visualizations. Templates must dynamically adapt to selected patterns while maintaining consistent visual style.

### Acceptance Criteria
- [ ] Tests written and failing (Red)
  - [ ] Visual validation checklist with diagram examples created
  - [ ] Template coverage matrix for all major patterns documented
- [ ] Implementation passes tests (Green)
  - [ ] System context diagram template shows external interactions (users, systems, services)
  - [ ] Component structure diagram template shows internal architecture
  - [ ] Templates support all major pattern types (monolithic, microservices, serverless, event-driven, modular)
  - [ ] Consistent styling applied (colors, shapes, layout direction)
  - [ ] Diagrams render correctly in Claude Desktop (validated manually)
- [ ] Code refactored (Refactor)
  - [ ] Template variables clearly documented
  - [ ] Common diagram components extracted for reuse
- [ ] Startup MVP test generates serverless diagram with API Gateway, Lambda, DynamoDB components

### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/diagram-templates/system-context-template.md` - External system interaction diagrams
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/diagram-templates/component-structure-templates.md` - Internal architecture diagrams per pattern type
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/diagram-templates/styling-guide.md` - Visual consistency rules

### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/custom-instructions.md` - Integrate diagram generation

### Test Data
- Startup MVP: "Unknown scale, 1 developer, 1-month timeline, tight budget"
- Expected: Serverless approach with system context (user → API Gateway → Lambda → DynamoDB) and component diagram (functions, data stores, event sources)
- Validation: Diagrams render without syntax errors and show appropriate components for pattern

---

## Task 4: Tradeoff Analysis Framework & Honest Recommendations

**Status:** [ ] Not Started
**Estimated Time:** 4-5 hours
**Dependencies:** Task 2 (patterns selected), Task 3 (diagrams generated)

### Description
Implement structured tradeoff analysis that evaluates each approach across standardized dimensions and ensures no approach is presented without disadvantages. This is critical for honest, context-driven recommendations.

### Acceptance Criteria
- [ ] Tests written and failing (Red)
  - [ ] Tradeoff validation checklist ensuring all approaches have pros AND cons
  - [ ] Analysis dimension coverage checklist documented
- [ ] Implementation passes tests (Green)
  - [ ] Tradeoff framework evaluates: complexity, scalability, cost, team fit, timeline fit
  - [ ] Every approach includes explicit cons/limitations (enforced by instructions)
  - [ ] Anti-patterns from knowledge base referenced when applicable
  - [ ] Context-driven recommendations based on stated constraints (not generic best practices)
  - [ ] Quantitative comparisons included where possible (team size thresholds, timeline estimates)
- [ ] Code refactored (Refactor)
  - [ ] Analysis dimensions standardized across all patterns
  - [ ] Clear structure for pros/cons presentation
- [ ] Simple CRUD test shows monolithic approach with advantages (simplicity, fast delivery) AND disadvantages (scaling limits, single point of failure)

### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/tradeoff-analysis-framework.md` - Analysis dimensions and evaluation logic
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/recommendation-engine-prompts.md` - Context-driven recommendation logic
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/anti-patterns-integration.md` - Knowledge base reference for known pitfalls

### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/custom-instructions.md` - Integrate tradeoff analysis

### Test Data
- Simple CRUD: "User management, 2-person team, 3-month timeline"
- Expected: Monolithic approach with:
  - Pros: Fast to build, simple deployment, easy debugging, fits small team
  - Cons: Harder to scale horizontally, single point of failure, difficult to split later if growth exceeds expectations
- Validation: No approach presented as "perfect" or without downsides

---

## Task 5: Clarification & Follow-up Handling

**Status:** [ ] Not Started
**Estimated Time:** 2-3 hours
**Dependencies:** Task 1-4 (all components needed for clarification context)

### Description
Implement conversation logic for handling user follow-up questions and clarification requests after initial approaches are presented. Enables deeper exploration of specific patterns or concerns.

### Acceptance Criteria
- [ ] Tests written and failing (Red)
  - [ ] Clarification scenario test cases documented
  - [ ] Follow-up response validation checklist created
- [ ] Implementation passes tests (Green)
  - [ ] Agent handles pattern-specific clarification questions
  - [ ] Knowledge base queried for detailed pattern explanations
  - [ ] Agent can suggest additional pattern variations from architecture-patterns-library
  - [ ] Comparisons between originally presented approaches and new patterns supported
  - [ ] Conversation can return to selection after clarifications
- [ ] Code refactored (Refactor)
  - [ ] Clarification handling logic clearly separated from initial exploration
  - [ ] Response templates standardized
- [ ] Enterprise integration test allows follow-up question: "How would CQRS fit here?" and receives detailed explanation comparing to original approaches

### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/clarification-handling.md` - Follow-up question logic
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/pattern-comparison-prompts.md` - Compare additional patterns to original approaches

### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/custom-instructions.md` - Integrate clarification handling
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/state-machine-logic.md` - Add clarification phase transitions

### Test Data
- Enterprise integration scenario: "Legacy system integration, compliance requirements, 20-person team"
- Initial approaches presented: Service-oriented, API Gateway, Event-driven
- Follow-up: "What about CQRS for handling complex read models?"
- Expected: Detailed CQRS explanation, comparison to original approaches, tradeoff analysis for this specific context
- Validation: Response references knowledge base and provides context-specific analysis

---

## Task 6: Validation Test Scenarios & Documentation

**Status:** [ ] Not Started
**Estimated Time:** 3-4 hours
**Dependencies:** Task 1-5 (all components implemented)

### Description
Execute manual validation across all required test scenarios from requirements.md and create comprehensive setup/usage documentation. This ensures the feature meets acceptance criteria before considering it complete.

### Acceptance Criteria
- [ ] Tests written and failing (Red)
  - [ ] Validation scenario execution checklist created
  - [ ] Expected outcomes documented for each scenario
- [ ] Implementation passes tests (Green)
  - [ ] Simple CRUD test: Monolithic presented as viable option with simplicity advantages
  - [ ] High-scale e-commerce test: Microservices and event-driven approaches with scalability tradeoffs
  - [ ] Startup MVP test: Serverless or monolithic recommended with cost/complexity analysis
  - [ ] Enterprise integration test: SOA or API Gateway patterns with integration complexity acknowledged
  - [ ] All scenarios generate 2-3 distinct approaches (not variations)
  - [ ] All scenarios include honest pros and cons for each approach
  - [ ] Diagrams render correctly for all scenarios
- [ ] Code refactored (Refactor)
  - [ ] Test scenarios organized for reusability
  - [ ] Documentation structured for maintainability
- [ ] All 4 validation scenarios pass with ≥80% requirements completeness

### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/validation-scenarios.md` - Test case definitions and expected outcomes
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/validation-results.md` - Actual test execution results
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/setup-guide.md` - Complete setup and configuration instructions
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/usage-examples.md` - Example conversations and outputs

### Files to Modify
- None

### Test Data
Execute all 4 scenarios from requirements.md:
1. **Simple CRUD**: User management, 2-person team, 3-month timeline
2. **High-Scale E-commerce**: 1M+ users, 100 TPS, 10-person team, 6-month timeline
3. **Startup MVP**: Unknown scale, 1 developer, 1-month timeline, tight budget
4. **Enterprise Integration**: Legacy integration, compliance, 20-person team

### Validation Criteria
- Each generates 2-3 distinct approaches ✓
- Diagrams render correctly ✓
- Tradeoffs specific to constraints ✓
- Simpler approaches recommended when appropriate ✓
- No approach without disadvantages ✓
- Multi-turn context maintained across conversation ✓

### Multi-Turn Context Validation
- **Test Scenario**: Simple CRUD with progressive requirement gathering
- **Turn 1**: "I need to build a task management app"
- **Turn 2**: Agent asks about team size → "3 engineers"
- **Turn 3**: Agent asks about timeline → "2 months"
- **Turn 4**: Agent asks about scale → "100-500 users initially"
- **Turn 5**: Agent presents approaches referencing ALL previous constraints
- **Expected**: Final recommendations explicitly reference team size (3), timeline (2 months), and scale (100-500) from earlier turns
- **Validation**: Context maintained without requiring user to repeat information

---

## Task 7: Integration Testing & Project Configuration

**Status:** [ ] Not Started
**Estimated Time:** 2-3 hours
**Dependencies:** Task 6 (validation complete)

### Description
Finalize Claude Desktop Project configuration, verify knowledge base integration, and perform end-to-end integration testing to ensure the complete workflow functions as designed.

### Acceptance Criteria
- [ ] Tests written and failing (Red)
  - [ ] Integration test checklist created
  - [ ] Configuration validation steps documented
- [ ] Implementation passes tests (Green)
  - [ ] Claude Desktop Project configured with custom instructions from Task 1-5
  - [ ] All 5 knowledge base files from REL-001 accessible during exploration
  - [ ] End-to-end conversation flow completes for all 4 validation scenarios
  - [ ] Performance: Architecture exploration completes within 60 seconds
  - [ ] Consistency: Similar requirements generate similar (not identical) patterns across sessions
  - [ ] Session state persists across conversation turns
- [ ] Code refactored (Refactor)
  - [ ] Project configuration optimized for performance
  - [ ] Instructions consolidated where possible to reduce token usage
- [ ] Full conversation from requirements gathering to approach selection completes successfully

### Files to Create
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/project-config.json` - Claude Desktop Project configuration
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/integration-test-results.md` - End-to-end test outcomes

### Files to Modify
- [ ] `/Users/rnorman/Projects/architecture-designer-claude-project/agents/architecture-exploration/custom-instructions.md` - Final optimizations based on integration testing

### Test Data
- Execute complete workflow for one scenario from each constraint type:
  1. Small team (2 people): Simple CRUD scenario
  2. Large team (10+ people): High-scale e-commerce scenario
  3. Solo developer: Startup MVP scenario
  4. Enterprise: Integration scenario
- Validate consistent behavior across 2 sessions for same requirements
- Measure response time from requirements complete to approaches presented

### Validation Criteria
- All 4 scenarios complete end-to-end ✓
- Response time < 60 seconds ✓
- Knowledge base referenced in recommendations ✓
- Consistent pattern selection for similar requirements ✓

---

## Implementation Notes

### Agent-Based Implementation Approach
This feature is implemented as a Claude Desktop Project agent configuration, not traditional software code. Key differences:
- **Custom Instructions** replace traditional application logic
- **Prompt Templates** replace function implementations
- **Manual Validation** replaces automated unit tests
- **Knowledge Base Integration** replaces external API calls

### Critical Success Factors
1. **Pattern Diversity**: Algorithm (prompt logic) must ensure genuinely different approaches
2. **Honest Tradeoffs**: Every approach must include disadvantages (enforced by instructions)
3. **Context-Driven**: Recommendations based on constraints, not generic best practices
4. **Structured Consistency**: Consistent output format despite conversational interface

### TDD Approach for Agent Development
- **Red Phase**: Document expected conversation flows and validation checklists
- **Green Phase**: Write custom instructions and prompt templates to achieve expected behavior
- **Refactor Phase**: Optimize instructions for token efficiency and clarity

### Knowledge Base Integration (REL-001 Dependency)
Required files from REL-001:
- `architecture-patterns-library.md` - Pattern selection reference
- `anti-patterns-case-studies.md` - Avoid known mistakes
- `technology-selection-guide.md` - Technology recommendations
- `deployment-strategies.md` - Deployment considerations
- `scalability-patterns.md` - Scaling approaches

### MVP Constraints
- 2-3 approaches only (not configurable)
- Fixed output format (no customization)
- Single user sessions (no collaboration)
- Manual testing (no automated test suite for conversational agent)

### Definition of Done
Each task is complete when:
- [ ] Validation checklist created (Red)
- [ ] Custom instructions/prompts implemented (Green)
- [ ] Instructions optimized for efficiency (Refactor)
- [ ] Manual test scenario passes with expected behavior
- [ ] Documentation complete (where applicable)

---

## Estimated Timeline

**Total Time**: 18-24 hours (2-3 days at 6-8 hours/day)

**Day 1** (8 hours):
- Task 1: Custom Instructions & Conversation State Management (4-5h)
- Task 2: Pattern Selection Engine (start, 3-4h)

**Day 2** (8 hours):
- Task 2: Pattern Selection Engine (complete, 1h)
- Task 3: Mermaid Diagram Generation (3-4h)
- Task 4: Tradeoff Analysis Framework (4-5h)

**Day 3** (6 hours):
- Task 5: Clarification Handling (2-3h)
- Task 6: Validation Test Scenarios (3-4h)
- Task 7: Integration Testing (1-2h)

---

## Success Metrics

Post-implementation validation:
- [ ] ≥60% session completion rate (users view at least 2 approaches)
- [ ] ≥70% multi-approach engagement (compare before selecting)
- [ ] ≥80% requirements completeness (all constraints gathered)
- [ ] 100% approach diversity (genuinely different patterns)
- [ ] 100% tradeoff quality (all approaches have pros AND cons)

---

**Ready to Begin**: Task 1
**Next Milestone**: After Task 3, validate diagram generation works correctly in Claude Desktop
**Final Milestone**: After Task 7, feature ready for user testing
