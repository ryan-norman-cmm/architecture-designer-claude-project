# [Feature Name] - Technology Epic Breakdown

## Overview
**Total Epics**: [X] epics across [X] releases
**Team Size**: [X] Backend + [X] Frontend + [X] Platform

---

## Epic Summary by Release

| Release | Epic ID | Epic Name | Team | Size | Dependencies | Key Deliverables |
|---------|---------|-----------|------|------|--------------|------------------|
| **[REL-XXX: Release Name]** | TECH-EPIC-XXX | [Epic Name] | [Team] | [S/M/L] | [Dependencies] | [Deliverables] |
| **[REL-XXX: Release Name]** | TECH-EPIC-XXX | [Epic Name] | [Team] | [S/M/L] | [Dependencies] | [Deliverables] |
| **[REL-XXX: Release Name]** | TECH-EPIC-XXX | [Epic Name] | [Team] | [S/M/L] | [Dependencies] | [Deliverables] |

---

## Delivery Timeline

```mermaid
gantt
    title [Feature Name] - Technology Epic Delivery
    dateFormat YYYY-MM-DD
    axisFormat %

    section ITR-XXX [Release Name]
    TECH-EPIC-XXX [Epic Name] ([Size])           :epic1, [start-date], [duration]
    TECH-EPIC-XXX [Epic Name] ([Size])           :epic2, [start-date], [duration]
    ITR-XXX Complete                             :milestone, m1, [date], 0d

    section ITR-XXX [Release Name]
    TECH-EPIC-XXX [Epic Name] ([Size])           :epic3, [start-date], [duration]
    ITR-XXX Complete                             :milestone, m2, [date], 0d
```

---

## [ITR-XXX]: [Release Name]

**Goal**: [Release user capability in one sentence]

### TECH-EPIC-XXX: [Epic Name] ([Team])
**Size**: [S/M/L]

```mermaid
graph TB
    subgraph Users
        [USER][User Type]
        style [USER] fill:#FFF,stroke:#00426A,stroke-width:2px
    end

    subgraph CorePlatform ["What We're Building"]
        [COMPONENT][Component Name<br/>Description]
        style [COMPONENT] fill:#FFE5EF,stroke:#E70665,stroke-width:3px
    end

    subgraph External
        [EXTERNAL][External System<br/>Name]
        style [EXTERNAL] fill:#E9F4FB,stroke:#1E91D6,stroke-width:2px
    end

    [USER] -->|[Action]| [COMPONENT]
    [COMPONENT] -->|[Action]| [EXTERNAL]
    [EXTERNAL] -->|[Result]| [COMPONENT]
    [COMPONENT] -->|[Display]| [USER]

    style Users fill:#F5F5F5,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5
    style CorePlatform fill:#F5F5F5,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5
    style External fill:#F5F5F5,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5
```

**What We're Building**:
- [Deliverable 1 in plain language]
- [Deliverable 2 in plain language]
- [Deliverable 3 in plain language]

**Why It Matters**: [Business value in 1-2 sentences]

**Dependencies**:
- [Critical blocker 1]
- [Critical blocker 2 if applicable]

**Success Looks Like**:
- [Measurable outcome 1]
- [Measurable outcome 2]

---

[Repeat for each epic in release]

---

[Repeat for each release - NO "Delivery Summary" sections]
