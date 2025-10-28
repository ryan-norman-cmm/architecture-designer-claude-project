# Architecture Exploration Workflow

**Purpose:** Enable users to explore 2-3 distinct architectural approaches through conversational interface with visual diagrams, honest tradeoff analysis, and contextual recommendations.

**Version:** v2.0 (3-phase-structure)
**Last Updated:** 2025-10-28

---

## Workflow Overview

This workflow implements a **3-Phase Architecture Design Pattern**:

1. **Phase 1: Understand the Problem** - Gather complete requirements and constraints
2. **Phase 2: Explore Solutions** - Present architectural options with honest tradeoffs
3. **Phase 3: Document Decisions** - Generate ADRs for critical decisions

### Core Principles

- **Progressive Disclosure**: Information delivered in manageable chunks with user control
- **One Question at a Time**: Reduce cognitive load with sequential questions
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

## Phase 2: Explore Solutions

**Goal:** Present 2-3 genuinely different architectural approaches with honest tradeoffs

**Duration:** 15-30 minutes

**Output:**
- Comparison table (100 lines)
- Detailed exploration of 1-2 selected approaches (300-500 lines each)

### Process Flow

```
2a. Generate Comparison Table (ALL approaches)
    ↓
User selects which to explore
    ↓
2b. Generate Detailed Exploration (SELECTED approach)
    ↓
CHECKPOINT: "See another approach or discuss this one?"
    ↓
2c. Generate Next Approach (if requested)
    ↓
Continue until user satisfied
```

### 2a: Comparison Table

**Goal:** Quick overview enabling filtering before detailed exploration

**Process:**
1. Query `kb-architecture-patterns.md` for candidate patterns
2. Score each pattern against constraints (team size, timeline, scale, budget)
3. Select 3 genuinely different patterns (ensure diversity)
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
I've identified 3 architecture approaches that fit your constraints. Here's a quick comparison:

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

### 2b: Detailed Exploration (Per Selected Approach)

**Goal:** Provide complete architectural design for one approach

**Trigger:** User selects approach from comparison table

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

1. **See another approach** - Explore Microservices or Serverless
2. **Discuss this approach** - Questions, concerns, deep dives
3. **Ready to decide** - Move to Phase 3 (ADR generation)

What would you like to do?
```

### 2c: Generate Next Approach

**Trigger:** User requests to see another approach

**Process:**
1. Generate full detailed exploration for next selected approach
2. Use same structure as 2b
3. Present checkpoint again
4. Continue until user satisfied or all approaches explored

**Key Principle:** Generate approaches **one at a time, on-demand**. Never generate all approaches upfront.

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

---

## Phase 3: Document Decisions

**Goal:** Generate ADRs for 1-2 most impactful architectural decisions

**Duration:** 5-10 minutes

**Output:** 1-2 ADRs (200-400 lines each)

### Process

1. User selects preferred approach from Phase 2
2. Confirm selection
3. Identify 1-2 critical decisions to document
4. Generate ADRs using context from Phase 1 and decisions from Phase 2
5. Present ADRs with diagrams

### Conversation Pattern

```
User: "I'll go with the Modular Monolith"

Agent: "Excellent choice! The Modular Monolith fits your constraints perfectly:
- ✅ 3-engineer team (simple deployment)
- ✅ 2-month timeline (fastest to production)
- ✅ 500-5K users (scales adequately)
- ✅ Limited budget ($100-200/month)
- ✅ Platform cohesion (95% - reuses auth, AWS services)

**Next Step: Document Your Decisions**

I'll generate Architecture Decision Records (ADRs) for your critical decisions.

I recommend documenting these 2 key decisions:

1. **ADR-001: Modular Monolith Architecture Pattern**
   - Why: Captures architecture choice vs. microservices/serverless
   - Impact: Affects entire system structure

2. **ADR-002: PostgreSQL with JSONB for Flexible Data**
   - Why: Captures database choice and extensibility approach
   - Impact: Affects data modeling and query patterns

These ADRs will help your team (and future teams) understand WHY these decisions were made.

Generating ADRs now..."

[Generate ADR-001]
[Generate ADR-002]

"**✅ Architecture design complete!**

You have:
- Requirements summary
- Modular Monolith architecture design
- Technology decisions with rationale
- 2 ADRs documenting key decisions

**What's next?**

1. **Technology Setup Guidance** - Help with specific stack setup
2. **Implementation Plan** - Detailed task breakdown
3. **Start Building** - You're ready to go!

