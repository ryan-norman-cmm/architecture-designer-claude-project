# Claude Desktop Projects

This directory contains Claude Desktop project templates following a **three-layer architecture pattern**. Each project is self-contained and ready to deploy.

## Three-Layer Architecture Pattern

All projects follow this standardized structure:

```
projects/<project-name>/
├── project-instructions.md              # Layer 1: Agent Instructions
│   └── WHO the agent is (personality, philosophy, principles)
└── files/
    ├── workflow-*.md                    # Layer 2: Workflow Definitions
    │   └── HOW the agent converses (phases, patterns, transitions)
    ├── kb-*.md                          # Layer 3: Knowledge Base Files
    │   └── WHAT the agent knows (patterns, frameworks, examples)
    └── template-*.md                    # Reusable templates
        └── Document formats, response templates
```

### How the Layers Work Together

```
User Input
    ↓
Layer 1 (project-instructions.md)
    ├─ Determines agent personality and approach
    ├─ References Layer 2 for conversation flow
    │       ↓
    │   Layer 2 (workflow-*.md)
    │       ├─ Identifies current phase
    │       ├─ Determines next steps
    │       └─ References Layer 3 for content
    │               ↓
    │           Layer 3 (kb-*.md)
    │               ├─ Queries patterns
    │               ├─ Retrieves examples
    │               └─ Returns domain knowledge
    │               ↓
    └─ Synthesizes response following Layer 1 principles
        ↓
Agent Response
```

## Available Projects

### architecture-designer

**Purpose**: Senior Principal Architect agent that transforms product requirements into production-ready system architectures.

**Layer 1: Agent Instructions** (`project-instructions.md`)
- Personality: Senior Principal Architect with 25+ years experience
- Core Principles: Present options not mandates, match reality, boring tech wins, visual communication
- Response Frameworks: Technology evaluation scoring, tradeoff analysis templates
- Domain Activation: Healthcare, Financial, E-Commerce, SaaS

**Layer 2: Workflow** (`files/workflow-architecture-exploration.md` - 926 lines)
- 3-phase conversational workflow
- Phases: Understand Problem → Explore Solutions → Document Decisions
- On-demand approach generation (reduces output by 40%)
- Progressive disclosure with checkpoints

**Layer 3: Knowledge Base** (11 files, 245K+ tokens)
- `kb-architecture-patterns.md` (78K): 12+ patterns with examples
- `kb-technology-selection.md` (38K): Tech evaluation frameworks
- `kb-anti-patterns.md` (18K): Common mistakes to avoid
- `kb-scaling-strategies.md` (37K): Scaling by growth phase
- `kb-adr-library.md` (23K): ADR templates and examples
- `kb-diagram-examples.md` (20K): Mermaid best practices
- `template-comparison-table.md` (2K): Comparison table format
- `template-learning-snippet.md` (5K): Learning snippet templates
- `template-progressive-questions.md` (3K): Progressive question patterns
- `template-checkpoint-format.md` (5K): Review checkpoint templates

**Setup**: Copy `project-instructions.md` into Claude Desktop project settings, upload `files/` to knowledge base

## Adding New Projects

To add a new Claude Desktop project following the three-layer pattern:

### 1. Create Project Structure

```bash
mkdir -p projects/<project-name>/files
cd projects/<project-name>
```

### 2. Write Layer 1: Agent Instructions

Create `project-instructions.md`:
- Define agent personality and communication style
- List core principles the agent always follows
- Create response frameworks and templates
- Reference Layer 2 workflow files
- Reference Layer 3 knowledge base files

### 3. Write Layer 2: Workflow Definitions

Create `files/workflow-<name>.md`:
- Define conversation phases (e.g., intake → exploration → selection)
- Specify conversation patterns for each phase
- Define transition logic between phases
- Provide example conversations
- Include quality gates and validation checkpoints

### 4. Write Layer 3: Knowledge Base Files

Create knowledge base files following the naming conventions (see `FILE-NAMING-CONVENTIONS.md`):

**Core types:**
- `kb-*.md`: Domain knowledge (`kb-patterns.md`, `kb-frameworks.md`, `kb-anti-patterns.md`)
- `template-*.md`: Reusable formats (`template-comparison-table.md`, `template-adr-format.md`)

**Optional types:**
- `guide-*.md`: Step-by-step tutorials
- `example-*.md`: Sample conversations or outputs
- `reference-*.md`: Quick reference sheets
- `decision-*.md`: Decision frameworks
- `checklist-*.md`: Validation checklists

### 5. Update Documentation

- Add project details to this README
- Update root `README.md` if needed
- Test the three-layer interaction with sample conversations

## Shared Resources

All projects can reference:
- **Documentation**: `documentation/` directory (product requirements, releases)
