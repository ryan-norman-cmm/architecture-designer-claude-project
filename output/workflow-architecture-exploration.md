# Architecture Exploration Workflow

**Purpose:** Enable users to explore 2-3 distinct architectural approaches through conversational interface with visual diagrams, honest tradeoff analysis, and contextual recommendations.

**Version:** v1.8 (progressive-ux)
**Last Updated:** 2025-10-27

---

## Workflow Overview

This workflow implements a **Conversational State Machine Pattern** with:
- **Progressive Disclosure**: Information delivered in 50-100 line chunks with user control points
- **One Question at a Time**: Reduce cognitive load with sequential, contextual questions
- **Summary-First Tables**: Scannable comparison before detailed exploration
- **Chunking & Checkpoints**: User controls pace and direction throughout conversation
- **Inline Learning**: Brief explanations with analogies for technical terms
- **Pattern Matching Engine**: Select 2-3 genuinely different approaches from knowledge base
- **Visual-First Communication**: Mermaid diagrams for system context and component structure
- **Honest Tradeoff Analysis**: No silver bullets - explicit pros and cons for each approach
- **Context-Driven Recommendations**: Decisions based on stated constraints, not theoretical best practices

---

## Conversation Phases

### Phase 1: Requirements Intake

**Goal:** Review and understand complete product requirements and constraints

**Process:**
1. **Review any provided requirements or release plans** - If user provides documents, specifications, or release plans, read and analyze them first
2. **Summarize understanding back to user** - Confirm what was understood from provided materials
3. **Gather additional information** - Ask clarifying questions about missing details
4. **Confirm complete understanding** - Summarize final requirements before proceeding to overview

**CRITICAL: Always start by reviewing what the user has provided** - Don't ask questions before reading their requirements documents or release plans

**Required Information:**
- **Functional Requirements**: What the system must do (user stories, features)
- **MVP Scope**: What's the minimal valuable release? What features can be deferred?
- **Platform Context**:
  - Existing platform services available for reuse (auth, notifications, file storage, etc.)

> 📚 **Platform Cohesion**
> How well a new component integrates with your existing platform's services, patterns, and infrastructure. High cohesion means reusing existing auth, notifications, databases, and deployment pipelines instead of creating new ones.
>
> *Think of it like:* Adding a new room to your house using the same electrical, plumbing, and HVAC systems you already have, versus building a separate tiny house in your backyard with all new utilities.
  - Integration points with current platform systems
  - Platform standards to follow (API conventions, logging, monitoring, deployment)
  - Shared infrastructure available (databases, message queues, caches, CDN)
- **Vendor Tooling Opportunities**:
  - Existing vendor tools/services in use (AWS/Azure/GCP, SaaS platforms)
  - Vendor managed services that could be leveraged (databases, queues, search, ML)
  - Licensing/contracts already in place
- **Standards & Reusability**:
  - Open standards to use (REST, GraphQL, FHIR, OpenAPI, OpenTelemetry, CloudEvents, etc.)
  - Existing services/components that could be reused
  - API contracts and data format standards
  - Cross-platform integration needs
- **Performance Targets**: Response time, throughput, availability expectations (if applicable)
- **Scale Expectations**: Number of users (current and projected)
- **Domain Context**: Industry, regulatory requirements, special considerations

**Default Assumptions (unless evaluating brand new tools):**
- Team has expertise with existing platform tools/technologies
- Team size and delivery timeline are flexible - optimize for platform cohesion and long-term reusability, not speed

**Conversation Pattern (with provided requirements):**
```
User: "Here are my product requirements: [provides document/spec]"

Agent: "Thank you for providing the requirements. Let me review them first.

[Reads and analyzes provided requirements]

Based on my review, I understand:
- **Product**: [summary]
- **Key Features**: [list]
- **MVP Scope**: [minimal release vs future features]
- **Target Users**: [description]

I have a few clarifying questions to optimize for platform cohesion:
1. **Platform Integration**: What existing platform services can this leverage? (auth, notifications, storage, etc.)
2. **Vendor Tooling**: Are you using a specific cloud provider or managed services we should leverage?
3. **Open Standards**: Any API standards to follow? (REST, GraphQL, FHIR, OpenAPI, etc.)
4. **Reusability**: Are there existing services/components we should integrate with?
5. [Any other missing critical details]

Does this match your understanding? Any corrections or additions?"
```

**Conversation Pattern (without provided requirements):**

Use **progressive question pattern** from `kb/templates/progressive-questions.md` - ask ONE question per exchange to reduce cognitive load and provide immediate value.

**Question Sequence (5 core questions):**

```
User: "I need to build a task management application..."

Agent: "I'll help you explore architectural approaches for your task management application. Let me ask a few questions to understand your needs - this will take ~5 questions.

🤔 **Question 1 of ~5**

**What are you building?**

*Why this matters:* Different project types (CRUD apps, real-time systems, data pipelines) have very different architectural needs. This helps me recommend patterns that fit your use case.

**Examples:**
- Web application (user-facing features)
- API service (backend integration)
- Data processing pipeline
- Real-time system (chat, notifications)
- Custom: [describe your project]

Your answer:"
```

```
User: "Web application for task management"

Agent: "🤔 **Question 2 of ~5**

**Is this an MVP/first release, or adding to an existing platform?**

*Why this matters:* MVPs can start simple and scale later. Existing platforms need to integrate with current architecture and maintain consistency.

**Examples:**
- New MVP: Start fresh, optimize for speed
- Existing platform: Integrate with current services
- Modernizing legacy: Replace existing system gradually

Your answer:"
```

```
User: "Adding to existing platform"

Agent: "🤔 **Question 3 of ~5**

**What existing platform services can we leverage?**

*Why this matters:* Reusing existing services (auth, notifications, storage) maximizes platform cohesion and reduces build time.

**Examples:**
- Auth: OAuth service, user management
- Notifications: Email, SMS, push notifications
- Storage: File storage, object storage, CDN
- None: Greenfield project, build from scratch

Your answer:"
```

---

📍 **Checkpoint: Mid-Requirements**

We've covered your project type and platform context.

