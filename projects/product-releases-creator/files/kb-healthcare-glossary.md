# Healthcare Glossary v1.0

**Purpose**: Single source of truth for healthcare terminology. Reference when understanding requirements, building releases, or communicating with stakeholders.

**How to Use**: Alphabetical reference. If unsure what a term means, search here. For cross-referenced terms, follow the links.

---

## A

### **ACO** (Accountable Care Organization)
**Definition**: Network of healthcare providers (hospitals, physicians, specialists) who coordinate care for Medicare patients, sharing financial risk and rewards.

**In Context**: "Our solution integrates with ACO patient lists for population health management."

**Related**: Payer, Provider Network, Value-Based Care

---

### **Adjudication**
**Definition**: Insurance company's process of reviewing a claim to determine if it's valid, how much to pay, and whether to deny it.

**In Context**: "Claims get adjudicated by payer within 30 days."

**Related**: Claim, Denial, Prior Authorization

---

### **Affinity**
**Definition**: When one medication or treatment is preferred over another based on clinical evidence, payer policy, or cost. Often affects Prior Authorization requirements.

**In Context**: "This beta-blocker has higher affinity in the formulary, so PA might not be required."

**Related**: Formulary, Prior Authorization, Step Therapy

---

## B

### **Batch Processing**
**Definition**: Processing multiple records together in one operation (typically 2-20 items in healthcare context, not 100s).

**In Context**: "Release 3 adds batch processing so admins can submit 5-10 enrollments simultaneously."

**Related**: Bulk Operations, Workflow

---

### **Benefit Design**
**Definition**: Insurance plan's rules about what's covered, how much patients pay, and under what conditions (deductibles, copays, restrictions).

**In Context**: "The patient's benefit design requires Prior Authorization for specialty medications."

**Related**: Formulary, Insurance Plan, Prior Authorization

---

## C

### **Claim**
**Definition**: Request for payment submitted to insurance company for healthcare services provided.

**In Context**: "Medical office submits claim to insurance company. If approved, office gets paid."

**Related**: Adjudication, Denial, Claim Status

---

### **Clinical Indication**
**Definition**: Medical reason for prescribing a specific medication or treatment. Required for Prior Authorization justification.

**In Context**: "The PA requires clinical indication: 'Type 2 Diabetes Mellitus, inadequately controlled on metformin.'"

**Related**: Prior Authorization, Diagnosis Code, Medical Necessity

---

### **Coverage Determination**
**Definition**: Insurance company's decision about whether a medication or treatment is covered, may require PA or other conditions.

**In Context**: "The coverage determination for this biologic is 'Covered with Prior Authorization.'"

**Related**: Prior Authorization, Formulary, Benefit Design

---

### **CoPay**
**Definition**: Fixed amount patient pays for prescription or medical service (e.g., "$10 copay for generic drugs").

**In Context**: "Patient's insurance plan has a $25 copay for specialty medications."

**Related**: Coinsurance, Deductible, Patient Cost

---

### **Clinical Workflow**
**Definition**: Sequence of steps a physician follows to provide patient care (diagnosis, treatment selection, prescription, follow-up).

**In Context**: "The clinical workflow is: diagnosis → select medication → check formulary → prescribe → prescribe → track response."

**Related**: Workflow, Prior Authorization, E-Prescribing

---

## D

### **Denial**
**Definition**: Insurance company's decision to NOT pay for a claim or to deny a Prior Authorization request.

**In Context**: "PA denial reason: 'Prior medication therapy required per formulary.'"

**Related**: Appeal, Adjudication, Prior Authorization

---

### **Diagnosis Code**
**Definition**: Standard code (ICD-10) that identifies a disease or condition, required for insurance claims and PA.

**In Context**: "ICD-10 code E11.9 = Type 2 Diabetes Mellitus"

**Related**: ICD-10, Prior Authorization, Medical Necessity

---

### **Drug Interaction**
**Definition**: When two medications affect each other's efficacy or safety when taken together.

**In Context**: "Clinical decision support warns: 'Drug interaction detected: this medication + patient's current aspirin.'"

**Related**: Clinical Decision Support, Drug-Allergy, Contraindication

---

### **Drug-Allergy Contraindication**
**Definition**: When a medication is unsafe for a patient due to a known allergy.

**In Context**: "Clinical decision support alerts: 'Patient allergic to penicillin - this medication contains penicillin derivative.'"

**Related**: Drug Interaction, Allergy, Contraindication

---

## E

### **EHR** (Electronic Health Record)
**Definition**: Digital record of patient's medical history, diagnoses, medications, test results, and clinical notes.

**In Context**: "Our solution auto-populates enrollment forms by pulling patient data from EHR."

**Related**: EMR, FHIR, HL7, Integration

---

