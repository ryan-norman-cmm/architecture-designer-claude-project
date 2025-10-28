# Claude Desktop Projects Repository

## Overview

This repository contains **Claude Desktop project templates** following a standardized **three-layer architecture pattern**. Each project is self-contained with agent instructions, workflow definitions, and knowledge base files.

### Three-Layer Architecture

Every Claude Desktop project follows this pattern:

```
projects/<project-name>/
├── project-instructions.md       # Layer 1: Agent Instructions
│   └── Personality, principles, response frameworks
└── output/
    ├── workflow-*.md             # Layer 2: Workflow Definitions
    │   └── Conversation phases, patterns, examples
    └── kb-*.md                   # Layer 3: Knowledge Base Files
        └── Patterns, frameworks, examples, templates
```

**How the layers work together:**
1. **Layer 1** defines WHO the agent is (personality, philosophy, principles)
2. **Layer 2** defines HOW the agent converses (workflow phases, patterns, transitions)
3. **Layer 3** defines WHAT the agent knows (domain knowledge, patterns, examples)

**Current Projects:**
- **architecture-designer**: Senior Principal Architect agent (230K+ tokens)

## Repository Structure

```
.
├── projects/                              # Claude Desktop projects
│   └── architecture-designer/             # Architecture Designer project
│       ├── project-instructions.md        # Agent personality and workflow
│       └── output/                        # Knowledge base (230K+ tokens)
│           ├── kb-architecture-patterns.md
│           ├── kb-technology-selection.md
│           ├── kb-anti-patterns.md
│           ├── kb-scaling-strategies.md
│           ├── kb-adr-library.md
│           ├── kb-diagram-examples.md
│           └── workflow-architecture-exploration.md
└── documentation/                         # Product requirements and releases
    ├── product-requirements.md
    └── initiative-releases.md
```

---

## Architecture Designer Project

A Claude Desktop agent that transforms product requirements into production-ready system architectures.

### Three-Layer Breakdown

**Layer 1: Agent Instructions** (`project-instructions.md`)
- Persona: Senior Principal Architect with 25+ years experience
- Principles: Present options not mandates, match reality, boring tech wins
- Framework: Technology evaluation scoring, tradeoff analysis templates

**Layer 2: Workflow** (`output/workflow-architecture-exploration.md`)
- 6-phase workflow: Requirements → Gap ID → Exploration → Clarification → Selection → Design
- Conversation patterns for each phase
- 26K tokens

**Layer 3: Knowledge Base** (7 files, 230K+ tokens)
- `kb-architecture-patterns.md` (78K): 12+ patterns with examples
- `kb-technology-selection.md` (38K): Tech evaluation frameworks
- `kb-anti-patterns.md` (18K): Common mistakes to avoid
- `kb-scaling-strategies.md` (37K): Scaling by growth phase
- `kb-adr-library.md` (18K): ADR templates
- `kb-diagram-examples.md` (20K): Mermaid best practices

## What This Agent Does

### Core Capabilities

1. **Requirements Analysis**
   - Extracts key architectural drivers from requirements
   - Identifies performance, scale, and complexity considerations
   - Flags critical gaps or unrealistic expectations

2. **Architecture Exploration**
   - Proposes 2-3 genuinely different architectural approaches
   - Creates visual Mermaid diagrams for each approach
   - Provides honest tradeoffs (no silver bullets)
   - Makes contextual recommendations based on team, timeline, and constraints

3. **Detailed Design**
   - Component architecture with clear responsibilities
   - Technology stack recommendations with specific versions
   - Data flow diagrams for critical paths
   - Deployment and scaling strategies
   - Monitoring and observability plans

4. **Architecture Decision Records (ADRs)**
   - Documents major architectural decisions
   - Captures context, rationale, and tradeoffs
   - Tracks alternatives considered and why they were rejected

## Project Setup

### 1. Create New Claude Project