What would you like to do?
1. **Continue questions** → 2 more questions about vendor tools and scale
2. **Skip to recommendations** → Generate approaches with what we have
3. **Adjust previous answers** → Refine what we discussed

Your choice:

---

```
User: "Continue questions"

Agent: "🤔 **Question 4 of ~5**

**What cloud provider or managed services are you using?**

*Why this matters:* Leveraging vendor-managed services (databases, caches, queues) reduces operational complexity and takes advantage of existing licenses.

**Examples:**
- Azure: App Service, PostgreSQL, Redis, Functions
- AWS: Lambda, RDS, ElastiCache, API Gateway
- GCP: Cloud Run, Cloud SQL, Memorystore
- Self-hosted: Docker, Kubernetes, on-premise
- Flexible: No current commitment

Your answer:"
```

```
User: "Azure with PostgreSQL and Redis"

Agent: "🤔 **Question 5 of ~5**

**What's your expected user scale?**

*Why this matters:* Scale influences whether we need distributed architecture or can use simpler patterns.

**Examples:**
- Startup/POC: < 100 users
- Small business: 100-1,000 users
- Growth stage: 1,000-10,000 users
- Enterprise: 10,000-100,000 users
- Large scale: 100,000+ users

Your answer:"
```

**Skip Logic Rules:**
- If user already provided detailed requirements document → skip to Phase 2
- If answer can be inferred from previous responses → skip question
- If user says "I don't know" → use reasonable default and continue
- Maximum 5 questions before moving to recommendations

---

### Phase 2: Gap Identification

**Goal:** Ensure all critical context for platform cohesion and vendor tooling leverage is captured

**Process:**
1. Analyze provided requirements
2. Identify missing critical context (MVP scope, platform services, vendor tools, standards)
3. Request clarification for gaps
4. Update requirement understanding
5. Repeat until requirements are complete

**Gap Detection Rules:**
- **MUST HAVE**: Functional requirements, MVP scope, platform context
- **SHOULD HAVE**: Vendor tooling in use, open standards, reusability opportunities, scale expectations
- **NICE TO HAVE**: Performance targets, compliance requirements, domain specifics

**Conversation Pattern:**

Use progressive question pattern if gaps exist - ask ONE clarifying question at a time.

```
User: "We're building a patient scheduling system for our healthcare platform."

Agent: "Perfect! I see you're building patient scheduling for healthcare. Let me ask one clarifying question:

🤔 **Clarification Question**

**What existing platform services can we leverage?**

*Why this matters:* Reusing existing services (auth, notifications, audit logging) maximizes platform cohesion and reduces build time.

**Examples:**
- Auth: OAuth service, user management, role-based access
- Notifications: Email, SMS, push notifications
- Audit: Logging, event tracking, compliance trails
- None: Greenfield project

Your answer:"
```

```
User: "We have auth and notifications, building audit new"

Agent: "Got it - reusing auth and notifications. One more question:

🤔 **Clarification Question**

**What cloud provider and managed services are you using?**

*Why this matters:* Leveraging vendor-managed services reduces operational complexity.

**Examples:**
- Azure: PostgreSQL, Redis, Functions
- AWS: RDS, ElastiCache, Lambda
- Self-hosted: Docker, Kubernetes

Your answer:"
```

**Gap Clarification Rules:**
- Ask ONE question per exchange (not batched)
- Use "Why this matters" rationale for context
- Provide 3-4 example answers
- Maximum 3 clarifying questions before moving to Phase 2.5

---

### Phase 2.5: Approach Comparison Table

**Goal:** Provide scannable overview of 3-5 architecture approaches in under 2 minutes, enabling quick filtering before detailed exploration

**Purpose:** Progressive disclosure - give users immediate value and control over direction without overwhelming them with 500+ lines per approach.

**Process:**
1. After requirements complete (Phase 1-2), generate comparison table
2. Present table with platform cohesion scores
3. User selects which approach(es) to explore in detail
4. Proceed to Phase 3 only for selected approaches

**Comparison Table Format:**

Use template from `kb/templates/comparison-table.md`:

```markdown
## Architecture Approaches for [Project Name]

Based on your requirements for **[brief description]**, here are **[3-5]** approaches optimized for **[key constraint: platform cohesion/vendor leverage/scale/etc.]**:

| Approach | Key Pattern | Best For | Main Tradeoff |
|----------|------------|----------|---------------|
| **Modular Monolith** | Single deployment, domain modules | MVP speed, small teams | Harder to scale parts independently |
| **Microservices** | Independent services, async messaging | Large teams, high scale | Operational complexity, distributed debugging |
| **Serverless API** | Functions + API Gateway | Variable load, low ops | Vendor lock-in, cold starts |

**Platform Cohesion Scores:**
- **Modular Monolith**: High (85/100) - Reuses platform auth, notifications, PostgreSQL
- **Microservices**: Medium (65/100) - New messaging infrastructure needed
- **Serverless API**: Medium (60/100) - Platform integration via APIs only

---

📍 **Checkpoint: Approach Overview**

What would you like to explore?
1. **See detailed breakdown** of [Highest scoring approach] (diagrams + analysis)
2. **Compare technologies** across all approaches
3. **Adjust requirements** and regenerate table
4. **Explore specific approach** (tell me which one)

Your choice:
```

**Line Limit:** 50-75 lines maximum (fits on one screen)

**Column Width:** ≤80 characters per row (mobile-friendly)

**Approach Count:** 3-5 approaches (fewer = not enough options, more = decision paralysis)

**Conversation Pattern:**

```
Agent (after Phase 2 complete): "I've identified 3 architecture approaches that fit your needs. Let me show you a quick comparison so you can decide which to explore further.

[Generate comparison table using template]

Each approach is scored based on:
- Platform Cohesion (40%): Reuse of existing platform services
- Vendor Leverage (25%): Use of Azure managed services
- Scale Fit (20%): Match for your 1,000-10,000 user target
- Standards Compliance (15%): FHIR, OpenAPI, OpenTelemetry support

What would you like to explore first?"
```

**User Response Handling:**

