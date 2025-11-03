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

## Phase 4: Document Decisions

**Goal:** Generate ADRs for ALL decisions made in Phase 2/3 (1 ADR per decision)

**Duration:** 5-10 minutes

**Output:** N ADRs (200-400 lines each), where N = number of decisions from Phase 2

**Typical Output:**
- 1 decision → 1 ADR (most common)
- 2 decisions → 2 ADRs
- 3+ decisions → 3+ ADRs (rare)

### Process

1. Review all decisions made in Phase 2 and approaches selected in Phase 3
2. Generate 1 ADR per decision using context from Phase 1 and exploration from Phase 3
3. Present ADRs with Mermaid diagrams
4. Each ADR documents:
   - The specific decision (from Phase 2)
   - The selected approach (from Phase 3)
   - Alternatives considered (from Phase 3 comparison table)
   - Rationale tied to requirements (from Phase 1)

### Conversation Pattern

```
[After completing Phase 3 - all decisions explored and selected]

Agent: "Perfect! We've completed exploration for all decisions:
- ✅ Decision 1: Modular Monolith Architecture Pattern (selected)
- ✅ Decision 2: PostgreSQL Database (selected)

**Next Step: Document Your Decisions**

I'll generate Architecture Decision Records (ADRs) to document your choices. These ADRs will help your team (and future teams) understand WHY these decisions were made.

**ADRs to Generate:**

1. **ADR-001: Modular Monolith Architecture Pattern**
   - Decision: Architecture pattern choice
   - Selected: Modular Monolith
   - Alternatives: Microservices, Serverless
   - Rationale: Team size, timeline, simplicity

2. **ADR-002: PostgreSQL for Primary Data Storage**
   - Decision: Database technology choice
   - Selected: PostgreSQL
   - Alternatives: DynamoDB, MongoDB
   - Rationale: Relational model, team expertise, cost

I'll generate each ADR as a separate artifact. Here's the first one:"

[Generate ADR-001 as separate artifact - full template, nothing else]

"Here's the second ADR:"

[Generate ADR-002 as separate artifact - full template, nothing else]

"**✅ Architecture design complete!**

You have:
- Requirements summary (Phase 1)
- 2 critical decisions identified (Phase 2)
- Approach exploration and selection (Phase 3)
- 2 ADRs documenting your decisions (Phase 4)

**Artifacts Generated:**
- `ADR-001-modular-monolith-architecture.md`
- `ADR-002-postgresql-data-storage.md`

**What's next?**

1. **Technology Setup Guidance** - Help with specific stack setup
2. **Implementation Plan** - Detailed task breakdown
3. **Start Building** - You're ready to go!

What would you like?"
```

### ADR Generation Rules

**Generate 1 ADR per decision from Phase 2:**

- 1 decision identified in Phase 2 → 1 ADR artifact
- 2 decisions identified in Phase 2 → 2 ADR artifacts
- 3+ decisions identified in Phase 2 → 3+ ADR artifacts (rare, scope warning already given)

**ADR Numbering:**
- ADR-001: First decision from Phase 2
- ADR-002: Second decision from Phase 2
- ADR-003: Third decision from Phase 2 (if applicable)

**ADR Artifact Format:**
- **One ADR per artifact** - Generate each ADR as a separate, standalone Claude artifact
- **Full template only** - No additional commentary, explanations, or surrounding text
- **Filename convention**: `ADR-00X-kebab-case-title.md`
- **Pure markdown** - Ready to save directly to file

**ADR Content Sources:**
- **Context/Problem**: From Phase 1 (requirements and constraints)
- **Decision Title**: From Phase 2 (decision scope)
- **Options Considered**: From Phase 3 (comparison table)
- **Selected Option**: From Phase 3 (user selection)
- **Rationale**: From Phase 3 (detailed exploration)
- **Consequences**: From Phase 3 (pros/cons/tradeoffs)

### ADR Template

**Use the standard template from `template-adr.md`**

The template includes:
- Full ADR structure with all required sections
- Guidance on what to include in each section
- Content mapping from Phases 1-3
- Diagram inclusion rules
- Quality checklist
- Example filenames

**Key Template Sections:**
- Decision (one-sentence statement)
- Context and Problem Statement (from Phase 1)
- Decision Drivers (from Phase 2)
- Considered Options (from Phase 3 comparison table)
- Decision Outcome with Rationale (from Phase 3 selection)
- Consequences (from Phase 3 pros/cons)
- Alternatives Analysis (from Phase 3 exploration)
- Diagram (Mermaid - for architecture/integration/data decisions)
- Implementation Notes (actionable guidance)
- References (links to discussions and documentation)