```
Project Name: Architecture Designer
Description: Expert architecture design agent that transforms requirements
into detailed, production-ready system architectures with multiple approaches,
honest tradeoffs, and comprehensive documentation.
```

### 2. Add Project Instructions

Copy the contents of `projects/architecture-designer/project-instructions.md` into the project's custom instructions field. These instructions define:

- Agent personality and philosophy
- Core workflow (intake → exploration → detailed design)
- Communication guidelines
- Quality standards and checklists

### 3. Upload Knowledge Base Files

Create and upload these 5 markdown files to the project's knowledge base:

#### File 1: `architecture-patterns-library.md` (~50K tokens)
**Purpose**: Comprehensive catalog of architectural patterns

**Contents:**
- 12+ architectural patterns with detailed descriptions
- When to use / avoid each pattern
- Technology stack options for each
- Scaling strategies and real-world examples
- Visual diagrams and decision frameworks

**Key Patterns Covered:**
- Monolithic Architecture
- Microservices Architecture
- Event-Driven Architecture
- Serverless Architecture
- Layered, Hexagonal, CQRS, Event Sourcing
- API Gateway, BFF, Strangler Fig, Circuit Breaker

#### File 2: `technology-selection-guide.md` (~50K tokens)
**Purpose**: Decision frameworks for selecting technologies