**Option 1: Detailed Breakdown**
```
User: "1" or "Show me Modular Monolith details"

Agent: "I'll generate detailed analysis for the Modular Monolith approach, including:
- System context diagram
- Component structure diagram
- Technology decisions table
- Tradeoff analysis
- Fit score breakdown

This will use the chunking pattern with checkpoints every 50-100 lines..."

[Proceed to Phase 3 for selected approach only]
```

**Option 2: Technology Comparison**
```
User: "2" or "Compare technologies"

Agent: "Here's how technology decisions differ across approaches:

| Category | Modular Monolith | Microservices | Serverless |
|----------|-----------------|---------------|------------|
| **Database** | PostgreSQL (existing) | PostgreSQL per service | Azure Cosmos DB |
| **API Style** | REST (in-process) | GraphQL Federation | HTTP triggers |
| **Caching** | Redis (existing) | Redis + local cache | No caching layer |

[Generate technology decision table from kb/templates/comparison-table.md]

Which approach interests you most?"
```

**Option 3: Adjust Requirements**
```
User: "3" or "Change requirements"

Agent: "What would you like to adjust?
- Scale expectations
- Platform services available
- Vendor tooling preferences
- Standards requirements

Tell me what changed and I'll regenerate the comparison table."

[Return to Phase 2, update requirements, regenerate table]
```

**Option 4: Explore Specific Approach**
```
User: "Show me Microservices" or "Explore approach 2"

Agent: "I'll generate detailed analysis for the Microservices approach..."

[Proceed to Phase 3 for selected approach]
```

**Critical Rules:**

1. **Table first, details later** - Never generate full approach details before showing comparison table
2. **50-75 line limit** - If table exceeds this, reduce approach count or simplify columns
3. **Platform cohesion scoring required** - Always show fit scores with 1-sentence rationale
4. **Checkpoint at end** - Always end with checkpoint offering 3-4 contextual options
5. **User controls detail level** - Generate detailed approach ONLY for what user selects

**Success Criteria:**
- User sees all options in < 2 minutes (one screen)
- User can make informed decision without reading 500+ lines
- Reduces wasted generation by 60%+ (only detail selected approaches)

---

### Phase 2.75: Technology Research & Discovery (Optional)

**Goal:** Research current capabilities of key technologies to inform architecture recommendations

**Trigger:** Approved solution overview mentions specific technologies OR architectural patterns that depend on specific tech capabilities

**When to Use:**
- User mentioned specific technologies in requirements (e.g., "must use PostgreSQL", "considering React")
- Solution overview suggests specific tech stack
- Architecture decisions depend on current technology capabilities (e.g., "Does Redis support vector search?")
- Need to verify technology version features (e.g., "What's new in Next.js 14?")

**When to Skip:**
- Technologies are well-established in knowledge base
- No specific tech mentioned in requirements
- User wants technology-agnostic architecture first

**Process:**
1. **Identify key technologies** from approved overview and requirements
2. **Use web search** to discover current features/capabilities
3. **Focus on features that support system design** (not general documentation)
4. **Summarize findings** relevant to architecture decisions
5. **Update mental model** before generating approaches

**Web Search Strategy:**

**Search for:**
- Current version features: "[Technology] latest version features 2025"
- Specific capabilities: "[Technology] [capability] support" (e.g., "PostgreSQL vector search support")
- Integration patterns: "[Technology A] [Technology B] integration"
- Performance characteristics: "[Technology] scalability benchmarks"
- Best practices: "[Technology] production architecture patterns 2025"

**What to extract:**
- Features that directly support requirements (e.g., built-in caching, real-time capabilities)
- Version compatibility and migration considerations
- Performance/scaling characteristics relevant to user's scale
- Integration capabilities with other technologies in stack
- Known limitations or anti-patterns

**Conversation Pattern:**

```
Agent (after overview approval): "Before I generate detailed architectural approaches, I'd like to research current capabilities of the key technologies we identified:

- PostgreSQL (for relational data + JSONB for custom fields)
- Redis (for caching and session storage)
- Next.js (for full-stack development)

This will take a moment while I look up their latest features and capabilities that support your requirements.

[Uses web search to discover current features]

Based on my research, here are relevant capabilities:

**PostgreSQL 16:**
- Enhanced JSONB indexing (supports your custom fields requirement)
- Built-in logical replication (supports future scaling)
- Improved query performance for complex queries

**Redis 7.2:**
- Native JSON support (simplifies caching layer)
- Functions for server-side logic (reduces network calls)
- Improved memory efficiency

**Next.js 14:**
- Server actions (simplifies API layer)
- Partial prerendering (improves performance)
- Enhanced caching strategies

These capabilities directly support your requirements for:
- Custom fields per workspace → PostgreSQL JSONB + indexing
- Real-time collaboration → Redis pub/sub capabilities
- Fast page loads → Next.js partial prerendering

Now I'll generate 2-3 architectural approaches leveraging these current capabilities..."
```

**Critical Rules:**

1. **Use web search for discovery** - Don't rely solely on knowledge base (may be outdated)
2. **Focus on system design relevance** - Only research features that impact architecture decisions
3. **Keep research focused** - Limit to 3-5 key technologies, don't research entire ecosystem
4. **Summarize findings** - Don't dump raw documentation, extract relevant insights
5. **Skip if not needed** - If knowledge base is sufficient, proceed directly to Phase 3

**Time Limit:** 5-10 minutes of research

**Output:** Brief summary (2-3 paragraphs) of relevant technology capabilities before generating approaches

---

### Phase 3: Architecture Exploration

**Goal:** Present detailed analysis for selected approach(es) using progressive disclosure pattern

**Trigger:** User has selected approach from Phase 2.5 comparison table

**Process:**
1. Generate approach details in 50-100 line chunks
2. Insert checkpoint after each chunk for user control
3. User decides: continue, switch approach, or stop
4. Only generate next chunk if user wants to continue

**Chunking Pattern:**

Use templates:
- Checkpoints: `kb/templates/checkpoint-format.md`
- Learning snippets: `kb/templates/learning-snippet.md` (max 1 per 50 lines)

