# Changelog

All notable changes to Claude Desktop Project Templates will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-11-17

### Added - Initial Release

#### Projects
- **Architecture Designer (v3.0)** - 252K tokens, 13 files
  - Senior Principal Architect agent for system architecture design
  - 4-phase workflow: Understand Problem → Identify Decisions → Explore Solutions → Document Decisions
  - Comprehensive knowledge base: patterns, anti-patterns, technology selection, scaling strategies, ADR library
  - Healthcare domain specialization (HIPAA, FHIR, HL7)
  - ASCII diagrams for exploration, Mermaid for documentation

- **Product Releases Creator (v2.0)** - 45K tokens, 12 files
  - Release strategist for initiative decomposition
  - Marty Cagan continuous discovery framework
  - Vertical slicing methodology
  - Learning velocity optimization
  - Healthcare user type standards

- **Product Requirements Validator (v1.0)** - 15K tokens, 6 files - STABLE
  - 10-stage requirements validation workflow
  - Requirements traceability and gap identification
  - CMM product capabilities knowledge base
  - Structured PRD generation
  - Extensively user-tested and validated

- **Technical Requirements Creator (v1.0)** - 25K tokens, 8 files - STABLE
  - Healthcare technical specifications
  - FHIR resource mappings
  - BPM workflow orchestration
  - 8-step requirements analysis workflow
  - Extensively user-tested and validated

- **Technical Solution Estimator (v1.0)** - 18K tokens, 7 files - STABLE
  - Development effort estimation
  - Risk analysis and confidence levels
  - Platform capability leverage
  - Component-level breakdowns
  - Extensively user-tested and validated

- **Technical Project Planner (v1.0)** - 12K tokens, 7 files - BETA
  - Epic delivery planning
  - Developer-ready task breakdown
  - Dependency mapping
  - Acceptance criteria definition
  - Needs user testing and validation

#### Documentation
- Comprehensive README with:
  - Quick start guide (3-minute setup)
  - Project comparison table
  - Detailed installation instructions per project
  - File naming conventions
  - Token limits and Claude Desktop guidance
  - FAQ section (8 questions)
  - Troubleshooting guide (6 common issues)
  - Success metrics per project
  - Customization and extension guide
  - Advanced topics (performance, multi-project workflows)
  - Quick reference command cheat sheet

- Three-layer architecture pattern documentation:
  - Layer 1: Agent Instructions (personality, principles)
  - Layer 2: Workflow Definitions (conversation phases)
  - Layer 3: Knowledge Base (domain knowledge, templates)

- Project-specific READMEs:
  - `projects/README.md` - Three-layer architecture detailed guide
  - Per-project setup and usage instructions

#### Repository Structure
- Standardized file naming conventions:
  - `workflow-*.md` - Conversation flows
  - `kb-*.md` - Knowledge base files
  - `template-*.md` - Reusable templates
  - `guide-*.md` - Step-by-step tutorials
  - `agent-*.md` - Sub-agent methodologies

- Git configuration:
  - `.gitignore` for Claude Code local settings
  - `CLAUDE.md` project instructions for Claude Code

#### Product Management
- `documentation/product-requirements.md` - Full PRD for repository
- `documentation/initiative-releases.md` - Release planning with 5 releases

### Changed

#### Architecture Designer
- **v3.0** - Added Phase 2: Identify Architecture Decisions
  - Decision-scoping phase ensures alignment before exploration
  - On-demand approach generation per decision (reduces output by 40%)
  - Cognitive load management improvements

- **v2.0** - Added Phase 2.5: Solution Overview & Approval
  - Minimal high-level overview (500 words max) before detailed exploration
  - User approval gate before extensive documentation

### Fixed
- Standardized structural organization across all three technical projects
- Cleaned up workflow templates
- Added comprehensive template and guide files
- Added validation checklists

---

## [Unreleased]