**Contents:**
- Backend language selection (Node.js, Python, Go, Java, Rust, C#)
- Database selection (PostgreSQL, MongoDB, MySQL, Redis, DynamoDB)
- Message queue / event streaming (RabbitMQ, Kafka, SQS, NATS)
- Frontend frameworks (React, Vue, Angular, Svelte, Next.js)
- Cloud providers (AWS, Azure, GCP, DigitalOcean)
- DevOps tools and monitoring solutions

**Decision Framework:**
- 40% Team Expertise (most important)
- 20% Community/Ecosystem
- 15% Performance Requirements
- 10% Scalability Needs
- 10% Development Velocity
- 5% Long-term Maintainability

#### File 3: `adr-library.md` (~40K tokens)
**Purpose**: Architecture Decision Record templates and examples

**Contents:**
- ADR template with all sections
- 10-15 real-world ADR examples covering:
  - Database selection decisions
  - API design choices (REST vs GraphQL vs gRPC)
  - Authentication approaches
  - Microservices vs monolith decisions
  - Caching strategies
  - Deployment platform choices
  - Monitoring and observability selections

**ADR Structure:**
- Context and problem statement
- Decision and rationale
- Consequences (positive and negative)
- Alternatives considered
- Implementation notes

#### File 4: `anti-patterns-case-studies.md` (~30K tokens)
**Purpose**: Learn from real-world mistakes

**Contents:**
- 15+ detailed anti-pattern case studies including:
  - Premature Microservices (startup with 8 engineers, 12 services)
  - The Distributed Monolith (shared database, synchronous coupling)
  - Resume-Driven Development (rewriting working stack)
  - The God Service, Event Chain Hell, Over-Engineering
  - The Scalability Cliff, Cargo Cult Architecture

**Each Case Study Includes:**
- What went wrong and why
- Financial and team impact
- Red flags that indicated problems
- How to fix or avoid
- Key lessons learned

#### File 5: `scaling-strategies.md` (~30K tokens)
**Purpose**: Practical scaling guidance

**Contents:**
- Scaling curve: What to do at each phase (0-1K, 1K-10K, 10K-100K, 100K-1M users)
- Bottleneck identification frameworks
- Capacity planning techniques
- Cost optimization strategies
- Real-world scaling case studies (Shopify, Netflix, Instagram, Stack Overflow)
- When to actually scale vs premature optimization

**Key Frameworks:**
- Performance optimization decision trees
- Database scaling strategies
- Caching layer design
- Load balancing approaches

### Knowledge Base Size

**Total: ~230K tokens** across 5 files

Claude Projects support up to 200K tokens normally, with automatic RAG (Retrieval-Augmented Generation) mode for larger knowledge bases. The system will automatically use RAG when needed for efficient retrieval.

## How to Use

### Typical Workflow

#### 1. Provide Requirements

```
You: "I need to design an architecture for a SaaS project management
tool with these requirements:
- 10K users at launch, 100K users in 1 year
- Team of 8 developers (5 backend, 3 frontend)
- Budget: $500/month initially
- Timeline: 3 months to MVP
- Key features: Projects, tasks, real-time collaboration, file uploads
- Need to support custom fields per workspace"
```

#### 2. Solution Overview & Approval ⭐ NEW

Claude will first generate a minimal high-level overview (500 words max):
- Problem understanding confirmation
- Proposed architectural direction (high-level only)
- Key assumptions about team, scale, timeline, budget
- Architectural principles guiding the solution
- What this enables and what it defers

You'll then approve, refine, or reject before proceeding to detailed exploration.

#### 3. Architecture Exploration

After you approve the overview, Claude will:
- Analyze requirements and identify key architectural drivers
- Flag any critical gaps (e.g., "No performance targets specified")
- Propose 2-3 distinct architectural approaches:
  - Approach A: Modular Monolith (recommended for team size)
  - Approach B: Event-Driven Microservices (if needed)
  - Approach C: Serverless (if cost-optimization priority)
- Provide Mermaid diagrams for each approach
- Present honest tradeoffs
- Make a recommendation with clear rationale

#### 4. Select Approach

```
You: "Let's go with Approach A - the modular monolith"
```

#### 5. Detailed Design

Claude will create:
- **System Context Diagram**: External interactions
- **Component Architecture**: Internal structure with clear boundaries
- **Sequence Diagrams**: Critical workflows (e.g., user creates project)
- **Component Specifications**: For each major component:
  - Responsibility
  - Interfaces exposed (APIs, events)
  - Dependencies
  - Technology choice with rationale
  - Scalability strategy
  - Error handling approach
  - Monitoring metrics
- **Data Architecture**: Database schema, access patterns, consistency requirements
- **Deployment Architecture**: Infrastructure, CI/CD pipeline, costs
- **Monitoring Strategy**: Metrics, logging, alerting

#### 6. Architecture Decision Records

Claude will generate 3-5 ADRs for major decisions:
- ADR-001: PostgreSQL as Primary Database
- ADR-002: Modular Monolith Architecture
- ADR-003: JWT-based Authentication
- ADR-004: Redis Caching Strategy
- ADR-005: Next.js for Full-Stack Development

### Iteration and Deep Dives

The agent maintains conversation context, so you can:

```
You: "Can you add more detail on the caching strategy?"
→ Claude expands caching section with specific patterns, TTLs, invalidation

You: "What if we need to scale to 1M users? How would this architecture evolve?"
→ Claude provides evolution path with specific milestones

You: "What are the security considerations for the file upload feature?"
→ Claude details security measures, storage options, scanning strategies

You: "Can you estimate monthly costs at 50K users?"
→ Claude provides detailed cost breakdown by component
```

### Asking "What If" Questions

```
You: "What if we used microservices instead?"
→ Claude explains tradeoffs for your specific context (team size, timeline)

You: "What if we need HIPAA compliance?"
→ Claude updates architecture with compliance requirements

You: "What if the team only knows Python, not Node.js?"
→ Claude adjusts technology recommendations accordingly
```

## Agent Philosophy

### Core Principles

1. **Present Options, Not Mandates**
   - Always shows 2-3 distinct approaches
   - Honest tradeoffs for each
   - User makes final decision

2. **Match Architecture to Reality**
   - Designs for actual team size and expertise
   - Considers real budget and timeline constraints
   - Not idealized textbook solutions

3. **Boring Technology Wins**
   - Prefers proven, well-understood tech
   - New technology requires compelling justification
   - "Resume-driven development" is called out

4. **Visual Communication**
   - Always creates Mermaid diagrams
   - Diagrams clarify, not decorate
   - System context, components, sequences, deployment

5. **Document Decisions**
   - ADRs for every major choice
   - Context, rationale, tradeoffs, alternatives
   - Future teams understand why decisions were made

6. **Pragmatic Tradeoffs**
   - Every architecture has downsides
   - Acknowledged honestly and upfront
   - Explains mitigation strategies

### Agent Personality

**Strategic Thinker**: Sees big picture and how pieces fit together

**Balanced & Impartial**: Presents tradeoffs objectively without favoritism

**Pragmatic**: Designs for real constraints (team, budget, timeline) not ideals

**Visual**: Thinks in diagrams and system interactions

**Experienced**: References real-world success and failure patterns

**Direct**: Calls out unrealistic expectations kindly but clearly

### Example Agent Voice

```
"Here are three approaches, each optimized for different priorities..."

"This works well if X, but struggles when Y..."

"Most teams choose A, but given your constraint of B, consider C instead..."

"You mentioned needing microservices. Before we go there, let me ask:
what specific problem are you trying to solve? Your team of 5 developers
might struggle with the operational overhead..."
```

## Key Features

### 1. Challenges Unrealistic Expectations

**Bad Request:**
```
"We need 99.99% uptime, microservices, Kubernetes, real-time
collaboration like Google Docs, ML-powered features, and we
have 3 developers and 3 months."
```

**Agent Response:**
```
"I need to be direct: This scope is unrealistic for a 3-person
team in 3 months. Let me break down why:

- 99.99% uptime: Requires infrastructure most startups don't need (and costs $$)
- Microservices + Kubernetes: Needs dedicated DevOps, adds 2-3 months
- Real-time collaboration: Complex feature, 1-2 months alone
- ML features: Requires data, training, optimization

Recommendation: Let's build an MVP that works well rather than
an over-engineered system that never launches. Here's what's achievable..."
```

### 2. Grounds Recommendations in Context

**Example:**
```
"Many teams use Kubernetes. Should we?"

Agent: "Kubernetes is powerful but let's look at your context:
- Team: 5 developers, no dedicated DevOps
- Scale: 10K users initially
- Deployment frequency: ~Weekly

Kubernetes adds significant complexity:
- Learning curve: 2-3 months
- Operational overhead: 20-40 hours/month
- Over-engineered for your scale

Recommendation: Start with Heroku or Render ($50-200/month).
Dead simple deployment, scales to 100K users easily. When you
have 50+ engineers and 20+ services, THEN consider Kubernetes."
```

### 3. Provides Specific Technology Recommendations

**Not Vague:**
❌ "Use a database and caching"

**Specific and Justified:**
✅ "PostgreSQL 15+ on AWS RDS (db.t3.medium, ~$70/month) for primary
database because:
1. Your data is relational (users → projects → tasks)
2. JSONB handles custom fields (no second database needed)
3. Built-in full-text search (no Elasticsearch initially)
4. Team knows SQL

Redis 7.0 via ElastiCache (cache.t3.small, ~$30/month) for:
- Session storage (30-day TTL)
- Frequently accessed projects (5-minute TTL)
- Rate limiting (1-hour sliding window)"
```

### 4. Creates Production-Ready Documentation

**Deliverables include:**
- System architecture diagrams (multiple views)
- Component specifications (6-10 components detailed)
- Technology stack with versions and justifications
- Data model with schema examples
- Deployment architecture with cost estimates
- Monitoring and alerting strategy
- 3-5 Architecture Decision Records
- Scaling plan with specific milestones

### 5. References Real-World Examples

**Not Theoretical:**
```
"Microservices are the modern approach..."
```

**Real-World Grounded:**
```
"Let's look at how successful companies actually scaled:

Shopify: Rails monolith to $billions GMV, only extracted services
after years with 100+ engineers

Stack Overflow: Still runs on ASP.NET monolith, serves billions
of requests with small team

Instagram: Started as Django monolith, scaled to 100M users before
extracting services

The pattern: Start simple, extract services only when feeling real pain."
```

## When to Use This Agent

### Perfect For:

✅ **New project design** - Starting from requirements
✅ **Architecture reviews** - Evaluating existing designs
✅ **Technology selection** - Choosing stack with justification
✅ **Scaling planning** - How to grow from 10K to 100K to 1M users
✅ **Team discussions** - Exploring architectural options
✅ **Documentation** - Creating ADRs and design docs
✅ **Learning** - Understanding architectural patterns and tradeoffs

### Not Suitable For:

❌ **Implementation code** - Agent designs architecture, doesn't write full applications
❌ **Quick answers** - Agent provides thoughtful, comprehensive responses (takes time)
❌ **Specific debugging** - Not for "why is my Express app crashing"
❌ **Tutorial requests** - Not "teach me React" (use for architecture decisions)

## Expected Output Quality

### What You Get

**Architecture Exploration Phase:**
- 2-3 page document with approaches
- 3-5 Mermaid diagrams
- Tradeoff analysis with specific pros/cons
- Recommendation with clear rationale
- 15-20 minute read

**Detailed Design Phase:**
- 10-15 page comprehensive design document
- 8-12 Mermaid diagrams (context, components, sequences, deployment)
- Component specifications for 6-10 major components
- Technology recommendations with versions
- Cost estimates
- Scaling strategy
- 30-45 minute read

**Architecture Decision Records:**
- 3-5 ADRs, each 2-3 pages
- Full context, decision, rationale, consequences
- Alternatives considered
- Implementation notes
- 5-10 minutes per ADR

### Example Output Structure

```markdown
# Architecture Design: [Project Name]

## 1. Requirements Summary
- Business context
- Key architectural drivers
- Critical constraints

## 2. Architectural Approaches

### Approach A: Modular Monolith
- High-level architecture diagram
- Key components
- Technology stack
- Strengths and tradeoffs
- Best fit scenarios

### Approach B: Event-Driven Microservices
[Similar structure]

### Approach C: Serverless
[Similar structure]

### Recommended Approach: Modular Monolith
- Clear rationale tied to requirements
- Acknowledging tradeoffs
- Evolution path

## 3. Detailed Architecture

### System Context Diagram
[Mermaid diagram showing external interactions]

### Component Architecture
[Mermaid diagram showing internal structure]

### Critical Workflows
[2-3 sequence diagrams]

### Component Specifications
[Detailed specs for 6-10 components]

### Data Architecture
[Database schema, access patterns]

### Deployment Architecture
[Infrastructure, CI/CD, costs]

### Monitoring & Observability
[Metrics, logging, alerting]

## 4. Architecture Decision Records

### ADR-001: PostgreSQL as Primary Database
[Full ADR with template]

### ADR-002: Modular Monolith Architecture
[Full ADR]

[Additional ADRs...]

## 5. Implementation Roadmap
- Phase 1: Foundation (Weeks 1-4)
- Phase 2: Core Features (Weeks 5-8)
- Phase 3: Polish & Launch (Weeks 9-12)
```

## Tips for Best Results

### 1. Provide Complete Requirements

**Better Input:**
```
- Target users: 10K at launch, 100K in year 1
- Team: 8 developers (5 backend, 3 frontend, all know JavaScript)
- Timeline: 3 months to MVP
- Budget: $500/month initially, can grow to $2K/month
- Performance: API responses < 200ms p95
- Key features: [list 5-7 main features]
- Compliance: None initially, might need SOC 2 later
```

**Incomplete Input:**
```
"Design a social media app"
→ Too vague, agent will ask many clarifying questions
```

### 2. Be Honest About Constraints

Don't hide:
- Small team size (agent will design appropriately)
- Limited budget (agent will optimize for cost)
- Tight timeline (agent will prioritize MVP scope)
- Team expertise gaps (agent will choose familiar tech)

Agent designs for YOUR reality, not ideal scenarios.

### 3. Ask Follow-Up Questions

```
"Why did you choose PostgreSQL over MongoDB?"
"What if our team only knows Python?"
"How would this handle 10x traffic?"
"What are the security implications?"
"Can you break down the costs?"
```

Agent maintains context and can dive deeper on any aspect.

### 4. Challenge Recommendations

```
"Everyone says we need microservices. Why are you recommending a monolith?"
→ Agent will explain reasoning specific to your context

"Isn't Kubernetes standard these days?"
→ Agent will explain when it's appropriate vs overkill
```

Agent welcomes pushback and will defend recommendations with reasoning.

### 5. Request Specific Artifacts

```
"Can you create ADRs for the database and authentication decisions?"
"Can you add a detailed caching strategy?"
"Can you show the sequence diagram for the payment flow?"
"Can you estimate costs at different user scales?"
```

### 6. Iterate on the Design

```
"Actually, we need to support mobile apps too. How does that change things?"
→ Agent updates architecture (adds BFF pattern, mobile considerations)

"Budget increased to $5K/month. Does that open new options?"
→ Agent revisits recommendations with higher budget

"Team is growing to 20 people next quarter. Should we reconsider microservices?"
→ Agent provides evolution path
```

## Common Usage Patterns

### Pattern 1: New Project Design

```
Session 1 (1 hour):
- Provide requirements
- Review 2-3 architectural approaches
- Ask clarifying questions
- Select approach

Session 2 (1-2 hours):
- Review detailed design
- Deep dive on specific components
- Challenge decisions
- Request additional diagrams

Session 3 (30 min):
- Review ADRs
- Finalize documentation
- Get cost estimates
- Confirm implementation plan
```

### Pattern 2: Technology Selection

```
You: "We're deciding between PostgreSQL and MongoDB.
Our data model has users, organizations, projects (hierarchical),
and tasks. We need complex reporting. Team knows SQL."

Agent: [Analyzes data model, query patterns, team expertise]
→ Recommends PostgreSQL with detailed reasoning
→ Shows when MongoDB would be better fit
→ Provides ADR documenting decision
```

### Pattern 3: Scaling Planning

```
You: "Our app currently handles 50K users on a monolith.
We're expecting to grow to 500K users in 6 months.
How should we prepare?"

Agent: [Analyzes current architecture, growth trajectory]
→ Phase 1: Optimize current monolith (database, caching)
→ Phase 2: Add read replicas and CDN
→ Phase 3: Consider extracting hot services
→ Provides specific metrics to watch
→ Cost estimates at each phase
```

### Pattern 4: Architecture Review

```
You: "Can you review our current architecture?
[pastes existing design or description]"

Agent: [Systematic review]
→ Strengths (what's done well)
→ Critical issues (must fix)
→ Major concerns (should address)
→ Risks with mitigation strategies
→ Recommendations with priorities
```

## Limitations

### What This Agent Cannot Do

1. **Write Full Implementation Code**
   - Agent designs architecture, doesn't implement entire applications
   - Can provide code snippets/examples for clarity
   - Not a replacement for development team

2. **Access External Systems**
   - Can't query your actual database for metrics
   - Can't profile your running application
   - Works from information you provide

3. **Make Business Decisions**
   - Can't decide product features
   - Can't prioritize business requirements
   - Focuses on technical architecture

4. **Predict Future with Certainty**
   - Provides guidance based on patterns, not guarantees
   - "Most teams experience X" not "You will experience X"

5. **Replace Human Judgment**
   - Agent is advisor, you make final decisions
   - Context-specific factors you know best
   - Tool to augment, not replace, your expertise

### Claude Desktop Specific Limitations

1. **No Real-Time Data**
   - Can't check current cloud pricing
   - Can't verify latest framework versions
   - Knowledge cutoff: January 2025

2. **No File Editing**
   - Can't directly edit your codebase
   - Provides recommendations, you implement

3. **Conversation Isolation**
   - Each conversation is independent
   - No memory between conversations (unless you paste previous context)

4. **Knowledge Base Static**
   - Uploaded files don't auto-update
   - Refresh knowledge base periodically for updates

## Maintenance

### Keeping Knowledge Base Current

**Quarterly Updates (Recommended):**

1. **architecture-patterns-library.md**
   - Add new emerging patterns
   - Update real-world case studies
   - Refresh technology versions

2. **technology-selection-guide.md**
   - Update framework versions and recommendations
   - Add new technologies gaining traction
   - Update cost estimates

3. **adr-library.md**
   - Add new ADR examples from your projects
   - Update template based on usage

4. **anti-patterns-case-studies.md**
   - Add new anti-pattern discoveries
   - Update case studies with outcomes

5. **scaling-strategies.md**
   - Update cost estimates
   - Add new scaling patterns
   - Refresh performance benchmarks

### Version Control

Consider versioning your knowledge base files:

```
architecture-patterns-library-v1.0.md (Oct 2025)
architecture-patterns-library-v1.1.md (Jan 2026)
```

### Custom Additions

Add your organization-specific content:

```
company-tech-standards.md
- Your organization's approved technologies
- Internal architecture patterns
- Company-specific compliance requirements
- Past architecture decisions to learn from
```

## Troubleshooting

### Agent Not Following Instructions

**Problem**: Agent doesn't seem to follow the persona
**Solution**: Custom instructions may not have saved properly. Re-paste and ensure they're applied.

### Responses Too Generic

**Problem**: Getting generic advice not specific to your context
**Solution**: Provide more detailed requirements (team size, expertise, budget, timeline, scale targets)

### Wrong Technology Recommendations

**Problem**: Recommending technologies your team doesn't know
**Solution**: Explicitly state team expertise in requirements: "Team knows JavaScript, has never used Go"

### Missing Diagrams

**Problem**: Not generating Mermaid diagrams
**Solution**: Explicitly request: "Can you create a component architecture diagram?"

### Too Much Detail / Not Enough Detail

**Problem**: Response is overwhelming or too shallow
**Solution**: Guide the agent:
- "Can you give me a high-level summary first?"
- "Can you go deeper on the database design?"

### Agent Recommending Over-Engineering

**Problem**: Suggesting Kubernetes for small team
**Solution**: This shouldn't happen if you provided team size. Remind agent:
"We only have 5 developers - is this realistic?"

## Success Metrics

You'll know this agent is working well when:

✅ **Realistic Designs**: Architectures match your actual team and constraints
✅ **Clear Tradeoffs**: You understand pros and cons of each decision
✅ **Implementable Plans**: You can hand design to team and start building
✅ **Good Questions**: Agent asks about things you hadn't considered
✅ **Honest Guidance**: Agent pushes back on unrealistic requests
✅ **Documented Decisions**: ADRs capture why decisions were made
✅ **Time Savings**: Architecture decisions made in hours, not weeks
✅ **Team Alignment**: Clear documentation helps team understand direction

## Example Conversations

### Example 1: MVP Design

**User:**
```
I need to design a SaaS invoicing tool. We're a 2-person team
(1 backend, 1 frontend), both know JavaScript. Need to launch
in 6 weeks with basic features: create invoices, send via email,
accept payments via Stripe. Budget is $100/month for infrastructure.
```

**Agent Response Highlights:**
- Recommends Next.js full-stack (one codebase, fast development)
- PostgreSQL for database (relational invoices/customers/line-items)
- Deploy to Vercel (~$20/month)
- Stripe for payments (no need to build)
- Simple architecture, no over-engineering
- Focuses on shipping fast

### Example 2: Scaling Existing App

**User:**
```
We have a Rails monolith serving 50K users. Database is hitting
limits (80% CPU). We're considering microservices. Team of 12
developers. What should we do?
```

**Agent Response Highlights:**
- Don't jump to microservices yet (team size okay for monolith)
- First optimize database:
  - Add read replicas
  - Review slow queries
  - Add caching layer
  - Connection pooling
- Provides specific optimization roadmap
- Microservices only if above fails
- Explains operational overhead of microservices

### Example 3: Technology Decision

**User:**
```
Deciding between REST and GraphQL for our API. Mobile and web
clients. Team hasn't used GraphQL before. What do you recommend?
```

**Agent Response Highlights:**
- Analyzes: Team expertise (REST), client needs (multiple clients), timeline
- Recommends REST for MVP (team knows it, ship faster)
- Explains when GraphQL worth the learning curve
- Provides evolution path: REST → GraphQL later if needed
- Creates ADR documenting decision
- Honest about tradeoffs

## Additional Resources

### Related Claude Desktop Projects

This agent pairs well with:
- **Requirements Analyst**: Defines requirements before architecture
- **Code Review Agent**: Reviews implementation against architecture
- **DevOps Advisor**: Infrastructure and deployment specifics

### Learning More About Architecture

The knowledge base files are educational resources:
- Read `architecture-patterns-library.md` to learn patterns
- Study `anti-patterns-case-studies.md` to avoid mistakes
- Review `adr-library.md` for decision documentation examples

### Contributing

To improve this agent:
1. Add examples from your projects to knowledge base
2. Document anti-patterns you've encountered
3. Update technology recommendations as tools evolve
4. Share ADRs from your architecture decisions

## Support & Feedback

### Common Questions

**Q: Can this agent design any type of system?**
A: Yes - web apps, mobile backends, data pipelines, microservices, APIs. Focuses on software architecture, not hardware/embedded systems.

**Q: How long does a design session typically take?**
A: Initial exploration: 30-60 min. Detailed design: 1-2 hours. Total: 2-3 hours for complete architecture documentation.

**Q: Do I need to be technical to use this?**
A: Some technical background helps, but agent explains concepts clearly. Best used by: CTOs, tech leads, senior engineers, architects.

**Q: Can I use this for architecture reviews?**
A: Yes! Paste your current architecture and ask for review. Agent will identify risks, gaps, and provide recommendations.

**Q: How often should I update the knowledge base?**
A: Quarterly recommended. Technology changes fast - keep recommendations current.

**Q: Can I customize for my company?**
A: Absolutely. Add company-specific files: approved technologies, internal patterns, compliance requirements, past decisions.

## Quick Start Checklist

- [ ] Create new Claude Desktop Project named "Architecture Designer"
- [ ] Copy custom instructions (2,800 words) into project settings
- [ ] Create 5 knowledge base markdown files:
  - [ ] architecture-patterns-library.md (~50K tokens)
  - [ ] technology-selection-guide.md (~50K tokens)
  - [ ] adr-library.md (~40K tokens)
  - [ ] anti-patterns-case-studies.md (~30K tokens)
  - [ ] scaling-strategies.md (~30K tokens)
- [ ] Upload all 5 files to project knowledge base
- [ ] Test with sample architecture request
- [ ] Verify agent follows persona and references knowledge base
- [ ] Customize with company-specific additions (optional)

## Version

**Project Version**: 1.0
**Last Updated**: October 27, 2025
**Knowledge Base Size**: ~230K tokens
**Claude Desktop Compatible**: Yes
**Requires**: Claude Desktop app with Projects feature

---

## Final Notes

This Architecture Designer agent represents hundreds of hours of distilled architectural wisdom, real-world case studies, and battle-tested patterns. It's designed to save you from common mistakes, guide you toward pragmatic solutions, and document decisions clearly.

**Remember**: The agent is a tool to augment your judgment, not replace it. Use it to explore options, understand tradeoffs, and document decisions - but you make the final call based on your specific context and expertise.

**Philosophy**: Start simple, add complexity only when needed, optimize for shipping and learning, not for theoretical perfection or resume keywords.

Happy architecting! 🏗️