### **EMR** (Electronic Medical Record)
**Definition**: Digital record of patient medical information within a single practice (more limited than EHR).

**In Context**: "EHR is broader (across providers), EMR is a single practice's medical record."

**Related**: EHR, FHIR, HL7

---

### **E-Prescribing**
**Definition**: Electronic transmission of prescription from physician to pharmacy using standardized formats.

**In Context**: "E-Prescribing reduces errors and speeds delivery compared to handwritten scripts."

**Related**: NCPDP, Pharmacy, Prescription

---

### **Enrollment**
**Definition**: Process of registering a patient in a healthcare program (insurance plan, specialty pharmacy program, patient assistance program).

**In Context**: "Release 1: Single Enrollment Submission - admin can enroll patient in hub program."

**Related**: Patient, Program, Specialty Pharmacy

---

## F

### **FHIR** (Fast Healthcare Interoperability Resources)
**Definition**: Modern healthcare data standard (uses JSON/XML) for exchanging patient information between systems.

**In Context**: "Our integration uses FHIR API to pull patient data from EHR."

**Related**: HL7, NCPDP, API, Standards

---

### **Formulary**
**Definition**: Insurance company's list of covered medications organized by tier (generic = cheapest, brand = more expensive, specialty = most expensive). Determines if patient needs Prior Authorization.

**In Context**: "This medication is on formulary tier 2 (brand), so patient will need Prior Authorization to access."

**Related**: Tier, Prior Authorization, Coverage Determination

---

## G

### **Generic Medication**
**Definition**: Medication with same active ingredient, dosage, and form as brand-name drug but usually cheaper.

**In Context**: "Formulary prefers generic atorvastatin over brand-name Lipitor."

**Related**: Brand-Name, Formulary, Tier

---

## H

### **HL7** (Health Level 7)
**Definition**: International healthcare messaging standard for exchanging patient data between systems (older than FHIR).

**In Context**: "Legacy EHR system uses HL7 format, newer systems use FHIR."

**Related**: FHIR, NCPDP, API, Standards

---

### **Hub** (Specialty Pharmacy Hub)
**Definition**: Centralized platform where specialty pharmacy programs (copay assistance, enrollment, refills) are managed. Requires integration for enrollment submission.

**In Context**: "Release 1: Enroll patient in Pfizer patient assistance program via the hub."

**Related**: Specialty Pharmacy, Patient Assistance Program, Enrollment

---

## I

### **ICD-10** (International Classification of Diseases, 10th Revision)
**Definition**: Standard diagnosis code system used for insurance claims and prior authorizations.

**In Context**: "PA requires ICD-10 diagnosis codes: E11.9 (Type 2 Diabetes), I10 (Hypertension)."

**Related**: Diagnosis Code, Prior Authorization, Medical Necessity

---

### **Insurance Plan**
**Definition**: Health insurance product offered by payer with specific benefits, costs, and coverage rules.

**In Context**: "Patient's insurance plan is 'Blue Shield PPO - requires PA for specialty medications.'"

**Related**: Payer, Formulary, Benefit Design

---

## L

### **Line Item**
**Definition**: Single medication or service on a claim or prior authorization request.

**In Context**: "The PA has 3 line items: medication A, medication B, lab test."

**Related**: Claim, Prior Authorization

---

## M

### **Medical Necessity**
**Definition**: Clinical justification for why a medication or treatment is needed for a specific patient. Required for Prior Authorization.

**In Context**: "PA approval requires documented medical necessity: 'Patient failed on standard therapy.'"

**Related**: Prior Authorization, Clinical Indication, Diagnosis Code

---

## N

### **NCPDP** (National Council for Prescription Drug Programs)
**Definition**: Standard for pharmacy data exchange including prescriptions, claims, and prior authorizations.

**In Context**: "E-Prescribing systems use NCPDP standards for transmitting prescriptions to pharmacies."

**Related**: E-Prescribing, FHIR, HL7, Pharmacy

---

## P

### **PA** (Prior Authorization) - See **Prior Authorization**

---

### **Patient Assistance Program** (PAP)
**Definition**: Medication manufacturer's program providing free or reduced-cost medications to eligible patients.

**In Context**: "Release 2: Enable patient self-enrollment in Novartis Patient Assistance Program."

**Related**: Specialty Pharmacy, Enrollment, Hub

---

### **Payer**
**Definition**: Organization that pays healthcare bills (insurance company, government programs like Medicare/Medicaid, employer).

**In Context**: "Our solution integrates with 15 major payers for Prior Authorization submission."

**Related**: Insurance Plan, Prior Authorization, Claim

---

### **Pharmacy**
**Definition**: Business that dispenses medications. Specialty pharmacies focus on complex, high-cost medications.

**In Context**: "Patient fills prescription at local pharmacy or specialty pharmacy depending on medication type."

