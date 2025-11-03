# Technical Requirements Analysis Workflow

## Overview

Transform Product Discovery Worksheets into comprehensive Technical Requirements Specifications using healthcare standards.

**Duration:** 90-120 minutes per feature
**Output:** Complete Technical Requirements Specification with FHIR mappings, workflows, events, and test scenarios

---

## Workflow Steps

### Step 1: Complete Document Review (MANDATORY)

Before completing ANY section:

1. Read the ENTIRE product requirements document thoroughly
2. Read the ENTIRE Platform Capabilities thoroughly
3. Read the ENTIRE FHIR Resources thoroughly
4. Identify and list:
   - The core problem being solved
   - The primary solution components
   - ALL workflows mentioned (main, additional, variations, edge cases)
   - What's marked as future/TBD (exclude from technical design)
   - All user types and their specific needs
   - Integration points and external dependencies
   - Performance expectations and constraints
5. Create a mental map of:
   - The technical boundaries of the solution
   - Required integrations and data flows
   - Security and compliance implications
   - Scalability requirements

**Validation Checklist**:
- [ ] Read entire product requirements document
- [ ] Read entire Platform Capabilities document
- [ ] Read entire FHIR Resources document
- [ ] Listed ALL workflows (main, additional, variations, edge cases)
- [ ] Identified every entity needing CRUD operations
- [ ] Mapped all user interactions to events
- [ ] Understood performance expectations
- [ ] Considered all relevant FHIR resources
- [ ] Thought through complete technical BPM workflow
- [ ] Identified security and compliance needs

---

### Step 2: Extract Workflows

Extract and expand ALL workflows:
- Document every workflow mentioned in product requirements (main, additional, future)
- Include workflow variations and edge cases as separate processes
- Create technical orchestration for each distinct path
- Don't consolidate similar workflows - keep them separate

**Validation Checklist**:
- [ ] Every process in "Main Workflow" sections captured
- [ ] Every process in "Additional Workflow" sections captured
- [ ] Every variation described in "Workflow Variations" captured
- [ ] Every decision path creating alternate flows captured
- [ ] Every error or exception path mentioned captured
- [ ] Every future/TBD workflow marked appropriately

---

### Step 3: Map Healthcare Standards

Think comprehensively about standards and patterns:
- Select appropriate FHIR resources for all data entities
- Choose relevant implementation guides
- Map to required coding systems
- Define integration patterns

**Validation Checklist**:
- [ ] All entities mapped to FHIR resources
- [ ] Implementation guides selected (US Core, Da Vinci, etc.)
- [ ] Coding systems mapped (ICD-10, CPT, NDC, etc.)
- [ ] Integration patterns defined (REST, events, batch, queues)

---

### Step 4: Derive Entity Events

Focus on important entity lifecycle events:
- Extract events directly stated in product requirements
- Derive create/update/delete events for key entities not captured elsewhere
- Focus on business-critical entities (e.g., notifications, preferences, documents)
- Skip routine CRUD operations that are standard
- Exclude detailed system events (health checks, startups)
- Exclude granular user interaction tracking

**Validation Checklist**:
- [ ] Every notification type from product requirements has event
- [ ] Key entity lifecycle events captured (not elsewhere)
- [ ] Critical business entity state changes documented
- [ ] Document/file operations included (if relevant)
- [ ] User preference changes included (if applicable)
- [ ] Avoided routine CRUD events
- [ ] Excluded system health events

---

### Step 5: Design Technical Solution

Transform product requirements into technical specifications:
- Convert user workflows into system orchestration
- Map data needs to specific services and APIs
- Translate performance expectations into SLAs
- Define security boundaries from access requirements
- Do not solution or identify technologies that have NOT been specified
- If there are no product requirements, do NOT try to guess on how to translate to technical requirements

**Validation Checklist**:
- [ ] User workflows converted to BPM orchestration
- [ ] Data needs mapped to services/APIs
- [ ] Performance SLAs defined
- [ ] Security boundaries defined
- [ ] Only specified technologies included
- [ ] No assumptions beyond product requirements

---

### Step 6: Create Test Scenarios

Generate comprehensive test scenarios:
- Cover all workflows with Gherkin scenarios
- Include critical failure paths
- Define testable acceptance criteria
- Specify error handling for each workflow

**Validation Checklist**:
- [ ] Test scenarios cover all workflows
- [ ] Test scenarios include critical failures
- [ ] Acceptance criteria are testable
- [ ] Error handling specified for each workflow

---

### Step 7: Document Technical Decisions

Use these markers consistently:
- **Not specified** - When information should exist but isn't provided
- **Not Applicable** - When the section doesn't apply
- **[Recommended]** - When suggesting best practices
- **[Inferred]** - When deriving from context
- **[Standard]** - When applying industry patterns
- **[Derived]** - When extracting implicit requirements

**Validation Checklist**:
- [ ] [Recommended] tags on technical suggestions
- [ ] [Inferred] tags on derived requirements
- [ ] [Derived] tags on implicit events
- [ ] "Not specified" used appropriately
- [ ] "Not Applicable" with specific reasons
- [ ] [Standard] tags on industry patterns

---

### Step 8: Final Quality Check

Before completing:
- Every workflow has its own process definition
- Every entity has complete CRUD events
- Every user action has corresponding events
- N/A sections have specific reasons
- Test scenarios cover all workflows
- Error handling specified for each workflow
- Focus maintained on MVP only
- All relevant FHIR resources considered
- Complete event catalog derived
- UI complexity identified
- Real-time requirements properly specified

**Final Validation Checklist**:
- [ ] Every workflow has process definition
- [ ] Every entity has CRUD events
- [ ] Every user action has events
- [ ] N/A sections have reasons
- [ ] Test scenarios complete
- [ ] Error handling specified
- [ ] MVP scope maintained
- [ ] FHIR resources comprehensive
- [ ] Event catalog complete
- [ ] UI complexity assessed
- [ ] Real-time requirements defined

---

## Clean Output Protocol

**DO NOT include in output:**
- Section instruction blocks or guidelines in asterisks/italics
- "Section Instructions:" headings
- "Guidelines:" blocks explaining what to include
- Complexity assessment guides or methodology
- Example entries marked "[Example]" or placeholder text
- Notes explaining how to complete tables
- Template usage instructions
- AI processing methodology explanations

**DO include in output:**
- All completed technical specification sections
- All filled-in tables with actual technical data
- FHIR resource mappings
- Workflow definitions with detailed steps
- Event schemas and consumer definitions
- Performance targets and scale projections
- Test scenarios in Gherkin format
- Clean, implementation-ready document

**Verification before output:**
- âœ… Section headers present
- âœ… Technical specifications with actual data
- âœ… Workflow orchestration details
- âœ… Event definitions
- âœ… Test scenarios
- âŒ No "Section Instructions:" text visible
- âŒ No "Guidelines:" blocks
- âŒ No "*Section Instructions:*" in italics
- âŒ No methodology explanations
- âŒ No template completion examples

---

## Common Pitfalls to Avoid

âŒ Consolidating similar workflows (keep separate)
âŒ Missing workflow variations or edge cases
âŒ Deriving routine CRUD events (focus on business-critical)
âŒ Including system health/startup events
âŒ Making assumptions beyond product requirements
âŒ Forgetting to tag technical recommendations
âŒ Including template instructions in final output
âŒ Creating technology solutions not specified in requirements
