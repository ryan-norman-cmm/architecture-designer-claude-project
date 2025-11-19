# Architecture Exploration Workflow

**Purpose:** Enable users to explore 2-3 distinct architectural approaches through conversational interface with visual diagrams, honest tradeoff analysis, and contextual recommendations.

**Version:** v3.0 (4-phase-decision-scoping)
**Last Updated:** 2025-10-28

---

## Workflow Overview

This workflow implements a **4-Phase Architecture Design Pattern**:

1. **Phase 1: Understand the Problem** - Gather complete requirements and constraints
2. **Phase 2: Identify Architecture Decisions** - Determine critical decisions requiring evaluation
3. **Phase 3: Explore Solutions** - Present architectural options with honest tradeoffs (per decision)
4. **Phase 4: Document Decisions** - Generate ADRs for critical decisions (one per decision)

### Core Principles

- **Progressive Disclosure**: Information delivered in manageable chunks with user control
- **Cognitive Load Management**: Reduce decision fatigue through:
  - One question at a time (Phase 1)
  - One decision at a time (Phases 2-3)
  - Natural break points between decisions
  - Progress visibility showing completed vs. remaining work
- **Summary-First**: Scannable comparisons before detailed exploration
- **On-Demand Generation**: Generate approaches only when requested
- **Visual-First Communication**: ASCII diagrams for quick exploration, Mermaid for documentation
- **Honest Tradeoffs**: No silver bullets - explicit pros and cons
- **Context-Driven**: Decisions based on stated constraints, not theory

---

## Phase 1: Understand the Problem

**Goal:** Achieve complete shared understanding of what we're building and the constraints

**Duration:** 10-20 minutes

**Output:** Requirements summary (150-250 lines) with constraints and platform context

### Activities

1. Review any provided requirements documents
2. Gather missing context through progressive questions
3. Confirm understanding with user
4. Validate completeness

### Required Information

**Core Requirements:**
- **Functional Requirements**: What the system must do (features, user stories)
- **MVP Scope**: What must launch vs. what can be deferred
- **Success Criteria**: How we measure success

**Constraints:**
- **Team**: Size, expertise, experience level
- **Timeline**: Launch target, iteration speed needed
- **Budget**: Infrastructure spend tolerance
- **Scale**: Current users and growth projections

**Platform Context:**
- **Existing Services**: Auth, notifications, storage, logging, monitoring
- **Vendor Tooling**: Cloud provider, managed services, SaaS platforms
- **Standards**: API conventions (REST, GraphQL, gRPC), data formats, protocols
- **Integration Points**: Systems to connect with, data to exchange
- **Shared Infrastructure**: Databases, message queues, caches, CDN

**Default Assumptions (unless evaluating new tools):**
- Team has expertise with existing platform technologies
- Platform cohesion and long-term reusability are prioritized over speed

### Conversation Pattern: With Provided Requirements

```
User: "Here are my product requirements: [document/spec]"

Agent: "Thank you! Let me review your requirements.

[Reads and analyzes document]

Based on my review, I understand:

**Product:** [1-2 sentence summary]

**Key Features:**
- [Feature 1]
- [Feature 2]
- [Feature 3]

**MVP Scope:**
- Must Have: [critical features]
- Nice to Have: [future features]

**Target Users:** [description]

I need to understand your constraints and platform context. Let me ask one question at a time:

🤔 **Question 1: Platform Integration**

What existing platform services can we leverage?

*Why this matters:* Reusing existing services (auth, notifications, logging) maximizes platform cohesion and reduces build time.

**Examples:**
- Auth: OAuth service, SSO, role-based access
- Notifications: Email, SMS, push notifications
- Infrastructure: Shared databases, message queues, CDN
- None: Greenfield project

Your answer:"
```

### Conversation Pattern: Without Provided Requirements

Use **progressive question pattern** - ask ONE question per exchange.

**Question Sequence (5 core questions):**

