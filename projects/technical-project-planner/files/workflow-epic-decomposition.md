# Epic Decomposition Workflow

## Overview

Transform product iterations into executable technology epics with business-friendly summaries and simple architecture diagrams.

**Duration:** 60-90 minutes per initiative
**Output:** Complete epic breakdown document with Gantt chart and architecture diagrams

---

## Workflow Steps

### Step 1: Retrieve Existing Diagrams

**FIRST STEP - ALWAYS DO THIS**: Search for all existing architecture diagrams for this initiative:

1. **Find the Project**:
   - Use `arch-diagrammer:list_projects` to search for projects
   - Match project name to initiative name (e.g., "Enrollment Forms Initiative")
   - Note the project ID and diagram count

2. **List All Diagrams** (if project exists):
   - Use `arch-diagrammer:list_diagrams` to retrieve diagrams
   - If there are more than 10 diagrams, paginate through all pages
   - Note diagram titles, types, and descriptions

3. **Document Findings**:
   - Record project name, ID, and total diagram count
   - Plan to reference these in the Appendix section
   - If no project exists, note that diagrams will be created as part of this initiative

**Validation Checklist**:
- [ ] Attempted diagram retrieval using arch-diagrammer tools
- [ ] Recorded project name and ID (if exists)
- [ ] Noted total diagram count
- [ ] Planned appendix reference

---

### Step 2: Create Overview & Summary Table

Generate overview with team size and a summary table showing all epics by iteration with key information (t-shirt size only, dependencies, deliverables).

**DO NOT include:**
- Week estimates
- Calendar timelines
- Specific dates in the overview

**Validation Checklist**:
- [ ] Overview shows team size
- [ ] Overview shows total epic count by iteration
- [ ] Summary table includes all epics
- [ ] T-shirt sizes only (S/M/L)
- [ ] Dependencies listed
- [ ] Key deliverables summarized
- [ ] NO week estimates or dates

---

### Step 3: Create Timeline Gantt Chart

Generate a Gantt chart showing:
- All epics across all iterations
- Parallel vs sequential work streams
- Product iteration milestones
- Use `axisFormat %` (not dates) to show relative progression only
- Label each epic clearly with its TECH-EPIC-XXX identifier

**Validation Checklist**:
- [ ] Gantt chart includes all epics
- [ ] Uses `axisFormat %` (not dates)
- [ ] Epic labels include TECH-EPIC-XXX identifiers
- [ ] Product iteration milestones marked
- [ ] Parallel/sequential work shown clearly

---

### Step 4: Analyze Iterations

Read Product Requirements (PRD) to understand:
- Iteration goals and user capabilities
- Scope (included/excluded)
- Dependencies between iterations
- Decision gates and success metrics

**Validation Checklist**:
- [ ] Iteration goals documented
- [ ] Scope boundaries clear (included/excluded)
- [ ] Dependencies between iterations identified
- [ ] Success metrics noted

---

### Step 5: Map Technical Scope

For each iteration, determine which teams need epics:
- **Backend**: APIs, integrations, workflows, FHIR resources
- **Frontend**: UI components, user flows
- **Platform**: Infrastructure, monitoring, feature flags

Use TED effort mapping to guide team assignments.

**Validation Checklist**:
- [ ] Backend scope identified per iteration
- [ ] Frontend scope identified per iteration
- [ ] Platform scope identified per iteration
- [ ] Team assignments align with TED effort mapping
- [ ] No gaps in team coverage

---

### Step 6: Create Epic Summaries

For each epic, create a concise summary with:
- Simple architecture diagram (3-6 components only)
- Business-friendly "What We're Building"
- Clear "Why It Matters" statement
- Critical dependencies only
- Measurable success criteria

**DO NOT include:**
- "Delivery Summary" sections after iterations
- Technical implementation details
- More than 6 components in diagrams

**Validation Checklist (per epic)**:
- [ ] Architecture diagram with 3-6 components only
- [ ] "What We're Building" uses plain language
- [ ] "Why It Matters" explains business value
- [ ] Dependencies list only critical blockers
- [ ] Success criteria are measurable
- [ ] Diagram uses standard color scheme

---

### Step 7: Create Appendix with Diagram Repository

Include an appendix section that:
- **Lists the project details** where detailed diagrams are stored
- **Notes the total count** of diagrams available
- **Describes diagram categories** (e.g., technical architecture, workflows, data flows)
- **Explains the purpose**: Simplified diagrams in the document are for business stakeholders; full technical details are in the diagram repository
- **Provides access instructions**: Directs readers to the project for complete technical specifications

**Validation Checklist**:
- [ ] Appendix references diagram repository
- [ ] Project details included (name, ID, count)
- [ ] Diagram categories described
- [ ] Purpose explained clearly
- [ ] Access instructions provided

---

### Step 8: Validate Complete Document

Ensure:
- Every iteration has complete team coverage
- Dependencies are clear and non-circular
- Diagrams are simple and focused
- NO week estimates or delivery summaries in main document body
- NO "Delivery Summary" sections after iterations
- Gantt chart uses axisFormat % (not dates)
- Gantt chart labels include TECH-EPIC-XXX identifiers
- Appendix references existing diagram repository
- Diagram retrieval was attempted in Step 1

**Final Validation Checklist**:
- [ ] All iterations have Backend/Frontend/Platform coverage
- [ ] Dependencies verified (no circular dependencies)
- [ ] All diagrams have 3-6 components maximum
- [ ] Plain language used throughout
- [ ] Business value explained for each epic
- [ ] NO week estimates in epic descriptions
- [ ] NO "Delivery Summary" sections
- [ ] Gantt chart properly formatted
- [ ] Appendix complete with diagram repository reference
- [ ] Change log included

---

## Quality Standards

### Diagram Standards

**Component Count**: 3-6 components maximum per diagram
**Color Scheme**:
- Core Platform (what we're building): `fill:#FFE5EF,stroke:#E70665,stroke-width:3px`
- Integration Layer: `fill:#FFF4E9,stroke:#FF8F1D,stroke-width:2px`
- External Systems: `fill:#E9F4FB,stroke:#1E91D6,stroke-width:2px`
- Users: `fill:#FFF,stroke:#00426A,stroke-width:2px`

**Arrow Labels**: Descriptive actions ("Request Forms", "Return Status")

### Language Standards

**Use Plain Language**:
- "Search for forms" not "Query discovery endpoint"
- "Display status" not "Render UI components"
- "Partner system" not "External integration layer"

**Focus on Business Value**:
- "Staff save 5 minutes per enrollment" not "API response time <2s"
- "Doctors see status at a glance" not "Dashboard implements real-time subscriptions"

---

## Common Pitfalls to Avoid

âŒ Including week estimates in epic descriptions
âŒ Adding "Delivery Summary" sections after iterations
âŒ Using calendar dates in Gantt chart (use axisFormat % only)
âŒ Showing more than 6 components in diagrams
âŒ Using technical jargon in "What We're Building"
âŒ Forgetting TECH-EPIC-XXX labels in Gantt chart
âŒ Not attempting diagram retrieval in Step 1
âŒ Missing appendix with diagram repository reference
