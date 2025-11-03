# Guide: FHIR Resource Mapping for Healthcare Requirements

This guide helps you map business entities to appropriate FHIR resources when transforming product requirements into technical specifications.

---

## The Challenge

Product requirements describe business entities in plain language. Technical specifications must map these entities to standard FHIR resources.

**Product Requirement**: "Care coordinators need to track prior authorization requests for procedures and medications."

**Technical Mapping Needed**:
- Prior authorization request → **FHIR CoverageEligibilityRequest** or **ServiceRequest**?
- Care coordinator → **FHIR Practitioner** or **PractitionerRole**?
- Tracking → **FHIR Task** or **Workflow** resource?

This guide helps you make these decisions systematically.

---

## Step-by-Step Mapping Process

### Step 1: Identify Entities in Product Requirements

Read the PRD and list all nouns that represent data:

**Example PRD**: "Patients submit enrollment forms through the portal. Care coordinators review forms and approve or reject them. The system sends notifications when status changes."

**Entities Found**:
- Patient
- Enrollment form
- Care coordinator
- Notification
- Status

---

### Step 2: Classify Entity Type

Classify each entity:

| Entity Type | Description | Example Entities |
|-------------|-------------|------------------|
| **Person** | People in the system | Patient, Practitioner, Care Coordinator, Administrator |
| **Clinical** | Clinical observations and assessments | Diagnosis, Vital Sign, Lab Result, Allergy |
| **Administrative** | Scheduling, billing, coverage | Appointment, Claim, Coverage, Eligibility |
| **Workflow** | Tasks, requests, orders | Task, ServiceRequest, MedicationRequest, CommunicationRequest |
| **Document** | Documents and forms | DocumentReference, Consent, Questionnaire, QuestionnaireResponse |
| **Organization** | Organizations and locations | Organization, Location, HealthcareService |

**Example Classification**:
- Patient → **Person**
- Enrollment form → **Document**
- Care coordinator → **Person**
- Notification → **Workflow**
- Status → **Workflow** (part of Task resource)

---

### Step 3: Select FHIR Resource

Use this decision tree:

#### For Person Entities

```
Is it a patient/member/consumer?
  → YES: Patient

Is it a healthcare provider (doctor, nurse, care coordinator)?
  → YES: Is it describing the person or their role?
      → Person: Practitioner
      → Role: PractitionerRole

Is it a family member or contact?
  → YES: RelatedPerson
```

**Common Mappings**:
- Patient, Member, Consumer → **Patient**
- Doctor, Nurse, Care Coordinator → **Practitioner** (person) + **PractitionerRole** (role)
- Family Member, Emergency Contact → **RelatedPerson**

---

#### For Clinical Entities

```
Is it a diagnosis or problem?
  → YES: Condition

Is it a measurement (vital sign, lab result)?
  → YES: Observation

Is it a medication?
  → YES: Is it a request/order or a record of administration?
      → Request/Order: MedicationRequest
      → Record: MedicationStatement or MedicationAdministration

Is it an allergy or intolerance?
  → YES: AllergyIntolerance

Is it a procedure?
  → YES: Is it a request/order or a record?
      → Request/Order: ServiceRequest
      → Record: Procedure
```

**Common Mappings**:
- Diagnosis, Problem, Condition → **Condition**
- Vital Sign, Lab Result, Assessment → **Observation**
- Medication Order → **MedicationRequest**
- Allergy → **AllergyIntolerance**
- Procedure Order → **ServiceRequest**

---

#### For Administrative Entities

```
Is it related to scheduling?
  → YES: Is it an appointment or slot availability?
      → Appointment: Appointment
      → Availability: Schedule + Slot

Is it related to insurance/coverage?
  → YES: What aspect?
      → Coverage details: Coverage
      → Eligibility check: CoverageEligibilityRequest + CoverageEligibilityResponse
      → Prior authorization: ServiceRequest or CoverageEligibilityRequest

Is it related to billing/claims?
  → YES: What aspect?
      → Claim: Claim
      → Payment: ClaimResponse
      → Invoice: Invoice
```

**Common Mappings**:
- Appointment → **Appointment**
- Insurance Coverage → **Coverage**
- Eligibility Check → **CoverageEligibilityRequest** + **CoverageEligibilityResponse**
- Prior Authorization → **ServiceRequest** (procedure/med request) or **CoverageEligibilityRequest** (coverage check)
- Claim → **Claim**

