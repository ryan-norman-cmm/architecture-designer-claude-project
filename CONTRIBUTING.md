# Contributing to Claude Desktop Project Templates

Thank you for considering contributing to this project! This document provides guidelines for contributing to CMM's Claude Desktop project templates.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Project Structure](#project-structure)
- [Development Guidelines](#development-guidelines)
- [Testing Guidelines](#testing-guidelines)
- [Submission Guidelines](#submission-guidelines)
- [Review Process](#review-process)

---

## Code of Conduct

### Our Standards

- **Be respectful** - Value diverse perspectives and experiences
- **Be constructive** - Provide helpful feedback and suggestions
- **Be collaborative** - Work together toward better solutions
- **Be professional** - Maintain CMM standards of conduct

### Unacceptable Behavior

- Harassment or discriminatory language
- Trolling, insulting, or derogatory comments
- Publishing private information without permission
- Other conduct inappropriate for a professional setting

---

## Getting Started

### Prerequisites

Before contributing, ensure you have:

1. **Claude Desktop** installed with Projects feature enabled
2. **Git** configured for CMM repositories
3. **Access** to this repository (internal CMM team members only)
4. **Understanding** of the three-layer architecture pattern (see README.md)

### Initial Setup

```bash
# Clone repository
git clone [repository-url]
cd architecture-designer-claude-project

# Create feature branch
git checkout -b feature/your-feature-name

# Test existing projects
# (Follow installation instructions in README.md)
```

---

## How to Contribute

### Types of Contributions

We welcome several types of contributions:

#### 1. **Bug Fixes**
- Agent not following instructions
- Incorrect knowledge base references
- Broken file links
- Typos or formatting issues

#### 2. **Knowledge Base Enhancements**
- New architectural patterns
- Additional anti-pattern case studies
- Updated technology recommendations
- More real-world examples
- Healthcare domain knowledge

#### 3. **New Templates**
- Additional ADR templates
- New document formats
- Response templates
- Comparison table formats

#### 4. **Workflow Improvements**
- Additional conversation phases
- Better transition logic
- Enhanced quality gates
- Improved example conversations

#### 5. **New Projects**
- Entirely new Claude Desktop project templates
- Must follow three-layer architecture
- Must solve specific product development pain point

#### 6. **Documentation Improvements**
- Clearer setup instructions
- More troubleshooting tips
- Additional FAQ entries
- Better example conversations

---

## Project Structure

### Repository Layout

```
architecture-designer-claude-project/
├── projects/                    # Claude Desktop projects
│   ├── <project-name>/
│   │   ├── project-instructions.md    # Layer 1: Agent instructions
│   │   └── files/                     # Layer 2 & 3: Workflows and knowledge
│   │       ├── workflow-*.md          # Conversation flows
│   │       ├── kb-*.md                # Domain knowledge
│   │       ├── template-*.md          # Reusable templates
│   │       └── guide-*.md             # Step-by-step tutorials
├── documentation/               # Product requirements and releases
├── README.md                    # Main documentation
├── CHANGELOG.md                 # Version history
├── CONTRIBUTING.md              # This file
└── CLAUDE.md                    # Claude Code configuration
```

### File Naming Conventions

**MUST follow these conventions:**

| Prefix | Purpose | Example |
|--------|---------|---------|
| `workflow-*.md` | Layer 2 - Conversation flows | `workflow-architecture-exploration.md` |
| `kb-*.md` | Layer 3 - Domain knowledge | `kb-architecture-patterns.md` |
| `template-*.md` | Layer 3 - Reusable templates | `template-adr.md` |
| `guide-*.md` | Layer 3 - Step-by-step tutorials | `guide-ascii-diagrams.md` |
| `agent-*.md` | Specialized - Sub-agent methods | `agent-requirements-analyst.md` |

**Naming rules:**
- Use kebab-case: `workflow-architecture-exploration.md`
- Be descriptive: `kb-scaling-strategies.md` not `kb-scale.md`
- No version numbers in filenames (use git for versioning)

---

## Development Guidelines

### Adding Knowledge Base Content

**Step 1: Identify the need**
- What gap does this fill?
- Which projects benefit?
- Is this general or CMM-specific knowledge?

**Step 2: Choose file type**
- **New pattern/framework?** → Add to existing `kb-*.md`
- **New domain knowledge?** → Create new `kb-*.md`
- **New template?** → Create `template-*.md`
- **Step-by-step guide?** → Create `guide-*.md`

**Step 3: Write content**

**Format for knowledge base files:**
```markdown
# kb-[topic-name].md

## Overview
[1-2 sentence summary of what this file contains]

## Section 1: [Topic]

### Pattern/Framework Name
**When to use:**
- [Scenario 1]
- [Scenario 2]

**When to avoid:**
- [Anti-scenario 1]

**Example:**
[Real-world example with context]

**Key Considerations:**
- [Consideration 1]
- [Consideration 2]

**Related Patterns:**
- See `kb-other-file.md` for [related topic]
```

**Step 4: Reference in project instructions**

Update `project-instructions.md`:
```markdown
### Knowledge Base Files

| File | Purpose | When to Use |
|------|---------|-------------|
| `kb-new-file.md` | [Description] | [When to reference] |
```

**Step 5: Test**
- Upload to Claude Desktop project
- Test with sample queries
- Verify agent references new content

### Adding New Templates

**Format for templates:**
```markdown
# template-[name].md

## Purpose
[What this template is for]

## When to Use
[Scenarios where this template applies]

## Template Structure

### Section 1: [Name]
[Description of what goes here]

**Example:**
[Filled-out example]

### Section 2: [Name]
[Description]

## Guidelines
- [Guideline 1]
- [Guideline 2]

## Common Mistakes
- [Mistake 1 and how to avoid]
```

### Modifying Workflows

**Before modifying workflows:**
1. Understand current flow (read entire workflow file)
2. Identify specific pain point or improvement
3. Consider backward compatibility
4. Test with multiple scenarios

**Workflow modification checklist:**
- [ ] Phase transitions still make sense
- [ ] Quality gates still enforce standards
- [ ] Example conversations updated
- [ ] Project instructions reference updated
- [ ] Tested with 3+ realistic scenarios

### Creating New Projects

**Use this checklist:**

#### Planning Phase
- [ ] Problem statement: What specific pain point does this solve?
- [ ] Target users: PMs? Engineers? Architects?
- [ ] Input/output: What goes in, what comes out?
- [ ] Scope: Does this overlap with existing projects?

#### Design Phase
- [ ] Layer 1 designed (agent personality, principles, frameworks)
- [ ] Layer 2 designed (workflow phases, transitions, examples)
- [ ] Layer 3 designed (knowledge base files, templates)
- [ ] File naming follows conventions

#### Implementation Phase
- [ ] `project-instructions.md` created
- [ ] All workflow files created
- [ ] All knowledge base files created
- [ ] All templates created
- [ ] Project tested in Claude Desktop

#### Documentation Phase
- [ ] Added to README project comparison table
- [ ] Installation instructions written
- [ ] Success metrics defined
- [ ] Example conversation created
- [ ] Troubleshooting tips added

---

## Testing Guidelines

### Manual Testing

**For knowledge base changes:**
1. Upload modified files to test Claude Desktop project
2. Test 5+ queries that should trigger new content
3. Verify agent cites new content appropriately
4. Check for hallucinations (agent making up content)

**For workflow changes:**
1. Create new Claude Desktop project with changes
2. Complete full workflow 3+ times with different inputs
3. Verify phase transitions work correctly
4. Confirm quality gates catch issues

**For new projects:**
1. Set up fresh Claude Desktop project
2. Test complete workflow end-to-end 5+ times
3. Test edge cases (missing inputs, unrealistic requirements)
4. Verify success metrics (see README.md)
5. Have 2+ other team members test independently

### Test Scenarios

**Architecture Designer:**
- Small team (3 developers), simple CRUD app
- Medium team (10 developers), SaaS application
- Large team (50+ developers), microservices migration
- Healthcare-specific with HIPAA requirements
- Unrealistic requirements (should push back)

**Requirements Validator:**
- Complete BRD with all sections
- Incomplete BRD with major gaps
- BRD with unclear requirements
- BRD with conflicting requirements

**Releases Creator:**
- Small initiative (2-3 releases expected)
- Large initiative (5-7 releases expected)
- Initiative with complex dependencies
- Initiative with regulatory requirements

### Quality Checklist

Before submitting changes:

**Content Quality:**
- [ ] No spelling or grammar errors
- [ ] Consistent terminology
- [ ] Clear, concise language
- [ ] Real-world examples provided
- [ ] No internal CMM systems exposed (if external release)

**Technical Quality:**
- [ ] All file references resolve
- [ ] Markdown renders correctly
- [ ] Code examples are valid
- [ ] Mermaid diagrams render
- [ ] No broken links

**Agent Quality:**
- [ ] Agent follows intended persona
- [ ] Agent references knowledge base appropriately
- [ ] Agent doesn't hallucinate content
- [ ] Agent asks clarifying questions when needed
- [ ] Output matches expected format

---

## Submission Guidelines

### Before You Submit

1. **Test thoroughly** (see Testing Guidelines)
2. **Update documentation**
   - README.md if adding new project
   - CHANGELOG.md with your changes
   - Project-specific docs if modified
3. **Follow conventions**
   - File naming
   - Markdown formatting
   - Git commit messages

### Git Workflow

**Branch naming:**
```
feature/add-scaling-patterns           # New feature
fix/architecture-designer-references   # Bug fix
docs/improve-setup-instructions        # Documentation
refactor/consolidate-kb-files          # Refactoring
```

**Commit messages:**
```
feat: add scaling patterns to architecture knowledge base

- Add 5 new scaling patterns for 100K-1M users
- Include real-world case studies (Shopify, Netflix)
- Update kb-scaling-strategies.md with cost estimates

Closes #42
```

**Format:**
```
<type>: <subject>

<body>

<footer>
```

**Types:**
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation only
- `refactor` - Code refactoring
- `test` - Testing improvements
- `chore` - Maintenance tasks

### Creating Pull Requests

**PR Title:**
```
feat: Add healthcare FHIR resource mappings to technical requirements
```

**PR Description Template:**
```markdown
## Description
[Clear description of what this PR does]

## Problem
[What problem does this solve?]

## Solution
[How does this PR solve it?]

## Testing
[How was this tested?]
- [ ] Tested in Claude Desktop
- [ ] Verified agent references new content
- [ ] Tested 5+ scenarios
- [ ] Reviewed by 2+ team members

## Changes
- [Change 1]
- [Change 2]

## Breaking Changes
[List any breaking changes, or write "None"]

## Screenshots
[If visual changes, include screenshots]

## Checklist
- [ ] Code follows project conventions
- [ ] Documentation updated
- [ ] CHANGELOG.md updated
- [ ] All tests pass
- [ ] No CMM internal systems exposed
```

---

## Review Process

### Review Criteria

**Reviewers will check:**

1. **Correctness**
   - Content is factually accurate
   - Examples are realistic
   - Code samples are valid
   - Agent behavior is appropriate

2. **Completeness**
   - All required files included
   - Documentation updated
   - Tests conducted
   - CHANGELOG updated

3. **Clarity**
   - Easy to understand
   - Well-organized
   - Proper formatting
   - Good examples

4. **Consistency**
   - Follows naming conventions
   - Matches existing style
   - Compatible with other projects
   - Three-layer architecture maintained

5. **Security**
   - No internal systems exposed
   - No production data included
   - No credentials or secrets
   - Privacy considerations addressed

### Review Timeline

- **Initial review:** Within 2 business days
- **Follow-up:** Within 1 business day
- **Final approval:** After all feedback addressed

### Addressing Feedback

**When reviewers request changes:**
1. Read feedback carefully
2. Ask questions if unclear
3. Make requested changes
4. Reply to each comment when addressed
5. Re-request review

**If you disagree:**
- Explain your reasoning
- Provide evidence or examples
- Suggest alternative approach
- Be open to compromise

---

## Style Guide

### Markdown Formatting

**Headers:**
```markdown
# H1 - Document Title
## H2 - Major Section
### H3 - Subsection
#### H4 - Detail Level
```

**Lists:**
```markdown
**Ordered (for sequences):**
1. First step
2. Second step
3. Third step

**Unordered (for items):**
- Item 1
- Item 2
- Item 3
```

**Code blocks:**
````markdown
```javascript
// Use language identifier
const example = "code";
```

```bash
# For shell commands
npm install
```
````

**Tables:**
```markdown
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Value 1  | Value 2  | Value 3  |
```

**Emphasis:**
```markdown
**Bold** for important terms
*Italic* for emphasis
`Code` for filenames, commands, variables
```

### Writing Style

**Be concise:**
- Short sentences (15-20 words)
- Short paragraphs (3-4 sentences)
- Active voice preferred
- Remove unnecessary words

**Be clear:**
- Define technical terms
- Provide examples
- Use consistent terminology
- Avoid ambiguity

**Be helpful:**
- Anticipate questions
- Provide context
- Include rationale
- Link to related content

---

## Getting Help

### Questions?

- **Slack:** #architecture-designer (CMM internal)
- **Email:** [Team email]
- **GitHub Issues:** Create issue with "Question" label

### Resources

- [README.md](README.md) - Main documentation
- [CHANGELOG.md](CHANGELOG.md) - Version history
- [projects/README.md](projects/README.md) - Three-layer architecture guide
- [Claude Desktop Projects Documentation](https://www.anthropic.com/claude/projects)

---

## Recognition

Contributors will be recognized in:
- CHANGELOG.md (with attribution)
- Internal team communications
- Project documentation (for major contributions)

---

**Thank you for contributing!** Your improvements help the entire CMM team build better products faster.

---

*Last Updated: November 17, 2025 | Maintained by CMM Team*
