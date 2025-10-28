# ADR Template

**Purpose:** Standard Architecture Decision Record format for Phase 4 documentation

**When to Use:** Generate one ADR per decision identified in Phase 2

**How to Use:**
- Fill out all sections with content from Phases 1-3
- Generate as separate artifact (one ADR per artifact)
- Include Mermaid diagram for architecture/integration/data decisions
- Use kebab-case filename: `ADR-00X-decision-title.md`

---

## Template

```markdown
# ADR-00X: [Decision Title]

**Status:** Accepted
**Date:** [YYYY-MM-DD]
**Context:** [One sentence summary from Phase 1 requirements]

## Decision

We will [specific decision statement - what was chosen].

## Context and Problem Statement

[Describe the problem being solved, referencing Phase 1 requirements]

**Requirements:**
- [Key requirement 1 from Phase 1]
- [Key requirement 2 from Phase 1]
- [Key requirement 3 from Phase 1]

**Constraints:**
- [Key constraint 1 from Phase 1 - team size, timeline, budget]
- [Key constraint 2 from Phase 1]
- [Key constraint 3 from Phase 1]

## Decision Drivers

[From Phase 2 - what influenced this decision]

- [Driver 1: e.g., Team size (3 engineers)]
- [Driver 2: e.g., Timeline (2 months to launch)]
- [Driver 3: e.g., Platform cohesion (reuse existing services)]
- [Driver 4: e.g., Scale expectations (500 → 5K users)]

## Considered Options

[From Phase 3 comparison table - alternatives explored]

1. **Option A: [Name]** - [Brief description from comparison table]
2. **Option B: [Name]** - [Brief description from comparison table]
3. **Option C: [Name]** - [Brief description from comparison table]

## Decision Outcome

**Chosen option:** Option [X] - [Name]

**Rationale:**

[Specific reasons tied to requirements and constraints from Phases 1-3. Reference:
- Why this option fits the requirements
- How it addresses the constraints
- Why it scored highest against decision drivers
- How it aligns with platform context]

### Consequences

**Positive:**
- [From Phase 3 detailed exploration - Pro 1]
- [From Phase 3 detailed exploration - Pro 2]
- [From Phase 3 detailed exploration - Pro 3]
- [From Phase 3 detailed exploration - Pro 4]
- [From Phase 3 detailed exploration - Pro 5]

**Negative:**
- [From Phase 3 detailed exploration - Con 1 with mitigation]
- [From Phase 3 detailed exploration - Con 2 with mitigation]
- [From Phase 3 detailed exploration - Con 3 with mitigation]

**Neutral:**
- [Implementation considerations]
- [Team learning required]
- [Migration strategy if replacing existing approach]

## Alternatives Analysis

### Option A: [Name]

**Pros:**
- [From Phase 3 comparison table or detailed exploration]
- [List all advantages]

**Cons:**
- [From Phase 3 comparison table or detailed exploration]
- [List all disadvantages]

**Why Not Selected:**

[Specific reason from Phase 3 discussion. Reference requirements/constraints that made this option less suitable.]

### Option B: [Name]

**Pros:**
- [From Phase 3 comparison table or detailed exploration]

**Cons:**
- [From Phase 3 comparison table or detailed exploration]

**Why Not Selected:**

[Specific reason from Phase 3 discussion]

### Option C: [Name]

[Similar structure - only include if this option was explored in detail]

## Diagram

[Include for architecture pattern, integration pattern, or data architecture decisions]

```mermaid
[Choose diagram type based on decision:
- Architecture Pattern → C4Context or Component diagram
- Integration Pattern → Sequence diagram
- Data Architecture → ER diagram
- See kb-diagram-examples.md for examples]
```

[Skip diagram section for technology selection decisions like database vendor, auth provider, etc.]

## Implementation Notes

[Practical guidance for implementing this decision]

- [Specific tools/frameworks to use]
- [Configuration considerations]
- [Migration steps if replacing existing approach]
- [Testing strategy]
- [Rollout plan]

## References

- [Link to Phase 3 detailed exploration discussion]
- [External documentation for chosen technology]
- [Team documentation or platform standards]
- [Related ADRs if this decision depends on others]
```

---

## Sections Explained

### Decision
One-sentence statement of what was chosen. Clear and unambiguous.

### Context and Problem Statement
Sets the stage - what problem needed solving? Include requirements and constraints from Phase 1.

### Decision Drivers
The key factors that influenced the decision. Pulled from Phase 2 decision identification and Phase 1 constraints.

### Considered Options
List of alternatives from Phase 3 comparison table. Brief descriptions only.

### Decision Outcome
The chosen option with detailed rationale. This is the "why" - tie back to requirements, constraints, and decision drivers.

### Consequences
Honest assessment of pros and cons from Phase 3 detailed exploration. Include mitigations for negative consequences.

### Alternatives Analysis
Deep dive on why each alternative was NOT selected. Pull from Phase 3 comparison table and detailed explorations.

### Diagram
Visual representation of the decision (if architecture/integration/data). Use Mermaid syntax. See `kb-diagram-examples.md`.

### Implementation Notes
Practical guidance for teams implementing this decision. Actionable next steps.

### References
Links to supporting documentation and related decisions.

---

## Example Filenames

- `ADR-001-modular-monolith-architecture.md`
- `ADR-002-postgresql-data-storage.md`
- `ADR-003-rest-api-integration.md`
- `ADR-004-redis-caching-strategy.md`

---

## Quality Checklist

Before delivering an ADR, verify:

- [ ] All sections filled out (no placeholders)
- [ ] Rationale ties back to Phase 1 requirements/constraints
- [ ] Pros and cons are specific (not vague)
- [ ] Alternatives analysis explains why NOT selected
- [ ] Diagram included (if architecture/integration/data decision)
- [ ] Implementation notes are actionable
- [ ] Filename uses kebab-case
- [ ] Generated as separate artifact (not inline)
- [ ] No surrounding commentary in the artifact
- [ ] Ready to save directly to file