---

#### For Workflow Entities

```
Is it a generic task or work item?
  → YES: Task

Is it a request for a service?
  → YES: What type of service?
      → Clinical procedure: ServiceRequest
      → Medication: MedicationRequest
      → Lab test: ServiceRequest (with lab category)
      → Communication/notification: CommunicationRequest

Is it a communication or message?
  → YES: Communication
```

**Common Mappings**:
- Task, Work Item, To-Do → **Task**
- Service Request, Procedure Order → **ServiceRequest**
- Notification Request → **CommunicationRequest**
- Message, Alert → **Communication**

---

#### For Document Entities

```
Is it a form to be filled out?
  → YES: Is it the template or a completed response?
      → Template: Questionnaire
      → Completed: QuestionnaireResponse

Is it a document or file?
  → YES: DocumentReference

Is it a consent form?
  → YES: Consent

Is it a care plan or protocol?
  → YES: CarePlan or PlanDefinition
```

**Common Mappings**:
- Form Template → **Questionnaire**
- Completed Form → **QuestionnaireResponse**
- Document, File, Attachment → **DocumentReference**
- Consent Form → **Consent**
- Care Plan → **CarePlan**

---

### Step 4: Select Implementation Guide and Profile

After selecting the FHIR resource, choose the appropriate profile:

| Implementation Guide | Purpose | When to Use |
|---------------------|---------|-------------|
| **US Core** | Foundation for US healthcare | Always use for core resources (Patient, Practitioner, Observation, etc.) |
| **Da Vinci** | Payer-provider interoperability | Use for prior auth, coverage, claims, payer workflows |
| **SMART on FHIR** | App authorization | Use for patient/provider app access |
| **IPA (International Patient Access)** | Patient access | Use for patient-facing apps (international) |
| **HL7 Base FHIR** | No profile constraints | Only when no US Core or Da Vinci profile exists |

**Example**:
- Patient entity → **Patient** resource → **US Core Patient** profile
- Prior authorization → **ServiceRequest** resource → **Da Vinci PAS ServiceRequest** profile
- Vital sign → **Observation** resource → **US Core Vital Signs** profile

---

### Step 5: Identify Coding Systems

Map coded fields to standard terminologies:

| Field Type | Coding System | Example |
|------------|---------------|---------|
| Diagnosis | ICD-10-CM | Diabetes Type 2 → E11.9 |
| Procedure | CPT, HCPCS | Office visit → 99213 |
| Medication | RxNorm | Metformin 500mg → 860975 |
| Lab test | LOINC | Glucose [Mass/volume] in Blood → 2339-0 |
| Vital sign | LOINC | Body weight → 29463-7 |
| Clinical observation | SNOMED CT | Fever → 386661006 |

---

## Real-World Mapping Examples

### Example 1: Prior Authorization Workflow

**Product Requirement**:
"Care coordinators submit prior authorization requests for procedures and medications. The system checks if authorization is required based on the patient's coverage. Requests are sent to the patient's insurance company for review. The system tracks status (pending, approved, denied) and notifies care coordinators when status changes."

**Entity Mapping**:

| Entity | FHIR Resource | Profile | Rationale |
|--------|---------------|---------|-----------|
| Prior Authorization Request | ServiceRequest | Da Vinci PAS ServiceRequest | Represents the procedure/medication request requiring authorization |
| Patient Coverage | Coverage | US Core Coverage | Stores patient's insurance information |
| Coverage Check | CoverageEligibilityRequest + Response | Da Vinci COV | Checks if authorization required |
| Status Tracking | Task | FHIR Base Task | Tracks prior auth workflow state (pending, approved, denied) |
| Notification | Communication | FHIR Base Communication | Records notification sent to care coordinator |
| Care Coordinator | Practitioner + PractitionerRole | US Core Practitioner + PractitionerRole | Person and role |
| Patient | Patient | US Core Patient | Patient demographics |

---

### Example 2: Patient Enrollment Workflow

**Product Requirement**:
"Patients complete an enrollment form with demographics, insurance, and consent. Care coordinators review forms for completeness. The system validates insurance eligibility and creates the patient record."

**Entity Mapping**:

