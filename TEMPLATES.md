# Custom Knowledge Base Templates

This document provides templates for creating custom knowledge base files to extend Claude Desktop projects with company-specific knowledge.

---

## Table of Contents

1. [Company Technology Standards Template](#company-technology-standards)
2. [Internal Architecture Patterns Template](#internal-architecture-patterns)
3. [Compliance Requirements Template](#compliance-requirements)
4. [Historical ADR Template](#historical-adr-library)
5. [Domain-Specific Patterns Template](#domain-specific-patterns)
6. [Integration Catalog Template](#integration-catalog)

---

## Company Technology Standards

**Filename:** `kb-company-tech-standards.md`
**Purpose:** Document approved technologies, frameworks, and tools
**Project:** All projects benefit, especially Architecture Designer

### Template

```markdown
# kb-company-tech-standards.md

## Overview
This document defines [Company Name]'s approved technology standards for software
development. All new projects must adhere to these standards unless exceptions
are explicitly approved by the Architecture Review Board.

**Last Updated:** [Date]
**Maintained By:** [Team/Person]

---

## Backend Technologies

### Programming Languages

| Language | Status | Use Cases | Version | Notes |
|----------|--------|-----------|---------|-------|
| TypeScript | Approved (Preferred) | All new services | 5.x+ | Mandatory for new Node.js projects |
| Python | Approved | Data science, ML, automation | 3.11+ | Not for web services |
| Java | Approved | Legacy maintenance only | 17+ | No new Java projects |
| Go | Under Evaluation | High-performance services | 1.21+ | Requires ARB approval |
| Rust | Not Approved | - | - | Too specialized, limited team expertise |

**Decision Framework:**
1. Default to TypeScript for new services
2. Python only for data science use cases
3. Request ARB approval for Go
4. Justify significant business value for new languages

### Backend Frameworks

| Framework | Language | Status | Use Cases |
|-----------|----------|--------|-----------|
| Express.js | TypeScript | Approved | REST APIs, webhooks |
| Nest.js | TypeScript | Approved | Complex services with DI |
| FastAPI | Python | Approved | ML model APIs |
| Spring Boot | Java | Legacy Only | No new projects |

---

## Frontend Technologies

### Frameworks

| Framework | Status | Use Cases | Version |
|-----------|--------|-----------|---------|
| React | Approved (Preferred) | Web applications | 18.x+ |
| Next.js | Approved | Full-stack apps, SSR | 14.x+ |
| Vue.js | Not Approved | - | - |
| Angular | Legacy Only | Maintenance only | - |
| Svelte | Under Evaluation | Pilot projects only | - |

### UI Component Libraries

| Library | Status | Use Cases |
|---------|--------|-----------|
| Material-UI (MUI) | Approved (Preferred) | Internal tools |
| Chakra UI | Approved | Customer-facing apps |
| Tailwind CSS | Approved | Utility-first styling |
| Bootstrap | Legacy Only | Maintenance only |

---

## Databases

### Relational Databases

| Database | Status | Use Cases | Version |
|----------|--------|-----------|---------|
| PostgreSQL | Approved (Preferred) | Primary database | 15.x+ |
| MySQL | Approved | Legacy systems | 8.x+ |
| SQL Server | Not Approved | - | - |

**Decision Rules:**
- PostgreSQL for all new projects
- MySQL only for legacy integration
- Require ARB approval for NoSQL databases

### NoSQL Databases

| Database | Status | Use Cases | Approval Required |
|----------|--------|-----------|-------------------|
| Redis | Approved | Caching, sessions | No |
| MongoDB | Conditional | Document storage with strong justification | Yes (ARB) |
| DynamoDB | Conditional | AWS serverless only | Yes (ARB) |
| Elasticsearch | Approved | Search, analytics | No |

---

## Cloud Platform

### Primary Provider: [AWS/Azure/GCP]

**Mandate:** All production workloads must run on [Provider].

**Approved Services:**
- Compute: [EC2/App Service/Compute Engine], [Lambda/Functions/Cloud Functions]
- Storage: [S3/Blob Storage/Cloud Storage]
- Database: [RDS/Azure Database/Cloud SQL]
- Caching: [ElastiCache/Redis Cache/Memorystore]
- Message Queue: [SQS/Service Bus/Pub/Sub]
- Event Streaming: [Kinesis/Event Hubs/Pub/Sub]

**Prohibited Services:**
- [List services not allowed]

---

## DevOps & Infrastructure

### CI/CD

| Tool | Status | Use Cases |
|------|--------|-----------|
| GitHub Actions | Approved (Preferred) | All CI/CD pipelines |
| Azure DevOps | Approved | Azure-specific deployments |
| Jenkins | Legacy Only | Phase out by Q4 2025 |

### Infrastructure as Code

| Tool | Status | Use Cases |
|------|--------|-----------|
| Terraform | Approved (Preferred) | Multi-cloud IaC |
| CloudFormation | Conditional | AWS-only projects |
| Bicep | Conditional | Azure-only projects |

### Container Orchestration

| Tool | Status | Use Cases |
|------|--------|-----------|
| Docker | Approved | All containerization |
| Kubernetes | Conditional | Requires ARB approval |
| ECS/ACS/GKE | Approved | Cloud-native orchestration |

---

## Monitoring & Observability

### Application Monitoring

| Tool | Status | Purpose |
|------|--------|---------|
| [Application Insights/Datadog/New Relic] | Approved (Standard) | APM, distributed tracing |
| Prometheus | Approved | Metrics collection |
| Grafana | Approved | Metrics visualization |

### Logging

| Tool | Status | Purpose |
|------|--------|---------|
| [CloudWatch/Log Analytics/Cloud Logging] | Approved (Standard) | Centralized logging |
| ELK Stack | Legacy Only | Phase out by Q4 2025 |

---

## Security & Compliance

### Authentication & Authorization

| Solution | Status | Use Cases |
|----------|--------|-----------|
| [Cognito/Azure AD/Cloud Identity] | Approved (Standard) | User authentication |
| OAuth 2.0 / OIDC | Approved | API authentication |
| SAML | Approved | Enterprise SSO |
| Custom auth | Not Approved | Security risk |

### Secrets Management

| Tool | Status | Purpose |
|------|--------|---------|
| [Secrets Manager/Key Vault/Secret Manager] | Approved (Standard) | Application secrets |
| HashiCorp Vault | Approved | Multi-cloud secrets |
| Environment variables | Not Approved for Production | Development only |

---

## Development Tools

### Version Control

| Tool | Status |
|------|--------|
| Git | Required |
| GitHub | Approved (Standard) |

### Package Managers

| Language | Tool | Status |
|----------|------|--------|
| TypeScript/JavaScript | npm | Approved (Preferred) |
| TypeScript/JavaScript | yarn | Approved |
| TypeScript/JavaScript | pnpm | Under Evaluation |
| Python | pip + venv | Approved |
| Python | poetry | Approved |

---

## Compliance Requirements

### Data Residency
- All production data must reside in [Region/Country]
- No data replication outside of approved regions

### Encryption
- Encryption at rest: Required for all databases and file storage
- Encryption in transit: TLS 1.2+ required for all network communication

### Audit Logging
- All data access must be logged
- Logs retained for [X] years
- Logs must include: User, action, timestamp, IP address, resource

---

## Exception Process

### How to Request Exception

1. Submit exception request to Architecture Review Board
2. Include:
   - Technology requested
   - Business justification
   - Risk analysis
   - Timeline and scope
   - Migration plan (if temporary)
3. ARB reviews within 2 weeks
4. Approval valid for single project only

### Exception Criteria

**Approved if:**
- Compelling business value (quantified)
- No approved alternative exists
- Team has required expertise
- Exit strategy defined

**Denied if:**
- Approved alternative available
- Adds significant risk
- Team lacks expertise
- No clear ROI

---

## Version History

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0 | [Date] | Initial standards | [Name] |

---

## Additional Resources

- Internal Wiki: [URL]
- ARB Meeting Schedule: [URL]
- Exception Request Form: [URL]
```

---

## Internal Architecture Patterns

**Filename:** `kb-internal-patterns.md`
**Purpose:** Document company-specific architectural patterns and practices
**Project:** Architecture Designer, Technical Requirements Creator

### Template

```markdown
# kb-internal-patterns.md

## Overview
Company-specific architectural patterns used across [Company Name] applications.
These patterns have been validated in production and should be the first choice
for common scenarios.

---

## Pattern 1: [Pattern Name]

### Description
[1-2 sentence description of what this pattern is]

### When to Use
- [Scenario 1]
- [Scenario 2]
- [Scenario 3]

### When to Avoid
- [Anti-scenario 1]
- [Anti-scenario 2]

### Architecture Diagram
```
[ASCII or Mermaid diagram showing pattern]
```

### Technology Stack (Company Standard)
- **Backend:** [Specific framework/version]
- **Database:** [Specific database/version]
- **Message Queue:** [Specific queue/version]
- **Hosting:** [Specific platform/config]

### Example Implementations
- **Project A**: [Description, link to repo]
- **Project B**: [Description, link to repo]

### Key Considerations
1. **Scaling:** [How this pattern scales]
2. **Cost:** [Typical cost profile]
3. **Team Size:** [Recommended team size]
4. **Complexity:** [Low/Medium/High]

### Common Pitfalls
- [Pitfall 1 and how to avoid]
- [Pitfall 2 and how to avoid]

### Related Patterns
- See [Other Pattern] for [related scenario]

---

## Pattern 2: API Gateway with Backend Services

### Description
Centralized API gateway routing requests to multiple backend microservices with
shared authentication, rate limiting, and monitoring.

### When to Use
- More than 3 backend services
- Need centralized authentication
- Multiple client types (web, mobile, partners)
- API versioning required
- Rate limiting needed

### When to Avoid
- Single monolithic application
- Fewer than 3 services
- Team unfamiliar with API gateway patterns
- No immediate need for API management

### Architecture Diagram
```
┌─────────────┐
│   Clients   │
│ (Web/Mobile)│
└──────┬──────┘
       │
       ↓
┌─────────────────────────────────┐
│   API Gateway (Kong/APIM)       │
│ - Authentication                │
│ - Rate Limiting                 │
│ - Request/Response Transform    │
│ - Monitoring                    │
└────┬─────┬─────┬──────┬────────┘
     │     │     │      │
     ↓     ↓     ↓      ↓
┌────────┐ ┌─────┐ ┌─────┐ ┌──────┐
│User Svc│ │Order│ │Pay  │ │Search│
└────────┘ └─────┘ └─────┘ └──────┘
     │        │       │        │
     ↓        ↓       ↓        ↓
┌──────────────────────────────────┐
│        Shared PostgreSQL         │
└──────────────────────────────────┘
```

### Technology Stack (Company Standard)
- **API Gateway:** Kong Enterprise (on Kubernetes)
- **Backend Services:** Express.js + TypeScript
- **Database:** PostgreSQL 15 (shared or per-service)
- **Message Queue:** Azure Service Bus (for async communication)
- **Monitoring:** Application Insights + custom dashboards

### Example Implementations
- **Customer Portal v2**: 5 backend services, 50K requests/day
- **Partner API Platform**: 8 backend services, 200K requests/day

### Key Considerations
1. **Scaling:** Gateway scales horizontally, can handle 100K+ req/min
2. **Cost:** $500-1000/month for gateway + service hosting
3. **Team Size:** 8-15 developers (2 per service)
4. **Complexity:** Medium-High (requires DevOps expertise)

### Common Pitfalls
1. **Shared Database Anti-Pattern**
   - Problem: All services sharing one database
   - Solution: Each service has own database or schema
   - Reference: kb-anti-patterns.md section on "Distributed Monolith"

2. **Synchronous Service Chains**
   - Problem: Service A → B → C → D (blocking calls)
   - Solution: Use message queue for async communication
   - Max depth: 2 levels of synchronous calls

3. **No Circuit Breakers**
   - Problem: One slow service cascades to all
   - Solution: Implement circuit breaker pattern (Polly library)

### Related Patterns
- See "Event-Driven Microservices" for async communication
- See "BFF Pattern" for client-specific APIs

---

[Continue with additional patterns...]

---

## Pattern Selection Decision Tree

```
START: Do you have 1 service or many?
├─ 1 Service
│  └─> Use "Modular Monolith Pattern"
└─ Many Services (3+)
   ├─> Need real-time sync?
   │   ├─ YES → Use "API Gateway with Backend Services"
   │   └─ NO  → Use "Event-Driven Microservices"
   └─> Ultra high scale (1M+ users)?
       └─> Use "CQRS + Event Sourcing Pattern"
```

---

## Anti-Patterns to Avoid

### 1. The God Service
**What it is:** Single service handling 50+ endpoints and 10+ domains
**Why it's bad:** Impossible to maintain, slow deployment, unclear ownership
**How to fix:** Split into domain-specific services
**Reference:** kb-anti-patterns.md for full case study

### 2. Database Per Developer
**What it is:** Each developer runs own database, different schemas
**Why it's bad:** Integration bugs, deployment failures, data inconsistencies
**How to fix:** Shared development database with migrations
**Reference:** Internal wiki on development environment standards

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | [Date] | Initial patterns |
```

---

## Compliance Requirements

**Filename:** `kb-compliance-requirements.md`
**Purpose:** Document regulatory and compliance requirements
**Project:** Architecture Designer, Technical Requirements Creator

### Template

```markdown
# kb-compliance-requirements.md

## Overview
Compliance requirements for [Company Name] applications. All new systems must
adhere to applicable regulations based on data handled and customer base.

---

## HIPAA (Health Insurance Portability and Accountability Act)

### Applicability
**When Required:**
- System handles Protected Health Information (PHI)
- System accessed by healthcare providers
- System integrates with HIPAA-covered entities

**PHI Examples:**
- Patient names + health information
- Medical record numbers
- Diagnostic codes
- Treatment information
- Prescription data
- Lab results

### Technical Requirements

#### 1. Access Control (164.312(a)(1))
- [ ] Unique user IDs for all users
- [ ] Emergency access procedures
- [ ] Automatic logoff after inactivity
- [ ] Encryption of authentication credentials

**Implementation:**
- Use [Company Auth Service] for authentication
- Session timeout: 15 minutes inactivity
- MFA required for PHI access
- Role-based access control (RBAC)

#### 2. Audit Controls (164.312(b))
- [ ] Log all PHI access (read, write, delete)
- [ ] Logs must include: user, action, timestamp, IP, resource
- [ ] Logs retained for 6 years
- [ ] Logs protected from modification

**Implementation:**
- Use [Company Logging Service]
- Enable audit log immutability
- Quarterly log reviews required
- Automated alerts for suspicious access

#### 3. Integrity Controls (164.312(c)(1))
- [ ] Detect unauthorized PHI modification
- [ ] Digital signatures for critical data
- [ ] Checksums for transmitted data

**Implementation:**
- Database triggers for audit trail
- API payload signing (HMAC-SHA256)
- File integrity monitoring (FIM)

#### 4. Transmission Security (164.312(e)(1))
- [ ] Encryption in transit (TLS 1.2+)
- [ ] Network segmentation for PHI
- [ ] VPN for remote access

**Implementation:**
- TLS 1.3 preferred, 1.2 minimum
- PHI network isolated from public internet
- VPN with MFA for remote access

#### 5. Encryption at Rest (164.312(a)(2)(iv))
- [ ] Database encryption (AES-256)
- [ ] File storage encryption
- [ ] Backup encryption

**Implementation:**
- Enable RDS encryption
- S3 bucket encryption (SSE-S3 or SSE-KMS)
- Encrypted EBS volumes

### Business Associate Agreements (BAAs)

**Required BAAs with:**
- Cloud providers (AWS, Azure, GCP)
- Email services (SendGrid, Mailgun)
- Analytics (if processing PHI)
- Monitoring (if logs contain PHI)
- Data storage (backup providers)

**Not Required:**
- Services that never touch PHI
- Pure infrastructure (load balancers, CDN without logs)

### HIPAA Compliance Checklist

Use this checklist for every HIPAA-regulated project:

- [ ] Completed risk assessment
- [ ] Documented policies and procedures
- [ ] Workforce trained on HIPAA (annually)
- [ ] BAAs signed with all vendors
- [ ] Access controls implemented
- [ ] Audit logging enabled
- [ ] Encryption at rest configured
- [ ] Encryption in transit enforced (TLS 1.2+)
- [ ] Incident response plan documented
- [ ] Breach notification procedures defined
- [ ] Regular security audits scheduled
- [ ] Penetration testing completed (annually)

---

## PCI DSS (Payment Card Industry Data Security Standard)

### Applicability
**When Required:**
- System stores, processes, or transmits credit card data
- System integrates with payment processors

**Recommended Approach:**
**DON'T store card data** - Use payment processor tokens instead (Stripe, Braintree)

### If You Must Handle Card Data

#### Requirement 1: Firewall Configuration
- [ ] Network segmentation (cardholder data environment isolated)
- [ ] DMZ for public-facing applications
- [ ] Deny all inbound traffic by default

#### Requirement 2: No Default Passwords
- [ ] Change all vendor-supplied defaults
- [ ] Remove unnecessary accounts
- [ ] Document all system components

#### Requirement 3: Protect Stored Cardholder Data
- [ ] Encrypt primary account numbers (PAN)
- [ ] Mask PAN in application (show last 4 digits only)
- [ ] Render data unreadable (encryption, truncation, hashing)
- [ ] Secure encryption key management

#### Requirement 4: Encrypt Transmission
- [ ] TLS 1.2+ for card data transmission
- [ ] Never send PAN via unencrypted channels (email, SMS, chat)

#### Requirement 10: Log and Monitor Access
- [ ] Log all access to cardholder data
- [ ] Daily log reviews
- [ ] Automated alerts for anomalies

### PCI DSS Levels

| Level | Transaction Volume | Requirements |
|-------|-------------------|--------------|
| 1 | >6M transactions/year | Annual on-site audit (QSA) |
| 2 | 1M-6M transactions/year | Annual Self-Assessment Questionnaire (SAQ) |
| 3 | 20K-1M transactions/year | Annual SAQ |
| 4 | <20K transactions/year | Annual SAQ |

**[Company] Level:** [X] (as of [Date])

---

## SOX (Sarbanes-Oxley Act)

### Applicability
- Company is publicly traded
- System handles financial reporting data
- System affects financial controls

### Technical Controls

#### 1. Access Controls
- [ ] Segregation of duties (SOD)
- [ ] Principle of least privilege
- [ ] Quarterly access reviews

#### 2. Change Management
- [ ] All changes require approval
- [ ] Testing before production
- [ ] Change log maintained

#### 3. Audit Trail
- [ ] All financial data changes logged
- [ ] Logs tamper-proof
- [ ] Retained for 7 years

---

## GDPR (General Data Protection Regulation)

### Applicability
- Company has EU customers
- System processes EU resident data

### Key Requirements

#### 1. Right to Access
- Users can request all their data
- Must provide within 30 days
- Machine-readable format

#### 2. Right to Erasure
- Users can request deletion
- Must delete within 30 days
- Exceptions for legal obligations

#### 3. Data Portability
- Users can export their data
- Common format (JSON, CSV)

#### 4. Breach Notification
- Notify authorities within 72 hours
- Notify affected users without delay

---

## Implementation Guidance by Project Type

### Web Application (Non-Healthcare)
**Minimum Requirements:**
- SOC 2 Type II controls
- GDPR compliance (if EU users)
- Standard security practices

**Optional:**
- HIPAA (only if handling PHI)
- PCI DSS (only if handling cards directly)

### Healthcare Application
**Required:**
- HIPAA compliance (full)
- SOC 2 Type II
- GDPR compliance (if EU users)

**Implementation Priority:**
1. HIPAA access controls and audit logging (highest priority)
2. Encryption (at rest and in transit)
3. BAA execution with all vendors
4. Risk assessment and documentation
5. Workforce training

### Financial Application
**Required:**
- SOX compliance
- SOC 2 Type II
- PCI DSS (if handling card data)

---

## Vendor Selection Checklist

Before selecting a vendor:

- [ ] Vendor has required certifications (SOC 2, HIPAA, PCI)
- [ ] BAA available (if applicable)
- [ ] Security questionnaire completed
- [ ] Incident response process documented
- [ ] Data residency confirmed
- [ ] Encryption standards meet requirements
- [ ] Audit rights included in contract

---

## Resources

- Internal Compliance Wiki: [URL]
- Security Team Contact: [Email]
- Compliance Training: [URL]
- Incident Reporting: [URL]
```

---

## How to Use These Templates

1. **Copy template** to your project's `files/` directory
2. **Customize** with your company's specific information
3. **Upload** to Claude Desktop project knowledge base
4. **Reference** in `project-instructions.md`:

```markdown
## Company-Specific Knowledge

Reference these files for company standards:
- `kb-company-tech-standards.md` - Approved technologies
- `kb-internal-patterns.md` - Proven architectural patterns
- `kb-compliance-requirements.md` - Regulatory requirements

When recommending technologies or architectures:
1. Check company standards first
2. Only recommend approved options
3. Justify exceptions with strong rationale and ARB approval process
```

---

*For additional templates or questions, see [CONTRIBUTING.md](CONTRIBUTING.md)*