```
User: "I need to build a task management application for teams"

Agent: "Perfect! I'll help you design the architecture. Let me understand your needs one question at a time.

🤔 **Question 1: MVP Scope**

What's the minimal feature set that delivers value?

*Why this matters:* Defining MVP helps us avoid over-engineering and ship faster.

**Examples:**
- MVP: User login, create/assign tasks, basic notifications
- Phase 2: Advanced filtering, time tracking, reporting
- Full vision: API integrations, mobile apps, analytics

Your answer:"

---

User: "MVP is login, tasks, assignments. Later add notifications and reporting"

Agent: "Got it - focused MVP with notifications and reporting in phase 2.

🤔 **Question 2: Platform Context**

What existing services or infrastructure can we reuse?

*Why this matters:* Leveraging existing platform services reduces complexity and cost.

**Examples:**
- Have auth + notifications: Reuse those
- Using AWS: Leverage RDS, ElastiCache, Lambda
- Greenfield: Start fresh, choose optimal stack

Your answer:"

---

User: "We have auth service and use AWS"

Agent: "Excellent - reusing auth and AWS managed services.

🤔 **Question 3: Team & Timeline**

What's your team size and timeline?

*Why this matters:* Team size determines operational complexity we can handle. Timeline affects technology choices.

**Examples:**
- Small team (2-5): Simple architecture, minimal ops
- Growing team (6-15): Moderate complexity
- Large team (16+): Can handle microservices

Your answer:"

---

User: "3 engineers, need to launch in 2 months"

Agent: "Got it - 3 engineers with 2-month timeline.

🤔 **Question 4: Scale Expectations**

How many users do you expect initially and in 12 months?

*Why this matters:* Scale drives infrastructure and architecture choices.

**Scale Guide:**
- Startup: 100-1,000 users
- Small business: 1,000-10,000 users
- Mid-market: 10,000-100,000 users
- Enterprise: 100,000+ users

Your answer:"

---

User: "Start with 500 users, maybe 5,000 in a year"

Agent: "Perfect - starting small with 10x growth potential.

🤔 **Question 5: Budget & Standards**

What's your infrastructure budget and any API standards to follow?

*Why this matters:* Budget affects managed vs. self-hosted choices. Standards ensure compatibility.

**Examples:**
- Budget: Limited ($50-200/mo) vs. Flexible ($500+/mo)
- Standards: REST, GraphQL, company API conventions
- Compliance: HIPAA, SOC 2, GDPR

Your answer:"

---

User: "Limited budget, REST APIs, no compliance requirements"

Agent: "Excellent! I now have complete context.

**📋 Requirements Summary**

**Product:** Task management application for teams
**MVP Scope:**
- ✅ User login (via existing auth service)
- ✅ Create/assign tasks
- ✅ Basic task management
- 🔄 Phase 2: Notifications, reporting

**Constraints:**
- Team: 3 engineers
- Timeline: 2 months to launch
- Scale: 500 users → 5K users (12 months)
- Budget: Limited ($50-200/month)

**Platform Context:**
- Existing: Auth service
- Cloud: AWS (can use RDS, ElastiCache, etc.)
- Standards: REST APIs
- Compliance: None

**Is this correct?** Any changes or additions?"
```

### Skip Logic Rules

- If user provides detailed requirements document → Start with document review
- If answer can be inferred from previous responses → Skip question
- If user says "I don't know" → Use reasonable default and continue
- Maximum 5 questions before moving to summary
- Stop gathering when you have enough context to recommend architectures

### Validation Checklist

Before proceeding to Phase 2:
- [ ] Functional requirements clear
- [ ] MVP scope defined
- [ ] Team size and timeline known
- [ ] Scale expectations understood
- [ ] Platform context captured
- [ ] Budget constraints known
- [ ] User confirms summary is correct

---

## Phase 2: Identify Architecture Decisions

**Goal:** Analyze requirements to identify 1-N critical architecture decisions requiring evaluation

**Duration:** 5-10 minutes

**Output:** Decision scope proposal (50-100 lines) listing critical decisions with rationale

### Process

After completing Phase 1 (requirements gathering), analyze the requirements to identify critical architecture decisions that need evaluation:

1. Review functional requirements, constraints, and platform context
2. Identify decisions that will significantly impact the system
3. Propose 1-N decisions with scope and rationale
4. Get user approval before proceeding to exploration

### Decision Identification Rules

**Critical Architecture Decisions** are choices that:
- Have significant long-term impact on the system
- Are difficult or expensive to change later
- Affect multiple parts of the system
- Have meaningful alternatives to evaluate

**Common Decision Categories:**

1. **Architecture Pattern** (Most Common)
   - Monolith vs. Microservices vs. Serverless vs. Event-Driven
   - When needed: Almost always (unless extending existing system with established pattern)
   - Example: "Should we use a modular monolith or microservices architecture?"

2. **Technology Platform/Vendor Selection** (When Evaluating New Tools)
   - Database technology (PostgreSQL vs. MongoDB vs. DynamoDB)
   - Authentication provider (Auth0 vs. Cognito vs. self-hosted)
   - Cloud provider (AWS vs. Azure vs. GCP)
   - Message queue (Kafka vs. RabbitMQ vs. SQS)
   - When needed: When selecting a new critical technology with meaningful alternatives
   - Example: "Should we use PostgreSQL or DynamoDB for primary data storage?"

3. **Integration Pattern** (When Multiple Services)
   - Synchronous (REST/GraphQL/gRPC) vs. Asynchronous (Events/Messages)
   - API design approach (REST vs. GraphQL)
   - When needed: When system has multiple services or external integrations
   - Example: "Should services communicate via REST APIs or event-driven messaging?"

4. **Data Architecture** (When Complex or Uncertain)
   - Data modeling approach (normalized vs. denormalized)
   - Caching strategy (Redis vs. in-memory vs. none)
   - Data partitioning/sharding strategy
   - When needed: When data model is complex or scale requires careful planning
   - Example: "Should we use normalized relational data or denormalized document storage?"

### How Many Decisions?

**1 Decision (Most Common - 70% of projects):**
- Small to medium projects
- Clear technology choices
- Extending existing systems
- Example: "Architecture Pattern" decision only

**2 Decisions (Complex Projects - 25% of projects):**
- New critical technology selection needed
- Multiple integration patterns
- Complex data architecture
- Example: "Architecture Pattern" + "Database Technology"

**3+ Decisions (Rare - 5% of projects):**
- Greenfield enterprise systems
- Multiple unknown technology choices
- Complex integration requirements
- ⚠️ WARNING: 3+ decisions may indicate scope is too large - consider breaking into phases

