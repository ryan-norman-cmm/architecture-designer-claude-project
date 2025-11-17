# Migration Guide: From Claude Desktop to Other AI Chat Clients

This guide explains how to adapt Claude Desktop Project Templates for use with other AI chat clients including GitHub Copilot, Windsurf, and Claude Code.

**Status:** 🚧 Future Feature - Not yet implemented
**Last Updated:** November 2025
**Target Completion:** Q1 2026

---

## Table of Contents

1. [Overview](#overview)
2. [Claude Desktop (Current)](#claude-desktop-current)
3. [GitHub Copilot](#github-copilot)
4. [Windsurf](#windsurf)
5. [Claude Code](#claude-code)
6. [Comparison Matrix](#comparison-matrix)
7. [Migration Checklist](#migration-checklist)

---

## Overview

### Current State: Optimized for Claude Desktop

These project templates are currently optimized for **Claude Desktop Projects**, which supports:
- ✅ Custom instructions (system prompts)
- ✅ Knowledge base file uploads (200K+ tokens with RAG)
- ✅ Persistent project context
- ✅ Markdown rendering with Mermaid diagrams
- ✅ Isolated conversations per project

### Future State: Multi-Client Support

We plan to support these additional platforms:

| Client | Status | Priority | Target Date |
|--------|--------|----------|-------------|
| Claude Desktop | ✅ Released | - | Current |
| Claude Code | 🚧 Planned | High | Q1 2026 |
| GitHub Copilot | 🚧 Planned | Medium | Q2 2026 |
| Windsurf | 🚧 Planned | Medium | Q2 2026 |

---

## Claude Desktop (Current)

### How It Works

**Project Structure:**
```
Claude Desktop Project
├── Custom Instructions (project-instructions.md content)
└── Knowledge Base (13-56 files, markdown)
    ├── workflow-*.md
    ├── kb-*.md
    └── template-*.md
```

**Setup Process:**
1. Create new project in Claude Desktop
2. Copy project-instructions.md into Custom Instructions field
3. Upload all knowledge base files
4. Start conversation

**Pros:**
- ✅ Designed for this use case
- ✅ Large knowledge base support (200K+ tokens)
- ✅ Automatic RAG for large files
- ✅ Persistent project context
- ✅ Easy to set up (3-5 minutes)

**Cons:**
- ⚠️ Desktop-only (no web access)
- ⚠️ No code execution
- ⚠️ No file editing capabilities

---

## GitHub Copilot

### Current Limitations

**What Copilot Supports:**
- ✅ Code suggestions in IDE
- ✅ Chat interface (Copilot Chat)
- ✅ Custom instructions (limited)
- ⚠️ Knowledge base (no native support)

**What It Doesn't Support:**
- ❌ Project-level knowledge base files
- ❌ Large context windows for documentation
- ❌ Structured conversation workflows
- ❌ Persistent project memory

### Migration Strategy (Planned)

**Option 1: Workspace Instructions (Recommended)**

```
Project Structure:
your-project/
├── .github/
│   └── copilot-instructions.md     # Custom instructions for this project
├── docs/
│   └── architecture/                # Documentation Copilot can reference
│       ├── patterns.md
│       ├── decisions.md
│       └── workflows.md
└── [source code]
```

**Setup:**
1. Create `.github/copilot-instructions.md` with adapted project-instructions.md
2. Add condensed knowledge base to `docs/architecture/`
3. Copilot reads these files when analyzing code

**Limitations:**
- Knowledge base must be smaller (~50K tokens max)
- Copilot won't proactively reference docs (user must ask)
- No structured workflows

**Option 2: Prompt Engineering**

Convert project instructions to inline prompts:

```
In your code:

// Architecture Designer Agent
// Role: Senior Principal Architect
// Principles: Present options not mandates, match reality, boring tech wins
// When designing architecture:
// 1. Ask about team size, expertise, budget, timeline
// 2. Propose 2-3 distinct approaches
// 3. Provide honest tradeoffs
// 4. Create Mermaid diagrams
// @see docs/architecture/patterns.md for common patterns
```

Then ask Copilot:
```
"Design architecture for this feature following the guidelines above"
```

### Adaptation Checklist

**To adapt for Copilot:**
- [ ] Condense knowledge base to ~50K tokens
- [ ] Move content to `docs/architecture/` directory
- [ ] Create `.github/copilot-instructions.md`
- [ ] Add inline doc references in code comments
- [ ] Test with typical architecture requests
- [ ] Document limitations for users

**Best For:**
- Architecture guidance during code writing
- Quick pattern lookups
- Technology recommendations inline with code
- ADR generation based on code context

**Not Suitable For:**
- Full architecture design sessions (use Claude Desktop)
- Large knowledge base queries
- Structured multi-phase workflows

---

## Windsurf

### Current Limitations

**What Windsurf Supports:**
- ✅ Code editing and execution
- ✅ Multi-file context
- ✅ Terminal integration
- ⚠️ Custom instructions (limited)
- ❌ Project knowledge base (no native support)

### Migration Strategy (Planned)

**Option 1: Workspace Knowledge Files**

```
Project Structure:
your-project/
├── .windsurf/
│   ├── instructions.md              # Agent instructions
│   └── knowledge/                    # Condensed knowledge base
│       ├── patterns.md
│       ├── workflows.md
│       └── templates.md
└── [source code]
```

**Setup:**
1. Create `.windsurf/instructions.md` with adapted instructions
2. Add condensed knowledge to `.windsurf/knowledge/`
3. Configure Windsurf to load these files on project open

**Limitations:**
- Similar to Copilot (limited knowledge base size)
- May need to prompt Windsurf to reference files
- No structured workflows

**Option 2: Command-Based Triggers**

Create Windsurf commands that trigger specific workflows:

```
# .windsurf/commands.json
{
  "architecture-design": {
    "description": "Design system architecture",
    "prompt": "You are a Senior Principal Architect. Follow the workflow in .windsurf/knowledge/workflow-architecture.md to design architecture for this feature."
  },
  "generate-adr": {
    "description": "Generate Architecture Decision Record",
    "prompt": "Generate an ADR following the template in .windsurf/knowledge/template-adr.md"
  }
}
```

Then invoke: `/architecture-design` in Windsurf

### Adaptation Checklist

**To adapt for Windsurf:**
- [ ] Create `.windsurf/` directory structure
- [ ] Adapt instructions for Windsurf format
- [ ] Condense knowledge base
- [ ] Create command-based triggers
- [ ] Test architecture design workflow
- [ ] Document setup process

**Best For:**
- Architecture design with immediate code generation
- ADR creation alongside code
- Component specifications with implementation
- Technology evaluation with proof-of-concept code

**Not Suitable For:**
- Large knowledge base queries
- Document-heavy workflows (PRD validation, release planning)

---

## Claude Code

### Current Capabilities

**What Claude Code Supports:**
- ✅ Code reading and editing
- ✅ Terminal execution
- ✅ File navigation
- ✅ Project-wide context
- ✅ Custom instructions (CLAUDE.md)
- ⚠️ Knowledge base (can read markdown files)

### Migration Strategy (Planned)

**Option 1: CLAUDE.md + Documentation Files (Recommended)**

```
Project Structure:
your-project/
├── CLAUDE.md                         # Custom instructions
├── docs/
│   └── architecture/                 # Knowledge base as documentation
│       ├── patterns/
│       │   ├── index.md
│       │   ├── monolith.md
│       │   ├── microservices.md
│       │   └── event-driven.md
│       ├── workflows/
│       │   └── architecture-exploration.md
│       └── templates/
│           ├── adr-template.md
│           └── comparison-table.md
└── [source code]
```

**Setup:**
1. Copy `project-instructions.md` to `CLAUDE.md` in project root
2. Place knowledge base files in `docs/architecture/`
3. Update CLAUDE.md to reference documentation paths
4. Claude Code can read these files on demand

**Advantages:**
- ✅ Knowledge base lives in version control
- ✅ Team can update patterns as markdown files
- ✅ Claude Code can navigate and read on demand
- ✅ Documentation useful for human developers too

**Limitations:**
- Claude Code doesn't pre-load all files (must request them)
- Need to prompt Claude to read specific documentation
- Workflow phases less structured than Claude Desktop

**Option 2: Inline Workflow Prompts**

For specific tasks, prompt Claude Code:

```
"Read docs/architecture/workflows/architecture-exploration.md and follow the
4-phase workflow to design architecture for the user authentication feature.
Reference patterns from docs/architecture/patterns/ as needed."
```

**Option 3: Custom Tools (Advanced)**

Create MCP server for architecture design:

```typescript
// mcp-server-architecture/index.ts
import { McpServer } from "@modelcontextprotocol/sdk";

const server = new McpServer({
  name: "architecture-designer",
  version: "1.0.0"
});

server.tool({
  name: "design-architecture",
  description: "Design system architecture following senior architect workflow",
  parameters: {
    requirements: "string",
    teamSize: "number",
    timeline: "string"
  },
  handler: async ({ requirements, teamSize, timeline }) => {
    // Load knowledge base from docs/architecture/
    // Apply workflow logic
    // Return structured architecture design
  }
});
```

Then invoke in Claude Code:
```
Use the design-architecture tool to create architecture for [requirements]
```

### Adaptation Checklist

**To adapt for Claude Code:**
- [ ] Move project-instructions.md to CLAUDE.md
- [ ] Place knowledge base in docs/architecture/
- [ ] Update file references to relative paths
- [ ] Create quick reference in CLAUDE.md
- [ ] Test workflow by prompting to read documentation
- [ ] Consider MCP server for complex workflows
- [ ] Document setup in project README

**Best For:**
- Architecture design with code generation
- Component specifications with implementation
- Refactoring with architectural guidance
- ADR generation based on actual code

**Not Suitable For:**
- Pure design work without code (better in Claude Desktop)
- Large document analysis (PRD validation)

---

## Comparison Matrix

| Feature | Claude Desktop | Claude Code | Copilot | Windsurf |
|---------|---------------|-------------|---------|----------|
| **Knowledge Base Support** | ✅ Native (200K+ tokens) | ⚠️ Files only | ❌ No native support | ❌ No native support |
| **Custom Instructions** | ✅ Project-level | ✅ CLAUDE.md | ⚠️ Limited | ⚠️ Limited |
| **Structured Workflows** | ✅ Excellent | ⚠️ Manual prompts | ❌ No support | ⚠️ Command-based |
| **Code Execution** | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| **File Editing** | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes |
| **Mermaid Diagrams** | ✅ Native rendering | ⚠️ Code blocks | ⚠️ Code blocks | ⚠️ Code blocks |
| **Project Isolation** | ✅ Full | ⚠️ Workspace-based | ⚠️ Repo-based | ⚠️ Workspace-based |
| **Best Use Case** | Design & planning | Implementation | Coding assistance | Full-stack dev |

---

## Migration Checklist

### For Each Project Template

**1. Claude Code Adaptation:**
- [ ] Copy `project-instructions.md` to `CLAUDE.md`
- [ ] Move knowledge base to `docs/architecture/`
- [ ] Update all file references to relative paths
- [ ] Test reading workflow files
- [ ] Create quick command reference
- [ ] Document in project README

**2. GitHub Copilot Adaptation:**
- [ ] Create `.github/copilot-instructions.md`
- [ ] Condense knowledge base to ~50K tokens
- [ ] Move condensed files to `docs/architecture/`
- [ ] Add inline code comments with doc references
- [ ] Test with architecture questions
- [ ] Document limitations

**3. Windsurf Adaptation:**
- [ ] Create `.windsurf/instructions.md`
- [ ] Create `.windsurf/knowledge/` directory
- [ ] Condense knowledge base
- [ ] Define custom commands in `.windsurf/commands.json`
- [ ] Test command triggers
- [ ] Document setup

### General Migration Steps

**Step 1: Assess Compatibility**
- [ ] Review client capabilities
- [ ] Identify unsupported features
- [ ] Plan workarounds for limitations

**Step 2: Adapt Content**
- [ ] Convert custom instructions to client format
- [ ] Condense knowledge base if needed
- [ ] Adjust file structure
- [ ] Update file references

**Step 3: Test Thoroughly**
- [ ] Test with 5+ realistic scenarios
- [ ] Verify workflows still function
- [ ] Check knowledge base references
- [ ] Validate output quality

**Step 4: Document**
- [ ] Write client-specific setup guide
- [ ] Document known limitations
- [ ] Provide example prompts
- [ ] Create troubleshooting section

---

## Timeline & Priorities

### Q1 2026: Claude Code Support
**Priority:** HIGH
**Effort:** 2-4 weeks
**Deliverables:**
- CLAUDE.md templates for all 6 projects
- Documentation file structure
- Setup guides
- Example prompts

### Q2 2026: GitHub Copilot Support
**Priority:** MEDIUM
**Effort:** 3-4 weeks
**Deliverables:**
- Copilot instructions templates
- Condensed knowledge bases
- Inline code comment patterns
- Setup guides

### Q2 2026: Windsurf Support
**Priority:** MEDIUM
**Effort:** 2-3 weeks
**Deliverables:**
- Windsurf configuration templates
- Custom commands
- Knowledge base adaptations
- Setup guides

---

## Contributing

Want to help with migration support?

1. Test adapting a project for your preferred client
2. Document what works and what doesn't
3. Create PR with your adaptation
4. Share example prompts that work well

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## Resources

**Claude Desktop:**
- Current documentation: [README.md](README.md)
- Example conversations: [EXAMPLES.md](EXAMPLES.md)

**Claude Code:**
- Documentation: https://code.claude.com/docs
- CLAUDE.md format: https://code.claude.com/docs/claude-md

**GitHub Copilot:**
- Documentation: https://docs.github.com/en/copilot
- Custom instructions: https://docs.github.com/en/copilot/customizing-copilot

**Windsurf:**
- Documentation: [Windsurf docs]
- Configuration: [Windsurf config guide]

---

## Feedback

Have you successfully migrated a project to another client? Let us know!

- Create GitHub issue with "Migration" label
- Include: Client name, project adapted, what worked, what didn't
- Share example prompts and configurations

---

*Last Updated: November 17, 2025 | Status: Planning Phase*
