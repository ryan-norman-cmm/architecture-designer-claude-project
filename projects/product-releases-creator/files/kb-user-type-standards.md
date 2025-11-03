# User Type Standards v1.0

**Purpose**: Detailed standards for each user type to ensure releases meet the correct expectations and constraints.

**When to use**: When identifying the primary user for a release and determining what standards apply.

---

## Quick Reference: Standards by User Type

```
WHO is the primary user?

├─ PHYSICIAN (prescribing, diagnosing, clinical decisions)
│  ├─ Standards: ZERO TOLERANCE
│  ├─ WoZ Allowed: NO (never, under any circumstance)
│  ├─ Read-Only Allowed: Information only (not action workflows)
│  ├─ Manual Steps: NEVER
│  ├─ Incomplete Features: NOT ACCEPTABLE
│  ├─ Release Size: 2-3 weeks typical
│  └─ Must Include: Complete automation, safety checks, integrations
│
├─ ADMINISTRATOR (billing, scheduling, PA admin, enrollment, user management)
│  ├─ Standards: STRATEGIC FLEXIBILITY
│  ├─ WoZ Allowed: YES (if 100% invisible to user)
│  ├─ Read-Only Allowed: YES (if viewing IS complete workflow)
│  ├─ Manual Steps: Only if invisible backend + professional UX
│  ├─ Incomplete Features: Acceptable if documented scope
│  ├─ Release Size: 1.5-2.5 weeks typical
│  └─ Can Use: WoZ validation, professional SaaS UX, read-only monitoring
│
└─ INTERNAL (system config, monitoring, technical operations, admins)
   ├─ Standards: MAXIMUM FLEXIBILITY
   ├─ WoZ Allowed: YES (even if visible, if documented)
   ├─ Read-Only Allowed: YES (widely acceptable)
   ├─ Manual Steps: OK if documented
   ├─ Incomplete Features: Acceptable if communicated
   ├─ Release Size: 1-2 weeks typical
   └─ Can Accept: Technical complexity, manual processes, read-only views
```

---

## User Type 1: Physician

### **Identifying Physician Users**

Physician users are clinical decision-makers who:
- **Prescribe medications** (E-prescribing, medication selection)
- **Diagnose patients** (clinical decision support, diagnosis documentation)
- **Order treatments** (referrals, procedures, care plans)
- **Document clinical encounters** (notes, assessments, plans)
- **Make clinical judgments** (medication approval, treatment selection)

**Key Indicator**: If the workflow involves clinical decision-making (not just data entry), user is likely Physician.

### **Physician Standards: Zero Tolerance**

Physicians require the **highest standard of automation and completeness**. This reflects:
- Clinical liability (errors in prescribing have patient safety implications)
- Physician workflow efficiency (time is critical, interruptions are costly)
- Professional expectations (physicians expect production-ready software)
- Regulatory requirements (clinical workflows must be auditable and complete)

#### **What's Mandatory for Physician Releases**

✅ **Complete Automation**
- Workflow is 100% automated end-to-end
- NO manual steps, no "copy and paste", no "please email"
- User can accomplish entire clinical task without leaving system

✅ **Clinical Safety Checks**
- Drug-drug interaction checking
- Drug-allergy contraindication warnings
- Dosage calculation and validation
- Clinical decision support (formulary, guidelines)
- Audit trail for clinical decisions

✅ **Prescription Routing & Integration**
- Automatic prescription submission to pharmacy
- Status tracking and confirmation numbers
- Refill management and recall capability
- Electronic signature and audit compliance

✅ **Production-Ready Quality**
- No "beta" or "pilot" labeling (users expect production quality)
- Performance optimized (fast response times)
- Error handling (clear error messages, recovery paths)
- Mobile-ready (physicians use phones/tablets in clinical settings)

✅ **Compliance & Auditing**
- HIPAA compliance built-in
- Audit logs of all clinical actions
- Regulatory documentation (DEA, state pharmacy board requirements)
- Version history of prescriptions

#### **What's Forbidden for Physician Releases**

❌ **NO Wizard of Oz** (even invisible)
- Manual backend work, even if invisible, violates trust
- Physicians expect automation, not hidden manual processes
- Example: "System shows 'Submitted' but ops team manually submits to pharmacy" = NOT ACCEPTABLE

❌ **NO Read-Only Action Workflows**
- Cannot view-only a prescription without ability to modify/submit
- Cannot view-only a referral without ability to route/approve
- View-only IS acceptable for: history, status, audit trails, clinical guidelines

