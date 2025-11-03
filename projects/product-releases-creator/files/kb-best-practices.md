# Release Patterns & Anti-Patterns Reference

**Purpose**: Quick reference for correct product value decomposition patterns and common mistakes to avoid.

**How to Use**: Consult this when decomposing Initiatives
---

## Pattern 1: Progressive Capability Build

Each release delivers a complete NEW capability, not progressive implementation of a single capability. Releases should expand SCOPE (more complete capabilities) rather than expand IMPLEMENTATION (building pieces of one capability).

**Correct Approach**:
- Release A: Complete workflow for use case 1
- Release B: Complete workflow for use case 2
- Release C: Complete workflow for use case 3

**Incorrect Approach**:
- Release A: Part 1 of workflow (view)
- Release B: Part 2 of workflow (edit)
- Release C: Part 3 of workflow (submit)

**Problem**: Splits essential workflow across multiple releases for implementation convenience, NOT user value

**Example - PA Initiative**:

Correct:
```
REL-001: Single PA Submission Workflow (2 weeks)
  - Complete prior authorization submission system
  - PA form search → field completion → submission → tracking
  - User gets: Complete PA submission capability

REL-002: PA Status Dashboard (1 week)
  - NEW capability: Centralized visibility into all PAs
  - List view, filtering, search, export

REL-003: Bulk PA Submission for 2-15 PAs (1.5 weeks)
  - NEW capability: Batch processing for typical scale
```

Incorrect:
```
REL-001: PA Form Library View (5 days) - read-only
  - Cannot accomplish any goal
  - Viewing empty forms has no value

REL-002: PA Form Field Completion (1 week)
  - Still cannot submit PA
  - Partial capability frustrates users

REL-003: PA Submission to Payer (1.5 weeks)
  - Three releases required to complete single workflow
```

---

## Pattern 2: Foundation-First Sequencing

Build minimal viable foundation, then expand scope progressively. Start with simplest complete workflow (foundation), then add additional complete capabilities that build on foundation.

**Sequencing Strategy**:
1. Core single-entity workflow - Complete CRUD for primary use case
2. Visibility and monitoring - Dashboard/list views for all entities
3. Scale capability - Bulk operations for typical scale (2-20 entities)
4. Enhancements - Additional complete capabilities

**Administrative Template**:
```
Release 1: Core Single-Entity Workflow (1.5-2 weeks)
  - Complete CRUD for primary administrative task
  - Example: Create/edit/submit/track single claim

Release 2: Dashboard or List View (1 week)
  - Visibility into all entities
  - Example: All claims dashboard with filtering

Release 3: Bulk Operations (1.5 weeks)
  - Multi-entity workflow for 2-20 entities
  - Example: Bulk claim submission for 15-30 claims

Releases 4-6: Additional Complete Capabilities
  - Enhancements that build on foundation
```

**Clinical Template**:
```
Release 1: Core Clinical Action (2-3 weeks)
  - Complete clinical workflow start to finish
  - Example: E-prescribe single medication

Release 2: Patient-Level Aggregation (1-2 weeks)
  - View multiple instances for patient
  - Example: Patient medication list with history

Release 3: Clinical Decision Support OR Bulk (1.5-2 weeks)
  - Enhancement to clinical workflow
  - Example: Drug interaction checking OR bulk prescription renewal
```

---

## Pattern 3: Risk-Driven Prioritization

Address biggest unknowns and risks first to maximize learning velocity. Sequence releases to test riskiest assumptions earliest for fast pivots or course corrections.

**Risk Priority Order**:
1. **Integration Risk** (Highest) - Will external APIs work reliably?
2. **Value Risk** - Will users adopt the workflow?
3. **Usability Risk** - Can users successfully complete tasks?
4. **Technical Risk** - Can we build it performantly?
5. **Feature Risk** (Lowest) - Do advanced features add value?

**Example - PA Initiative with Integration Risk**:
```
REL-001: PA Submission with Payer API (2 weeks) - HIGHEST RISK
  Tests: API reliability, response time, data format
  Why First: Biggest technical unknown, could invalidate initiative

REL-002: PA Status Dashboard (1 week) - VALUE RISK
  Tests: User behavior, status checking frequency

REL-003: Bulk PA Submission (1.5 weeks) - USABILITY
  Tests: Scale usage patterns, typical batch size

REL-004: PA Form Search and Favorites (1 week) - FEATURE
  Tests: Usability enhancement value
```

