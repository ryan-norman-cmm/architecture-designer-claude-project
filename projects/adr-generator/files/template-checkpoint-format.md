# Checkpoint Format Template

Use this template to insert conversational control points throughout the workflow.

## Standard Checkpoint Format

---

📍 **Checkpoint: [Context Name]**

[Optional: 1-2 sentence recap of what was just covered]

What would you like to do next?
1. **[Action 1]** → [Brief description of outcome]
2. **[Action 2]** → [Brief description of outcome]
3. **[Action 3]** → [Brief description of outcome]

Your choice (1-3) or describe what you need:

---

## Checkpoint Types & Examples

### After Requirements Gathering
---

📍 **Checkpoint: Requirements Complete**

I've gathered your project context: [brief 1-sentence summary].

What would you like to explore next?
1. **See comparison table** → Quick overview of 3-5 architecture approaches
2. **Adjust requirements** → Refine what we discussed
3. **Ask a question** → Clarify architecture concepts before we proceed

Your choice:

---

### After Comparison Table
---

📍 **Checkpoint: Approaches Overview**

You've seen the high-level comparison of [N] approaches optimized for your needs.

What would you like to do?
1. **Explore [Approach Name]** → See detailed breakdown with diagrams
2. **Compare technologies** → See technology decisions across all approaches
3. **Adjust requirements** → Change constraints and regenerate table
4. **Ready to decide** → Skip details and select an approach

Your choice:

---

### Mid-Approach Details (After Diagrams)
---

📍 **Checkpoint: Architecture Overview**

So far we've covered:
- System context and component structure
- High-level benefits and tradeoffs

What's next?
1. **Continue with details** → Technology decisions and fit analysis
2. **See another approach** → Switch to [Alternative Name]
3. **Explain a concept** → Learn more about [mentioned term]

Your choice:

---

### After Approach Complete
---

📍 **Checkpoint: Approach Exploration Complete**

You've seen the full analysis of [Approach Name] including diagrams, technology decisions, and tradeoffs.

Ready to move forward?
1. **Select this approach** → Proceed to ADR generation
2. **Compare with [Other]** → See alternative approach details
3. **Ask questions** → Dive deeper into specific aspects

Your choice:

---

### Before Detailed Component Design (Phase 6)
---

📍 **Checkpoint: What Level of Detail?**

I can generate implementation specs now, or you can skip to ADRs.

What fits your needs?
1. **Generate ADRs** → Quick decision records (5-10 min) ⭐ Recommended
2. **Full component design** → Detailed implementation specs (1-2 hours)
3. **Technology deep-dive** → Specific guidance on chosen stack
4. **All set** → You have what you need

Your choice:

---

## Checkpoint Placement Rules

### When to Insert Checkpoints

1. **After every 50-100 lines of output**
   - Monitor line count during generation
   - Insert at natural break point (section boundary, paragraph end)
   - Never break tables, code blocks, or bullet lists mid-content

2. **At phase transitions**
   - Phase 1 → Phase 2: After requirements gathering
   - Phase 2 → Phase 2.5: Before generating comparison table
   - Phase 2.5 → Phase 3: After table, before detailed approaches
   - Phase 3 → Phase 4: After approach exploration
   - Phase 4 → Phase 5: After clarification
   - Phase 5 → Phase 6: Before detailed design (optional)

3. **After user-requested content**
   - User asks "show me [X]" → generate [X] → checkpoint
   - User selects approach from table → show approach → checkpoint mid-way

4. **Before context switches**
   - Switching from one approach to another
   - Moving from overview to details
   - Changing from technical to business perspective

### Checkpoint Options Guidelines

- **Limit to 2-4 options**: Too many choices = decision paralysis
- **Include common actions**: Continue, adjust, explain appear frequently
- **Contextual to current phase**: Options match what makes sense next
- **Default action**: Always offer "continue" as safest option
- **Custom requests**: Allow freeform text input beyond numbered choices

### Visual Formatting

- **Separator lines**: Use `---` before and after checkpoint block
- **Emoji marker**: Use 📍 for visual recognition
- **Bold actions**: Make option text bold for scannability
- **Arrow notation**: Use → to show outcome of each choice

## Template Constraints

- **Line count**: Checkpoint itself should be 8-12 lines (brief)
- **Option descriptions**: Keep to one line each (< 60 characters)
- **Recap**: Optional, only if needed for context (1-2 sentences max)
- **Consistency**: Always use same format for visual familiarity
