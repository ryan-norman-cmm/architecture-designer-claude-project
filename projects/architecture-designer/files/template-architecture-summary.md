# Architecture Summary Template

**Purpose:** Lightweight architecture summary format for feeding into Technical Requirements agent or ADR Generator

**Version:** v1.0
**Last Updated:** 2025-11-19

---

## Template Structure

```markdown
# Architecture Summary: [Project Name]

**Date:** YYYY-MM-DD
**Prepared By:** Architecture Designer Agent
**Status:** Ready for Technical Requirements

---

## Project Context

**Product:** [1-2 sentence description of what you're building]

**Team:**
- Size: [N engineers]
- Expertise: [Key technologies team knows]
- Experience Level: [Senior, mid-level, junior mix]

**Timeline:**
- Launch Target: [Date or duration]
- MVP Scope: [What must launch]
- Phase 2 Scope: [What can wait]

**Scale:**
- Initial Users: [N users]
- 12-Month Target: [N users]
- Growth Rate: [Expected growth pattern]

**Platform Context:**
- Cloud Provider: [AWS, Azure, GCP, etc.]
- Existing Services: [Auth, notifications, logging, etc.]
- Vendor Tooling: [Managed services available]
- Standards: [REST, GraphQL, FHIR, etc.]

**Constraints:**
- Budget: [Monthly infrastructure spend tolerance]
- Compliance: [HIPAA, SOC 2, GDPR, etc.]
- Integration Points: [External systems to connect]
- Shared Infrastructure: [Databases, queues, caches to reuse]

---

## Architecture Decisions Made

### Decision 1: [Decision Category] - [Decision Name]

**What We Decided:**
[Selected approach name]

**Why This Decision Was Critical:**
[1-2 sentences explaining significance and impact]

**Selected Approach:**
[Approach name with 1-sentence description]

**Rationale:**
- [Key reason 1 tied to project context]
- [Key reason 2 tied to constraints]
- [Key reason 3 tied to platform fit]

**Alternatives Considered:**
1. **[Alternative 1 Name]**: [1-sentence description] - Not selected because [specific reason]
2. **[Alternative 2 Name]**: [1-sentence description] - Not selected because [specific reason]
3. **[Alternative 3 Name]**: [1-sentence description] - Not selected because [specific reason]

**Key Trade-offs Accepted:**
- ✅ Benefit 1: [Specific positive consequence]
- ✅ Benefit 2: [Specific positive consequence]
- ⚠️ Tradeoff 1: [Specific limitation or constraint]
- ⚠️ Tradeoff 2: [Specific limitation or constraint]

**High-Level Architecture:**

```
[ASCII diagram showing system context or component structure]

Example:
┌─────────────────────────────────────────────┐
│         Task Management Monolith            │
├─────────────────────────────────────────────┤
│                                             │
│  [API] ──> [Business Logic] ──> [Data]    │
│                                             │
│  • REST endpoints                           │
│  • Task/User/Notif modules                 │
│  • PostgreSQL data layer                   │
│                                             │
└─────────────────────────────────────────────┘
         │
         ├──> [Auth Service]
         ├──> [PostgreSQL DB]
         └──> [Email Service]
```

---

### Decision 2: [Decision Category] - [Decision Name]

[Same structure as Decision 1]

---

[Repeat for each decision - typically 1-3 decisions total]

---

## Technology Stack Summary

**Core Technologies Selected:**
- **Architecture Pattern**: [Monolith, Microservices, Serverless, etc.]
- **Backend**: [Language/framework]
- **Database**: [PostgreSQL, MongoDB, DynamoDB, etc.]
- **Caching**: [Redis, Memcached, none, etc.]
- **Message Queue**: [RabbitMQ, Kafka, SQS, none, etc.]
- **Deployment**: [Docker + ECS, Kubernetes, Lambda, etc.]
- **Infrastructure**: [Terraform, CloudFormation, CDK, etc.]

**Platform Services Reused:**
- [Auth service name/description]
- [Notification service name/description]
- [Logging/monitoring service name/description]

---

## Implementation Priorities

**Phase 1: Foundation (Weeks 1-2)**
- Infrastructure setup
- Platform service integration (auth, logging)
- Database schema design
- Basic deployment pipeline

**Phase 2: Core Features (Weeks 3-N)**
- [Feature 1]
- [Feature 2]
- [Feature 3]

**Phase 3: Launch Prep (Final Weeks)**
- Testing and quality gates
- Performance validation
- Production deployment

---

## Next Steps

**For Technical Requirements Agent:**
1. Use this summary as input for detailed technical requirements
2. Reference architecture decisions when defining features
3. Align technical specs with selected technology stack
4. Consider trade-offs when prioritizing features

**For ADR Generator (Optional):**
1. Feed architecture decisions to ADR Generator agent
2. Generate comprehensive ADRs for documentation
3. Save ADRs to `/docs/adr/` directory
4. Share with team for alignment

**For Implementation:**
1. Set up infrastructure based on technology stack
2. Configure platform service integrations
3. Follow implementation priorities
4. Reference trade-offs during development

---

## Cost Estimate

**Monthly Infrastructure Cost:**
- Initial (at launch): $[X]
- 12 months (at target scale): $[Y]
- Breakdown: [Compute $X, Database $X, Caching $X, etc.]

---

## Risk Mitigation

**Top Risks Identified:**
1. **[Risk 1]**: [Description] - Mitigate by [strategy]
2. **[Risk 2]**: [Description] - Mitigate by [strategy]
3. **[Risk 3]**: [Description] - Mitigate by [strategy]

---

**Generated by:** Architecture Designer Agent
**Source:** Architecture Exploration Workflow v3.0
```