---

## Pattern 4: Minimum Testable Scope

Each release should be the SMALLEST possible vertical slice that validates a specific hypothesis. Challenge every capability: "Do we NEED this to test the hypothesis?"

**Challenge Questions**:
1. Can we test this assumption with LESS scope?
2. What's the absolute minimum users need for meaningful feedback?
3. Can we defer any capability without blocking learning?
4. Are we including "nice to have" disguised as "must have"?

**Example - Too Large**:
```
REL-001: Complete PA Management System
- Submit PAs to all 15 payers
- Track status across all payers
- Analytics dashboard
- Form template library
- Bulk submission
- Automated reminders

Problem: Too much scope. Cannot isolate what's working/failing.
```

**Example - Right-Sized**:
```
REL-001: Single PA Submission to UnitedHealthcare Only

Included:
- Submit PA to ONE payer (UnitedHealthcare - 40% market share)
- View submission confirmation
- Email notification on status change
- Basic status list view

Tests: "Will admins adopt electronic PA submission?"

Explicitly Excluded:
- Other payers → REL-004 (if UHC successful)
- Bulk submission → REL-003 (after single validated)
- Analytics → REL-005 (once volume justifies)
- Form templates → REL-006 (optimization)
- Auto-population → REL-007 (enhancement)

Why This Works: Smallest slice that tests core hypothesis.
Single payer isolates API risk. Can expand if successful.
```

---

## Anti-Pattern 1: Progressive Implementation Split

**Problem**: Splitting a single coherent workflow across multiple releases for implementation convenience rather than user value.

**Wrong Approach**:
```
REL-001: PA Form Display (3 days, view-only)
  Problem: User cannot accomplish anything

REL-002: PA Form Editing (1 week)
  Problem: Still cannot submit PA

REL-003: PA Submission Integration (1 week)
  Problem: Three releases to complete one workflow
```

**Why This Fails**:
- No release delivers standalone value
- User cannot accomplish goal until Release 3
- Adoption delayed across multiple releases
- Each partial release frustrates users

**Correct Approach**:
```
REL-001: Complete PA Submission Workflow (2 weeks)
  - PA form search and selection
  - Form field completion with validation
  - Patient data auto-population
  - Payer submission integration
  - Status tracking with notifications

User Gets: Can complete entire PA workflow immediately
```

---

## Anti-Pattern 2: Visible Manual Steps (Wizard of Oz Failure)

**Problem**: Using Wizard of Oz approach with visible manual instructions that break self-service perception. For Administrator users only - NEVER acceptable for Physicians.

**Unacceptable**:
```
User Experience:
- Admin completes enrollment form
- System displays: "Warning: Enrollment Form Complete

  Next Steps:
  1. Click 'Download PDF' below
  2. Email PDF to: hub-enrollments@pharma.com
  3. Subject: 'New Enrollment - [Patient Name]'
  4. Check email in 3-5 days for confirmation"

Why This Fails:
- Manual steps visible to user
- User must leave application
- Multi-step manual process defeats automation
- No time savings over previous process
```

**Acceptable WoZ** (Administrator user):
```
User Experience:
- Admin completes enrollment form
- Clicks "Submit to Pfizer CoPay Connect Hub"
- Sees: "Submitting enrollment..." + spinner
- "Enrollment submitted successfully. Confirmation: ENR-789456"

Backend Reality (Invisible):
- Operations team receives notification
- Manually accesses hub portal
- Posts form data
- Captures confirmation number
- Updates system

Why This Works:
- Manual work 100% invisible to admin
- Professional automation UX maintained
- No external manual actions required
```

---

## Anti-Pattern 3: Bulk Operations Misunderstanding

**Problem**: Misunderstanding bulk operations as rare large-scale operations (50+ entities) rather than common workflow (2-20 entities).

**Wrong - Bulk as Edge Case**:
```
REL-009: Bulk Claim Submission (conditional, 2 weeks)
  - Positioned late (Release 9)
  - Conditional on: >50 claims per operation
  - Estimated for: 50-100 claims per batch

Why This Fails:
- Bulk positioned too late (should be Release 3-4)
- Wrong scale threshold (should be 2-20)
- Made conditional when it's core workflow
```