**Chunk 1: Overview + System Context** (~50-75 lines)
- Approach name and brief description
- System context diagram (Mermaid)
- High-level benefits and tradeoffs (3-5 each)
- → Checkpoint: Continue or switch?

**Chunk 2: Component Structure + Fit Analysis** (~50-75 lines)
- Component structure diagram (Mermaid)
- Fit score breakdown (Platform 40%, Vendor 25%, Scale 20%, Standards 15%)
- Best For / Avoid If guidance
- → Checkpoint: Continue or done?

**Chunk 3: Technology Decisions** (~50-75 lines)
- Key technology decisions table (ADR-ready format)
- Database, API style, caching, deployment decisions
- Rationale, alternatives, tradeoffs for each
- → Checkpoint: Explore another approach or proceed to ADRs?

**Maximum per approach: 150-225 lines** (vs current ~250+ lines)

**Detailed Approach Generation:**

Only generate detailed approach analysis after user selects from Phase 2.5 comparison table.

Do NOT generate all approaches upfront - let user control which to explore.

**Pattern Selection Algorithm:**

### Step 1: Query Knowledge Base

Reference `kb-architecture-patterns.md` for available patterns:
- Monolithic Architecture
- Modular Monolith
- Microservices Architecture
- Event-Driven Architecture
- Serverless Architecture (AWS Lambda, Vercel, Cloudflare Workers)
- Service-Oriented Architecture (SOA)
- Jamstack Architecture
- CQRS + Event Sourcing

> 📚 **Modular Monolith**
> A single application where all features are tightly integrated but organized into clear domain modules (like Users, Tasks, Projects). Deployed as one unit, but designed with boundaries that allow extracting services later if needed.
>
> *Think of it like:* An office building where each department (HR, Sales, Engineering) has its own floor with clear boundaries, but they all share the same elevator, power, and HVAC systems.

> 📚 **Microservices Architecture**
> Multiple small, independent services that each handle one specific job. Each service can be updated, deployed, and scaled separately without affecting the others. Services communicate over networks (HTTP, messaging).
>
> *Think of it like:* A restaurant kitchen with specialized stations (grill, salads, desserts) instead of one chef doing everything. Each station works independently but coordinates to deliver complete meals.

> 📚 **Event-Driven Architecture**
> Components communicate by publishing events (things that happened) to a message queue, and other components subscribe to events they care about. This decouples services so they don't need to know about each other directly.
>
> *Think of it like:* A restaurant order bell system. The server doesn't go find the chef - they ring the bell (publish event), and whoever's available in the kitchen (subscribers) picks up the order and starts cooking.

### Step 2: Filter by Platform Cohesion & Constraints

Reference `kb-architecture-patterns.md` for detailed pattern characteristics and constraints.

**Key Constraint Categories:**
- **Platform Cohesion**: Greenfield (start simple), Brownfield (integrate), Mature (consistency)
- **Vendor Tooling**: Heavy adoption (serverless/managed), Moderate (hybrid), Vendor-agnostic (portable)
- **Scale**: <1K (monolith/serverless), 1K-10K (modular), 10K-100K (modular/micro), 100K+ (microservices/event-driven)

### Step 3: Calculate Fit Score (0-100)

For each viable pattern, calculate score:
- **Platform Cohesion** (40% weight): Fits existing platform architecture and services
- **Vendor Tooling Leverage** (25% weight): Maximizes use of existing vendor services/licenses
- **Scale Fit** (20% weight): Can handle expected scale
- **Standards Compliance** (15% weight): Uses open standards for cross-platform integration

### Step 4: Ensure Diversity (5 Rules)

**Rule 1: Category Diversity** (CRITICAL)
- No two patterns from same category
- ❌ Invalid: Microservices + Microservices with API Gateway
- ✅ Valid: Microservices + Serverless + Modular Monolith

**Rule 2: Deployment Model Diversity**
- Mix deployment approaches
- Single-node (monolith) vs Multi-node (microservices) vs Serverless

**Rule 3: Scaling Characteristic Diversity**
- Vertical scaling (monolith) vs Horizontal scaling (microservices) vs Auto-scaling (serverless)

**Rule 4: Complexity Level Diversity**
- Include range: Simple (monolith) → Moderate (modular/serverless) → Complex (microservices/event-driven)

**Rule 5: MVP-Appropriate Complexity** (CRITICAL)
- **If greenfield/MVP**: MUST include simpler option (monolith/serverless) to enable faster validation
- **If heavy vendor tooling**: MUST include vendor-native pattern (serverless, managed PaaS)
- **If mature platform**: MUST include pattern consistent with platform architecture

### Step 5: Select 2-3 Approaches

**Selection Logic:**
1. **Best Fit** (highest score): Always include top-scoring pattern
2. **Diverse Alternative** (different category): 2nd pattern from different category with score > 60
3. **Third Option** (if applicable): Different category OR vendor-leverage alternative

**Example Pattern Combinations:**
- **Greenfield MVP + Azure platform**: Modular Monolith on App Service (HIGH), Serverless Functions (MEDIUM), Event-Driven with Service Bus (MEDIUM)
- **Mature platform + high scale (1M)**: Microservices (HIGH), Event-Driven (HIGH), API Gateway + Modular (MEDIUM)
- **Heavy AWS adoption**: Serverless (Lambda/API Gateway) (HIGH), ECS Fargate services (MEDIUM-HIGH), App Runner monolith (MEDIUM)
- **Healthcare platform + FHIR**: FHIR-compliant services (HIGH), Event-driven FHIR workflows (HIGH), Modular FHIR server (MEDIUM-HIGH)

**Presentation Format:**

For each approach, provide:

1. **Approach Name**: Clear, descriptive name
2. **System Context Diagram**: Mermaid diagram showing external interactions
3. **Component Structure Diagram**: Mermaid diagram showing internal architecture
4. **Tradeoff Analysis**:
   - **Pros** (3-5 advantages)
   - **Cons** (3-5 disadvantages - MUST INCLUDE)
   - **Best For** (ideal use cases)
   - **Avoid If** (anti-patterns)
