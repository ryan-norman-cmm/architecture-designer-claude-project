# Requirements Validation Workflow

## Workflow Guide

Present ONE requirement at a time for validation. After user confirms, move to the next item.

## Checkpoint Pattern

After each stage output:

```markdown
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📍 WORKFLOW STATUS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Initiative: [Name]
Current Stage: [X of 10] - [Stage Name]
Last Action: [What was just presented]
Next Step: [What to do next]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

**Is this accurate? Any changes?**

Options:
1. **Approved** → Move to Stage [X+1]
2. **Change [X] to [Y]** → Update and re-present
3. **Add [item]** → Insert additional requirement
4. **Go back to Stage [N]** → Return to earlier stage
```

**Validation Rules:**
- [ ] All information extracted from explicit BRD statements
- [ ] "Not specified" used for missing information
- [ ] "TBD" used for explicitly pending items
- [ ] Cross-references to related stages accurate
- [ ] User explicitly approved before proceeding

<!--
AI AGENT CRITICAL INSTRUCTION:

VALIDATION vs FINAL OUTPUT

During Stages 1-9 (Validation):
- Present ONLY the CONCISE formats shown in each stage below
- Get user approval on KEY FACTS only
- DO NOT present full Product Requirements Template sections
- DO NOT include detailed tables, assumptions lists, or success metrics
- Keep responses SHORT and focused on validation

During Stage 10 (PRD Generation):
- NOW use /mnt/project/template-product-requirements.md
- Generate COMPLETE detailed sections with all formatting
- Include full Problem Statement, Solution Overview, Assumptions, Success Metrics
- Populate all tables and detailed breakdowns

REMEMBER: Stages 1-9 collect the FACTS. Stage 9 formats them into the final document.

If you find yourself writing multi-paragraph responses with detailed tables during Stages 1-9,
you are doing it WRONG. Stop and present only the concise format shown below.
-->

---

## 1. Initiative Overview

<!--
AI AGENT INSTRUCTION:
This is a CONCISE validation format - NOT the final PRD section.

PRESENT ONLY:
- Initiative Name (1 line)
- Core Problem (1 sentence)
- Proposed Solution (1 sentence)

DO NOT PRESENT during this stage:
- Multi-paragraph problem statements
- "Who has this problem and how painful is it?" breakdowns
- Detailed solution overview with bullet points
- Assumptions lists
- Success metrics tables
- Any content from template-product-requirements.md

Those details belong in Stage 9 (final PRD generation), not here.
-->

**Present**:
```
INITIATIVE OVERVIEW

Initiative Name: [Name from BRD]

Core Problem: [1 sentence problem statement]

Proposed Solution: [1 sentence solution overview]

```

**Ask**: "Accurate? Any corrections?"

**Responses**:
- "Correct" → Move to User Roles
- Changes → Update and re-present

**Validation Checklist**:
- [ ] Initiative name extracted from BRD
- [ ] Core problem is 1 sentence from BRD (not elaborated)
- [ ] Proposed solution is 1 sentence from BRD (not elaborated)
- [ ] No assumptions added beyond BRD statements
- [ ] User explicitly approved before proceeding

---

## 2. User Roles (all at once)

**Present**:
```
USER ROLE [N of X]

User Type: [Role name]
Network Category: [Provider/Pharmacy/Pharma/Payer/Patient/CoverMyMeds]

Responsibilities:
- [Key responsibility 1]
- [Key responsibility 2]
- [Key responsibility 3]

Volume: [Count or "Not specified"]
Frequency: [Usage frequency or "Not specified"]
```

**Ask**: "Correct? Any changes?"

**After all roles**: "Any roles missing?"

**Validation Checklist**:
- [ ] All user roles extracted from BRD
- [ ] Each role assigned correct network category
- [ ] Responsibilities listed are from BRD (not inferred)
- [ ] Volume/frequency data extracted or marked "Not specified"
- [ ] No duplicate or overlapping roles
- [ ] User confirmed all roles captured