❌ **NO Incomplete Features**
- Cannot ship "form entry" without "submission"
- Cannot ship "order entry" without "fulfillment tracking"
- Cannot ship "diagnostic suggestion" without full clinical context

❌ **NO Manual Steps**
- "Please type patient name in pharmacy system"
- "Please fax this prescription"
- "Please email confirmation to patient"
- ALL of these violate zero-tolerance standard

❌ **NO Workarounds**
- Cannot require physician to use workarounds
- Cannot require scripting, macros, or technical knowledge
- Cannot require switching between systems

### **Physician Release Examples**

#### **✅ Acceptable Physician Release**

```
REL-001: Complete E-Prescription Workflow for Medication

Includes:
- Drug search by name, NDC, or class
- Patient allergy and medication history display
- Formulary checking against patient's insurance
- Drug-drug and drug-allergy interaction warnings
- Dosage suggestions with age/weight adjustment
- Prescription writing (quantity, refills, special instructions)
- Electronic signature capture
- Automatic submission to patient's pharmacy
- Confirmation number and receipt
- Refill management (approve/deny patient refill requests)
- Status tracking (pending, filled, dispensed)
- Audit log of all changes

Outcome: Physician can write, submit, and track prescription from start to finish
Time: 3 weeks (includes safety checks, pharmacy integration, compliance)
```

#### **❌ Unacceptable Physician Release**

```
âŒ REL-001: Medication Order Entry Form (view-only, 5 days)
   Problem: Incomplete. Physician cannot submit or track prescription.

âŒ REL-002: Pharmacy Integration (manual submission, 2 weeks)
   Problem: Requires manual steps (copy data, email to pharmacy)

âŒ REL-003: E-Signature (separate auth system, 1 week)
   Problem: Workflow split across releases. Physician frustrated.

âŒ Better Approach:
   Single release with complete workflow (all above) delivered together
```

### **Physician Release Sizing Guidelines**

| Complexity | Typical Duration | Examples |
|-----------|------------------|----------|
| Simple single action (no integration) | 2-3 weeks | Medical history viewing, clinical notes |
| Single action with external integration | 2.5-3.5 weeks | E-prescribing, referral ordering |
| Multi-step workflow with safety checks | 3-4 weeks | Prior authorization, medication reconciliation |
| Complex workflow with clinical algorithms | 4-5 weeks | Diagnosis support, treatment planning |

**Minimum time**: 2 weeks (even simple clinical features need safety checks)
**Maximum per release**: 5 weeks (break into separate complete workflows if larger)

---

## User Type 2: Administrator

### **Identifying Administrator Users**

Administrator users handle operational tasks that support clinical care:
- **Billing and Claims** (claim entry, submission, appeals)
- **Scheduling** (appointment booking, rescheduling, no-show tracking)
- **Prior Authorization** (PA submission, status tracking, denial appeals)
- **Enrollment** (patient enrollment in programs, coverage verification)
- **User Management** (staff access, permissions, credentials)
- **Practice Operations** (inventory, equipment, room management)

**Key Indicator**: If user handles business processes or operations (not clinical), user is Administrator.

### **Administrator Standards: Strategic Flexibility**