**Correct - Bulk as Core Capability**:
```
REL-003: Bulk Claim Submission for 15-30 Claims (1.5 weeks)
  - Positioned early (Release 3)
  - Always included as core capability
  - Estimated for typical scale: 15-30 claims

Reality of Bulk Usage:
- Billing staff submit 15-30 claims daily
- PA coordinators submit 5-10 PAs weekly
- Enrollment staff process 3-8 patients per session

Bulk is NOT edge case - it's daily workflow at 2-20 entity scale
```

---

## Anti-Pattern 4: Read-Only for Action Workflows

**Problem**: Shipping view-only release for workflows that inherently require editing/action capability.

**Wrong - Split View and Edit**:
```
REL-002: Patient Demographics View (read-only, 5 days)
  Problem: Cannot update address when patient moves

REL-007: Patient Demographics Editing (1.5 weeks)
  Problem: User waits 5+ releases to accomplish basic admin task
```

**Correct - Complete CRUD**:
```
REL-002: Patient Demographics Management (1.5 weeks)
  Includes:
  - View patient demographics
  - Edit all demographic fields with validation
  - Audit log of changes
  - Duplicate patient detection

User Gets: Complete demographic management workflow
```

**Exception - When Read-Only IS Appropriate**:
```
REL-003: PA Status Dashboard (read-only, 1 week)
  Why Acceptable:
  - Viewing IS the complete workflow (status tracking)
  - PA status controlled by payer (not editable by provider)
  - Standalone value delivered (monitoring capability)
```

---

## Anti-Pattern 5: Foundation Release Too Thin

**Problem**: Under-sizing foundation release, shipping incomplete workflow that doesn't meet user type standards. Particularly critical for Physician users (zero tolerance).

**Wrong - Thin Foundation for Physicians**:
```
REL-001: Medication Order Form Display (3 days, physician user)
  Includes: Drug name entry, dosage selection

  Does NOT Include:
  - Formulary checking
  - Drug interaction warnings
  - Allergy checking
  - Prescription routing to pharmacy

Why This Fails:
- Incomplete for physician workflow
- Violates zero-tolerance standard
- Cannot safely prescribe without checks
- Feature provides no value

Result: Zero adoption, product abandoned
```

**Correct - Production-Complete Foundation**:
```
REL-001: Complete Medication Order Workflow (2.5-3 weeks, physician user)
  Includes:
  - Drug search with favoriting
  - Formulary checking against patient's insurance
  - Drug-drug interaction warnings
  - Drug-allergy contraindication checking
  - Dosage calculation with adjustments
  - Prescription routing to pharmacy
  - E-signature and submission
  - Confirmation with prescription number
  - Status tracking

Why This Works:
- Meets physician zero-tolerance standard
- Complete automation from start to finish
- All clinical decision support included
- Production-ready for physician use
```

---

## Anti-Pattern 6: Technical Infrastructure as User-Facing Release

**Problem**: Creating releases for technical infrastructure, auditing, logging, or other backend capabilities that deliver no direct user value. These are implementation details, not product releases.

**Wrong - Technical Releases Disguised as User Value**:
```
REL-002: Audit Logging System (1.5 weeks)
  Problem: No user can accomplish any new goal
  Problem: Technical requirement, not user capability

REL-004: Performance Monitoring Dashboard (1 week)
  Problem: Internal tool for engineers, not user-facing value

REL-006: Data Migration Framework (2 weeks)
  Problem: Technical enabler, delivers no user capability
```

**Why This Fails**:
- No user can do anything new
- Technical debt/infrastructure work packaged as product value
- Delays actual user value delivery
- Conflates engineering tasks with product releases

**Correct - Option 1: Include as Part of User-Facing Release**:
```
REL-001: Complete PA Submission Workflow (2 weeks)
  User Capabilities:
  - Submit PA to payer
  - Track submission status
  - Receive confirmation notification

  Technical Components (NOT separate releases):
  - Audit logging of all PA actions
  - Performance monitoring
  - Error tracking and alerting
  - Data validation framework

User Gets: Complete PA submission capability
Technical Gets: Audit, monitoring, validation (as implementation details)
```

**Correct - Option 2: Exclude from User-Facing Releases Entirely**:
```
Product Releases (User Value):
REL-001: PA Submission (2 weeks)
REL-002: PA Status Dashboard (1 week)
REL-003: Bulk PA Submission (1.5 weeks)

Engineering Work (NOT Product Releases):
- Sprint 1-3: Audit logging implementation
- Sprint 2-4: Performance monitoring setup
- Sprint 5: Data migration execution

Separation: Product releases deliver user value.
            Engineering work enables product releases.
```