---

## Usage Guidelines

### When to Use This Template

**Use this template when:**
- Completing Architecture Designer workflow (Phase 4 output)
- Feeding architecture decisions into Technical Requirements agent
- Providing lightweight architecture context for downstream agents
- Documenting high-level decisions WITHOUT full ADR detail

**Don't use this template when:**
- Need comprehensive ADRs (use ADR Generator instead)
- Architecture is still being explored (template is for completed decisions)
- Only have partial decision context (complete Phase 1-3 first)

### Template Filling Guidelines

**Project Context Section:**
- Complete ALL fields (no "TBD" or blanks)
- Be specific with numbers (team size, user count, timeline)
- List concrete technologies (not "standard database")

**Architecture Decisions Section:**
- Include 1-3 decisions (typical: 1 decision 70% of time)
- Each decision must have selected approach + 2-3 alternatives
- Rationale must tie to specific project context
- Trade-offs must include both benefits and limitations

**Technology Stack Section:**
- List specific technologies (PostgreSQL, not "relational database")
- Include version numbers if relevant (Node.js 18+)
- Mention managed vs. self-hosted (RDS PostgreSQL vs. EC2 PostgreSQL)

**ASCII Diagrams:**
- Keep simple (5-8 components max)
- Show key relationships only
- Use consistent formatting (boxes, arrows)
- Label all components clearly

### Output Format Options

**Option 1: Standalone Markdown File**
```
Save as: `/docs/architecture/architecture-summary-YYYY-MM-DD.md`
Use for: Documentation, team sharing, future reference
```

**Option 2: Inline Response**
```
Paste directly in chat for Technical Requirements agent
Use for: Immediate handoff to downstream agent
```

**Option 3: Structured Data**
```
Extract just Architecture Decisions section
Use for: ADR Generator input
```

---

## Example: Minimal Summary (1 Decision)

```markdown
# Architecture Summary: Task Management Application

**Date:** 2025-11-19
**Status:** Ready for Technical Requirements

## Project Context

**Product:** Task management application for small teams with assignment tracking and basic notifications

**Team:** 3 engineers (2 senior, 1 mid-level), Node.js expertise
**Timeline:** 2 months to MVP launch
**Scale:** 500 users initially → 5K users in 12 months
**Platform:** AWS with existing auth service, REST APIs

## Architecture Decisions Made

### Decision 1: Architecture Pattern - Modular Monolith

**Selected Approach:** Modular Monolith (single deployable with internal module boundaries)

**Rationale:**
- Team size (3 engineers) limits operational complexity
- Timeline (2 months) requires fast iteration
- Scale (500-5K users) fits monolith capacity

**Alternatives Considered:**
1. **Microservices**: Too complex for 3-person team
2. **Serverless**: Cold start latency impacts UX

**Key Trade-offs:**
- ✅ Fast development velocity, simple deployment
- ⚠️ Scaling limits at 100K+ users (acceptable for MVP)

## Technology Stack

- Architecture: Modular Monolith
- Backend: Node.js + Express
- Database: PostgreSQL (AWS RDS)
- Deployment: Docker + AWS App Runner

## Next Steps

Feed this summary to Technical Requirements agent for detailed technical specs.
```

---

## Example: Comprehensive Summary (2 Decisions)