---

## 3. UI Screens/Components (all at once)

**Present**:
```
SCREEN [N of X]

Name: [Screen name]
Type: [Screen | Component]
Purpose: [What this accomplishes]
Used By: [User types]
```

**Ask**: "Correct? Any changes?"

**After all screens**: "Any screens/components missing?"

**Validation Checklist**:
- [ ] All UI screens/components extracted from BRD
- [ ] Each screen has clear purpose stated
- [ ] User types accessing each screen documented
- [ ] Data elements and actions listed from BRD
- [ ] Cross-referenced to user roles (Stage 2)
- [ ] User confirmed all screens captured

---

## 4. Workflows (all at once)

**Present**:
```
WORKFLOW [N of X]

Name: [Workflow name]
Trigger: [What starts this]
Success: [What indicates completion]
```

**Ask**: "Accurate? Any changes to steps?"

**After all workflows**: "Any workflows missing?"

**Validation Checklist**:
- [ ] All workflows extracted from BRD
- [ ] Each workflow has trigger and success criteria
- [ ] Steps are from BRD (not inferred)
- [ ] Decision points documented
- [ ] Cross-referenced to user roles (Stage 2) and screens (Stage 3)
- [ ] User confirmed all workflows captured

---

## 5. Services (all at once)

**Present**:
```
INTERNAL CMM SERVICES

1. [Service Name]
   Consumes: [Data consumed]
   Actions: [Actions requested]

2. [Service Name]
   [Same structure...]
```

**Ask**: "Internal services correct? Any changes?"

**Validation Checklist**:
- [ ] All internal CMM services identified from BRD
- [ ] Each service has clear data/action description
- [ ] Service dependencies documented
- [ ] Cross-referenced to workflows (Stage 4)
- [ ] User confirmed all services captured

---

## 6. External Integrations (all at once)

**Present**:
```
EXTERNAL PARTNERS

1. [Partner Name]
   We Send: [Data/requests]
   They Send: [Data/responses]

2. [Partner Name]
   [Same structure...]
```

**Ask**: "External integrations correct? Any changes?"

**Validation Checklist**:
- [ ] All external partners identified from BRD
- [ ] Data exchange patterns documented (what we send/receive)
- [ ] Integration criticality noted
- [ ] Cross-referenced to workflows (Stage 4)
- [ ] User confirmed all integrations captured

---

## 7. Notifications (all at once)

**Present**:
```
NOTIFICATION EVENT [N of X]

Event: [What triggers this]
Who Gets Notified: [Roles]
```

**Ask**: "Notification correct? Any changes?"

**After all events**: "Any notifications missing?"

**Validation Checklist**:
- [ ] All notification events extracted from BRD
- [ ] Trigger conditions documented
- [ ] Recipients (roles) identified
- [ ] Notification methods noted (email/SMS/in-app)
- [ ] Cross-referenced to workflows and roles
- [ ] User confirmed all notifications captured

---

## 8. Scope & Priority (all at once)

**MVP Requirements**:
```
1. [Requirement]: [What this enables]
2. [Requirement]: [What this enables]
3. [Requirement]: [What this enables]

**Ask**: "MVP scope correct? Any changes?"
```

**Validation Checklist**:
- [ ] MVP requirements clearly identified from BRD
- [ ] Should Have items documented
- [ ] Could Have items documented
- [ ] Won't Have items with rationale
- [ ] Scope filtering rules applied (MVP/Phase 1/In Scope)
- [ ] User confirmed scope priorities

---

## 9. Final Summary

<!--
AI AGENT INSTRUCTION:
This is the LAST validation stage. After this, you move to Stage 10 (PRD Generation).

Stage 10 is where you:
1. Read /mnt/project/template-product-requirements.md
2. Generate the COMPLETE formatted document
3. Include ALL detailed sections that were NOT shown during validation stages
4. Transform validated facts into full PRD format