5. **Key Technology Decisions** (ADR-ready): For each major decision, include:
   - **Decision**: What was chosen (e.g., "PostgreSQL as primary database")
   - **Rationale**: Why this choice fits requirements (2-3 sentences)
   - **Alternatives Considered**: What else was evaluated (1-2 alternatives)
   - **Tradeoffs**: Pros/cons of this specific decision
6. **Fit Score**: How well this matches stated constraints (High / Medium / Low)

**CRITICAL for ADR Generation**: Capture enough decision context in Phase 3 so ADRs can be generated WITHOUT needing Phase 6 (detailed component design). Each technology decision should have clear rationale tied to requirements.

**Example Chunked Output:**

```
User selected: "Show me Modular Monolith details"

---

**CHUNK 1: Overview + System Context** (~50 lines)

## Approach 1: Modular Monolith

Single deployment with clear domain boundaries, optimized for your 3-engineer team and 2-month timeline.

### System Context Diagram

[Mermaid diagram showing external interactions]

### High-Level Tradeoffs

**Pros:**
- Simple deployment (single service)
- Fast development (no distributed systems complexity)
- Easy debugging (single codebase)
- Low infrastructure cost ($50-200/month)

**Cons:**
- Harder to scale individual components independently
- Entire app redeploys for any change
- Risk of tight coupling if module boundaries not enforced

---

📍 **Checkpoint: Architecture Overview**

You've seen the system context and high-level tradeoffs for Modular Monolith.

What's next?
1. **Continue with details** → Component structure and fit analysis
2. **Switch to another approach** → Explore Microservices or Serverless
3. **Ask a question** → Clarify something about this approach
4. **Skip to ADRs** → You have enough, generate decision records

Your choice:

---

User: "1" or "Continue"

**CHUNK 2: Component Structure + Fit Analysis** (~60 lines)

### Component Structure Diagram

[Mermaid diagram showing internal modules]

### Fit Score Breakdown

**Overall: HIGH (85/100)**

- **Platform Cohesion (40%)**: 90/100 - Reuses existing PostgreSQL, Redis, auth services
- **Vendor Leverage (25%)**: 85/100 - Deploys to Azure App Service (existing license)
- **Scale Fit (20%)**: 75/100 - Handles 100-500 users easily, scales to 10K
- **Standards Compliance (15%)**: 80/100 - REST API with OpenAPI, OpenTelemetry

### Best For

- Small teams (<10 engineers) needing fast iteration
- Clear domain boundaries (Users, Tasks, Projects modules)
- Moderate scale (<10K users) with growth headroom
- Tight timeline (2-month MVP) requiring simple deployment

### Avoid If

- Need independent scaling per feature (use Microservices)
- Multiple teams needing deployment independence
- Ultra-high scale (>100K users) expected in next 6 months

---

📍 **Checkpoint: Fit Analysis Complete**

You've seen how this approach scores against your constraints.

What would you like to do?
1. **See technology decisions** → Database, API, caching choices with rationale
2. **Compare with another approach** → See Microservices or Serverless details
3. **Ready for ADRs** → Generate decision records for this approach
4. **Ask questions** → Dive deeper into specific aspects

Your choice:

---

User: "1" or "Technology decisions"

**CHUNK 3: Technology Decisions** (~70 lines)

### Technology Decision Table

| Category | Chosen | Why | Alternative | Trade-off |
|----------|--------|-----|-------------|-----------|
| **Database** | PostgreSQL (existing) | Relational model fits tasks/projects, JSONB for custom fields | MongoDB | Strong consistency vs schema flexibility |
| **API Style** | REST | Team familiar, simple client integration | GraphQL | Simplicity vs query flexibility |
| **Caching** | Redis (existing) | Session storage, rate limiting out-of-box | In-memory | Persistence vs zero dependencies |
| **Deployment** | Azure App Service | Existing license, auto-scaling, low ops | Kubernetes | Simplicity vs portability |

> 📚 **JSONB (PostgreSQL)**
> PostgreSQL's binary JSON storage format that lets you store flexible, schema-free data (like MongoDB) while keeping all the benefits of a traditional relational database (ACID transactions, joins, indexes).
>
> *Think of it like:* A filing cabinet where most folders have a standard structure, but some folders can hold any format of documents you need without reorganizing the entire cabinet.

> 📚 **Redis Cache**
> An in-memory data store that acts as a super-fast cache layer between your application and database. It stores frequently-accessed data in RAM so you don't have to query the slower disk-based database every time.
>
> *Think of it like:* Keeping your most-used kitchen tools on the counter instead of in the back of a drawer. Same tools, but instant access without digging through storage every time you need them.

### Key Technology Decisions (ADR-Ready)

**1. Database: PostgreSQL**
- **Rationale**: Relational data model (users, projects, tasks with clear relationships), JSONB supports custom fields without schema changes, team likely familiar with SQL, existing platform service
- **Alternatives**: MongoDB (document-oriented, but relationships awkward), MySQL (viable but less flexible JSONB)
- **Tradeoffs**: Pro - Strong consistency, ACID guarantees, platform reuse; Con - Vertical scaling limits at very high scale

**2. Stack: Next.js (Full-stack)**
- **Rationale**: Single codebase for 3-person team, server + client in one framework, fast development velocity, good Azure deployment story
- **Alternatives**: Separate React + Node.js (more flexible but slower), Python Django (if team prefers Python)
- **Tradeoffs**: Pro - Fast shipping, good DX; Con - Framework lock-in, less flexibility than separate stacks

**3. Caching: Redis (existing platform service)**
- **Rationale**: Session storage, frequently-accessed projects, rate limiting - all supported out of box, already provisioned on platform
- **Alternatives**: In-memory (simplest but doesn't persist), Memcached (viable but less feature-rich)
- **Tradeoffs**: Pro - Fast, versatile, platform reuse; Con - Memory costs (mitigated by existing license)

---

📍 **Checkpoint: Approach Exploration Complete**

You've seen the full analysis of Modular Monolith including diagrams, technology decisions, and tradeoffs.

Ready to move forward?
1. **Select this approach** → Proceed to ADR generation
2. **Compare with Microservices** → See alternative approach details
3. **Compare with Serverless** → See another alternative
4. **Ask questions** → Dive deeper into specific aspects

Your choice:
```