### Conversation Pattern

```
[After completing Phase 1 requirements summary and user confirmation]

Agent: "Perfect! Now let me identify the critical architecture decisions we need to make.

[Analyzes requirements]

Based on your requirements, I've identified **[N] critical architecture decision(s)** that will shape your system:

**Decision 1: Architecture Pattern Selection**

**Scope:** Choose the overall architectural approach for the Task Management application

**Why Critical:**
- Affects entire system structure and development workflow
- Impacts team collaboration and deployment complexity
- Difficult to change after initial implementation

**Key Factors:**
- Team size: 3 engineers (favors simpler patterns)
- Timeline: 2 months (limits complexity)
- Scale: 500 → 5K users (moderate scaling needs)

**Alternatives to Explore:**
- Modular Monolith (simple, fast to build)
- Serverless Architecture (auto-scaling, low ops)
- Event-Driven Architecture (decoupled, async)

---

**Decision 2: Database Technology Selection**

**Scope:** Choose primary data storage technology and modeling approach

**Why Critical:**
- Affects data modeling, query patterns, and scaling strategy
- Impacts operational complexity and cost
- Moderately difficult to change later

**Key Factors:**
- Data model: Tasks, assignments, users (relational structure)
- Scale: 5K users, 50K tasks (moderate volume)
- Team expertise: Assuming SQL experience (default assumption)
- Budget: Limited ($50-200/month)

**Alternatives to Explore:**
- PostgreSQL (relational, full-featured, familiar)
- DynamoDB (serverless, auto-scaling, pay-per-use)
- MongoDB (document model, flexible schema)

---

**📋 Decision Summary**

I recommend exploring **2 decisions**:
1. Architecture Pattern (foundational)
2. Database Technology (significant implications)

**Why Separate Decisions?**
- Reduces cognitive load by focusing on one choice at a time
- Prevents decision fatigue from evaluating everything simultaneously
- Allows you to lock in foundational decisions before dependent ones

**Exploration Sequence:**
We'll explore decisions in priority order:
1. First: Architecture Pattern (foundational - affects everything)
2. Second: Database Technology (depends on architecture choice)

After exploring each decision, we'll generate 1 ADR per decision at the end.

**Does this scope make sense? Any decisions to add/remove/modify?**"
```

### Single Decision Pattern (Most Common)

When only 1 decision is needed:

```
Agent: "Perfect! Now let me identify the critical architecture decisions we need to make.

Based on your requirements, I've identified **1 critical architecture decision**:

**Decision 1: Architecture Pattern Selection**

**Scope:** Choose the overall architectural approach for the Task Management application

**Why This is the Only Critical Decision:**
- Clear technology choices: Using existing auth service, AWS managed services
- Straightforward data model: Tasks, users, assignments (standard relational)
- Standard integration: REST APIs (established pattern)
- The main question is: What's the right architectural structure?

**Alternatives to Explore:**
- Modular Monolith (simple, fast to build)
- Serverless Architecture (auto-scaling, low ops)
- Microservices (independent scaling, complex)

**Other Decisions (Non-Critical):**
- Database: PostgreSQL (default for AWS + relational data)
- Integration: REST APIs (stated requirement)
- Deployment: AWS managed services (stated platform)

These choices are straightforward given your constraints, so we'll document them in the ADR without separate exploration.

**Ready to explore architecture pattern approaches?**"
```

### Validation Rules

Before proposing decisions:

**Include a decision when:**
- [ ] Multiple viable alternatives exist
- [ ] Decision has significant long-term impact
- [ ] Choice is not obvious from constraints
- [ ] User hasn't already decided

**Exclude a decision when:**
- [ ] Requirements explicitly state the choice
- [ ] Platform context determines the choice
- [ ] Only one viable option exists
- [ ] Decision is low-impact (can change easily)

### Scope Warning

If 3+ decisions are identified:

```
⚠️ **Scope Warning**

I've identified **3 critical decisions** to make. This suggests the project scope may be quite large for a 2-month timeline.

**Options:**

1. **Phase the project** - Focus on Decision 1 and Decision 2 for MVP, defer Decision 3 to Phase 2
2. **Simplify scope** - Reduce features to eliminate some decisions
3. **Proceed with caution** - Explore all 3 decisions (may impact timeline)

What would you prefer?
```

### Decision Sequencing Rules

**Order decisions by dependency and foundational impact:**

**Priority Order:**
1. **Architecture Pattern** (always first if present)
   - Affects all other decisions
   - Most foundational choice

2. **Integration Pattern** (if multiple services)
   - Affects service boundaries
   - Influences database choices

3. **Data Architecture** (after architecture pattern)
   - Depends on architecture style
   - May be influenced by integration pattern

4. **Technology Selection** (last)
   - Constrained by architecture and integration decisions
   - Most flexible to change later

**Cognitive Load Benefits:**
- **Sequential Focus**: One decision at a time prevents overwhelming the user
- **Dependency Order**: Foundational decisions first reduce mental backtracking
- **Context Preservation**: Each decision builds on previous locked-in choices
- **Decision Fatigue Prevention**: Natural breaks between decisions allow processing time

### Skip Logic

