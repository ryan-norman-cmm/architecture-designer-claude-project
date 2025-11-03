# Requirements Validation - Section Prompts

## Getting Started

**User provides**: Business Requirements Document (BRD)

**User says**:
- "Start requirements validation"
- "Analyze this BRD"
- "Begin extraction workflow"

**What happens**: Agent reads BRD and prompts the user for approval or changes

---

## Section Responses

### Universal Responses (All Sections)

**Approve**:
- "Correct"
- "Approved"
- "Looks good"
- "Move forward"

**Request Changes**:
- "Change [X] to [Y]"
- "Add [item]"
- "Update [detail]"
- "Remove [item]"

**Navigate**:
- "Go back to [section name]"
- "Show status"
- "What section am I at?"

---

## 1. Initiative Overview

**Changes**:
- "Change problem to: [new description]"
- "Update solution: [changes]"

**Next**: User Roles

---

## 2. User Roles

**Changes**:
- "Add role: [name] - [network] - [responsibilities]"
- "Change [role] responsibilities to: [new description]"
- "Split [role] into: [role A] and [role B]"
- "Update network category for [role] to: [category]"

**After all roles**: "Any roles missing?"

**Next**: UI Screens/Components

---

## 3. UI Screens/Components

**Changes**:
- "Add screen: [name] - [purpose]"
- "Remove [screen]"

**After all screens**: "Any screens/components missing?"

**Next**: Workflows

---

## 4. Workflows

**Changes**:
- "Add workflow: [name]"
- "Remove [workflow]"

**After all workflows**: "Any workflows missing?"

**Next**: Services

---

## 5. Services

**Internal Services Changes**:
- "Add internal service: [name] - [what we need]"
- "Change [service] to: [new description]"
- "Remove [service]"

**Next**: External Integration

---

## 6. External Integrations

**External Integration Changes**:
- "Add external partner: [name] - [details]"
- "Change [partner] integration to: [new description]"
- "Remove [partner]"

**Next**: External Integration

---

## 7. Notifications

**Changes**:
- "Add notification: [event] - [recipient] - [method]"
- "Change [event] method to: [new method]"
- "Update timing for [event] to: [new timing]"
- "Add [user type] as recipient for [event]"
- "Remove [event]"

**After all notifications**: "Any notification events missing?"

**Next**: Scope & Priority

---

## 8. Scope & Priority

**Changes**:
- "Move [requirement] from MVP to Future"
- "Move [requirement] from Future to MVP"
- "Add MVP requirement: [requirement]"
- "Add to Won't Have: [item] - [reason]"
- "Change TBD [item] to: [decision]"

**Next**: Final Summary

---

## 9. Final Summary

**Approve**: "Ready for PRD generation"

**Changes**:
- "Go back to [section] to fix [issue]"
- "Update summary: [correction]"

**Next**: PRD Generation

---

## 10. PRD Generation

**Agent generates complete PRD automatically**

**Approve**: "PRD is complete"

**Changes**:
- "Update [section] with: [change]"
- "Go back to [section] to fix [issue]"

---

## Navigation Commands

| Command | Action |
|---------|--------|
| "Correct" / "Approved" | Move to next section |
| "Change [X] to [Y]" | Update current item |
| "Add [item]" | Insert new item |
| "Remove [item]" | Delete item |
| "Go back to [section]" | Return to section |
| "Show status" | Display progress |
| "What section am I at?" | Check current position |

---

## Cross-Section References

When making changes that affect other sections:

**Agent automatically**:
- Identifies dependent sections
- Regenerates affected sections
- Presents updated sections for review

**Example**:
```
User: "Go back to User Roles and add Pharmacist role"
Agent:
1. Updates Section 2 (User Roles)
2. Regenerates Section 3 (UI Screens) with new role
3. Regenerates Section 4 (Workflows) with new role
4. Presents each for re-approval
```

---

## Common Patterns

### Fast Path (Clear BRD, Quick Approvals)
```
Section 1 → Approved (2 min)
Section 2 → Approved (3 min)
Section 3 → Approved (3 min)
Section 4 → Approved (5 min)
Section 5 → Approved (3 min)
Section 6 → Approved (3 min)
Section 7 → Approved (2 min)
Section 8 → Approved (2 min)
Section 9 → Approved (2 min)
Section 10 → Generate (5 min)

Total: ~30 minutes
```

### Iterative Path (Typical Case)
```
Section 1 → Approved (2 min)
Section 2 → Change → Approved (5 min)
Section 3 → Add role → Approved (6 min)
Section 4 → Add screen → Approved (6 min)
Section 5 → Update workflow → Approved (8 min)
Section 6 → Clarify service → Approved (5 min)
Section 6 → Clarify integration → Approved (5 min)
Section 7 → Add notification → Approved (3 min)
Section 8 → Adjust scope → Approved (4 min)
Section 9 → Approved (3 min)
Section 10 → Generate (5 min)

Total: ~47 minutes
```

### Cross-Section Revision
```
Sections 1-4 → Completed (20 min)
Section 5 → Identify missing role
User: "Go back to User Roles"
Section 2 → Add role → Approved (3 min)
Sections 3-7 → Regenerate → Review → Approved (12 min)
Sections 8-10 → Complete (20 min)

Total: ~55 minutes
```

---

## Tips

### Do:
- Review each section thoroughly
- Be specific with changes
- Ask for clarification when needed
- Approve when satisfied
- Go back if something's wrong

### Don't:
- Rush approvals
- Skip validation
- Assume clarity
- Batch changes across sections
- Proceed with doubts

---

## Quick Reference

**Most Used Commands**:
- "Approved" → Continue
- "Add [item]" → Insert item
- "Change [X] to [Y]" → Update detail
- "Go back to [section]" → Return to section
- "Show status" → Check progress

**Section Flow**:
1. Initiative Overview
2. User Roles
3. UI Screens/Components
4. Workflows
5. Services
6. Integrations
7. Notifications
8. Scope & Priority
9. Final Summary
10. PRD Generation

---

## Completion

**When finished, you receive**:
- Complete Product Requirements Document
- Summary of validated sections
- List of "Not specified" items
- List of "TBD" items
- Next steps for technical design