**Exception - When Audit/Infrastructure IS a Release**:
```
REL-005: Compliance Audit Trail for Administrators (1 week)

User Capabilities:
- View complete audit log of all system actions
- Filter by user, date range, action type
- Export audit reports for compliance reviews
- Search audit history

Why This Works:
- Delivers user capability (admin can audit system)
- Administrator user type (not physician)
- Viewing audit trail IS the complete workflow
- Standalone value for compliance/security needs
```

**Key Distinction**:
- **Not a Release**: Backend infrastructure with no user interface
- **Valid Release**: User-facing audit dashboard with query/export capabilities

- **Not a Release**: Logging framework for debugging
- **Valid Release**: Admin tool to view logs and troubleshoot issues

- **Not a Release**: Data migration script
- **Valid Release**: User tool to export/import their data

**Test**: Can a user accomplish a goal they couldn't before?
- If NO: Not a release (engineering work)
- If YES: Valid release (user capability)

**Examples**:

Wrong - Technical Infrastructure as Releases:
```
REL-001: Core PA Workflow (2 weeks)
REL-002: Audit Logging System (1.5 weeks)
REL-003: Performance Monitoring (1 week)
REL-004: Error Tracking Setup (1 week)
REL-005: Data Validation Framework (1.5 weeks)

Problem: Only REL-001 delivers user value
Problem: REL-002 through REL-005 are engineering tasks
```

Correct - Infrastructure Bundled with User Value:
```
REL-001: Core PA Workflow (2 weeks)
  - Includes: Audit logging, monitoring, validation
  - User capability: Submit and track PAs
  - Technical: All infrastructure built-in

REL-002: PA Status Dashboard (1 week)
  - Includes: Performance optimization, error handling
  - User capability: View all PA statuses
  - Technical: Infrastructure already in place

No separate infrastructure releases
All technical work supports user capabilities
```

Correct - Admin-Facing Audit Tool (Valid Release):
```
REL-004: System Audit and Compliance Dashboard (1 week)

User: System Administrator
Capabilities:
- Search full audit history by date, user, action type
- Export compliance reports (CSV, PDF)
- View user action details (who, what, when, where)
- Filter by compliance categories (HIPAA, regulatory)

Why Valid:
- Administrator can now audit system (couldn't before)
- Viewing audit data IS the complete workflow
- Standalone compliance value
- Read-only appropriate (audit data is historical)
```

---

## Quick Reference: Decision Flowchart

```
Start Release Decomposition
        ↓
Does release deliver direct USER capability?
    NO → Anti-Pattern 6: Technical Infrastructure Release
    YES → Continue
        ↓
Does release deliver COMPLETE NEW capability?
    NO → Anti-Pattern 1: Progressive Implementation Split
    YES → Continue
        ↓
Is release the SMALLEST testable slice?
    NO → Reduce scope, document exclusions
    YES → Continue
        ↓
Does release address HIGHEST remaining risk?
    NO → Resequence releases
    YES → Continue
        ↓
Is release independently valuable and deployable?
    NO → Depends on future releases
    YES → Continue
        ↓
Does release meet user type standards?
    NO → Anti-Pattern 5: Foundation Too Thin
    YES → Valid Release
```

---

## Pattern Application Checklist

Before finalizing initiative release decomposition, verify:

**Progressive Capability Build**:
- Each release delivers complete NEW capability
- No release splits essential workflow across multiple releases
- Releases expand scope, not implement pieces of one capability

**Foundation-First Sequencing**:
- Release 1 is core single-entity workflow (complete CRUD)
- Release 2 provides visibility/monitoring
- Release 3 provides bulk operations (if applicable)
- Later releases build enhancements on foundation

**Risk-Driven Decomposition**:
- Highest risk release positioned first
- Value risk tested early (Release 2-3)
- Feature enhancements positioned later (Release 4+)

**Minimum Testable Scope**:
- Cannot reduce scope further without losing learning ability
- Excluded capabilities explicitly documented
- Each inclusion justified as essential for hypothesis testing

**User Value Focus**:
- No technical infrastructure releases
- All releases deliver direct user capabilities
- Engineering work bundled or excluded from releases