**Related**: Specialty Pharmacy, E-Prescribing, Prescription

---

### **PBM** (Pharmacy Benefit Manager)
**Definition**: Organization that manages prescription drug benefits for insurance companies and employers.

**In Context**: "The PBM manages the patient's insurance formulary and Prior Authorization process."

**Related**: Payer, Insurance Plan, Formulary

---

### **Prescription**
**Definition**: Written or electronic order from physician to pharmacy for patient medication.

**In Context**: "Physician writes prescription for atorvastatin, sends electronically to pharmacy via E-Prescribing."

**Related**: E-Prescribing, NCPDP, Pharmacy

---

### **Prior Authorization** (PA)
**Definition**: Insurance company's requirement to approve a medication BEFORE it's dispensed. Required for high-cost, brand-name, or specialty medications.

**In Context**: "Before patient can fill this biologic, office must get Prior Authorization from insurance company."

**Related**: Medical Necessity, Clinical Indication, Coverage Determination

---

### **Provider**
**Definition**: Healthcare professional or organization providing patient care (physician, specialist, hospital, clinic).

**In Context**: "Our solution integrates with provider EHR systems for enrollment submission."

**Related**: Physician, Healthcare Network, Practice

---

### **Provider Network**
**Definition**: Group of healthcare providers (physicians, specialists, hospitals) contracted with an insurance plan.

**In Context**: "Patient's insurance plan covers providers within the Blue Shield network."

**Related**: In-Network, Out-of-Network, Insurance Plan

---

## R

### **Refill**
**Definition**: Request to dispense additional quantity of previously prescribed medication.

**In Context**: "Patient requests refill of blood pressure medication - office can approve or deny per clinical guidelines."

**Related**: Prescription, Pharmacy, E-Prescribing

---

### **Revenue Cycle**
**Definition**: Process from patient encounter through claim submission, insurance payment, and patient billing.

**In Context**: "Our solution automates part of revenue cycle: claim submission and status tracking."

**Related**: Claim, Billing, Adjudication

---

## S

### **SMART on FHIR**
**Definition**: Security and authorization standard allowing apps to integrate securely with EHR systems without requiring separate login.

**In Context**: "Release 2: SMART on FHIR Encounter Launch - form auto-populates from EHR without leaving system."

**Related**: FHIR, EHR, OAuth2, API

---

### **Specialty Pharmacy**
**Definition**: Pharmacy specializing in high-cost, complex medications (biologics, oncology drugs, immunology) requiring special handling and patient support.

**In Context**: "Patient's specialty medication is dispensed through specialty pharmacy with enhanced counseling."

**Related**: Pharmacy, Hub, Patient Assistance Program

---

### **Specialty Medication**
**Definition**: Complex, high-cost medication typically biologics or injectable drugs requiring pharmacy support, patient monitoring, and often Prior Authorization.

**In Context**: "Release 1 targets specialty medications - these have highest PA requirements and costs."

**Related**: Specialty Pharmacy, Prior Authorization, Biologic

---

### **Step Therapy**
**Definition**: Insurance requirement to try less expensive medication first before approving more expensive alternative.

**In Context**: "Step Therapy requires patient to try generic atorvastatin before approving Crestor."

**Related**: Prior Authorization, Formulary, Generic, Brand-Name

---

## T

### **Tier** (Formulary Tier)
**Definition**: Insurance formulary's classification of medications by cost (Tier 1 = generic/cheap, Tier 2 = brand/expensive, Tier 3 = specialty/very expensive).

**In Context**: "Medication is Tier 3 specialty - higher copay and likely requires PA."

**Related**: Formulary, CoPay, Prior Authorization

---

### **Therapeutic Class**
**Definition**: Group of medications that treat similar conditions or have similar mechanisms.

**In Context**: "These statin medications are in the same therapeutic class - insurance typically requires trying cheapest one first."

**Related**: Medication, Formulary, Step Therapy

---

## U

### **USP** (Unified Service Platform)
**Definition**: Medication management platform integrating enrollment, prior authorization, refills, and patient support.

**In Context**: "Release 1: Submit specialty drug enrollment through USP platform."

**Related**: Hub, Specialty Pharmacy, Enrollment

---

## V

### **Value-Based Care**
**Definition**: Healthcare payment model where providers are paid based on patient outcomes rather than volume of services.

**In Context**: "ACO model is value-based - providers share risk and reward based on patient outcomes."

**Related**: ACO, Fee-for-Service, Healthcare Model

---

## W

### **Workflow**
**Definition**: Sequence of steps a person follows to accomplish a goal (administrative, clinical, or operational).

**In Context**: "Prior Authorization workflow: identify patient → search PA form → complete form → submit → track status."

**Related**: Process, Clinical Workflow, User Task

---

---