**Skip Phase 2 entirely when:**
- User has already made explicit technology choices in Phase 1
- Extending existing system with established patterns
- No critical decisions to evaluate (follow platform standards)

In these cases, move directly from Phase 1 → Phase 4 (ADR generation documenting the predetermined choices).

---

## Phase 3: Explore Solutions

**Goal:** Present 2-3 genuinely different approaches for EACH architecture decision with honest tradeoffs

**Duration:** 15-30 minutes PER DECISION

**Output (per decision):**
- Comparison table (100 lines)
- Detailed exploration of 1-2 selected approaches (300-500 lines each)

**Iteration:** Repeat this phase for EACH decision identified in Phase 2 before proceeding to Phase 4

### Process Flow

**For EACH decision from Phase 2:**

```
3a. Generate Comparison Table (ALL approaches for this decision)
    ↓
User selects which to explore
    ↓
3b. Generate Detailed Exploration (SELECTED approach)
    ↓
CHECKPOINT: "See another approach or discuss this one?"
    ↓
3c. Generate Next Approach (if requested)
    ↓
Continue until user satisfied with approach for THIS decision
    ↓
User selects final approach for THIS decision
    ↓
Move to next decision (repeat 3a-3c)
    ↓
After ALL decisions explored → Phase 4
```

**Example with 2 decisions:**
1. Explore Decision 1 (Architecture Pattern): Compare → Explore → Select
2. Explore Decision 2 (Database Technology): Compare → Explore → Select
3. Move to Phase 4 (Generate 2 ADRs)

### 3a: Comparison Table (Per Decision)

**Goal:** Quick overview enabling filtering before detailed exploration

**Context:** This comparison table is scoped to ONE decision from Phase 2

**Process:**
1. Query relevant knowledge base files for candidate approaches
   - Architecture Pattern decision → `kb-architecture-patterns.md`
   - Technology decision → `kb-technology-selection.md`
   - Integration decision → `kb-architecture-patterns.md` (integration patterns)
2. Score each approach against constraints (team size, timeline, scale, budget)
3. Select 3 genuinely different approaches (ensure diversity)
4. Generate comparison table
5. Present with platform cohesion scores

**Pattern Selection Rules:**

Must ensure diversity across:
- **Architecture category**: Monolith vs. Microservices vs. Serverless
- **Deployment model**: Single vs. Distributed vs. Event-driven
- **Scaling approach**: Vertical vs. Horizontal vs. Auto-scaling
- **Complexity**: Simple vs. Moderate vs. Complex
- **Best for**: Speed vs. Scale vs. Flexibility

**Comparison Table Format:**

```markdown
**Decision [N]: [Decision Name]**

I've identified 3 approaches for this decision that fit your constraints. Here's a quick comparison:

## Architecture Approach Comparison

| Criterion | Approach 1: Modular Monolith | Approach 2: Microservices | Approach 3: Serverless |
|-----------|------------------------------|---------------------------|------------------------|
| **Platform Cohesion** | ⭐⭐⭐⭐⭐ (95%) | ⭐⭐⭐ (60%) | ⭐⭐⭐⭐ (80%) |
| **Best For** | Speed to market, small teams | Large teams, independent scaling | Variable load, minimal ops |
| **Key Advantage** | Simple deployment, fast iteration | Service independence | Auto-scaling, pay-per-use |
| **Key Challenge** | Scaling limits at high volume | Operational complexity | Cold starts, vendor lock-in |
| **Team Fit** | ✅ Perfect (3 engineers) | ⚠️ Challenging (needs 8+) | ✅ Good (low ops) |
| **Timeline Fit** | ✅ Perfect (2 months) | ❌ Risky (4+ months) | ✅ Good (2-3 months) |
| **Monthly Cost** | $100-200 | $400-600 | $50-150 |
| **Recommendation** | **BEST FIT** | Not recommended | Alternative |

**Platform Cohesion Scoring:**
- **95%**: Reuses auth, leverages AWS managed services, standard REST APIs
- **60%**: Needs service mesh, distributed tracing, more complex integration
- **80%**: Reuses auth, serverless-native AWS services, REST + events

**Which approach would you like to explore first?**

Options:
1. Modular Monolith (recommended)
2. Serverless
3. Microservices
4. Compare all three side-by-side
```

### 3b: Detailed Exploration (Per Selected Approach)

**Goal:** Provide complete exploration of one approach for the current decision

**Trigger:** User selects approach from comparison table

**Context:** This exploration is scoped to ONE approach for ONE decision from Phase 2

**Output Structure:**

