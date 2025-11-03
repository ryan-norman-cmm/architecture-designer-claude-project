### Summary
*Section Instructions: Provide a quick snapshot of the initiative's scale and moving parts before diving into details.*

- **User Roles**: [# total] (List roles briefly)
- **UI Screens/Components**: [# total]
- **Key Workflows**: [# total] (e.g., X MVP)
- **Internal Services**: [# total] (List key services)
- **External Integrations**: [# total] (List partners/vendors)

### Missing Requirements
*Section Instructions: List all requirements that are missing required to fully complete template, frame each as a question to be answered by a product manager. Don't try to answer any of the messing requirement questions*

| Missing Requirement | Answer | Answered By | Answered On |
|---------------------|------------------|----------------------|------------|
| [How many users will we expect?] |  |  |  |
| [Will the integration be a real-time API or batch file?] |  |  |  |
| [Requirement question] |  |  |  |

## Problem & Solution

### Problem Statement
*Section Instructions: Synthesize the primary problem from the BRD's problem statement. Include all pain points explicitly mentioned. Quantify impacts when provided. Identify and list the major solution capabilities as distinct bullet points. Avoid generic descriptions; focus on large, distinct capabilities that a product manager would need to plan for*

In one succinct paragraph, describe the problem we're solving: [Write as if explaining to a customer who knows nothing about our internal systems. Include all pain points mentioned in source documents.]

**Who has this problem and how painful is it?**
- **Primary sufferer**: [Describe role and time/cost impact - only include quantified impacts if provided in source documents]
- **Secondary impact**: [Who else is affected and how]

### Solution Overview
Describe the solution in plain English: [What will users be able to do that they can't do today?]

- **User-Facing Capabilities** [List what users will experience or be able to do]
- **Core Services** [List foundational components that enable the solution (at a product level, not low-level infrastructure)]

### Assumptions
- [High-impact assumption 1 - scope limitation or architectural constraint]
- [High-impact assumption 2 - integration or data boundary]
- [Optional third assumption if absolutely critical]

**Guidelines:**
- Only include assumptions that significantly impact technical design or effort estimation
- Focus on what is NOT included rather than what IS included
- Limit to 1-2 generated assumptions, maximum of 3 total
- Human reviewers can add clarifications here during requirements validation
- Examples: data migration scope, integration boundaries, workflow coverage, infrastructure dependencies

### Success Metrics

*Instructions for Quality Metrics: Success Indicator should be a clear user or business outcome (not a feature). Leading Indicators are early signals you can track and influence (user behavior, adoption). Lagging Indicators are final proof of success (business outcomes, satisfaction). Use "Not specified" when BRD doesn't provide measurable targets.*

| Success Indicator | Leading Indicators | Lagging Indicators |
|------------------|-------------------|-------------------|
| [Clear user/business outcome we're driving toward] | [Early signals we can monitor and influence - user behaviors, feature adoption] | [Final proof points of success - business outcomes, user satisfaction] |
| [Clear user/business outcome we're driving toward] | [Early signals we can monitor and influence - user behaviors, feature adoption] | [Final proof points of success - business outcomes, user satisfaction] |

## 2. Users & Stakeholders

*Section Instructions: Define all user types mentioned (use industry common terminology). Note internal vs. external users. Capture usage frequency if provided. Extract from explicit statements only - don't assume user needs not documented. For Network Category, this should be Provider (for physicians and staff), Pharmacy, Pharma (for field teams and hub agents), Payer, Patient, or CoverMyMeds for internal users. Please identify unique roles and document separately based on key responsibility, e.g., Physician vs Office Staff, Patient vs CareGiver, Field Team Representative vs Hub Agent*

### User Roles & Goals
Define ALL user types mentioned in source documents, including those marked as "TBD" or uncertain

| User Type | What They Need To Do | Anticipated User Volume | Usage Frequency | Network Category |
|-----------|---------------------|-------------------|---------------------------|-----------------|------------------|
| [Role name] | [Primary responsibilities and tasks - list all mentioned] | [Approximate number or "Not specified"] | [Approximate number or "Not specified"] | [Frequency or "Not specified"] | [Provider/Pharmacy/Pharma/Payer/Patient/CoverMyMeds] |
| [Role name] | [Primary responsibilities and tasks - list all mentioned] | [Approximate number or "Not specified"] | [Approximate number or "Not specified"] | [Frequency or "Not specified"] | [Provider/Pharmacy/Pharma/Payer/Patient/CoverMyMeds] |

## Access & Permissions

*Section Instructions: Extract from user descriptions and workflow steps. Document what users can and cannot do. If one user role has permission but the other does not, ensure it as added to "Cannot Do".  Use "Not specified" for unclear permissions.*

### User Access Matrix
Based on user types defined above

| User Type | Can Do | Cannot Do |
|-----------|--------|-----------|
| [User Type from above] | [Allowed action 1]; [Allowed action 2]; [Mark as "Not fully specified" if incomplete] | [Restricted action 1]; [Restricted action 2]; [Mark as "Not specified" if unknown] |
| [User Type from above] | [Allowed action 1]; [Allowed action 2]; [Mark as "Not fully specified" if incomplete] | [Restricted action 1]; [Restricted action 2]; [Mark as "Not specified" if unknown] |

## User Interface Requirements

*Section Instructions: Only document screens and components explicitly described. Determine if user interface will be standalone screen or component on another screen. Note data elements and their sources. Identify complex interactions mentioned. Don't create screens or components not referenced. Document frequency of usage of screen or component.*

### Screen Inventory
For each major screen/page mentioned in workflows and requirements

| Screen Name | Type | Purpose | Users |
|-------------|------|---------|-------|
| [Screen Name] | [Screen\|Component] | [What this screen accomplishes] | [Which user types from Users section will use this] |
| [Screen Name] | [Screen\|Component] | [What this screen accomplishes] | [Which user types from Users section will use this] |

### Screen Details
For each screen above, provide detailed breakdown:

#### Screen: [Screen Name]

**Data Displayed:**

| Data Element | Description |
|--------------|-------------|
| [Patient address] | [Brief description of data element] |
| [List of Insurance plans] | [Brief description of data element] |
| [Medication price] | [Brief description of data element] |
| [Notification summary] | [Brief description of data element] |
| [Read status] | [Brief description of data element] |
| [Subject patient name] | [Brief description of data element] |
| [Urgent flag] | [Brief description of data element] |

**User Actions:**

| Action | Description |
|--------|-------------|
| [Submit request] | [What this action accomplishes] |
| [Save draft] | [What this action accomplishes] |
| [Cancel] | [What this action accomplishes] |
| [Navigate to patient details] | [What this action accomplishes] |
| [Bulk approve] | [What this action accomplishes] |

*Repeat for each screen*

## Workflows & Processes

*Section Instructions: Document each workflow with defined steps focused on what the user experiences vs a software system. Identify decision points and branches. List workflows mentioned but not detailed in TBD section. IMPORTANT: Capture ALL workflows mentioned in source documents, not just the primary happy path.*

### Workflow Definitions

| Workflow Name | Frequency | Volume | Starting Point | Success Endpoint |
|---------------|-----------|--------|----------------|------------------|
| [Workflow Name] | [How often this occurs or "Not specified"] | [Expected # per day/week/month or "Not specified"] | [What triggers this process?] | [What indicates success?] |
| [Workflow Name] | [How often this occurs or "Not specified"] | [Expected # per day/week/month or "Not specified"] | [What triggers this process?] | [What indicates success?] |

### Workflow Steps Detail
*Section Instructions: The following section must contain the same number of workflow breakdowns as rows as workflow definitions*

For each workflow above, detail the steps a user will take to complete the process:

#### Workflow #1: [Workflow Name]

| Step | Action | Who Does This |
|------|--------|---------------|
| 1 | [Action taken] | [Role from Users section] |
| 2 | [Action taken] | [Role from Users section] |

#### Workflow #2: [Workflow Name]
*[Repeat table structure for each workflow]*

### Decision Points
Where do users need to make choices?

| Decision | Information Needed | Outcomes | Decision Maker |
|----------|-------------------|----------|----------------|
| [Decision description] | [Data required or "Not specified"] | [What happens] | [User role] |
| [Users preferred notification channel] | [User communication preferences] | [Send SMS, send email, create in-app notification, do nothing] | [Physician & Office Staff] |
| [Initiate PA] | [Coverage requirements, alternative medications] | [Start PA, switch drugs, do nothing] | [Office staff] |


## Services & Integration Points

*Section Instructions: List all systems mentioned as data sources or providing actions. Separate CMM internal services using CMM Product Services & Platform Capabilities document vs external/legacy systems. Only list out external services critical to this feature. Note medical coding systems referenced. Identify real-time requirements stated. Identify if the system is just emitting events for consumption. For internal services, don't list "What We Need From Them" if data doesn't need to be accessed again after event consumed. Internal services should follow this naming structure "[Business Domain Name] Service". Document batch processing needs mentioned.*

Technical touchpoints identified from requirements

### CMM Service Dependencies
What internal services are involved?

| Service | What We Need From Them | Actions We Ask Them To Do |
|---------|----------------------|--------------------------|
| [Service name] | [Data consumed] | [Actions requested] |
| [Service name] | [Data consumed] | [Actions requested] |
| [Service name] | [Data consumed] | [Actions requested] |

### External Partners & Systems
What external companies/systems are critical to this feature?

| Partner | What We Send Them | What They Send Us | Workflow Blocked if Unavailable? | How we send data | How we consume data |
|---------|------------------|------------------|--------------------------------|-----------------|-------------------|
| [Partner name] | [Data/requests sent] | [Data/responses received] | [Yes/No/Partial] | [Real-time API] | [Real-time API] |
| [Drug Pricing Partner] | [Not applicable] | [Drug Pricing CSV File] | [Yes/No/Partial] | [Not applicable] | [Batch file] |

## Requirements Priority

*Section Instructions: Strictly follow document's priority markers. Items marked "MVP" go in In-Scope Requirements section. Items marked "Future" and "TBD" go in Future Capabilities. Items marked "TBD" go in TBD section.*

### In Scope Requirements

| Requirement | Description |
|-------------|-------------|
| [Core capability required for launch] | [Brief description of what this enables] |
| [Core capability required for launch] | [Brief description of what this enables] |


### Future Capabilities

| Requirement | Description | Potential Value |
|-------------|-------------|-----------------|
| [Ideal future capability] | [Brief description] | [Potential benefit] |
| [Ideal future capability] | [Brief description] | [Potential benefit] |


## Risks & Dependencies
- **Business risks**: [List any mentioned business concerns]
- **Dependencies**: [List any mentioned dependencies on external partners]

## 10. Appendix

### Key Terms

| Term | Definition | Context |
|------|------------|---------|
| [Term] | [Plain English definition] | [Where this term is used in requirements] |
| [Term] | [Plain English definition] | [Where this term is used in requirements] |