## Cross-Reference Index

### **Workflows**
- **Prior Authorization Workflow**: Prior Authorization → Medical Necessity → Clinical Indication → Claim → Adjudication → Denial (possibly)
- **Prescription Workflow**: Diagnosis → Clinical Indication → Formulary Check → Step Therapy → Prior Authorization (possibly) → E-Prescribing → Pharmacy → Refill
- **Enrollment Workflow**: Patient → Insurance Plan → Enrollment → Hub (possibly) → Program (Patient Assistance or Specialty Pharmacy)
- **Claims Workflow**: Healthcare Service → Claim → Adjudication → Coverage Determination → Payer (insurance company) → Payment

### **Insurance & Payment**
- **Insurance Company (Payer)** → Insurance Plan → Benefit Design → Formulary → Prior Authorization → Claim → Adjudication
- **Pharmacy Benefit Manager (PBM)** manages: Formulary, Prior Authorization, Adjudication for Payer
- **Provider** submits: Prescriptions (E-Prescribing), Claims, Prior Authorization Requests to Payer

### **Medications & Authorization**
- **Medication** → Therapeutic Class → Formulary Tier → Coverage Determination → Prior Authorization (possibly) → Medical Necessity (possibly)
- **Generic** (Tier 1) vs **Brand-Name** (Tier 2) vs **Specialty** (Tier 3)
- **Step Therapy**: Try Generic first → Try Brand-Name second → Approve Specialty if needed
- **Prior Authorization** requires: Clinical Indication + Medical Necessity + Diagnosis Code (ICD-10)

### **Healthcare Standards**
- **FHIR** / **HL7** / **NCPDP** = Data exchange standards between systems
- **SMART on FHIR** = Secure app integration with EHR
- **ICD-10** = Diagnosis codes
- **NDC** = Drug identifier codes

### **Data Exchange**
- **EHR** (full patient record) ← → **Provider** system via FHIR/HL7
- **E-Prescribing** (prescription data) ← → **Pharmacy** via NCPDP
- **Prior Authorization** (clinical data) ← → **Payer** via FHIR or proprietary APIs

---

## Quick Definition Reference

| Term | Quick Definition | Context |
|------|---|---|
| **ACO** | Network of providers sharing financial risk | Population health, value-based care |
| **Adjudication** | Insurance review of claim to determine payment | Claims processing |
| **Affinity** | Preferred medication in formulary | Prior Authorization |
| **Clinical Indication** | Medical reason for medication | Prior Authorization justification |
| **Coverage Determination** | Insurance decision if medication is covered | Prescription approval |
| **Denial** | Insurance refusal to pay or approve | Prior Authorization, Claims |
| **Diagnosis Code** | Standard code (ICD-10) for disease | Claims, Prior Authorization |
| **EHR** | Digital patient medical record | Integration, Data access |
| **E-Prescribing** | Electronic prescription transmission | Pharmacy, Clinical workflow |
| **Enrollment** | Register patient in program | Patient Assistance, Specialty Pharmacy |
| **FHIR** | Modern healthcare data standard (JSON/XML) | API integration |
| **Formulary** | Insurance list of covered medications | Prior Authorization, Tier |
| **Hub** | Specialty pharmacy enrollment platform | Enrollment, Patient Assistance |
| **ICD-10** | Diagnosis code system | Prior Authorization, Medical necessity |
| **Medical Necessity** | Clinical justification for medication | Prior Authorization |
| **NCPDP** | Pharmacy data exchange standard | E-Prescribing |
| **Payer** | Organization paying healthcare bills | Insurance, Claims |
| **Prior Authorization** | Insurance approval required BEFORE dispensing | High-cost, specialty medications |
| **Prescription** | Physician order for patient medication | E-Prescribing, Pharmacy |
| **Provider** | Healthcare professional or organization | EHR integration |
| **Specialty Pharmacy** | Pharmacy for complex, high-cost medications | Specialty drugs, Patient support |
| **Step Therapy** | Try cheaper medication before expensive | Prior Authorization, Formulary |
| **Tier** | Formulary medication classification by cost | Copay, Prior Authorization |

---

## When to Reference This Glossary

Use this glossary when you:
- Read product requirements with unfamiliar healthcare terms
- Discuss features with stakeholders
- Write release descriptions or hypothesis statements
- Define scope exclusions
- Build technical integrations
- Validate user-facing terminology
- Train product and engineering teams

**Example Usage**:
```
"Requirements mention 'Prior Authorization workflow for specialty medications.'

Check Glossary:
- Prior Authorization = Insurance approval required before prescription
- Specialty Medication = Complex, high-cost drugs requiring pharmacy support
- Medical Necessity = Clinical justification for why medication is needed

Now I understand: We're helping offices get insurance approval for expensive drugs."
```