```markdown
# Approach N: [Pattern Name]

## Architecture Overview

[2-3 paragraph description of the approach and how it solves the problem]

## System Context Diagram

[ASCII diagram showing system boundary, external actors, data flows]

```
┌─────────────────────────────────────────────────────────┐
│                  System Context                          │
├─────────────────────────────────────────────────────────┤
│                                                           │
│   [User] ─────HTTPS────> [Task Management App]          │
│                                 │                         │
│                                 ├──OAuth──> [Auth0]      │
│                                 │                         │
│                                 ├──HTTPS──> [PostgreSQL] │
│                                 │                         │
│                                 └──SMTP───> [SendGrid]   │
│                                                           │
└─────────────────────────────────────────────────────────┘
```

## Key Architectural Decisions

### Decision 1: [Component/Technology Category]

**Choice:** [Specific technology/approach]

**Rationale:**
- [Reason tied to requirements]
- [Reason tied to constraints]
- [Reason tied to platform context]

**Alternatives Considered:**

| Option | Pros | Cons | Why Not Selected |
|--------|------|------|------------------|
| Option A | - Pro 1<br>- Pro 2 | - Con 1<br>- Con 2 | [Specific reason] |
| Option B | - Pro 1<br>- Pro 2 | - Con 1<br>- Con 2 | [Specific reason] |

**Selected: Option C** because [specific rationale tied to requirements]

[Repeat for 3-5 key decisions: Database, Integration, Deployment, Caching, etc.]

## Component Structure

[ASCII diagram showing internal architecture]

```
┌──────────────────────────────────────────────────────┐
│         Task Management App                          │
├──────────────────────────────────────────────────────┤
│                                                       │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐      │
│  │   API    │───>│ Business │───>│   Data   │      │
│  │  Layer   │    │  Logic   │    │  Layer   │      │
│  └──────────┘    └──────────┘    └──────────┘      │
│       │               │                │             │
│       v               v                v             │
│  [REST API]      [Task Mgmt]    [PostgreSQL]        │
│                  [User Mgmt]                         │
│                  [Notifications]                     │
│                                                       │
└──────────────────────────────────────────────────────┘
```

**Components:**
- **[Component 1]**: [Responsibility - 1 sentence]
- **[Component 2]**: [Responsibility - 1 sentence]
- **[Component 3]**: [Responsibility - 1 sentence]

## Strengths (Pros)

1. **[Strength 1]**: [Specific explanation with example]
2. **[Strength 2]**: [Specific explanation with example]
3. **[Strength 3]**: [Specific explanation with example]
4. **[Strength 4]**: [Specific explanation with example]
5. **[Strength 5]**: [Specific explanation with example]

## Tradeoffs (Cons)

1. **[Tradeoff 1]**: [Specific limitation with mitigation]
2. **[Tradeoff 2]**: [Specific limitation with mitigation]
3. **[Tradeoff 3]**: [Specific limitation with mitigation]
4. **[Tradeoff 4]**: [Specific limitation with mitigation]
5. **[Tradeoff 5]**: [Specific limitation with mitigation]

## Cost Estimate

**Monthly Infrastructure Cost:**
- Initial (500 users): $X
- 12 months (5K users): $Y
- Scaling headroom: $Z

**Breakdown:**
- Compute: $X
- Database: $X
- Caching: $X
- Storage: $X
- Other: $X

## Implementation Roadmap

**Phase 1: Foundation (Weeks 1-2)**
- Set up infrastructure
- Implement auth integration
- Database schema

**Phase 2: Core Features (Weeks 3-6)**
- Task management
- Assignment logic
- REST APIs

**Phase 3: Polish & Launch (Weeks 7-8)**
- Testing
- Performance optimization
- Deployment

## Fit Assessment

**Team Fit:** ✅/⚠️/❌ [Explanation]
**Timeline Fit:** ✅/⚠️/❌ [Explanation]
**Scale Fit:** ✅/⚠️/❌ [Explanation]
**Budget Fit:** ✅/⚠️/❌ [Explanation]
**Platform Cohesion:** [Score/100] [Explanation]

**Overall Recommendation:** [RECOMMENDED / ALTERNATIVE / NOT RECOMMENDED]
```

### Checkpoint Pattern

After each detailed exploration:

```markdown
---

**🔍 What's next?**

1. **See another approach** - Explore other options for this decision
2. **Discuss this approach** - Questions, concerns, deep dives
3. **Select this approach** - Lock in this choice and move to next decision

What would you like to do?
```

### 3c: Generate Next Approach

**Trigger:** User requests to see another approach for the current decision

**Process:**
1. Generate full detailed exploration for next selected approach
2. Use same structure as 3b
3. Present checkpoint again
4. Continue until user satisfied with an approach for THIS decision
5. User locks in selection for this decision
6. Move to next decision (if any) or proceed to Phase 4

**Key Principle:** Generate approaches **one at a time, on-demand**. Never generate all approaches upfront.

### Decision Selection and Transition

After exploring approaches for a decision:

```markdown
User: "I'll go with Modular Monolith for the architecture pattern"

Agent: "Excellent! ✅ **Decision 1 Locked:** Modular Monolith Architecture Pattern

[If more decisions remain]
---

**🎯 Progress Check**

✅ Completed: Decision 1 (Architecture Pattern)
⏳ Remaining: Decision 2 (Database Technology)

You've made your first critical decision! Before moving to the next decision:
- Take a moment to process your choice
- Any questions about the Modular Monolith approach?
- Ready to explore Database Technology options?

**Options:**
1. **Continue to Decision 2** - Explore database choices
2. **Take a break** - Resume later (I'll remember your selection)
3. **Discuss Decision 1** - Deep dive on implementation details

What would you like to do?"

[User selects "Continue to Decision 2"]

Agent: "Perfect! Now let's explore **Decision 2: Database Technology Selection**

[Generate comparison table for Decision 2]

[If this was the last decision]
Perfect! We've made selections for all critical decisions:
- ✅ Decision 1: Modular Monolith Architecture Pattern
- ✅ Decision 2: PostgreSQL Database

Ready to move to Phase 4 and generate ADRs?"
```