| Entity | FHIR Resource | Profile | Rationale |
|--------|---------------|---------|-----------|
| Enrollment Form (template) | Questionnaire | FHIR Base Questionnaire | Form definition with questions |
| Completed Enrollment Form | QuestionnaireResponse | FHIR Base QuestionnaireResponse | Patient's answers |
| Patient Record | Patient | US Core Patient | Demographics from form |
| Insurance Info | Coverage | US Core Coverage | Insurance details from form |
| Consent | Consent | FHIR Base Consent | Patient consent for data sharing |
| Review Task | Task | FHIR Base Task | Care coordinator's review task |
| Eligibility Check | CoverageEligibilityRequest + Response | Da Vinci COV | Validates insurance |

---

### Example 3: Medication Synchronization

**Product Requirement**:
"Patients view their current medications from their doctor's EHR. Patients can request refills. Pharmacy receives refill requests and updates status."

**Entity Mapping**:

| Entity | FHIR Resource | Profile | Rationale |
|--------|---------------|---------|-----------|
| Current Medication | MedicationStatement | US Core MedicationStatement | Patient's current medication list |
| Refill Request | MedicationRequest | US Core MedicationRequest | Request for refill |
| Medication | Medication | US Core Medication | Medication details (RxNorm code) |
| Patient | Patient | US Core Patient | Patient demographics |
| Prescriber | Practitioner + PractitionerRole | US Core | Prescribing provider |
| Pharmacy | Organization | US Core Organization | Pharmacy details |

---

## Common Mapping Mistakes

### Mistake 1: Confusing ServiceRequest and Procedure ❌

**Problem**: Using **Procedure** when **ServiceRequest** is correct

**Rule**:
- **ServiceRequest**: Request/order for a procedure (future event)
- **Procedure**: Record of a procedure that happened (past event)

**Example**:
- Prior authorization for surgery → **ServiceRequest** ✅
- Record of surgery performed → **Procedure** ✅

---

### Mistake 2: Not Using US Core Profiles ❌

**Problem**: Using base FHIR resources without US Core constraints

**Solution**: Always use US Core profiles for core resources

**Example**:
- Patient → **US Core Patient** ✅ (not base Patient)
- Observation → **US Core Observation** or **US Core Vital Signs** ✅
- MedicationRequest → **US Core MedicationRequest** ✅

---

### Mistake 3: Using Custom Resources Instead of Extensions ❌

**Problem**: Creating custom resources for additional data

**Solution**: Use FHIR extensions on standard resources

**Example**:
- ❌ Custom "PatientPreferences" resource
- ✅ Patient resource with custom extension for preferences

---

### Mistake 4: Wrong Practitioner Representation ❌

**Problem**: Confusing **Practitioner** (person) with **PractitionerRole** (job)

**Rule**:
- **Practitioner**: The person (name, NPI, contact info)
- **PractitionerRole**: Their role at an organization (cardiologist at Hospital X)

**Example**:
- Dr. Jane Smith (person) → **Practitioner**
- Dr. Smith working as Cardiologist at Hospital X → **PractitionerRole**

---

### Mistake 5: Overusing Task Resource ❌

**Problem**: Using **Task** for everything workflow-related

**Solution**: Use specific request resources when appropriate

**Example**:
- ❌ Task for "Request lab test" → Use **ServiceRequest** (category=laboratory)
- ❌ Task for "Send notification" → Use **CommunicationRequest**
- ✅ Task for generic work item (review form, approve document) → Use **Task**

---

## Mapping Validation Checklist

Before finalizing FHIR resource mappings, verify:

### Resource Selection
- [ ] Every entity in PRD mapped to FHIR resource
- [ ] Correct resource selected using decision tree
- [ ] No custom resources (unless absolutely necessary)
- [ ] Request vs Record distinction correct (ServiceRequest vs Procedure, etc.)

### Profile Selection
- [ ] US Core profiles used for core resources
- [ ] Da Vinci profiles used for payer workflows
- [ ] Profile constraints meet requirements
- [ ] Profile supported by Aidbox (if using Aidbox)

### Coding Systems
- [ ] Diagnoses use ICD-10-CM
- [ ] Procedures use CPT or HCPCS
- [ ] Medications use RxNorm
- [ ] Lab tests use LOINC
- [ ] Clinical observations use SNOMED CT (when appropriate)