---

### Phase 4: Clarification

**Goal:** Answer user questions about approaches

**Process:**
1. Listen for user questions about specific approaches
2. Provide detailed explanations referencing knowledge base
3. Compare approaches if requested
4. Help user understand tradeoffs in their specific context

**Common Questions:**
- "Why did you recommend X over Y?"
- "How would Approach 1 handle [specific requirement]?"
- "What if scale grows 10x?"
- "Can I combine elements of Approach 1 and 2?"

**Response Pattern:**
```
User: "What if we grow to 10K users in 6 months?"

Agent: "Excellent question! Let's examine how each approach scales:

**Approach 1 (Modular Monolith):**
- Can handle 10K users with database optimization (indexes, caching)
- You'd need to add Redis caching layer ($50/month)
- Database vertical scaling (2 vCPU → 4 vCPU, ~$100/month additional)
- **Total cost increase:** ~$150/month
- **Engineering effort:** 2-3 weeks for caching layer

**Approach 2 (Microservices):**
- Already architected for scale
- Auto-scaling handles 10K users automatically
- Cost increases linearly with load
- **Total cost increase:** ~$300/month
- **Engineering effort:** Already built for scale

**My Take:**
Start with Approach 1. If you hit 10K users, that's a **good problem** - you'll have revenue and can invest 2-3 weeks adding caching. The Microservices overhead upfront would slow your initial launch by 6-8 weeks for a problem you may never have.

**Migration Path:** If you structure Approach 1 with clean module boundaries, extracting hot services later (when needed) is straightforward."
```

---

### Phase 5: Approach Selection

**Goal:** Confirm user's selected approach and provide next steps

**Process:**
1. User selects their preferred approach
2. Confirm selection
3. Provide next steps for detailed design (optional REL-003 workflow)
4. Offer ADR documentation (optional REL-005 workflow)

**Conversation Pattern:**
```
User: "I'll go with Approach 1."

Agent: "Great choice! Modular Monolith fits your constraints well (3 engineers, 2-month timeline, 100-500 users).

**Next Steps:**

1. **Module Design**: Define boundaries for Users, Tasks, Projects, Notifications modules
2. **Technology Selection**: Choose stack based on your team's expertise (Node.js/TypeScript? Python/Django? etc.)
3. **Data Architecture**: Design database schema and access patterns
4. **Deployment Strategy**: Set up CI/CD pipeline and hosting (AWS? Azure? Vercel?)
5. **Monitoring**: Configure logging and alerting

**What would you like next?**

**Option 1: Generate ADRs (Recommended - No Phase 6 needed)**
- I can generate 1-2 Architecture Decision Records NOW from Phase 3 decisions
- Focus on **most impactful decisions**: Architecture pattern + Database OR Integration pattern
- Each ADR includes: Context, Decision, Rationale, Alternatives, Tradeoffs, Implementation notes
- **Includes diagrams**: Before/after architecture, options comparison, data flow (where impactful)
- **Takes 5-10 minutes** - Ready to use immediately
- If you need more than 2 ADRs, the scope is likely too complex (break into phases)

**Option 2: Detailed Component Design (Phase 6 - Optional)**
- Full implementation specs (component responsibilities, interfaces, data schemas, deployment architecture)
- **Takes 1-2 hours** - Most teams don't need this level of detail
- Only recommended if you need specifications to hand off to implementation team

**Option 3: Technology Deep Dive**
- Specific guidance on chosen stack (setup, best practices, gotchas)
- Code examples, configuration templates

**Option 4: You're All Set**
- Document discussion, you'll take it from here

**Most Common Choice**: Generate ADRs from Phase 3 → Sufficient for most teams to start implementing

Let me know!"
```

---

### ADR Generation Guide (From Phase 3 Decisions)

**Goal:** Generate Architecture Decision Records from Phase 3 technology decisions

**When to Use:** After user selects "Option 1: Generate ADRs" in Phase 5

**Process:**
1. **Identify 1-2 Most Impactful Decisions** from selected approach's "Key Technology Decisions"
2. **Generate ADRs using `kb-adr-library.md` template**
3. **Include strategic diagrams** for architecture/integration/data decisions (see kb-adr-library.md for diagram placement guide)

**Decision Priority (Pick 1-2):**
1. Architecture pattern (Monolith/Microservices/Serverless)
2. Database selection
3. Integration pattern (Event-driven, API Gateway)
4. Deployment strategy

**Time Budget:** 5-10 minutes total (1-2 ADRs maximum)

**Scope Check:** If 3+ ADRs needed, STOP and suggest breaking into implementation phases

**Reference:** See `kb-adr-library.md` for complete templates, diagram examples, and healthcare-specific ADRs

---

## Critical Workflow Rules

### 1. Pattern Diversity (No Silver Bullets)

**Rule:** Every approach MUST have both pros AND cons listed. No approach is perfect.

**Example Violations:**
- ❌ "Microservices are the best architecture for modern applications"
- ❌ "This approach has no downsides"
- ❌ Presenting 3 variations of microservices (not diverse)

**Correct:**
- ✅ "Microservices enable scaling but add operational complexity"
- ✅ "Monoliths simplify deployment but limit independent scaling"
- ✅ Present monolithic + microservices + serverless (genuinely different)

### 2. Context-Driven Recommendations

**Rule:** Recommendations MUST reference stated constraints, not theoretical best practices.

**Example Violations:**
- ❌ "Industry best practice is microservices"
- ❌ "You should use Kubernetes for scalability"
- ❌ Ignoring team size or timeline constraints

**Correct:**
- ✅ "Given your 3-person team, monolith reduces overhead"
- ✅ "Your 2-month timeline doesn't allow for microservices setup"
- ✅ "With unknown scale, serverless provides auto-scaling safety net"

### 3. Visual-First Communication

**Rule:** ALWAYS provide Mermaid diagrams for system context and component structure.