### Planned Features
- **CONTRIBUTING.md** - Internal contribution guidelines
- **Example conversation transcripts** - Show projects in action
- **Visual setup guide** - Screenshots of Claude Desktop setup process
- **Migration guide** - Support for Copilot, Windsurf, Claude Code
- **Custom knowledge base templates** - Help users extend with company-specific content

### Under Consideration
- **Cost estimation capability** (Architecture Designer) - Infrastructure cost estimates based on scale
- **Evolution path planning** (Architecture Designer) - Detailed roadmaps from MVP to 1M+ users
- **Company-specific knowledge base customization** - Organization-specific patterns and compliance
- **Integration with architecture review workflow** - Formal review templates and approval workflows
- **Real-time knowledge base updates** - Quarterly content refresh automation

---

## Maturity Assessment Criteria

Projects are assigned maturity levels based on these criteria:

### Stable (⭐⭐⭐)
**Requirements:**
- Extensively user-tested with real use cases
- Workflow proven effective through actual usage
- Production-ready for team adoption
- User feedback incorporated
- No critical issues blocking usage

**Current Stable Projects:**
- architecture-designer (v3.0) - Extensively tested, multiple iterations
- product-releases-creator (v2.0) - Extensively tested, multiple iterations
- product-requirements-validator (v1.0) - User-validated, production-ready
- technical-requirements-creator (v1.0) - User-validated, production-ready
- technical-solution-estimator (v1.0) - User-validated, production-ready

### Beta (⭐⭐)
**Requirements:**
- Core features complete and functional
- Workflow defined and documented
- Knowledge base created
- Ready for user testing and feedback
- May need refinement based on actual usage

**Current Beta Projects:**
- technical-project-planner (v1.0) - Needs user testing and validation

### Alpha (⭐)
**Requirements:**
- Experimental features
- Incomplete functionality
- Limited documentation
- Early internal testing only
- Not recommended for production use

**Current Alpha Projects:** None

---

## Version History

### Architecture Designer
- **v3.0** (2025-11-03) - STABLE - Added decision identification phase, cognitive load management
- **v2.0** (2025-10-27) - STABLE - Added solution overview approval gate
- **v1.0** (2025-10-01) - BETA - Initial release with 6-phase workflow

### Product Releases Creator
- **v2.0** (2025-10-28) - STABLE - Added alternative approaches workflow, option explorer agent
- **v1.0** (2025-10-15) - BETA - Initial release with release decomposition workflow

### Product Requirements Validator
- **v1.0** (2025-10-28) - STABLE - 10-stage validation workflow, extensively user-tested

### Technical Requirements Creator
- **v1.0** (2025-11-03) - STABLE - 8-step analysis workflow, extensively user-tested

### Technical Solution Estimator
- **v1.0** (2025-11-03) - STABLE - Estimation methodology, extensively user-tested

### Technical Project Planner
- **v1.0** (2025-11-03) - BETA - Epic decomposition workflow, needs user testing

---

## Migration Notes

### From Previous Versions

**If you have Architecture Designer v2.0 or earlier:**
1. Update `workflow-architecture-exploration.md` to include Phase 2: Identify Architecture Decisions
2. Replace `project-instructions.md` with v3.0 version
3. Test with sample architecture request to verify decision-scoping works

**If you have Product Releases Creator v1.0:**
1. Add new agent files: `agent-option-explorer.md`, `agent-validation.md`
2. Update `workflow-release-decomposition.md` to include alternative approaches
3. Add `template-option-comparison.md` for comparing alternatives

---

## Breaking Changes

### None (v1.0 Initial Release)

Future breaking changes will be documented here with migration instructions.

---

## Deprecation Notices

### None

Future deprecations will be announced here at least one version in advance.

---

## Support

For questions or issues:
- Check README.md [Troubleshooting section](README.md#troubleshooting)
- Review [FAQ](README.md#faq)
- Create GitHub issue with "Bug" or "Enhancement" label

---

*Maintained by CMM Team | Last Updated: November 17, 2025*