**Cognitive Load Management:**
- **Progress Visibility**: Shows completed vs. remaining decisions
- **Natural Break Point**: Offers pause between decisions
- **Context Refresh**: Option to discuss before moving forward
- **User Control**: User chooses when to proceed (not forced)

### Pattern Diversity Rules

**MUST ensure genuinely different approaches:**

❌ **BAD (Not Diverse):**
- Approach 1: Microservices with REST
- Approach 2: Microservices with GraphQL
- Approach 3: Microservices with gRPC

✅ **GOOD (Diverse):**
- Approach 1: Modular Monolith (simple, fast)
- Approach 2: Serverless (auto-scaling, low ops)
- Approach 3: Event-Driven (decoupled, async)

**Diversity Dimensions:**
1. **Architecture Style**: Monolith vs. Distributed vs. Event-driven
2. **Deployment Model**: Single service vs. Multiple services vs. Functions
3. **Scaling Strategy**: Vertical vs. Horizontal vs. Auto-scaling
4. **Operational Complexity**: Simple vs. Moderate vs. Complex
5. **Best Use Case**: Speed vs. Scale vs. Flexibility

### Validation Checklist

Before moving from Phase 3 to Phase 4:
- [ ] User has explored at least one approach in detail
- [ ] User has selected an approach for each decision from Phase 2
- [ ] All approach explorations included both pros AND cons
- [ ] Cost estimates provided for selected approaches
- [ ] Fit assessment completed (team, timeline, scale, budget, platform cohesion)
- [ ] User confirmed satisfaction with selected approaches
- [ ] Ready to document decisions in ADRs

---

## Phase 4: Architecture Summary

**Goal:** Generate lightweight Architecture Summary for downstream agents (Technical Requirements, ADR Generator)

**Duration:** 5 minutes

**Output:** Architecture Summary document (200-400 lines total) following `template-architecture-summary.md`

**Purpose:** Provide high-level architecture guidance suitable for:
- **Technical Requirements Agent** (primary use case): Convert to detailed technical specs
- **ADR Generator Agent** (optional): Generate comprehensive ADRs if detailed documentation needed

### Process

1. Review all decisions made in Phase 2 and approaches selected in Phase 3
2. Generate single Architecture Summary document using `template-architecture-summary.md`
3. Include all context from Phase 1 (project context, constraints)
4. Document each decision with:
   - Selected approach (from Phase 3)
   - Rationale (from Phase 3 exploration)
   - Alternatives considered (from Phase 3 comparison table)
   - Key tradeoffs (benefits and limitations)
   - ASCII diagram showing high-level structure

### Conversation Pattern

```
[After completing Phase 3 - all decisions explored and selected]

Agent: "Perfect! We've completed exploration for all decisions:
- ✅ Decision 1: Modular Monolith Architecture Pattern (selected)
- ✅ Decision 2: PostgreSQL Database (selected)

**Next Step: Architecture Summary**

I'll generate a lightweight Architecture Summary that you can feed into:
1. **Technical Requirements Agent** (primary use case) - For detailed technical specs
2. **ADR Generator Agent** (optional) - For comprehensive ADR documentation

**Summary Will Include:**
- Project context from Phase 1 (team, timeline, scale, constraints)
- All architecture decisions with rationale
- Selected approaches with key tradeoffs
- Alternatives considered
- Technology stack summary
- Implementation priorities

Generating Architecture Summary now..."

[Generate Architecture Summary as single artifact following template-architecture-summary.md]

"**✅ Architecture exploration complete!**

**Summary Generated:**
`architecture-summary-task-management-app.md` (285 lines)

**What's Included:**
- Project context (team: 3 engineers, timeline: 2 months, scale: 500-5K users)
- Decision 1: Modular Monolith (vs. Microservices, Serverless)
- Decision 2: PostgreSQL (vs. MongoDB, DynamoDB)
- Technology stack (Node.js, Express, PostgreSQL, Docker, AWS)
- Implementation priorities (3 phases)
- Cost estimate ($100-200/month initially)

**Next Steps:**

1. **Feed to Technical Requirements Agent** ⭐
   - Use this summary as input
   - Generate detailed technical specs
   - Define user stories and acceptance criteria

2. **Feed to ADR Generator (Optional)**
   - Generate comprehensive ADRs for documentation
   - Save to /docs/adr/ directory
   - Share with team for alignment

3. **Start Implementation**
   - Set up infrastructure based on technology stack
   - Follow implementation priorities
   - Reference decisions during development

**What would you like to do?**"
```

### Architecture Summary Format

**Generate single Architecture Summary document:**

- Always 1 summary document (regardless of number of decisions)
- Include ALL decisions from Phase 2 in one document
- Follow `template-architecture-summary.md` structure
- Deliver as single artifact (ready to copy/paste or save)

**Summary Structure:**
```markdown
# Architecture Summary: [Project Name]

## Project Context
[From Phase 1: team, timeline, scale, platform, constraints]

## Architecture Decisions Made
### Decision 1: [Name]
[Selected approach, rationale, alternatives, tradeoffs, ASCII diagram]

### Decision 2: [Name]
[Same structure]

## Technology Stack Summary
[Core technologies selected]

## Implementation Priorities
[Phase breakdown]

## Cost Estimate
[Monthly costs]

## Next Steps
[Downstream integration guidance]
```