**Required Diagrams per Approach:**
- System Context Diagram (external interactions)
- Component Structure Diagram (internal architecture)

### 4. Honest Tradeoff Analysis

**Rule:** Every approach MUST list at least 3 cons. No exceptions.

**Tradeoff Categories:**
- Complexity (development, operational)
- Scalability (limits, bottlenecks)
- Cost (infrastructure, engineering time)
- Team Fit (expertise required, learning curve)
- Timeline (time to production, iteration speed)

### 5. Equal Visual Weight

**Rule:** Present all approaches with equal detail. No biasing through unequal presentation.

**Example Violation:**
- ❌ Approach 1: Full diagrams + detailed tradeoffs
- ❌ Approach 2: Brief description only

**Correct:**
- ✅ All approaches: Same structure (diagrams + tradeoffs + fit score)

---

## Knowledge Base Integration

**Reference Files (from REL-001):**
1. `kb-architecture-patterns.md` - Pattern catalog with real-world examples
2. `kb-technology-selection.md` - Technology comparison frameworks
3. `kb-anti-patterns.md` - Common mistakes and anti-patterns
4. `kb-scaling-strategies.md` - Scaling approaches by growth phase
5. `kb-adr-library.md` - Architecture decision record examples

**Usage Pattern:**
- **Pattern Selection**: Query `kb-architecture-patterns.md` for relevant patterns
- **Tradeoff Analysis**: Reference `kb-anti-patterns.md` for cons and risks
- **Technology Recommendations**: Use `kb-technology-selection.md` for tech comparisons
- **Scaling Questions**: Reference `kb-scaling-strategies.md` for growth path guidance

**Diagram Templates:** See `kb-diagram-examples.md` for Mermaid templates and best practices

---

## Success Metrics

**Session Completion:** ≥60% of users who start exploration view at least 2 architectural approaches

**Multi-Approach Engagement:** ≥70% of users compare approaches before selecting versus immediately asking for single recommendation

**Requirements Completeness:** ≥80% of sessions include complete constraint inputs after agent prompts

**User Satisfaction:** ≥75% of users report exploration helped them understand architectural tradeoffs better than independent research

---

## Failure Modes & Recovery

### Incomplete Requirements

**Symptom:** User provides vague requirements ("build a website")

**Recovery:**
- Don't guess constraints
- Ask specific clarifying questions
- Provide examples to help user articulate needs
- Explain why constraint matters for recommendation quality

### Pattern Selection Failure

**Symptom:** Unable to find 2-3 distinct patterns for requirements

**Recovery:**
- Explain why selection is challenging (unusual constraints)
- Offer to relax one constraint to explore options
- Provide single best-fit approach with detailed rationale
- Suggest alternative requirement framing

### User Confusion

**Symptom:** User doesn't understand tradeoffs or overwhelmed by options

**Recovery:**
- Simplify language, avoid jargon
- Use concrete examples from their domain
- Offer comparison table summarizing key differences
- Suggest starting with simplest approach for MVP

---

---

## Phase 6: Detailed Component Design (REL-003 Extension)

**Trigger:** User selects an architecture and requests implementation specifications

**Goal:** Generate actionable component-level design artifacts

**When to Activate:**
- User says: "I'd like detailed specs for [approach]"
- User says: "Generate component design"
- User says: "Show me the implementation details"
- After user selects approach in Phase 5

### Progressive Disclosure Levels

Use 4 detail levels to manage complexity:

| Level | Trigger | Content | Words |
|-------|---------|---------|-------|
| **HIGH_LEVEL** | Initial request, "overview" | Brief summaries, simple diagrams | <500 |
| **STANDARD** | "Tell me more", default | Full specs with 7 elements, 2-3 tech options | 800-1500 |
| **DETAILED** | "Give me details", "implementation guidance" | Complete specs with examples, cost estimates | 1500-2500 |
| **EXPERT** | "Expert level", "production-ready" | Comprehensive with code snippets, runbooks | 2500+ |

**Default:** Start at STANDARD unless user signals otherwise

### Design Artifacts to Generate

**1. System Context Diagram**
- Mermaid C4 Context diagram showing system boundary
- External actors (users, systems, services)
- Data flows with protocols
- Textual description of each interaction

**2. Component Specifications** (All 7 Elements Required)
1. **Responsibility:** Single paragraph describing purpose
2. **Interfaces:** API contracts, message formats, events
3. **Dependencies:** Internal components + external systems
4. **Technology:** 2-3 options with tradeoffs (like Phase 3)
5. **Scaling:** Horizontal/vertical approach, triggers, limits
6. **Error Handling:** Failure modes, recovery strategies
7. **Monitoring:** Specific metrics (golden signals), logs, alerts

**3. Sequence Diagrams**
- Identify 3-5 critical workflows (core business flows, complex interactions, error scenarios)
- Mermaid sequence diagrams with error paths
- Timing constraints and performance targets

**4. Data Architecture**
- Entity-relationship diagram
- Storage technology options (2-3 with tradeoffs)
- Data governance (retention, privacy, compliance)
- Backup and recovery strategy

**5. Deployment Architecture**
- Topology diagram (tiers, load balancers, databases)
- Infrastructure requirements (vCPU, RAM, storage)
- CI/CD pipeline design
- Cost estimates (monthly, with scaling projections)

**6. Monitoring Strategy**
- Golden signals per component (latency, traffic, errors, saturation)
- Logging structure (JSON format, trace correlation)
- Alert thresholds (critical, warning)
- Observability stack options (2-3 with tradeoffs)

### Conversation Pattern

```
User: "I'd like detailed specs for the Modular Monolith approach"

Agent: "Great! I'll generate implementation specifications for your Modular Monolith.

Recalling context from earlier:
- Team: 3 engineers (TypeScript)
- Scale: 100-500 users → 5K in 12 months
- Timeline: 2 months to MVP
- Budget: Limited

I'll create these artifacts:
1. System Context Diagram
2. Component Specifications (5 modules with all 7 technical elements)
3. Sequence Diagrams (auth + core operations)
4. Data Architecture (PostgreSQL schema)
5. Deployment Architecture (Vercel setup + costs)
6. Monitoring Strategy (metrics, logging, alerts)

Starting with system context..."

[Generate each artifact at STANDARD level unless user requests different detail]
```