Do NOT generate the full PRD until Stage 10.
-->

**Present**:
```
✅ VALIDATION COMPLETE

Initiative: [Name]
Validated Sections:
- User Roles: [Count]
- Workflows: [Count]
- Screens: [Count]
- Services: [Internal count] internal, [External count] external
- Notifications: [Count]

Status:
✓ All sections completed
✓ Cross-references validated

Next Steps:
1. Review complete product requirements generation
```

**Ask**: "Ready for product requirements generation?"

**Validation Checklist**:
- [ ] All 8 validation stages completed (1-8)
- [ ] Cross-references between sections validated
- [ ] "Not specified" items documented
- [ ] "TBD" items documented
- [ ] Gaps explicitly identified
- [ ] User ready to proceed to PRD generation

---

<!--
AI AGENT CRITICAL INSTRUCTION - STAGE 10 TRANSITION:

You have now completed Stages 1-9 (fact validation).

STAGE 10 is COMPLETELY DIFFERENT from Stages 1-9.

In Stage 10 you will:
1. Read /mnt/project/template-product-requirements.md in full
2. Take ALL validated facts from Stages 1-9
3. Generate the COMPLETE Product Requirements Document
4. Include ALL detailed sections, tables, and formatting
5. This is where assumptions, success metrics, detailed workflows appear
6. Remove ALL "Section Instructions:" and template guidance
7. Produce a presentation-ready document

Stage 10 = Full document generation, not validation.
-->

## 10. PRD Generation

<!--
AI AGENT INSTRUCTION:
NOW you generate the complete Product Requirements Document.

Use /mnt/project/template-product-requirements.md as your structure.
Include everything that was NOT shown during validation stages.

Critical for Stage 10:
- Generate full Problem & Solution section (multi-paragraph)
- Include detailed User Roles table with all columns
- Create complete Workflow Steps Detail sections
- Populate all Services & Integrations tables
- Include Assumptions, Success Metrics, all appendices
- Remove ALL section instructions and template guidance
- Output should be presentation-ready for stakeholders
-->

**Agent generates complete PRD automatically**

**Approve**: "PRD is complete"

**Changes**:
- "Update [section] with: [change]"
- "Go back to [section] to fix [issue]"

**Validation Checklist**:
- [ ] Complete PRD generated using template-product-requirements.md
- [ ] All validated facts from Stages 1-9 incorporated
- [ ] Section instructions and template guidance REMOVED
- [ ] Problem & Solution section complete (multi-paragraph)
- [ ] All tables populated (User Roles, Workflows, Services, etc.)
- [ ] Assumptions and Success Metrics included
- [ ] Cross-references accurate throughout document
- [ ] Presentation-ready for stakeholders
- [ ] User approved final PRD

---

## Navigation Commands

- **"Go back to [section]"** → Return to specific section
- **"Add [item]"** → Insert new item in current section
- **"Change [X] to [Y]"** → Update specific detail
- **"Skip to [section]"** → Jump forward (not recommended)
- **"Show status"** → Display workflow progress
- **"Start over"** → Return to Initiative Overview

---

## Quality Checks

Before moving sections, verify:
- ✓ Current section approved
- ✓ All items in section covered
- ✓ Cross-references are valid
- ✓ User explicitly confirmed

---

## Best Practices

**For Users**:
- Review thoroughly before approving
- Be specific with changes
- Flag errors immediately
- Ask for clarification when needed

**For Agent**:
- Quote the BRD when extracting
- Preserve original terminology
- Flag all assumptions
- Maintain traceability
- Cross-reference between sections
- Highlight gaps explicitly

---

## Success Criteria

✓ All PRD sections populated
✓ Information traces to BRD
✓ Each section user-approved
✓ Cross-references validated
✓ Gaps clearly documented
✓ Sufficient detail for technical design