Administrators have **more flexibility than physicians** because:
- Administrative tasks have lower clinical risk (errors don't immediately harm patients)
- Administrators often have technical comfort (more willing to work with partial solutions)
- Administrative workflows are often repetitive (patterns enable optimization)
- Professional SaaS UX is acceptable (users expect web application experience)

#### **What's Allowed for Administrator Releases**

✅ **Wizard of Oz Approach** (if invisible)
- Manual backend work is acceptable IF:
  - User sees professional automation UX ("Processing..." → "Complete")
  - NO visible manual instructions ("Please email...", "Copy and paste...")
  - Backend operations completely invisible
  - User cannot tell work is being done manually

✅ **Read-Only Releases** (if viewing IS complete workflow)
- View-only acceptable ONLY IF:
  - Viewing is the complete user goal (status dashboard, audit log, history)
  - User doesn't need to modify data
  - Professional information architecture and filtering
  - Examples: PA status dashboard, claim history, enrollment tracking

✅ **Progressive Automation**
- Ship with manual steps, automate later
- Example: Release 1 = manual data entry + system notification
           Release 2 = auto-population from EHR
           Release 3 = automatic submission to hub
- Enables faster learning and incremental value

✅ **Professional SaaS UX**
- Administrators expect web application experience
- Dashboard views, filtering, search, export
- Mobile-friendly interfaces
- Responsive design (works on tablet, desktop)

#### **What's Forbidden for Administrator Releases**

❌ **VISIBLE Manual Steps**
- "Please email this form to..."
- "Please download and upload to..."
- "Please call and confirm..."
- "Please copy data into..."
- All violate professional self-service expectation

❌ **Incomplete Workflows** (when can be avoided)
- If user needs to take action elsewhere, provide path to complete action
- Cannot ship "form viewer" without "form submission" (if submission is user goal)
- Cannot ship "list view" without ability to act on items (if action is the goal)

❌ **Unprofessional UX**
- Plain text output instead of formatted displays
- No filtering or search on large datasets
- Broken mobile experience
- Broken session management
- No error recovery

#### **Administrator Approach: Wizard of Oz Validation Progression**

Strategic progression for administrator workflows:

```
Release 1: Manual Process with System Support (1-1.5 weeks)
├─ Users enter data manually
├─ System creates task list and notifications
├─ Operations team does work (manually)
├─ User sees professional "Processing" → "Complete" UX
├─ Goal: Validate user value and workflow
└─ Hypothesis: "Will admins use system? What's the workflow?"

↓

Release 2: Semi-Automated with Human-in-the-Loop (1.5-2 weeks)
├─ System auto-populates some fields
├─ Users review and modify
├─ Operations team handles exceptions
├─ System routes exceptions appropriately
└─ Hypothesis: "Where can we reduce manual effort?"

↓

Release 3: Fully Automated (2-2.5 weeks)
├─ System handles 80%+ automatically
├─ Only exceptions require user action
├─ Operations team only handles true exceptions
├─ User confidence in automation is high
└─ Outcome: Complete self-service workflow
```

### **Administrator Release Examples**

#### **✅ Acceptable Administrator Release**

```
REL-001: Single Enrollment Submission with Manual Backend

Includes (User Sees):
- Enrollment form with patient demographics
- Insurance verification lookup
- Program selection and requirement verification
- Form field completion with validation
- "Submit to Hub" button
- Success message with confirmation number
- Status tracking ("Pending", "Enrolled", "Denied")

Backend (User Doesn't See - Manual):
- Operations team receives submission notification
- Team manually accesses hub portal
- Team submits enrollment
- Team captures confirmation and updates system

Outcome: Admin completes entire enrollment workflow in 3 minutes
         Professional UX maintained (no visible manual steps)
         Status tracking works (admin sees result in system)

Goal: Validate admin adoption and workflow efficiency
```

#### **✅ Acceptable Read-Only Administrator Release**

```
REL-003: Prior Authorization Status Dashboard

Includes:
- List of all submitted PAs with status
- Filtering by: date range, status (pending/approved/denied), payer
- Search by patient name or PA number
- Export to CSV for reporting
- Drill-down to see PA details (form fields, submission date, responses)
- Sortable columns (newest first, oldest first, by payer)
- Historical view of past PAs with outcomes

Goal: Admin can track status and answer provider questions
Outcome: Read-only IS the complete workflow (monitoring/tracking)
```

#### **❌ Unacceptable Administrator Release**

```
âŒ "Read-Only PA Management" (unacceptable)
   Problem: "Management" implies ability to modify (create, update, cancel)
   Should include: Create PA, edit PA, cancel PA, plus tracking

âŒ "Enrollment with Visible Manual Steps" (unacceptable)
   Flow: Admin fills form → Sees "Please fax to XYZ" → Must leave system
   Problem: Defeats automation purpose

âŒ "Manual Enrollment Process" with no UX (unacceptable)
   Admin receives email → Downloads form → Fills Excel → Emails back
   Problem: Not improved from current process

✅ Better Approach:
   Manual backend (Release 1) but professional UI ("Processing...")
   Or: Read-only if just tracking
   Or: Complete automation when backend is ready
```

### **Administrator Release Sizing Guidelines**

| Complexity | Typical Duration | Examples |
|-----------|------------------|----------|
| Simple single action | 1-1.5 weeks | Patient lookup, simple form entry |
| Single action with external lookup | 1.5-2 weeks | Insurance verification, provider search |
| Workflow with WoZ backend | 1.5-2 weeks | Form + manual hub submission |
| Multi-step workflow (semi-automated) | 2-2.5 weeks | Enrollment with verification + exceptions |
| Full automation | 2-3 weeks | Complete self-service workflow |
| Bulk operations (2-20 items) | 1.5-2 weeks | Batch submission, multi-enrollment |

**Minimum time**: 1-1.5 weeks (simpler than clinical workflows)
**Maximum per release**: 2.5 weeks (break into separate workflows if larger)

---

## User Type 3: Internal

### **Identifying Internal Users**

Internal users manage technical systems and operations:
- **System Configuration** (settings, feature toggles, user provisioning)
- **Monitoring & Analytics** (system health, usage reports, performance)
- **Technical Operations** (backup/restore, maintenance, troubleshooting)
- **Support** (customer support staff, internal IT)
- **Developers** (engineers building integrations, APIs)

**Key Indicator**: If user manages technical systems (not end-user facing), user is Internal.

### **Internal Standards: Maximum Flexibility**

Internal users have **maximum flexibility** because:
- Technical risk is contained (errors affect operations, not patient care)
- Internal users are technical-minded (comfortable with complexity)
- Internal tools are traded-off against external user experience
- Speed of internal enablement often matters more than UX polish

#### **What's Allowed for Internal Releases**

✅ **Wizard of Oz Approach** (even visible)
- Manual steps acceptable if:
  - Process is documented
  - Triggers are clear
  - Expected timeline is stated
  - Example: "System shows 'Pending approval', approval team emails within 2 hours"

✅ **Read-Only Releases** (widely acceptable)
- View-only acceptable for:
  - Monitoring and analytics
  - Reports and dashboards
  - Audit logs and history
  - Configuration review (not modification)

✅ **Manual Steps** (if well-documented)
- "Please manually [action]" acceptable if:
  - Instructions are clear
  - Process is repeatable
  - Expected frequency is documented
  - Example: "Manually trigger backup via admin console (daily, 2am)"

✅ **Technical Complexity**
- Command-line interfaces acceptable
- Scripting and automation friendly
- API-first approaches acceptable
- Advanced configuration options encouraged

✅ **Incomplete Features** (if roadmap is clear)
- "Beta" features acceptable
- Feature flags and toggle acceptable
- Partial implementation acceptable if documented
- Example: "Supports 3 payers in MVP, expanding to 10 by Q2"

#### **Internal Release Examples**

#### **✅ Acceptable Internal Release**

```
REL-001: System Monitoring Dashboard (Internal Operations)

Includes:
- Real-time system health metrics
- Error rate and error logs
- API latency and throughput
- Database performance metrics
- User activity and usage patterns
- Alert configuration (email alerts on high error rate)
- Manual trigger for health check/restart

Manual Component (Documented):
- If error rate > 5%, operator receives email alert
- Operator has 2 hours to investigate or escalate
- Manual escalation path documented
- Rollback procedure documented

Outcome: Operations team can monitor system health
         Mixed automated (dashboards) + manual (escalation) acceptable
```

#### **✅ Acceptable Read-Only Internal Release**

```
REL-002: API Usage Analytics (Internal Developers)

Includes:
- Real-time API call counts by endpoint
- Error rates and error types
- Response time percentiles (p50, p95, p99)
- Rate limit status and throttled requests
- Historical trends (daily/weekly/monthly)
- Export to CSV for reporting

Outcome: Developers can troubleshoot API issues
         Read-only IS the goal (monitoring/analysis)
```

#### **✅ Acceptable With Manual Steps**

```
REL-001: Patient Data Migration Tool (Internal Operations)

Includes (Automated):
- CSV upload interface for patient data
- Validation and error reporting
- Preview of changes before applying
- Batch processing (10K records per batch)

Manual Process (Documented):
- Operations team runs "validate" function
- Reviews error report (5-10 min)
- If <1% errors: Approves migration
- System processes batch (typically 30-60 min)
- Post-migration verification (automated checks)
- If issues found: Rollback procedure (documented)

Expected Workflow:
- 1-2 migrations per week
- 30 minutes per migration (validation + approval + processing)
- Clear escalation if errors exceed threshold

Outcome: Scalable data migration without requiring custom scripts
```

### **Internal Release Sizing Guidelines**

| Complexity | Typical Duration | Examples |
|-----------|------------------|----------|
| Simple read-only view | 1 week | Analytics dashboard, status page |
| Configuration tool | 1-1.5 weeks | Settings management, feature toggles |
| Monitoring with alerts | 1.5-2 weeks | Health dashboard, automated notifications |
| Manual operational process | 1-1.5 weeks | Migration tool, batch operations |
| Integration for other teams | 1.5-2 weeks | API, webhook, data export |

**Minimum time**: 1 week (simpler than external-facing workflows)
**Maximum per release**: 2 weeks (can split internal workflows more aggressively)

---

## User Type Decision Framework

### **How to Identify Primary User Type**

When a release serves multiple user types, use this hierarchy:

```
If workflow includes CLINICAL decision-making (diagnosis, prescribing, treatment)
  → PRIMARY USER = Physician (apply Physician standards)

Else if workflow is OPERATIONAL/ADMINISTRATIVE (billing, scheduling, enrollment)
  → PRIMARY USER = Administrator (apply Administrator standards)

Else if workflow is TECHNICAL/INTERNAL (monitoring, configuration, operations)
  → PRIMARY USER = Internal (apply Internal standards)

Else if mixed (e.g., administrator AND internal)
  → Identify PRIMARY (who uses most frequently or critically)
  → Apply PRIMARY user's standards
  → Note SECONDARY users in release description
```

### **What if User Type is Unclear?**

If you cannot definitively identify user type:

1. **Ask stakeholders**: "Who is the primary user who needs this daily?"
2. **Look at workflow**: Does it involve clinical decisions? Operations? Technical management?
3. **Default conservatively**: If unsure between Administrator and Internal, treat as Administrator (higher standard)
4. **Document assumption**: Note your reasoning in release description

---

## Validation Checklist: Did We Apply Standards?

Use this checklist for each release to verify standards are correctly applied.

### **For Physician Releases**

- ☑ Release is complete automation (no manual steps)
- ☑ Clinical safety checks included (drug interactions, allergies, etc.)
- ☑ Integration to pharmacy/external system included
- ☑ Prescription routing/tracking included
- ☑ NO Wizard of Oz (even invisible)
- ☑ NO read-only for action workflows
- ☑ Audit trail and compliance built-in
- ☑ Mobile-friendly experience
- ☑ Production-quality (not beta/pilot)
- ☑ User can accomplish entire clinical task without leaving system

**Standard**: Zero Tolerance ✅

### **For Administrator Releases**

- ☑ If WoZ used: Manual work is 100% invisible
- ☑ If WoZ used: Professional "Processing..." → "Complete" UX
- ☑ If read-only: Viewing IS the complete workflow (not partial)
- ☑ If actions required: User can act within system (no external steps)
- ☑ Professional SaaS UX (filtering, search, mobile-friendly)
- ☑ Clear path to complete workflows (don't leave user hanging)
- ☑ Error recovery and help available
- ☑ Scope exclusions documented (automation vs manual deferred)

**Standard**: Strategic Flexibility ✅

### **For Internal Releases**

- ☑ If manual steps: Process is well-documented
- ☑ If manual steps: Expected frequency and timeline clear
- ☑ If read-only: Appropriate for monitoring/analysis use case
- ☑ If technical: Acceptable complexity level for target audience
- ☑ If incomplete: Roadmap is transparent
- ☑ If incomplete: Feature flags or toggle clearly marked
- ☑ Documentation clear and actionable

**Standard**: Maximum Flexibility ✅

---

## Cross-Reference Examples

### **Example 1: Prior Authorization Release**

| Standard | Physician User | Administrator User | Internal User |
|----------|---|---|---|
| Use Case | PA approval decision | PA submission | PA system monitoring |
| Allowed Approach | Complete automation (no WoZ) | Manual backend OK (invisible) | Manual monitoring OK (visible) |
| Release 1 | E-sign PA + auto-submit | Manual submission + visibility | Health dashboard |
| Release 2 | Bulk PA approval | Auto-submission | Performance alerts |
| Release 3 | Decision support (drug alternatives) | Dashboard | Custom reporting |

### **Example 2: Patient Enrollment Release**

| Standard | Physician User | Administrator User | Internal User |
|----------|---|---|---|
| Use Case | (N/A - not clinical) | Form entry + submission | Enrollment pipeline monitor |
| Allowed Approach | (N/A) | WoZ or progressive automation | Manual escalation acceptable |
| Release 1 | - | Manual backend (invisible) | Status dashboard |
| Release 2 | - | Auto-population from EHR | Enrollment metrics |
| Release 3 | - | Bulk enrollment | Reporting & exports |

---

## Summary by User Type

| Dimension | Physician | Administrator | Internal |
|-----------|-----------|---|---|
| **Standard** | Zero Tolerance | Strategic Flexibility | Maximum Flexibility |
| **WoZ** | ❌ Never | ✅ If invisible | ✅ Even visible |
| **Read-Only** | ❌ For actions | ✅ For consumption | ✅ Widely |
| **Manual Steps** | ❌ None | ❌ Visible steps | ✅ If documented |
| **Incomplete Features** | ❌ Not acceptable | ⚠️ If scoped | ✅ If documented |
| **Release Size** | 2-3 weeks | 1.5-2.5 weeks | 1-2 weeks |
| **Quality Expectation** | Production-ready | Professional SaaS UX | Technical clarity |
| **Typical Workflows** | Prescribing, diagnosis | Billing, scheduling, PA | Monitoring, config |