```markdown
# Architecture Summary: Patient Scheduling Platform

**Date:** 2025-11-19
**Status:** Ready for Technical Requirements

## Project Context

**Product:** HIPAA-compliant patient scheduling system with provider availability, appointment booking, and reminder notifications

**Team:**
- Size: 5 engineers (3 senior, 2 mid-level)
- Expertise: Azure, PostgreSQL, FHIR R4, TypeScript
- Experience: 3+ years building healthcare platforms

**Timeline:**
- Launch Target: 3 months
- MVP Scope: Provider schedules, patient booking, email reminders
- Phase 2 Scope: SMS reminders, waitlist, recurring appointments

**Scale:**
- Initial: 20 providers, 2K patients
- 12-Month: 100 providers, 20K patients
- Growth: Adding 10 providers/month average

**Platform Context:**
- Cloud: Azure (existing platform)
- Existing Services: Auth (OAuth 2.0), Audit Logging, Notifications
- Vendor Tooling: Azure PostgreSQL, Redis, Service Bus, Functions
- Standards: FHIR R4, REST APIs, OpenTelemetry

**Constraints:**
- Budget: $500-1K/month infrastructure
- Compliance: HIPAA, SOX, SOC 2
- Integration: Existing EHR system (HL7 feeds)

---

## Architecture Decisions Made

### Decision 1: Architecture Pattern - Modular Monolith with Event-Driven Extensions

**What We Decided:**
Modular Monolith for core scheduling logic + Event-Driven extensions for notifications and integrations

**Why Critical:**
Balances development speed (monolith) with async processing needs (events)

**Selected Approach:**
Core scheduling in monolith, async notifications/integrations via Service Bus events

**Rationale:**
- Team size (5 engineers) can handle moderate async complexity
- Timeline (3 months) benefits from monolith simplicity for core domain
- Notification patterns require async processing (SMS, email, HL7 feeds)
- Platform has existing Service Bus infrastructure

**Alternatives Considered:**
1. **Pure Monolith**: Can't handle async HL7 feeds efficiently
2. **Full Microservices**: Too complex for 3-month timeline
3. **Pure Event-Driven**: Over-engineering for core scheduling domain

**Key Trade-offs:**
- ✅ Fast core development + async flexibility for notifications
- ✅ Reuses platform Service Bus (no new infrastructure)
- ⚠️ Dual paradigm (sync + async) adds cognitive load
- ⚠️ Event debugging more complex than sync-only

**High-Level Architecture:**

```
┌───────────────────────────────────────────┐
│      Scheduling Monolith                   │
│  • Provider API (sync)                     │
│  • Booking API (sync)                      │
│  • Availability logic                      │
│  • PostgreSQL data layer                   │
└───────────────────────────────────────────┘
          │
          ├──> [Auth Service]
          ├──> [PostgreSQL]
          └──> [Service Bus] ──> Events
                                   │
                                   ├──> [Notification Handler]
                                   ├──> [HL7 Integration]
                                   └──> [Audit Logger]