### Operations
- [ ] CRUD operations specified (Create, Read, Update, Delete, Search)
- [ ] Search parameters identified
- [ ] Required vs optional operations documented

---

## Quick Reference Table

### Common Entity → FHIR Resource Mappings

| Business Entity | FHIR Resource | Profile | Coding System |
|-----------------|---------------|---------|---------------|
| Patient | Patient | US Core Patient | - |
| Provider | Practitioner + PractitionerRole | US Core | NPI |
| Diagnosis | Condition | US Core Condition | ICD-10-CM |
| Medication Order | MedicationRequest | US Core MedicationRequest | RxNorm |
| Lab Result | Observation | US Core Lab | LOINC |
| Vital Sign | Observation | US Core Vital Signs | LOINC |
| Appointment | Appointment | FHIR Base | - |
| Prior Auth | ServiceRequest | Da Vinci PAS | CPT, HCPCS |
| Coverage | Coverage | US Core Coverage | - |
| Eligibility Check | CoverageEligibilityRequest/Response | Da Vinci COV | - |
| Form Template | Questionnaire | FHIR Base | - |
| Completed Form | QuestionnaireResponse | FHIR Base | - |
| Document | DocumentReference | US Core DocumentReference | LOINC (document type) |
| Consent | Consent | FHIR Base | - |
| Task | Task | FHIR Base | - |
| Notification | Communication | FHIR Base | - |

---

## Advanced Mapping Scenarios

### Scenario 1: Prior Authorization - ServiceRequest or CoverageEligibilityRequest?

**Question**: "Should prior authorization use ServiceRequest or CoverageEligibilityRequest?"

**Answer**: It depends on the workflow:

**Use ServiceRequest (Da Vinci PAS)**:
- When requesting authorization for a specific procedure or medication
- When you need to submit clinical details (diagnosis, procedure codes, etc.)
- When payer needs to review and approve/deny
- Example: "Request authorization for knee surgery"

**Use CoverageEligibilityRequest (Da Vinci COV)**:
- When checking if authorization is required (not requesting authorization)
- When validating coverage for a service
- Example: "Is prior auth required for this procedure?"

**Best Practice**: Use both:
1. CoverageEligibilityRequest first (check if auth required)
2. ServiceRequest second (submit authorization request if required)

---

### Scenario 2: Workflow State - Task or Custom Resource?

**Question**: "Should workflow state use Task resource or custom tracking?"

**Answer**: Use **Task** for most workflows:

**Task is appropriate when**:
- Workflow has discrete steps
- Human tasks required (review, approve, reject)
- Status tracking needed (pending, in-progress, completed, failed)
- Multiple actors involved

**Example**:
```
Prior Authorization Workflow:
- Task 1: Care coordinator submits request
- Task 2: Payer reviews request
- Task 3: Care coordinator notified of decision

Main Task (parent):
  - status: in-progress
  - owner: Payer

Sub-Task 1 (child):
  - status: completed
  - owner: Care Coordinator

Sub-Task 2 (child):
  - status: in-progress
  - owner: Payer Reviewer
```

---

### Scenario 3: Notifications - Communication or CommunicationRequest?

**Question**: "Should notifications use Communication or CommunicationRequest?"

**Answer**: It depends on timing:

**Use CommunicationRequest**:
- When requesting a notification be sent (future event)
- Example: "Send notification when status changes"

**Use Communication**:
- When recording a notification that was sent (past event)
- Example: "Notification sent to care coordinator at 2:30pm"

**Best Practice**: Use both:
1. CommunicationRequest (request to send notification)
2. Communication (record of sent notification, references CommunicationRequest)

---

## Summary

**The Process**:
1. Identify entities in PRD (nouns representing data)
2. Classify entity type (Person, Clinical, Administrative, Workflow, Document)
3. Select FHIR resource using decision tree
4. Select implementation guide and profile (US Core, Da Vinci, etc.)
5. Identify coding systems (ICD-10, CPT, RxNorm, LOINC, SNOMED CT)
6. Validate mapping with checklist

**The Goal**: Map every business entity to a standard FHIR resource with appropriate profile and coding system.

**The Test**: Can you explain why you chose each FHIR resource, profile, and coding system?

If yes → mapping is complete ✅

If no → review decision tree and examples 🔄
