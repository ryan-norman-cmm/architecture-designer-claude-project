# File Naming Conventions

This document defines the standardized file naming conventions for Claude Desktop projects in this repository.

## Overview

All files within a project's `files/` directory follow a **type-based prefix pattern** to clearly identify file purpose and enable easy filtering.

## Standard Prefixes

### Core File Types

| Prefix | Purpose | Layer | Examples |
|--------|---------|-------|----------|
| `workflow-` | Conversation flows, phases, patterns | Layer 2 | `workflow-architecture-exploration.md` |
| `kb-` | Domain knowledge, patterns, frameworks | Layer 3 | `kb-architecture-patterns.md`, `kb-technology-selection.md` |
| `template-` | Reusable templates, document formats | Layer 3 | `template-comparison-table.md`, `template-checkpoint-format.md` |

### Extended File Types (Optional)

| Prefix | Purpose | Layer | Examples |
|--------|---------|-------|----------|
| `guide-` | Step-by-step guides and tutorials | Layer 3 | `guide-getting-started.md`, `guide-advanced-patterns.md` |
| `example-` | Standalone example conversations or outputs | Layer 3 | `example-architecture-session.md`, `example-design-output.md` |
| `reference-` | Quick reference sheets and cheatsheets | Layer 3 | `reference-decision-criteria.md`, `reference-pattern-quick-lookup.md` |
| `decision-` | Decision frameworks and scoring rubrics | Layer 3 | `decision-technology-scoring.md`, `decision-pattern-selection.md` |
| `checklist-` | Validation checklists and quality gates | Layer 3 | `checklist-architecture-review.md`, `checklist-design-complete.md` |

## Naming Convention Rules

### 1. Format

```
<prefix>-<descriptive-name>.md
```

- **Prefix**: Lowercase, from standard prefixes above
- **Separator**: Single hyphen (`-`)
- **Descriptive name**: Lowercase, hyphens between words
- **Extension**: `.md` (markdown)

### 2. Descriptive Names

**Good:**
- `kb-architecture-patterns.md` (clear scope)
- `workflow-requirements-gathering.md` (specific phase)
- `template-adr-format.md` (clear purpose)

**Bad:**
- `kb-patterns.md` (too vague - patterns of what?)
- `workflow.md` (missing description)
- `template-1.md` (non-descriptive)

### 3. Multi-Word Names

Use hyphens to separate words in descriptive names:
- `kb-scaling-strategies.md` ✅
- `kb-scaling_strategies.md` ❌ (underscore)
- `kb-scalingStrategies.md` ❌ (camelCase)
- `kb-ScalingStrategies.md` ❌ (PascalCase)

### 4. Consistency

Files covering related content should use parallel naming:
- `kb-architecture-patterns.md`
- `kb-anti-patterns.md`
- `kb-scaling-strategies.md`

### 5. Abbreviations

Use common abbreviations sparingly and consistently:
- `kb-` (knowledge base) ✅
- `adr-` (Architecture Decision Record) ✅
- `e2e-` (end-to-end) ✅

## File Organization by Type

### Layer 2: Workflow Files (`workflow-*.md`)

Workflow files define conversation phases and patterns:

```
files/
├── workflow-architecture-exploration.md     # Main workflow
├── workflow-requirements-gathering.md       # Sub-workflow
└── workflow-detailed-design.md              # Sub-workflow
```

**Content structure:**
1. Workflow overview
2. Phase definitions
3. Conversation patterns
4. Transition logic
5. Examples
6. Quality gates

### Layer 3: Knowledge Base Files (`kb-*.md`)

Knowledge base files contain domain expertise:

```
files/
├── kb-architecture-patterns.md        # Pattern catalog
├── kb-technology-selection.md         # Tech evaluation frameworks
├── kb-anti-patterns.md                # Mistakes to avoid
├── kb-scaling-strategies.md           # Growth approaches
├── kb-adr-library.md                  # ADR examples
└── kb-diagram-examples.md             # Visual communication
```

**Content structure:**
1. Overview/purpose
2. Main content (patterns, frameworks, examples)
3. Decision criteria
4. Real-world case studies
5. When to use / avoid

### Layer 3: Template Files (`template-*.md`)

Template files provide reusable formats:

```
files/
├── template-comparison-table.md        # For comparing options
├── template-learning-snippet.md        # For teaching concepts
├── template-progressive-questions.md   # For guided discovery
└── template-checkpoint-format.md       # For review checkpoints
```

**Content structure:**
1. Template purpose
2. When to use
3. Template format (with placeholders)
4. Filled example
5. Customization guidance

## Glob Patterns for Tooling

Use these patterns to filter files by type:

```bash
# All workflow files
ls files/workflow-*.md

# All knowledge base files
ls files/kb-*.md

# All template files
ls files/template-*.md

# All Layer 3 files (KB + templates)
ls files/{kb,template}-*.md

# Count files by type
echo "Workflows: $(ls files/workflow-*.md 2>/dev/null | wc -l)"
echo "Knowledge Base: $(ls files/kb-*.md 2>/dev/null | wc -l)"
echo "Templates: $(ls files/template-*.md 2>/dev/null | wc -l)"
```

## Migration Guide

When adding files to an existing project:

### 1. Determine File Type

Ask:
- Is this a conversation flow? → `workflow-`
- Is this domain knowledge? → `kb-`
- Is this a reusable format? → `template-`
- Is this a guide/tutorial? → `guide-`
- Is this an example output? → `example-`

### 2. Create Descriptive Name

- Be specific about scope
- Use hyphens for multi-word names
- Keep under 40 characters if possible

### 3. Validate Naming

Checklist:
- [ ] Uses standard prefix
- [ ] Descriptive name is clear and specific
- [ ] Uses lowercase with hyphens
- [ ] Ends with `.md`
- [ ] No duplicate names in project

## Examples from Architecture Designer

Current files following this convention:

```
projects/architecture-designer/files/
├── workflow-architecture-exploration.md      (51K)
├── kb-architecture-patterns.md               (78K)
├── kb-technology-selection.md                (38K)
├── kb-anti-patterns.md                       (18K)
├── kb-scaling-strategies.md                  (37K)
├── kb-adr-library.md                         (23K)
├── kb-diagram-examples.md                    (20K)
├── template-comparison-table.md              (2K)
├── template-learning-snippet.md              (5K)
├── template-progressive-questions.md         (3K)
└── template-checkpoint-format.md             (5K)
```

Total: 11 files, 245K+ tokens

## Benefits of This Convention

1. **Self-Documenting**: File purpose clear from name
2. **Tooling-Friendly**: Easy to glob/filter by type
3. **Scalable**: Add new prefixes without restructuring
4. **Consistent**: Same pattern across all projects
5. **Searchable**: Easy to find files by type or topic
6. **Layer-Aligned**: Prefixes map to Layer 2/3 structure

## Anti-Patterns to Avoid

❌ **Generic names**: `notes.md`, `misc.md`, `temp.md`
❌ **No prefix**: `architecture-patterns.md` (should be `kb-architecture-patterns.md`)
❌ **Mixed case**: `KB-Architecture-Patterns.md` (should be lowercase)
❌ **Underscores**: `kb_patterns.md` (should use hyphens)
❌ **Versioning in name**: `kb-patterns-v2.md` (use git for versioning)
❌ **Dates in name**: `kb-patterns-2024.md` (use git history)

## Related Documentation

- `CLAUDE.md` - Overall repository structure
- `projects/README.md` - Project creation guide
- `README.md` - Repository overview