What would you like?"
```

### ADR Selection Rules

**Identify 1-2 MOST IMPACTFUL decisions to document:**

**Priority Order:**
1. **Architecture Pattern** (Monolith/Microservices/Serverless/Event-Driven)
2. **Database Strategy** (SQL/NoSQL, specific technology, data modeling approach)
3. **Integration Pattern** (REST/GraphQL/Events, API design, service communication)
4. **Deployment Strategy** (PaaS/Containers/Serverless, CI/CD, infrastructure)

**Selection Guide:**
- If architecture pattern is non-obvious → Document it (ADR-001)
- If database choice is complex or contentious → Document it (ADR-002)
- If integration has significant implications → Document it (ADR-002 or ADR-003)
- **Maximum 2 ADRs** - More signals scope is too large

**Scope Check:**
- If 3+ ADRs seem necessary → Suggest breaking project into phases
- If user insists on 3+ ADRs → Warn that scope may be too ambitious

### ADR Template

Use template from `kb-adr-library.md`:

```markdown
# ADR-00X: [Decision Title]

**Status:** Accepted
**Date:** [YYYY-MM-DD]
**Context:** [From Phase 1 - requirements and constraints]

## Decision

We will [specific decision statement].

## Context and Problem Statement

[Describe the problem being solved, referencing Phase 1 requirements]

**Requirements:**
- [Key requirement 1]
- [Key requirement 2]
- [Key requirement 3]

**Constraints:**
- [Key constraint 1 from Phase 1]
- [Key constraint 2 from Phase 1]
- [Key constraint 3 from Phase 1]

## Decision Drivers

[From Phase 2 - what influenced this decision]

- [Driver 1: e.g., Team size (3 engineers)]
- [Driver 2: e.g., Timeline (2 months)]
- [Driver 3: e.g., Platform cohesion (reuse existing services)]

## Considered Options

[From Phase 2 - alternatives explored]

1. **Option A: [Name]** - [Brief description]
2. **Option B: [Name]** - [Brief description]
3. **Option C: [Name]** - [Brief description]

## Decision Outcome

**Chosen option:** Option [X] - [Name]

**Rationale:**
[Specific reasons tied to requirements and constraints from Phases 1-2]

### Consequences

**Positive:**
- [From Phase 2 Pros]
- [From Phase 2 Pros]
- [From Phase 2 Pros]

**Negative:**
- [From Phase 2 Cons with mitigations]
- [From Phase 2 Cons with mitigations]
- [From Phase 2 Cons with mitigations]

**Neutral:**
- [Implementation considerations]
- [Team learning required]

## Alternatives Analysis

### Option A: [Name]

**Pros:**
- [From Phase 2 alternatives table]

**Cons:**
- [From Phase 2 alternatives table]

**Why Not Selected:** [From Phase 2]

### Option B: [Name]

[Similar structure]

## Diagram (if applicable)

[For architecture/integration/data decisions - include Mermaid diagram for proper documentation]

```mermaid
[C4Context, Component, Sequence, or ER diagram depending on decision type]
```

## Implementation Notes

- [Specific guidance for implementing this decision]
- [Tools/frameworks to use]
- [Configuration considerations]

## References

- [Link to Phase 2 detailed exploration]
- [External documentation]
- [Team documentation]
```

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
- Phase 2 (Exploration): Use ASCII diagrams for speed and scannability
- Phase 3 (Documentation): Use Mermaid diagrams for proper ADR documentation

**Reference:** See `kb-diagram-examples.md` for Mermaid diagram examples and placement guidance

---

## Critical Workflow Rules

### 1. Progressive Disclosure

**Rule:** Deliver information in manageable chunks with user control points

**Application:**
- Phase 1: ONE question at a time (never batch)
- Phase 2a: Table first, details on demand
- Phase 2b: Generate approaches one at a time
- Phase 3: 1-2 ADRs maximum

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

**Rule:** Use ASCII diagrams for exploration (Phases 1-2), Mermaid for documentation (Phase 3)

**Required Diagrams:**
- Phase 1: None (requirements text only)
- Phase 2a: None (comparison table only)
- Phase 2b: ASCII System Context + Component Structure (quick to scan)
- Phase 3: Mermaid diagrams in ADRs (proper documentation quality)

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

### Phase 2 (Solutions)
- `kb-architecture-patterns.md` - Pattern catalog with characteristics
- `kb-technology-selection.md` - Technology evaluation frameworks
- `kb-anti-patterns.md` - Common mistakes to avoid
- `kb-scaling-strategies.md` - Scaling approaches by size
- `guide-ascii-diagrams.md` - ASCII diagram patterns and templates
- `template-comparison-table.md` - Comparison table format

### Phase 3 (Documentation)
- `kb-adr-library.md` - ADR templates and examples
- `kb-diagram-examples.md` - Mermaid diagram examples for ADRs

**Query Pattern:**

When recommending architectures in Phase 2:
1. Query `kb-architecture-patterns.md` for candidate patterns
2. Filter by constraints (team size, timeline, scale)
3. Score each pattern on fit dimensions
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
