# Claude Desktop Project Templates

**Version:** 1.0 | **Last Updated:** November 2025 | **For:** CMM Product Managers & Engineers

A collection of specialized Claude Desktop project templates that accelerate product development from requirements to delivery. Each project follows a proven **three-layer architecture** for maximum effectiveness.

---

## Quick Start

### What This Is

Six ready-to-use Claude Desktop projects that transform how you work:

| When You Need To... | Use This Project | Time Saved |
|---------------------|------------------|------------|
| **Design system architectures** | `architecture-designer` | Weeks → Hours |
| **Validate product requirements** | `product-requirements-validator` | Days → Hours |
| **Break initiatives into releases** | `product-releases-creator` | Days → Hours |
| **Create technical specifications** | `technical-requirements-creator` | Days → Hours |
| **Estimate development effort** | `technical-solution-estimator` | Days → Hours |
| **Plan epic delivery** | `technical-project-planner` | Days → Hours |

### Installation (3 Minutes)

1. **Open Claude Desktop** → Click "+" → "New Project"
2. **Copy project instructions** from `projects/<project-name>/project-instructions.md` into Custom Instructions
3. **Upload knowledge base files** from `projects/<project-name>/files/` to Project Knowledge
4. **Start using** - Type your first request!

**Full setup guide:** See [Installation Instructions](#installation-instructions) below

---

## Project Comparison

Choose the right project for your task:

| Project | Role | Best For | Input | Output | Knowledge Base Size |
|---------|------|----------|-------|--------|---------------------|
| **architecture-designer** | Senior Principal Architect | System architecture, technology selection, scaling strategy | Product requirements, constraints | Architecture diagrams, component specs, ADRs, tech recommendations | 252K tokens (13 files) |
| **product-requirements-validator** | Requirements Analyst | Validating completeness of BRDs | Business requirements document | Structured PRD with gaps identified | 15K tokens (4 files) |
| **product-releases-creator** | Release Strategist | Breaking initiatives into smallest testable releases | Product requirements | Release breakdown with MVP priorities | 45K tokens (12 files) |
| **technical-requirements-creator** | Technical Requirements Analyst | Transforming PRDs into technical specs | Product requirements | Technical specifications with FHIR mappings, API designs | 25K tokens (6 files) |
| **technical-solution-estimator** | Solution Estimator | Estimating development effort | Technical requirements | Hour estimates with risk analysis | 18K tokens (5 files) |
| **technical-project-planner** | Project Planner | Breaking epics into developer tasks | Technical requirements | Epic delivery plan with tasks and dependencies | 12K tokens (5 files) |

**Maturity Indicators:**
- **architecture-designer**: ⭐⭐⭐ Stable (v3.0)
- **product-releases-creator**: ⭐⭐⭐ Stable (v2.0)
- **product-requirements-validator**: ⭐⭐ Beta
- **technical-requirements-creator**: ⭐⭐ Beta
- **technical-solution-estimator**: ⭐⭐ Beta
- **technical-project-planner**: ⭐⭐ Beta

---

## Repository Structure

```
architecture-designer-claude-project/
├── projects/                           # 6 Claude Desktop projects
│   ├── architecture-designer/         # System architecture design (252K tokens)
│   ├── product-releases-creator/      # Initiative decomposition (45K tokens)
│   ├── product-requirements-validator/# PRD validation (15K tokens)
│   ├── technical-requirements-creator/# Technical specifications (25K tokens)
│   ├── technical-solution-estimator/  # Effort estimation (18K tokens)
│   └── technical-project-planner/     # Epic delivery planning (12K tokens)
├── documentation/                      # Product requirements and releases
│   ├── product-requirements.md
│   └── initiative-releases.md
├── README.md                           # This file
├── CLAUDE.md                           # Claude Code configuration
└── .gitignore
```

**Each Project Contains:**
```
projects/<project-name>/
├── project-instructions.md            # Layer 1: Agent personality and principles
└── files/                             # Layer 2 & 3: Workflows and knowledge
    ├── workflow-*.md                  # Conversation flows and phases
    ├── kb-*.md                        # Domain knowledge and patterns
    ├── template-*.md                  # Reusable document templates
    └── guide-*.md                     # Step-by-step tutorials
```

---

## Three-Layer Architecture

Every project follows this proven pattern:

### **Layer 1: Agent Instructions** (`project-instructions.md`)
**WHO the agent is**
- Personality and communication style
- Core principles and philosophy
- Response frameworks
- Domain expertise

### **Layer 2: Workflow Definitions** (`files/workflow-*.md`)
**HOW the agent converses**
- Conversation phases (intake → exploration → delivery)
- Transition logic between phases
- Quality gates and checkpoints
- Example conversations

### **Layer 3: Knowledge Base** (`files/kb-*.md`, `template-*.md`, `guide-*.md`)
**WHAT the agent knows**
- Domain knowledge and patterns
- Decision frameworks
- Real-world examples
- Reusable templates

### How Layers Work Together

```
User Input
    ↓
Layer 1 (project-instructions.md)
    ├─ Agent determines response approach
    ├─ References Layer 2 for conversation flow
    │       ↓
    │   Layer 2 (workflow-*.md)
    │       ├─ Identifies current phase
    │       ├─ Determines next steps
    │       └─ References Layer 3 for content
    │               ↓
    │           Layer 3 (kb-*.md, template-*.md)
    │               ├─ Queries patterns
    │               ├─ Retrieves examples
    │               └─ Returns domain knowledge
    │               ↓
    └─ Synthesizes response following Layer 1 principles
        ↓
Agent Response
```

---

## Installation Instructions

### Prerequisites

- **Claude Desktop** application installed
- **Projects feature** enabled (check Settings → Features)
- **Token limit awareness**: Claude Desktop supports 200K tokens per project, with automatic RAG mode for larger knowledge bases

### Step-by-Step Setup

<details>
<summary><strong>Architecture Designer (Recommended First Project)</strong></summary>

**Time:** 5 minutes | **Files:** 1 instructions + 13 knowledge base files

**Step 1: Create Project**
1. Open Claude Desktop → Click "+" button → "New Project"
2. **Project Name:** `Architecture Designer`
3. **Description:** `Expert system architecture design from requirements to implementation-ready specifications`

**Step 2: Add Custom Instructions**
1. Copy entire contents of `projects/architecture-designer/project-instructions.md`
2. Paste into Custom Instructions field
3. Save

**Step 3: Upload Knowledge Base Files**

Upload all 13 files from `projects/architecture-designer/files/`:

**Core Knowledge (5 files, ~200K tokens):**
- `kb-architecture-patterns.md` (78K tokens) - 12+ architectural patterns
- `kb-technology-selection.md` (38K tokens) - Technology evaluation frameworks
- `kb-anti-patterns.md` (18K tokens) - Common mistakes to avoid
- `kb-scaling-strategies.md` (37K tokens) - Scaling by growth phase
- `kb-adr-library.md` (23K tokens) - Architecture Decision Record examples
- `kb-diagram-examples.md` (20K tokens) - Mermaid diagram best practices

**Workflow & Templates (7 files, ~35K tokens):**
- `workflow-architecture-exploration.md` (15K tokens) - Main conversation workflow
- `guide-ascii-diagrams.md` (5K tokens) - ASCII diagram patterns
- `template-adr.md` (2K tokens) - ADR template
- `template-comparison-table.md` (2K tokens) - Comparison table format
- `template-learning-snippet.md` (5K tokens) - Learning snippet templates
- `template-progressive-questions.md` (3K tokens) - Progressive question patterns
- `template-checkpoint-format.md` (5K tokens) - Review checkpoint templates

**Step 4: Verify Setup**

Test with: *"I need to design an architecture for a SaaS application with 5 developers and a 3-month timeline. Can you help?"*

**Expected Response:**
- Agent introduces itself as Senior Principal Architect
- Asks clarifying questions about team, scale, budget
- References knowledge base patterns

**Success Criteria:**
- Agent responds with architect persona
- Asks for missing requirements (performance, scale, features)
- References architectural patterns from knowledge base

</details>

<details>
<summary><strong>Product Requirements Validator</strong></summary>

**Time:** 3 minutes | **Files:** 1 instructions + 4 knowledge base files

**Step 1: Create Project**
1. Claude Desktop → "+" → "New Project"
2. **Name:** `Requirements Validator`
3. **Description:** `Validate and structure business requirements documents`

**Step 2: Add Custom Instructions**
- Copy `projects/product-requirements-validator/project-instructions.md`
- Paste into Custom Instructions

**Step 3: Upload Knowledge Base (4 files, ~15K tokens)**
- `workflow-requirements-validation.md` - 10-stage validation workflow
- `workflow-state.md` - State tracking patterns
- `workflow-stage-prompts.md` - Stage-specific prompts
- `agent-requirements-analyst.md` - Analysis methodology
- `kb-cmm-product-capabililties.md` - Platform capabilities
- `template-product-requirements.md` - PRD template

**Step 4: Verify**

Test: *"Analyze this BRD: [paste requirements]"*

**Expected:** Agent starts Stage 1 with document intake review

</details>

<details>
<summary><strong>🔄 Product Releases Creator</strong></summary>

**Time:** 4 minutes | **Files:** 1 instructions + 12 knowledge base files

**Step 1: Create Project**
1. Name: `Releases Creator`
2. Description: `Break initiatives into smallest testable releases`

**Step 2: Add Custom Instructions**
- Copy `projects/product-releases-creator/project-instructions.md`

**Step 3: Upload Knowledge Base (12 files, ~45K tokens)**

**Workflow Files:**
- `workflow-release-decomposition.md` - Main decomposition workflow
- `workflow-state.md` - State tracking
- `workflow-stage-prompts.md` - Stage prompts

**Knowledge Base:**
- `kb-user-type-standards.md` - User type definitions
- `kb-healthcare-glossary.md` - Healthcare terminology
- `kb-best-practices.md` - Release decomposition best practices

**Templates:**
- `template-releases-complete.md` - Final output format
- `template-release-review.md` - Review template
- `template-option-comparison.md` - Alternative comparison
- `template-release-diagrams.md` - Diagram formats
- `template-report-card.md` - Maturity scoring

**Agents:**
- `agent-decomposition.md` - Decomposition methodology
- `agent-option-explorer.md` - Alternative exploration
- `agent-validation.md` - Validation rules

**Step 4: Verify**

Test: *"Please decompose these requirements: [paste PRD]"*

**Expected:** Agent starts release decomposition workflow

</details>

<details>
<summary><strong>⚙️ Technical Requirements Creator</strong></summary>

**Time:** 3 minutes | **Files:** 1 instructions + 6 knowledge base files

**Step 1:** Create project `Technical Requirements`

**Step 2:** Copy `projects/technical-requirements-creator/project-instructions.md`

**Step 3:** Upload 6 files (~25K tokens):
- `workflow-requirements-analysis.md` - 8-step analysis workflow
- `workflow-state.md`, `workflow-stage-prompts.md`
- `template-technical-requirements.md` - Technical spec template
- `template-workflow-specification.md` - Workflow specification format
- `kb-cmm-product-capabililties.md` - Platform capabilities
- `kb-fhir-resources.md` - FHIR resource mappings
- `guide-fhir-resource-mapping.md` - FHIR mapping guide

**Step 4:** Test: *"Create technical requirements from this PRD: [paste]"*

</details>

<details>
<summary><strong>Technical Solution Estimator</strong></summary>

**Time:** 3 minutes | **Files:** 1 instructions + 5 knowledge base files

**Step 1:** Create project `Solution Estimator`

**Step 2:** Copy `projects/technical-solution-estimator/project-instructions.md`

**Step 3:** Upload 5 files (~18K tokens):
- `workflow-estimation-analysis.md` - Estimation methodology
- `workflow-state.md`, `workflow-stage-prompts.md`
- `template-technical-estimates.md` - Estimate output format
- `template-component-estimate.md` - Component-level estimates
- `kb-cmm-product-capabililties.md` - Platform capabilities
- `guide-platform-capabilities.md` - Platform capability guide

**Step 4:** Test: *"Estimate effort for: [paste technical requirements]"*

</details>

<details>
<summary><strong>📅 Technical Project Planner</strong></summary>

**Time:** 3 minutes | **Files:** 1 instructions + 5 knowledge base files

**Step 1:** Create project `Project Planner`

**Step 2:** Copy `projects/technical-project-planner/project-instructions.md`

**Step 3:** Upload 5 files (~12K tokens):
- `workflow-epic-decomposition.md` - Epic breakdown workflow
- `workflow-state.md`, `workflow-stage-prompts.md`
- `template-epic-delivery.md` - Epic delivery format
- `template-epic-summary.md` - Epic summary template
- `kb-healthcare-glossary.md` - Healthcare terminology
- `guide-diagram-simplification.md` - Diagram simplification guide

**Step 4:** Test: *"Plan epic delivery for: [paste technical requirements]"*

</details>

---

## Usage Examples

### Example 1: Architecture Designer

**Input:**
```
I need to design an architecture for a SaaS project management tool:
- 10K users at launch, 100K users in 1 year
- Team: 8 developers (5 backend, 3 frontend, all know TypeScript)
- Budget: $500/month initially
- Timeline: 3 months to MVP
- Features: Projects, tasks, real-time collaboration, file uploads
- Must support custom fields per workspace
```

**Output:**
1. **Requirements Analysis** - Gap identification (missing performance targets, security requirements)
2. **Architecture Exploration** - 2-3 approaches:
   - Approach A: Modular Monolith (Next.js + PostgreSQL)
   - Approach B: Microservices (Express services + Postgres + Redis)
   - Approach C: Serverless (AWS Lambda + DynamoDB)
3. **Tradeoff Analysis** - Honest pros/cons for each
4. **Recommendation** - Contextual recommendation based on team size/expertise
5. **Detailed Design** - Component specs, data architecture, deployment plan
6. **ADRs** - 3-5 Architecture Decision Records documenting major choices

**Time:** 2-3 hours for complete architecture documentation

### Example 2: Product Releases Creator

**Input:** Product requirements document for new feature

**Output:**
- **Release Breakdown** - 4-5 releases prioritized by learning value
- **Dependency Map** - Visual diagram showing release dependencies
- **Decision Gates** - Validation checkpoints between releases
- **Risk Analysis** - What could go wrong and how to mitigate
- **Scope Boundaries** - Clear MVP vs future capabilities

**Time:** 1-2 hours for complete release plan

### Example 3: Workflow Progression

**Complete Product Development Workflow:**

```
1. Requirements Validator
   ↓ (Structured PRD)
2. Releases Creator
   ↓ (Release breakdown)
3. Technical Requirements Creator
   ↓ (Technical specs)
4. Architecture Designer
   ↓ (System architecture)
5. Solution Estimator
   ↓ (Effort estimates)
6. Project Planner
   ↓ (Epic delivery plan)
```

---

## File Naming Conventions

All knowledge base files follow standardized prefixes:

| Prefix | Purpose | Examples |
|--------|---------|----------|
| `workflow-*.md` | **Layer 2** - Conversation flows, phases, transitions | `workflow-architecture-exploration.md` |
| `kb-*.md` | **Layer 3** - Domain knowledge, patterns, frameworks | `kb-architecture-patterns.md`, `kb-anti-patterns.md` |
| `template-*.md` | **Layer 3** - Reusable document formats | `template-adr.md`, `template-comparison-table.md` |
| `guide-*.md` | **Layer 3** - Step-by-step tutorials | `guide-ascii-diagrams.md` |
| `agent-*.md` | **Specialized** - Sub-agent methodologies | `agent-requirements-analyst.md` |

**Naming Rules:**
- Use kebab-case: `workflow-architecture-exploration.md`
- Descriptive names: `kb-scaling-strategies.md` not `kb-scale.md`
- No version numbers in filename (use git for versioning)

---

## Token Limits & Claude Desktop

### Understanding Token Limits

Claude Desktop projects have token limitations:

- **Standard Mode**: ~200K tokens across all knowledge base files
- **RAG Mode**: Automatically activates for larger knowledge bases (200K+ tokens)
  - RAG mode retrieves relevant sections dynamically
  - Slightly slower but supports unlimited knowledge base size

### Token Counts by Project

| Project | Total Tokens | Mode | Notes |
|---------|-------------|------|-------|
| architecture-designer | 252K | RAG | Largest project, comprehensive patterns |
| product-releases-creator | 45K | Standard | Fits in standard mode |
| product-requirements-validator | 15K | Standard | Lightweight |
| technical-requirements-creator | 25K | Standard | FHIR resources add bulk |
| technical-solution-estimator | 18K | Standard | Platform-specific |
| technical-project-planner | 12K | Standard | Smallest project |

### Optimizing Token Usage

**If you hit token limits:**
1. **Remove examples** - Keep templates, remove example conversations
2. **Consolidate files** - Merge related KB files
3. **Trim descriptions** - Keep essential information only
4. **Split projects** - Create multiple focused projects instead of one large one

**Check token count:**
```bash
# Approximate tokens (1 token ≈ 0.75 words)
wc -w projects/architecture-designer/files/*.md
```

---

## FAQ

<details>
<summary><strong>Which project should I start with?</strong></summary>

**For engineers:** Start with `architecture-designer` - most mature and immediately useful

**For product managers:** Start with `product-requirements-validator` - helps structure requirements before development

**For project managers:** Start with `product-releases-creator` - breaks initiatives into deliverable releases
</details>

<details>
<summary><strong>Can I customize projects for my company?</strong></summary>

**Yes!** Add company-specific knowledge base files:
- `kb-company-tech-standards.md` - Approved technologies
- `kb-internal-patterns.md` - Internal architecture patterns
- `kb-compliance-requirements.md` - Company compliance needs
- `kb-past-decisions.md` - Historical ADRs and lessons learned

Just add files to `projects/<project-name>/files/` and reference in custom instructions.
</details>

<details>
<summary><strong>How often should I update knowledge bases?</strong></summary>

**Quarterly recommended:**
- Update technology versions and costs
- Add new patterns discovered
- Include recent anti-pattern examples
- Refresh real-world case studies

**Track updates in** `CHANGELOG.md` (create if needed)
</details>

<details>
<summary><strong>Can I use multiple projects together?</strong></summary>

**Yes!** Common workflows:
1. **Requirements → Architecture:** Validate requirements first, then design architecture
2. **Requirements → Releases → Technical Specs:** Full product development pipeline
3. **Architecture → Estimation → Planning:** Design → estimate → plan sequence

**Note:** Each project is separate conversation - copy outputs between projects as needed
</details>

<details>
<summary><strong>What if agent doesn't follow instructions?</strong></summary>

**Common fixes:**
1. **Re-paste custom instructions** - May not have saved properly
2. **Provide more context** - Agent needs detailed requirements (team size, timeline, constraints)
3. **Explicitly reference workflow** - Say "Follow the architecture exploration workflow"
4. **Check knowledge base upload** - Verify all files uploaded successfully

**Still not working?** See [Troubleshooting](#troubleshooting) section
</details>

<details>
<summary><strong>Can I share these projects with my team?</strong></summary>

**Yes! Two options:**

**Option 1: Share repository access**
- Team members clone repository
- Each sets up their own Claude Desktop projects
- Everyone gets identical agents

**Option 2: Export/import (future)**
- Claude Desktop doesn't currently support project export
- For now, share the repository link and setup instructions
</details>

<details>
<summary><strong>Will these work with Copilot, Windsurf, or Claude Code?</strong></summary>

**Currently:** Optimized for Claude Desktop only

**Future:** We plan to support other AI chat clients
- **Copilot:** Needs custom instructions format adaptation
- **Windsurf:** Needs project structure adaptation
- **Claude Code:** Can use knowledge base files directly, but workflow needs adaptation

**See:** `documentation/migration-guide.md` (coming soon)
</details>

<details>
<summary><strong>How do I know if a project is working correctly?</strong></summary>

**Validation checklist per project in:** [Success Metrics](#success-metrics) section

**Quick test:**
1. Agent responds with correct persona (check first response)
2. Agent asks clarifying questions (not generic answers)
3. Agent references knowledge base (cites patterns, examples)
4. Output matches expected format (ADRs, diagrams, structured docs)
</details>

---

## Troubleshooting

### Agent Not Following Instructions

**Problem:** Agent doesn't use correct persona or workflow

**Solutions:**
1. **Verify custom instructions saved:**
   - Check project settings
   - Re-paste `project-instructions.md` if needed

2. **Explicitly trigger workflow:**
   - Say: "Follow the architecture exploration workflow"
   - Say: "Start Phase 1 of the requirements validation workflow"

3. **Check knowledge base files:**
   - Verify all files uploaded successfully
   - Look for file size warnings (>10MB files may fail)

### Responses Too Generic

**Problem:** Getting generic advice, not specific to your context

**Solutions:**
1. **Provide complete requirements:**
   ```
   Good: "Team of 5 JS developers, $500/month budget, 3-month timeline"
   Bad: "Design an app"
   ```

2. **State constraints explicitly:**
   - Team size and expertise
   - Budget limits
   - Timeline pressure
   - Performance requirements

3. **Reference specific needs:**
   - "We need HIPAA compliance"
   - "Team has never used Kubernetes"
   - "Must integrate with Salesforce"

### Missing Diagrams

**Problem:** No Mermaid diagrams in output

**Solutions:**
1. **Explicitly request:** "Can you create a component architecture diagram?"
2. **Check project:** Architecture Designer includes diagram examples, others may not
3. **Verify Mermaid rendering:** Some Claude Desktop versions have rendering issues

### Knowledge Base Not Referenced

**Problem:** Agent doesn't cite patterns or examples from KB

**Solutions:**
1. **Verify files uploaded:** Check project settings → Knowledge
2. **Check token limits:** If >200K tokens, may need RAG mode (automatic)
3. **Explicitly request:** "What architectural patterns from the knowledge base fit this?"

### Too Much Detail / Too Little Detail

**Problem:** Overwhelming output or too shallow

**Solutions:**
1. **Request specific depth:**
   - "Give me a high-level summary first"
   - "Can you expand on the database design?"

2. **Use progressive disclosure:**
   - Review summary first
   - Request deep dives on specific sections

### Agent Recommends Over-Engineering

**Problem:** Suggests Kubernetes for 3-person team

**Solutions:**
1. **Verify team size in input:** Agent should scale recommendations to team
2. **Remind of constraints:** "We only have 3 developers - is this realistic?"
3. **Check persona:** Architecture Designer should push back on over-engineering

### File Upload Failures

**Problem:** Knowledge base files won't upload

**Solutions:**
1. **Check file size:** Individual files >10MB may fail
2. **Check format:** Must be `.md` files
3. **Check total size:** If total >50MB, split into smaller files
4. **Try uploading one at a time:** Identifies problematic files

---

## Success Metrics

### How to Know Projects Are Working

#### Architecture Designer

**Working Correctly:**
- Agent introduces as "Senior Principal Architect with 25+ years experience"
- Asks clarifying questions about team, scale, budget, timeline
- Proposes 2-3 distinct architectural approaches
- Provides honest tradeoffs (not just pros)
- Creates Mermaid diagrams for system context and components
- References patterns from knowledge base (monolith, microservices, event-driven)
- Makes contextual recommendations based on YOUR constraints

**Not Working:**
- Generic "you should use microservices" without context
- No diagrams
- Doesn't ask about team size or expertise
- Recommends technologies without rationale
- No references to knowledge base patterns

**Validation Test:**
```
Input: "Design architecture for 3-person team, 6-week timeline, basic CRUD app"
Expected: Agent recommends simple monolith (Next.js or Rails), not microservices
```

#### Product Requirements Validator

**Working Correctly:**
- Starts "Stage 1 of 10" workflow
- Presents ONE stage at a time
- Asks: "Is this accurate? Any changes?" after each stage
- Uses "Not specified" for missing info (doesn't assume)
- Final PRD has all required sections

**Not Working:**
- Presents all 10 stages at once
- Assumes missing information
- Skips approval gates
- Doesn't follow stage sequence

#### Product Releases Creator

**Working Correctly:**
- Breaks initiative into 4-6 small releases
- Each release has user-facing capability
- Includes dependency diagram
- MVP prioritized by learning value
- Includes validation gates

**Not Working:**
- Creates releases by technical layer (backend → frontend)
- Releases too large (>2 weeks)
- No clear user value per release

#### Technical Requirements Creator

**Working Correctly:**
- Maps FHIR resources for healthcare entities
- Extracts ALL workflows (no consolidation)
- Includes BPM workflow orchestration
- Tags recommendations: [Recommended], [Inferred], [Derived]
- Marks non-applicable sections

**Not Working:**
- Generic technical specs
- No FHIR resource mappings
- Missing workflows
- No BPM orchestration

#### Technical Solution Estimator

**Working Correctly:**
- Provides hour estimates per component
- Includes risk factors
- References existing platform capabilities
- Gives confidence levels (high/medium/low)

**Not Working:**
- Single total estimate without breakdown
- No risk analysis
- Doesn't leverage platform capabilities

#### Technical Project Planner

**Working Correctly:**
- Breaks epic into developer-ready tasks
- Includes dependencies and sequence
- Task sizes: 4-16 hours each
- Clear acceptance criteria

**Not Working:**
- Tasks too large (>2 days)
- Missing dependencies
- No acceptance criteria

---

## Customization & Extension

### Adding Company-Specific Knowledge

**Step 1:** Create custom knowledge base file

```markdown
# kb-company-standards.md

## Approved Technologies

### Backend
- **Languages:** TypeScript (preferred), Python (data science only)
- **Frameworks:** Express.js, Nest.js
- **Databases:** PostgreSQL (primary), Redis (caching)

### Cloud
- **Provider:** Azure (mandatory)
- **Services:** App Service, Functions, PostgreSQL, Service Bus

## Internal Patterns

### Authentication
All services must use Azure AD B2C...

### Logging
All services must use Azure Application Insights...

## Compliance
- HIPAA required for all PHI
- SOC 2 Type II certification
- Data residency: US only
```

**Step 2:** Upload to project knowledge base

**Step 3:** Reference in custom instructions

```markdown
## Company Context

Reference `kb-company-standards.md` for approved technologies and internal patterns.

When recommending technologies:
1. Check company standards first
2. Only recommend approved options
3. Justify exceptions with strong rationale
```

### Creating New Templates

**Example:** Custom ADR template for your company

```markdown
# template-company-adr.md

# ADR-XXX: [Decision Title]

**Date:** YYYY-MM-DD
**Status:** [Proposed | Accepted | Deprecated | Superseded]
**Deciders:** [List team members]
**Company Standard Compliance:** [Yes/No/Partial]

## Context
[What prompted this decision? Include business context.]

## Decision
[What are we doing?]

## Rationale
[Why this decision? Reference company standards.]

## Alternatives Considered
[What else did we evaluate? Why rejected?]

## Consequences
**Positive:**
- [Benefit 1]

**Negative:**
- [Tradeoff 1]

**Company Standards Impact:**
- [How this affects existing standards]

## Implementation Notes
[How to implement this decision]

## Review Date
[When should we revisit this?]
```

### Extending Workflows

**Example:** Add company approval gate to architecture workflow

Edit `workflow-architecture-exploration.md`:

```markdown
## Phase 3.5: Architecture Review Board Approval (NEW)

**Trigger:** After user selects architectural approach

**Agent Actions:**
1. Generate Architecture Review Board (ARB) submission package:
   - Executive summary (1 page)
   - Architecture diagrams
   - Cost analysis
   - Risk assessment
   - Compliance checklist

2. Provide ARB presentation template

3. Include common ARB questions and answers

**User Actions:**
- Present to ARB
- Return with approval or requested changes

**Transition:** After ARB approval → Phase 4 (Detailed Design)
```

---

## Additional Resources

### Learning Materials

**Understanding Three-Layer Architecture:**
- See `projects/README.md` for detailed explanation
- Each project's `project-instructions.md` shows practical implementation

**Example Conversations:**
- **[EXAMPLES.md](EXAMPLES.md)** - 6 detailed example conversations showing each project in action
- Real inputs, full agent responses, complete workflows
- Learn by seeing projects work end-to-end

**Healthcare Domain Knowledge:**
- `kb-fhir-resources.md` - FHIR resource mappings
- `kb-healthcare-glossary.md` - Healthcare terminology
- `kb-cmm-product-capabililties.md` - CMM platform capabilities

**Architecture Patterns:**
- `kb-architecture-patterns.md` - 12+ patterns with examples
- `kb-anti-patterns.md` - Common mistakes to avoid
- `kb-scaling-strategies.md` - Scaling by growth phase

**Customization Templates:**
- **[TEMPLATES.md](TEMPLATES.md)** - Ready-to-use templates for extending projects
- Company technology standards template
- Internal architecture patterns template
- Compliance requirements template

### Related Tools

**CMM Internal:**
- **JIRA:** Create epics/stories from Technical Project Planner output
- **Confluence:** Store architecture documentation and ADRs
- **Azure DevOps:** Import technical requirements

**External:**
- **Mermaid Live Editor:** Test diagrams (https://mermaid.live)
- **ADR Tools:** GitHub ADR tools (https://adr.github.io)
- **FHIR Validator:** Validate FHIR resource mappings

### Product Development Resources

**Inside Repository:**
- `documentation/product-requirements.md` - Full PRD for this repository
- `documentation/initiative-releases.md` - Release planning for this repository

**External References:**
- **Marty Cagan:** "Inspired" and "Empowered" (product discovery framework)
- **Martin Fowler:** Architecture patterns (martinfowler.com/architecture)
- **FHIR Documentation:** hl7.org/fhir

**Migration Guide:**
- **[MIGRATION-GUIDE.md](MIGRATION-GUIDE.md)** - Using these projects with other AI chat clients
- Claude Code adaptation guide (planned Q1 2026)
- GitHub Copilot support (planned Q2 2026)
- Windsurf integration (planned Q2 2026)

---

## Contributing

### How to Improve Projects

**Adding New Content:**
1. Create feature branch: `git checkout -b feature/new-content`
2. Add knowledge base files to `projects/<project-name>/files/`
3. Update `project-instructions.md` to reference new files
4. Test in Claude Desktop
5. Create PR with description of changes

**Reporting Issues:**
1. Test issue in fresh Claude Desktop instance
2. Include:
   - Which project
   - Input provided
   - Expected vs actual output
   - Screenshots if relevant
3. Create GitHub issue with "Bug" label

**Suggesting Improvements:**
1. Create GitHub issue with "Enhancement" label
2. Describe:
   - Which project
   - What improvement
   - Why it would help
   - Example use case

### Internal CMM Guidelines

**Before Contributing:**
- Ensure changes don't expose internal CMM systems/data
- Test with sample data, not production data
- Follow existing file naming conventions
- Update README if adding new projects

**Review Process:**
1. Create PR with detailed description
2. Request review from project maintainer
3. Address feedback
4. Merge after approval

---

## Changelog

### Version 1.0 (November 2025)

**Projects:**
- Architecture Designer (v3.0) - 252K tokens, 13 files
- Product Releases Creator (v2.0) - 45K tokens, 12 files
- Product Requirements Validator (Beta) - 15K tokens, 4 files
- Technical Requirements Creator (Beta) - 25K tokens, 6 files
- Technical Solution Estimator (Beta) - 18K tokens, 5 files
- Technical Project Planner (Beta) - 12K tokens, 5 files

**Documentation:**
- Comprehensive README with installation instructions
- File naming conventions documented
- Token limit guidance added
- Troubleshooting section created
- FAQ section added
- Success metrics defined per project

**Repository:**
- Three-layer architecture pattern established
- Standardized file naming across all projects
- Product requirements and release documentation
- Git configuration for Claude Code

---

## Support

### Getting Help

**Questions?** Ask in:
- **Slack:** #architecture-designer (CMM internal)
- **Email:** [Your team email]

**Found a Bug?**
1. Check [Troubleshooting](#troubleshooting) first
2. Create GitHub issue with reproduction steps

**Feature Requests?**
- Create GitHub issue with "Enhancement" label
- Describe use case and expected benefit

### Maintenance

**Repository Maintainers:**
- [Your name/team]

**Update Schedule:**
- **Quarterly:** Knowledge base content refresh
- **Monthly:** Bug fixes and small improvements
- **As needed:** New projects or major features

---

## Advanced Topics

### Performance Optimization

**For Large Knowledge Bases (>200K tokens):**
1. **Enable RAG mode** (automatic) - Claude retrieves relevant sections dynamically
2. **Consolidate files** - Merge related content to reduce file count
3. **Use references** - Link between files instead of duplicating content
4. **Prioritize content** - Put most-used content in smaller files for faster access

**Token Reduction Strategies:**
1. Remove verbose examples (keep templates, remove walkthroughs)
2. Use tables instead of prose
3. Link to external docs instead of embedding
4. Split large files by topic

### Multi-Project Workflows

**Product Development Pipeline:**

```mermaid
graph LR
    A[BRD] --> B[Requirements Validator]
    B --> C[Releases Creator]
    C --> D[Technical Requirements]
    D --> E[Architecture Designer]
    E --> F[Solution Estimator]
    F --> G[Project Planner]
    G --> H[Implementation]
```

**How to Chain Projects:**
1. Export output from Project 1
2. Import as input to Project 2
3. Maintain context by copying key decisions
4. Reference previous outputs in prompts

**Example:**
```
Architecture Designer output →
Solution Estimator input:
"Estimate this architecture: [paste component specs]"
```

### Creating New Projects

**Step 1: Define Scope**
- What specific problem does this solve?
- What inputs/outputs?
- Who uses this? (PM, engineer, architect)

**Step 2: Design Three Layers**
- **Layer 1:** Agent personality and principles (project-instructions.md)
- **Layer 2:** Conversation workflow (workflow-*.md)
- **Layer 3:** Domain knowledge (kb-*.md, template-*.md)

**Step 3: Create Knowledge Base**
- Start with templates (10-20K tokens)
- Add patterns and examples (20-50K tokens)
- Include real-world case studies (20-30K tokens)

**Step 4: Test and Iterate**
- Test with 3-5 real scenarios
- Refine based on output quality
- Add missing knowledge iteratively

**Step 5: Document**
- Add to project comparison table
- Write installation instructions
- Define success metrics
- Create example conversations

**See:** `projects/README.md` for detailed project creation guide

---

## Quick Reference

### Command Cheat Sheet

**Architecture Designer:**
- "Design architecture for [requirements]"
- "Review this architecture: [paste]"
- "What if we need HIPAA compliance?"
- "Compare PostgreSQL vs MongoDB for [use case]"
- "Create ADR for [decision]"

**Requirements Validator:**
- "Analyze this BRD: [paste]"
- "Stage X complete, proceed"
- "Mark [section] as not specified"

**Releases Creator:**
- "Decompose these requirements: [paste]"
- "Generate alternative approaches"
- "I select approach 2"

**Technical Requirements:**
- "Create technical requirements from PRD: [paste]"
- "List all workflows"
- "Show FHIR resource mappings"

**Solution Estimator:**
- "Estimate effort for: [paste technical requirements]"
- "Add risk analysis"
- "Break down by component"

**Project Planner:**
- "Plan epic delivery for: [paste]"
- "Add task dependencies"
- "Include acceptance criteria"

### Token Estimate Calculator

**Quick calculation:**
```
Words × 0.75 = Approximate tokens
```

**Example:**
- 10,000 words ≈ 7,500 tokens
- 50,000 words ≈ 37,500 tokens

**Check actual tokens:**
```bash
# Count words
wc -w projects/architecture-designer/files/*.md

# Multiply by 0.75 for token estimate
```

### Project Selection Matrix

| If You Need... | Use This | Alternative |
|----------------|----------|-------------|
| System architecture | Architecture Designer | - |
| Validate requirements | Requirements Validator | Manual review |
| Break into releases | Releases Creator | Manual planning |
| Technical specs | Technical Requirements | Template only |
| Effort estimates | Solution Estimator | Expert judgment |
| Task breakdown | Project Planner | Manual planning |

---

**Ready to get started? [Jump to Installation Instructions](#installation-instructions)**

**Questions? [Check the FAQ](#faq) or [Troubleshooting](#troubleshooting) section**

**Want to contribute? [See Contributing](#contributing) section**

---

*Last Updated: November 2025 | Version 1.0 | Maintained by CMM Team*