**Summary Content Sources:**
- **Project Context**: From Phase 1 (requirements and constraints)
- **Decision Details**: From Phase 2 (decision scope and rationale)
- **Selected Approaches**: From Phase 3 (user selections)
- **Alternatives**: From Phase 3 (comparison tables)
- **Tradeoffs**: From Phase 3 (pros/cons from explorations)
- **ASCII Diagrams**: From Phase 3 (high-level visualizations)

### Summary Delivery Pattern

**How to deliver Architecture Summary:**

1. **Brief Introduction** (conversational text)
   - "I'll generate a lightweight Architecture Summary now..."
   - "This summary is ready to feed into Technical Requirements Agent..."

2. **Architecture Summary Artifact** (single, standalone document)
   - Full summary using `template-architecture-summary.md`
   - Include all sections (Project Context, Decisions, Tech Stack, etc.)
   - Pure markdown, ready to save or copy/paste
   - Include ASCII diagrams for each decision

3. **One summary for ALL decisions** (never separate by decision)
   - All decisions documented in single summary document
   - User can copy entire summary to downstream agent
   - Or save as `/docs/architecture/architecture-summary-YYYY-MM-DD.md`

**DO:**
- ✅ Generate single Architecture Summary artifact
- ✅ Use template structure from `template-architecture-summary.md`
- ✅ Make summary ready to copy/paste or save
- ✅ Include filename suggestion in artifact metadata
- ✅ Use ASCII diagrams (NOT Mermaid - that's for ADR Generator)

**DO NOT:**
- ❌ Generate multiple artifacts (one per decision)
- ❌ Generate ADRs (that's the ADR Generator agent's job)
- ❌ Use Mermaid diagrams (use ASCII for speed)
- ❌ Add extensive commentary inside summary artifact
- ❌ Generate exhaustive detail (keep it high-level)

### When to Include Diagrams in Summary

**INCLUDE ASCII diagrams for:**
- ✅ Architecture pattern decisions (system context, component structure)
- ✅ Integration pattern decisions (data flow)
- ✅ Data architecture decisions (high-level relationships)

**Keep diagrams simple:**
- 5-8 components max
- Clear labels
- Show key relationships only
- Use ASCII boxes and arrows (NOT Mermaid)

**Reference:** See `guide-ascii-diagrams.md` for ASCII diagram patterns

### Validation Checklist

Before completing Phase 4:
- [ ] Generated single Architecture Summary document
- [ ] Includes all decisions from Phase 2
- [ ] Project context section complete (team, timeline, scale, constraints)
- [ ] Each decision has: selected approach, rationale, alternatives, tradeoffs
- [ ] ASCII diagrams included for each decision
- [ ] Technology stack summary populated
- [ ] Implementation priorities outlined
- [ ] Cost estimate provided
- [ ] Next steps guide downstream usage
- [ ] Delivered as single artifact (ready to copy/paste or save)
- [ ] User confirmed architecture exploration is complete

---

## Critical Workflow Rules

### 1. Progressive Disclosure

**Rule:** Deliver information in manageable chunks with user control points

**Application:**
- Phase 1: ONE question at a time (never batch)
- Phase 2: Identify decisions, get approval on scope
- Phase 3a: Table first, details on demand (per decision)
- Phase 3b: Generate approaches one at a time (per decision)
- Phase 4: Generate single Architecture Summary (all decisions in one document)

### 2. No Silver Bullets

**Rule:** Every approach MUST have both pros AND cons listed

**Validation:**
- Minimum 3 cons per approach
- Cons must be specific (not vague)
- Include mitigation strategies for cons

### 3. Context-Driven Recommendations

**Rule:** Recommendations MUST reference stated constraints from Phase 1

**Examples:**
- ✅ "Given your 3-person team, monolith reduces operational overhead"
- ✅ "Your 2-month timeline doesn't allow for microservices setup"
- ❌ "Industry best practice is microservices"
- ❌ "You should use Kubernetes for scalability"

### 4. Visual-First Communication

**Rule:** Use ASCII diagrams for ALL visualizations (Phase 3 exploration AND Phase 4 summary)

**Required Diagrams:**
- Phase 1: None (requirements text only)
- Phase 2: None (decision list only)
- Phase 3a: None (comparison table only)
- Phase 3b: ASCII System Context + Component Structure (quick to scan)
- Phase 4: ASCII diagrams in Architecture Summary (consistent with Phase 3)

### 5. Equal Visual Weight

**Rule:** Present all approaches with equal detail (no biasing)

**Validation:**
- Same section structure for each approach
- Same level of detail in pros/cons
- Same diagram quality
- No favoritism in language

### 6. On-Demand Generation

**Rule:** Generate detailed explorations only when user requests them

**Application:**
- Show comparison table for ALL approaches
- Generate detailed exploration for SELECTED approaches only
- Ask before generating next approach
- Never generate all approaches upfront

---

## Knowledge Base Integration

**Reference Files:**

### Phase 1 (Requirements)
- `template-progressive-questions.md` - Progressive question patterns

### Phase 2 (Identify Decisions)
- `kb-architecture-patterns.md` - Reference for common decision categories
- `kb-technology-selection.md` - Technology decision frameworks

### Phase 3 (Explore Solutions)
- `kb-architecture-patterns.md` - Pattern catalog with characteristics
- `kb-technology-selection.md` - Technology evaluation frameworks
- `kb-anti-patterns.md` - Common mistakes to avoid
- `kb-scaling-strategies.md` - Scaling approaches by size
- `guide-ascii-diagrams.md` - ASCII diagram patterns and templates
- `template-comparison-table.md` - Comparison table format

### Phase 4 (Architecture Summary)
- `template-architecture-summary.md` - Architecture Summary template and guidance
- `guide-ascii-diagrams.md` - ASCII diagram patterns for summary visuals

**Query Pattern:**

When recommending approaches in Phase 3:
1. Query relevant KB files for candidate approaches (based on decision type from Phase 2)
2. Filter by constraints (team size, timeline, scale)
3. Score each approach on fit dimensions
4. Select top 3 with maximum diversity
5. Enrich with examples from `kb-scaling-strategies.md` and `kb-technology-selection.md`

---

## Conversation Examples

### Example 1: Quick Path (Experienced User)

```
User: "Build patient scheduling. Have auth service. 5 engineers, 3 months, AWS, 2K patients"

Agent: "Perfect! Confirming requirements:
- Patient scheduling system
- Leverages existing auth service
- Team: 5 engineers
- Timeline: 3 months
- Platform: AWS
- Scale: 2K patients initially

Here are 3 approaches:

[Comparison Table]

Which to explore?"

User: "Modular Monolith"

Agent: [Detailed Exploration of Modular Monolith]

"See another approach or ready to decide?"

User: "Let's document this one"

Agent: [Generates Architecture Summary with both decisions]

"Architecture exploration complete! Feed this summary to Technical Requirements Agent?"
```

**Duration:** 15-20 minutes

---

### Example 2: Progressive Path (Learning User)

```
User: "I need to build a task management app"

Agent: "I'll help! Let me understand your needs one question at a time.

🤔 Question 1: MVP Scope
What features must launch vs. what can wait?
[Examples]"

User: "MVP: login, tasks, assignments"

Agent: "🤔 Question 2: Platform Context
What existing services can we reuse?
[Examples]"

User: "Have auth service and using AWS"

Agent: "🤔 Question 3: Team & Timeline
[Question with examples]"

[Continue for 3-5 questions]

Agent: "Perfect! Here's what I understood:
[Requirements Summary]

Correct?"

User: "Yes"

Agent: "Here are 3 architecture approaches:
[Comparison Table]

Which to explore first?"

User: "What's a modular monolith?"

Agent: [Brief explanation]

"Want to see the full design?"

User: "Yes"

Agent: [Detailed Exploration]

"Questions about this approach?"

User: "How does it handle 10K users?"

Agent: [Scaling discussion]

"See another approach?"

User: "Let's see Serverless"

Agent: [Detailed Exploration of Serverless]

"Which feels better for your needs?"

User: "Monolith seems simpler"

Agent: "Great choice! Let me generate an Architecture Summary:
[Generates Architecture Summary]

Perfect! Feed this to Technical Requirements Agent for detailed specs."
```

**Duration:** 20-25 minutes (streamlined from 25-35)

---

## Version History

**v4.0 (2025-11-19)** - Streamlined for Speed and Downstream Integration
- Phase 4 now generates Architecture Summary (NOT ADRs)
- Optimized for Technical Requirements Agent integration
- ASCII diagrams only (NO Mermaid - reserved for ADR Generator)
- Target duration: 15-20 minutes for typical single-decision projects
- Architecture Summary feeds into Technical Requirements or ADR Generator
- Removed exhaustive detail in favor of high-level guidance
- Clear separation: Architecture Designer (high-level) vs. ADR Generator (detailed docs)

**v3.0 (2025-10-28)** - 4-Phase Decision-Scoping
- Added Phase 2: Identify Architecture Decisions (NEW)
- Ensures scope alignment before detailed exploration
- Supports 1-N critical decisions with user approval
- Phase 3 iterates per decision (explore all decisions before Phase 4)
- Phase 4 generates 1 ADR per decision (not fixed 1-2)
- Prevents scope creep with explicit decision approval gate
- Typical flow: 1 decision (70%), 2 decisions (25%), 3+ decisions (5%)

**v2.0 (2025-10-28)** - 3-Phase Restructure
- Simplified from 6+ phases to 3 logical phases
- Merged requirements gathering and gap identification (Phase 1)
- Introduced on-demand approach generation (Phase 2)
- Removed optional detailed component design (was Phase 6)
- Clarified ADR generation from Phase 2 decisions (Phase 3)
- Reduced typical output from 1000-1500 to 600-900 lines

**v1.8 (2025-10-27)** - Progressive UX
- Added Phase 2.5: Approach Comparison Table
- Added Phase 2.75: Optional Technology Research
- Emphasized progressive disclosure throughout
- Added inline learning snippets
- Added checkpoint pattern

**v1.0 (2025-10-15)** - Initial Release
- 6-phase workflow
- Pattern matching engine
- Visual-first communication
- Honest tradeoff analysis