**Reference:** See `template-adr.md` for the complete template with detailed section guidance and examples.

### ADR Delivery Pattern

**How to deliver ADRs:**

1. **Brief Introduction** (conversational text)
   - "Here's the first ADR:"
   - "Here's the second ADR:"

2. **ADR Artifact** (separate, standalone document)
   - Full ADR template filled out
   - No surrounding commentary
   - Pure markdown, ready to save
   - Include Mermaid diagram if applicable

3. **One ADR per artifact** (never combine multiple ADRs)
   - Each ADR is a complete, standalone document
   - User can save each directly to a file

**Example:**

```
Agent: "Here's ADR-001:"

[Artifact: ADR-001-modular-monolith-architecture.md]
# ADR-001: Modular Monolith Architecture Pattern

**Status:** Accepted
**Date:** 2025-10-28
...
[Complete ADR template with no additional commentary]
[/Artifact]

Agent: "Here's ADR-002:"

[Artifact: ADR-002-postgresql-data-storage.md]
# ADR-002: PostgreSQL for Primary Data Storage
...
[Complete ADR template]
[/Artifact]

Agent: "Architecture design complete! You now have 2 ADRs ready to save."
```

**DO NOT:**
- ❌ Include both ADRs in the same artifact
- ❌ Add commentary or explanations inside the ADR artifact
- ❌ Wrap ADR in conversational text
- ❌ Generate ADR inline with surrounding discussion

**DO:**
- ✅ Generate each ADR as a separate artifact
- ✅ Use full template with all sections
- ✅ Make ADR ready to save directly to file
- ✅ Include filename in artifact metadata

### When to Include Diagrams in ADRs

**INCLUDE Mermaid diagrams for:**
- Architecture pattern decisions (system context, component structure)
- Integration pattern decisions (sequence diagrams, data flow)
- Data architecture decisions (entity-relationship diagrams)

**SKIP diagrams for:**
- Technology selection within category (React vs. Vue)
- Deployment details (infrastructure diagrams)
- Monitoring/logging decisions

**Diagram Quality:**
- Phase 3 (Exploration): Use ASCII diagrams for speed and scannability
- Phase 4 (Documentation): Use Mermaid diagrams for proper ADR documentation

**Reference:** See `kb-diagram-examples.md` for Mermaid diagram examples and placement guidance

### Validation Checklist

Before completing Phase 4:
- [ ] Generated 1 ADR per decision from Phase 2
- [ ] Each ADR includes decision statement and context
- [ ] Considered options documented with pros/cons
- [ ] Selected option clearly stated with rationale
- [ ] Consequences (positive and negative) documented
- [ ] Mermaid diagrams included (for architecture/integration/data decisions)
- [ ] Implementation notes provided
- [ ] All ADRs delivered as separate artifacts
- [ ] User confirmed architecture design is complete

---

## Critical Workflow Rules

### 1. Progressive Disclosure

**Rule:** Deliver information in manageable chunks with user control points

**Application:**
- Phase 1: ONE question at a time (never batch)
- Phase 2: Identify decisions, get approval on scope
- Phase 3a: Table first, details on demand (per decision)
- Phase 3b: Generate approaches one at a time (per decision)
- Phase 4: Generate 1 ADR per decision

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

**Rule:** Use ASCII diagrams for exploration (Phase 3), Mermaid for documentation (Phase 4)

**Required Diagrams:**
- Phase 1: None (requirements text only)
- Phase 2: None (decision list only)
- Phase 3a: None (comparison table only)
- Phase 3b: ASCII System Context + Component Structure (quick to scan)
- Phase 4: Mermaid diagrams in ADRs (proper documentation quality)

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

### Phase 4 (Document Decisions)
- `template-adr.md` - Standard ADR template and guidance
- `kb-adr-library.md` - ADR examples and best practices
- `kb-diagram-examples.md` - Mermaid diagram examples for ADRs

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

Agent: [Generates ADR-001 and ADR-002]

"Architecture complete! Ready to build?"
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

Agent: "Great choice! Let me document your decisions:
[Generates ADRs]

You're ready to build!"
```

**Duration:** 25-35 minutes

---

## Version History

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