```

---

### Decision 2: Database Technology - PostgreSQL with FHIR JSON Columns

**What We Decided:**
Azure PostgreSQL with FHIR resources stored as JSON columns + relational scheduling tables

**Why Critical:**
Must support both FHIR interoperability and performant scheduling queries

**Selected Approach:**
Hybrid model: Relational tables for scheduling domain, JSONB columns for FHIR resources

**Rationale:**
- FHIR compliance requires storing Patient, Practitioner, Appointment resources
- Scheduling queries need relational performance (appointments by provider/date)
- Team has PostgreSQL expertise (5+ years)
- Azure managed PostgreSQL reduces ops complexity

**Alternatives Considered:**
1. **Aidbox FHIR Server**: Full FHIR but overkill for scheduling-only use case
2. **Pure Relational**: Can't store FHIR resources for EHR integration
3. **MongoDB**: Team lacks NoSQL expertise, ACID guarantees important

**Key Trade-offs:**
- ✅ FHIR compliance + relational query performance
- ✅ Team expertise + Azure managed service
- ⚠️ JSONB queries slightly slower than pure relational
- ⚠️ Schema migration complexity (relational + JSON)

---

## Technology Stack Summary

**Core Technologies:**
- Architecture: Modular Monolith + Event-Driven extensions
- Backend: Node.js 18 + TypeScript + Express
- Database: Azure PostgreSQL 14 (with JSONB for FHIR)
- Caching: Azure Redis (session + availability cache)
- Message Queue: Azure Service Bus (Standard tier)
- Deployment: Docker + Azure App Service
- Infrastructure: Terraform

**Platform Services Reused:**
- Auth: OAuth 2.0 service (existing platform)
- Notifications: Email/SMS service (existing platform)
- Audit Logging: Centralized HIPAA audit logs (existing)
- Monitoring: Azure Monitor + Application Insights (existing)

---

## Implementation Priorities

**Phase 1: Foundation (Weeks 1-3)**
- PostgreSQL schema (relational + FHIR JSONB columns)
- Auth integration (OAuth 2.0)
- Service Bus event publishing setup
- Docker + Terraform infrastructure

**Phase 2: Core Scheduling (Weeks 4-8)**
- Provider availability API
- Patient booking API
- Appointment management
- FHIR resource mappings (Patient, Practitioner, Appointment)

**Phase 3: Async Extensions (Weeks 9-11)**
- Notification event handlers (email reminders)
- HL7 integration (EHR feed processing)
- Audit event logging

**Phase 4: Launch Prep (Week 12)**
- HIPAA compliance validation
- Load testing (100 concurrent bookings)
- Production deployment + monitoring

---

## Cost Estimate

**Monthly Infrastructure Cost:**
- Initial (20 providers, 2K patients): $350
  - App Service: $100
  - PostgreSQL: $150
  - Redis: $50
  - Service Bus: $25
  - Storage: $25

- 12 Months (100 providers, 20K patients): $850
  - App Service: $250 (2 instances)
  - PostgreSQL: $400 (read replica added)
  - Redis: $100 (cache cluster)
  - Service Bus: $50
  - Storage: $50

---

## Risk Mitigation

**Top Risks:**
1. **FHIR Interoperability**: EHR system sends malformed HL7
   - Mitigation: Validate HL7 messages, fallback to manual data entry

2. **Dual Paradigm Complexity**: Team unfamiliar with event-driven patterns
   - Mitigation: Start with simple event handlers, add complexity gradually

3. **PostgreSQL JSONB Performance**: Slow FHIR resource queries at scale
   - Mitigation: Add GIN indexes on JSONB columns, monitor query performance

---

**Generated by:** Architecture Designer Agent
**Source:** Architecture Exploration Workflow v3.0
```

---

## Integration with Downstream Agents

### Technical Requirements Agent Integration

**Input Format:**
```
Technical Requirements Agent receives:
- Complete Architecture Summary (all sections)
- Uses Project Context for constraints
- Uses Architecture Decisions for technology guidance
- Uses Technology Stack for implementation specs
```

**Expected Output from Tech Requirements:**
```
- Detailed user stories aligned with MVP scope
- Technical acceptance criteria referencing selected technologies
- Database schema design using selected database
- API specifications following selected patterns
- Non-functional requirements aligned with scale targets
```

### ADR Generator Integration

**Input Format:**
```
ADR Generator receives:
- Just "Architecture Decisions Made" section
- Expands each decision into full ADR
- Adds comprehensive consequences, diagrams, implementation notes
```

**Expected Output from ADR Generator:**
```
- ADR-001.md (Decision 1 with full template)
- ADR-002.md (Decision 2 with full template)
- Ready to save to /docs/adr/ directory
```

---

## Validation Checklist

Before delivering Architecture Summary:

**Completeness:**
- [ ] Project Context fully populated (no TBD/blanks)
- [ ] 1-3 Architecture Decisions documented
- [ ] Each decision has selected approach + 2-3 alternatives
- [ ] Rationale ties to specific project context
- [ ] Trade-offs include benefits AND limitations
- [ ] ASCII diagram included for each decision
- [ ] Technology Stack lists specific technologies
- [ ] Implementation Priorities phase out MVP scope
- [ ] Cost Estimate provides initial + 12-month costs
- [ ] Next Steps guide downstream usage

**Quality:**
- [ ] Rationale avoids vague language ("better", "simpler")
- [ ] Trade-offs are specific with examples/thresholds
- [ ] Alternatives explain "why not selected"
- [ ] ASCII diagrams are clear and focused
- [ ] Technology choices match team expertise
- [ ] Timeline aligns with stated launch target

**Usability:**
- [ ] Summary is scannable (headers, bullets, whitespace)
- [ ] Each decision can stand alone (complete context)
- [ ] Ready to copy/paste to downstream agent
- [ ] Ready to save as documentation artifact

---

**Template Version:** 1.0
**Last Updated:** 2025-11-19
**Owner:** Architecture Designer Agent