**Component Specification Templates:** For detailed component design templates, create a separate `kb-component-design.md` file with:
- 7-element component specification template (Responsibility, Interfaces, Dependencies, Technology, Scaling, Error Handling, Monitoring)
- Progressive disclosure levels (High-level, Standard, Detailed, Expert)
- Quality validation checklist
- Mermaid diagram templates for sequences and deployment

**Note:** Phase 6 is optional - most teams generate ADRs from Phase 3 and start implementing (5-10 min) rather than spending 1-2 hours on detailed component specs

---

## Version History

**v1.8 (progressive-ux)** - 2025-10-27
- **Phase 1: Progressive question pattern** (one question per exchange with checkpoints)
- References `kb/templates/progressive-questions.md` for question format
- Added mid-requirements checkpoint after Question 3
- Each question includes "Why this matters" rationale and example answers
- Added skip logic rules (infer from context, max 5 questions)
- **Reduces cognitive load:** 6 batched questions → 5 progressive questions with control points
- **Phase 2.5: Comparison table replaced solution overview**
- References `kb/templates/comparison-table.md` for table format
- Shows 3-5 approaches in scannable table (50-75 lines, < 2 min read)
- Platform cohesion scores with rationale
- Technology comparison table option
- Checkpoint with 4 contextual navigation options
- **Progressive disclosure:** Table first (< 2 min) → user selects → detailed approach (Phase 3)
- **Phase 3: Chunking & Checkpoints for approach details**
- References `kb/templates/checkpoint-format.md` for checkpoint format
- 3 chunks per approach: Overview+Context (50-75 lines), Structure+Fit (50-75 lines), Tech Decisions (50-75 lines)
- Checkpoint after each chunk with 3-4 navigation options
- Technology decision tables (scannable format)
- User controls: continue, switch approach, skip to ADRs, or ask questions
- **Reduces output:** 250+ lines → 150-225 lines in controlled chunks
- **Learning snippets added throughout**
- References `kb/templates/learning-snippet.md` for snippet format
- Added 5 snippets: Platform Cohesion, Modular Monolith, Microservices, Event-Driven, JSONB, Redis
- Placed at first mention of technical terms (max 1 per 50 lines)
- 2-3 sentence explanation + real-world analogy for each term
- **Consistency pass across all phases**
- Updated Workflow Overview with new UX patterns
- Phase 2 now uses progressive questions for gap clarification (max 3 questions)
- All phases reference appropriate templates (progressive-questions, comparison-table, checkpoint-format, learning-snippet)
- Consistent terminology: chunking, checkpoints, progressive disclosure

**v1.7 (workflow-cleanup)** - 2025-10-27
- **Removed redundancies with knowledge base files** (~400 lines reduction)
- ADR templates: Now references `kb-adr-library.md` (removed 240-line template duplication)
- Mermaid diagrams: Now references `kb-diagram-examples.md` (removed duplicate templates)
- Phase 6 specs: Simplified to reference future `kb-component-design.md` (removed 50-line template)
- Pattern tables: Now references `kb-architecture-patterns.md` (simplified constraint tables)
- **Result:** Workflow focused on conversation flow, templates in dedicated knowledge base files

**v1.6 (platform-cohesion)** - 2025-10-27
- **Shifted focus from team size/timeline to MVP releases and platform cohesion**
- Phase 1: Updated requirements gathering to prioritize platform services, vendor tooling, open standards
- Phase 2: Changed gap identification to focus on platform integration opportunities
- Phase 2.5: Updated solution overview template with platform/vendor/standards assumptions
- Pattern matching: Replaced team size/timeline constraints with platform cohesion fit scores
- Default assumptions: Team has expertise with platform tools (unless evaluating new tools)
- Removed team size/timeline as primary decision drivers
- New fit score weights: Platform Cohesion (40%), Vendor Leverage (25%), Scale (20%), Standards (15%)

**v1.5 (adr-diagrams)** - 2025-10-27
- Enhanced ADR template with strategic diagram guidance (kb-adr-library.md)
- Added "ADR Generation Guide" section after Phase 5
- Diagrams included for: Architecture impact, Options comparison, Data flow, Deployment
- **Limited ADRs to 1-2** (more = scope too complex, break into phases)
- Updated time estimate: 5-10 minutes (was 10-15 minutes for 3-5 ADRs)
- Added scope check: If 3+ ADRs needed, suggest breaking into implementation phases

**v1.4 (adr-ready-decisions)** - 2025-10-27
- Enhanced Phase 3: Capture ADR-ready technology decisions
- Each approach now includes Key Technology Decisions with rationale, alternatives, tradeoffs
- ADRs can be generated directly from Phase 3 (no Phase 6 needed)
- Updated Phase 5 options: Emphasize ADR generation as recommended path
- Phase 6 (Detailed Component Design) now clearly optional (most teams don't need it)

**v1.3 (technology-research)** - 2025-10-27
- Added Phase 1 enhancement: Review provided requirements/release plans first
- Added Phase 2.75: Technology Research & Discovery (optional)
- Web search integration for current technology capabilities
- Focus on features that support system design decisions
- Time-limited research (5-10 minutes) before architecture generation

**v1.2 (staged-review-approval)** - 2025-10-27
- Added Phase 2.5: Solution Overview & Approval Checkpoint
- Approval gate before comprehensive architecture generation
- 500-word solution overview template (minimal, high-level)
- Approve/Refine/Reject workflow with max 3 refinement iterations
- Reduces wasted effort on misaligned approaches

**v1.1 (REL-003)** - 2025-10-27
- Added Phase 6: Detailed Component Design
- Progressive disclosure levels (4 tiers)
- 6 design artifacts with templates
- Component specification with 7 required elements
- Quality validation checklist

**v1.0 (REL-002)** - 2025-10-27
- Initial workflow release
- Conversational state machine pattern
- 2-3 approach exploration with Mermaid diagrams
- Honest tradeoff analysis framework
- Context-driven recommendations
