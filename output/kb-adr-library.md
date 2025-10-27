# Healthcare Architecture Decision Records Library

**Purpose:** Template and examples of Architecture Decision Records (ADRs) for healthcare enterprise systems with HIPAA, SOX, and SOC 2 compliance considerations.

**Target Audience:** Technical architects, engineering leads, and compliance officers documenting major architectural decisions.

**Last Updated:** October 2025

---

## ADR Template

```markdown
# ADR-XXX: [Decision Title]

**Status:** [Proposed | Accepted | Deprecated | Superseded]
**Date:** YYYY-MM-DD
**Deciders:** [List of decision makers]
**Technical Story:** [Ticket/Issue reference]

## Context and Problem Statement

[Describe the context and problem that needs to be solved. Include business drivers, technical constraints, and compliance requirements.]

## Decision Drivers

* [Driver 1 - e.g., HIPAA compliance requirement]
* [Driver 2 - e.g., Team expertise]
* [Driver 3 - e.g., Performance requirements]

## Considered Options

* [Option 1]
* [Option 2]
* [Option 3]

## Decision Outcome

**Chosen option:** "[Option X]"

**Rationale:** [Explain why this option was chosen]

## Consequences

### Positive
* [Positive consequence 1]
* [Positive consequence 2]

### Negative
* [Negative consequence 1]
* [Mitigation: How we'll address this]

## Compliance Impact

**HIPAA:** [Impact on PHI protection, audit trails, encryption]
**SOX:** [Impact on financial data integrity, change control]
**SOC 2:** [Impact on security, availability, confidentiality]

## Implementation Notes

[Technical details for implementation team]

## References

* [Link to related documentation]
* [Link to compliance requirements]
```

---

## ADR-001: Azure PostgreSQL as Primary Database

**Status:** Accepted
**Date:** 2025-10-27
**Deciders:** Architecture Team, DBA Team
**Technical Story:** ARCH-1001

### Context and Problem Statement

Healthcare application needs relational database for patient demographics, clinical orders, and billing data. Must support FHIR JSON storage, provide encryption at rest/transit, and enable complete audit logging for HIPAA compliance.

### Decision Drivers

* HIPAA: Encryption, audit logging, access controls required
* Team Expertise: Team experienced with PostgreSQL (40% weight)
* FHIR Support: Native JSONB for FHIR resources
* Cost: Fully managed service reduces operational overhead
* Aidbox Compatibility: Aidbox FHIR server requires PostgreSQL

### Considered Options

1. **Azure Database for PostgreSQL Flexible Server**
2. Azure SQL Database with Always Encrypted
3. Azure Cosmos DB for PostgreSQL

### Decision Outcome

**Chosen option:** "Azure Database for PostgreSQL Flexible Server"

**Rationale:**
- Native JSONB support ideal for FHIR resources
- pgAudit extension provides comprehensive audit logging
- pgcrypto for PHI column-level encryption
- Aidbox FHIR server requires PostgreSQL backend
- Team has PostgreSQL expertise from previous projects
- Zone-redundant high availability for 99.99% SLA

### Consequences

**Positive:**
- JSONB eliminates need for separate document database
- Built-in logical replication for read replicas
- Point-in-time restore for disaster recovery
- Azure-managed backups with 35-day retention (HIPAA compliant)

**Negative:**
- Slightly higher cost than basic Azure SQL ($600/month vs $500)
- Mitigation: JSONB support eliminates second database, net savings

### Compliance Impact

**HIPAA:**
✅ Encryption at rest with customer-managed keys
✅ TLS 1.2+ for data in transit
✅ pgAudit logs all PHI access with timestamp, user, query
✅ 35-day backup retention meets requirements

**SOX:**
✅ Audit logs immutable and tamper-proof
✅ Role-based access control for financial database

**SOC 2:**
✅ High availability with zone redundancy
✅ Automated patching and updates
✅ Azure Monitor integration for alerting

### Implementation Notes

```hcl
# Terraform configuration
resource "azurerm_postgresql_flexible_server" "main" {
  name                   = "psql-healthcare-prod"
  resource_group_name    = azurerm_resource_group.main.name
  location               = "eastus"
  version                = "15"
  administrator_login    = "healthcare_admin"
  storage_mb             = 32768
  sku_name               = "GP_Standard_D4s_v3"

  high_availability {
    mode = "ZoneRedundant"
  }

  backup_retention_days = 35

  tags = {
    compliance          = "HIPAA,SOX"
    data_classification = "PHI"
  }
}
```

### References

- [Azure PostgreSQL Documentation](https://docs.microsoft.com/azure/postgresql/)
- [pgAudit Extension](https://www.pgaudit.org/)
- [Aidbox PostgreSQL Requirements](https://docs.aidbox.app/)

---

## ADR-002: Confluent Kafka for Event Streaming

**Status:** Accepted
**Date:** 2025-10-27
**Deciders:** Architecture Team, Platform Team

### Context and Problem Statement

Need event-driven architecture for HL7 message processing, clinical workflows, and billing events. Requires complete audit trail, exactly-once semantics for financial transactions, and ability to replay events for regulatory audits.

### Decision Drivers

* SOX: Immutable event log for financial transactions
* HIPAA: Complete audit trail of all PHI access
* Scale: Process 100K+ HL7 messages daily
* Reliability: Exactly-once semantics for billing
* Team Expertise: Team has Kafka experience from prior project

### Considered Options

1. **Confluent Kafka on Azure AKS**
2. Azure Service Bus Premium
3. Azure Event Hubs

### Decision Outcome

**Chosen option:** "Confluent Kafka on Azure AKS"

**Rationale:**
- Event sourcing provides immutable audit trail (SOX requirement)
- Exactly-once semantics prevent duplicate billing charges
- Schema Registry enforces FHIR/HL7 message contracts
- Replay capability for regulatory audits
- Team already Kafka-certified

### Consequences

**Positive:**
- Complete audit trail via event sourcing
- Horizontal scalability to millions of messages/day
- Schema Registry prevents malformed messages
- Kafka Connect integrations with HL7 systems

**Negative:**
- Higher operational complexity than managed Azure Service Bus
- Mitigation: Confluent Cloud manages Kafka operations
- Monthly cost: $2,000 vs $300 for Service Bus
- Mitigation: Audit trail value justifies cost for regulated healthcare

### Compliance Impact

**HIPAA:**
✅ All HL7 messages logged with timestamp, facility, patient ID
✅ TLS 1.3 encryption in transit
✅ Topic-level ACLs restrict PHI access

**SOX:**
✅ Billing events immutable post-publish
✅ 7-year retention for financial event audit
✅ Exactly-once semantics prevent duplicate transactions

**SOC 2:**
✅ Multi-zone deployment with replication factor 3
✅ Automated backups to Azure Blob Storage

### Implementation Notes

```yaml
# Docker Compose - Kafka cluster
kafka:
  image: confluentinc/cp-kafka:7.5.0
  environment:
    KAFKA_LOG_RETENTION_HOURS: 61320  # 7 years for SOX
    KAFKA_LOG_RETENTION_BYTES: -1      # Unlimited (S3 tiering)
    KAFKA_COMPRESSION_TYPE: gzip
    KAFKA_MIN_INSYNC_REPLICAS: 2
```

### References

- [Confluent Kafka Documentation](https://docs.confluent.io/)
- [Kafka for Healthcare](https://www.confluent.io/blog/healthcare-data-streaming/)

---

## ADR-003: Apollo GraphQL Federation

**Status:** Accepted
**Date:** 2025-10-27
**Deciders:** Architecture Team, API Team

### Context and Problem Statement

Need unified API gateway for microservices (Patient, Clinical, Billing). Must efficiently fetch FHIR resources, minimize over-fetching, and provide type-safe schema for frontend teams.

### Decision Drivers

* Developer Experience: Type-safe schema, single endpoint
* Performance: Minimize API round-trips for clinical workflows
* FHIR Integration: Aidbox provides native GraphQL API
* Team Expertise: Team prefers GraphQL over REST

### Considered Options

1. **Apollo GraphQL Federation**
2. REST API Gateway (Azure API Management)
3. gRPC with Envoy Gateway

### Decision Outcome

**Chosen option:** "Apollo GraphQL Federation"

**Rationale:**
- Single query fetches patient + observations + medications (vs 3 REST calls)
- Aidbox FHIR server has native GraphQL API
- Federation allows independent microservice deployment
- Type-safe schema prevents runtime errors

### Consequences

**Positive:**
- Efficient data fetching reduces API latency by 60%
- Frontend teams use generated TypeScript types
- Federation enables gradual microservices migration

**Negative:**
- Learning curve for team unfamiliar with GraphQL
- Mitigation: 2-week GraphQL training, pair programming
- Complex queries can cause N+1 problems
- Mitigation: DataLoader pattern, query complexity limits

### Compliance Impact

**HIPAA:**
✅ Field-level authorization (hide PHI based on permissions)
✅ GraphQL queries logged for audit trail

**SOX:**
✅ Billing resolver has separate authentication

**SOC 2:**
✅ Query complexity limits prevent DoS attacks

### Implementation Notes

```typescript
// Apollo Federation Gateway
const gateway = new ApolloGateway({
  supergraphSdl: composeServices([
    { name: 'patients', url: 'http://patient-service/graphql' },
    { name: 'clinical', url: 'http://clinical-service/graphql' },
    { name: 'billing', url: 'http://billing-service/graphql' },
  ]),
});
```

### References

- [Apollo Federation Docs](https://www.apollographql.com/docs/federation/)
- [Aidbox GraphQL API](https://docs.aidbox.app/api-1/graphql-api)

---

## ADR-004: Health Samurai Aidbox for FHIR

**Status:** Accepted
**Date:** 2025-10-27
**Deciders:** Architecture Team, Clinical Informatics

### Context and Problem Statement

Need FHIR R4 server for storing clinical resources (Patient, Observation, Condition, Medication). Must support custom FHIR extensions, provide sub-100ms query performance, and integrate with GraphQL API.

### Decision Drivers

* FHIR R4 Compliance: Required for healthcare interoperability
* Performance: Sub-100ms queries for clinical workflows
* Custom Extensions: Hospital-specific FHIR profiles
* GraphQL Support: Integrate with Apollo Federation
* Team Expertise: Team prefers PostgreSQL-backed solution

### Considered Options

1. **Health Samurai Aidbox**
2. HAPI FHIR Server (open source)
3. Azure API for FHIR (managed service)

### Decision Outcome

**Chosen option:** "Health Samurai Aidbox"

**Rationale:**
- Best performance: Sub-100ms queries (vs 500ms+ for HAPI)
- Native GraphQL API integrates with Apollo Federation
- Custom resources without server rebuild
- PostgreSQL-backed (team expertise, familiar ops)
- Commercial support with SLA

### Consequences

**Positive:**
- Excellent performance enables real-time clinical workflows
- GraphQL API reduces frontend API calls
- Custom FHIR profiles without code changes

**Negative:**
- Commercial license: $2,000/month (vs free HAPI)
- Mitigation: Performance and support justify cost
- Vendor lock-in risk
- Mitigation: FHIR R4 compliance ensures data portability

### Compliance Impact

**HIPAA:**
✅ Built-in AuditEvent resource logging
✅ Access control policies at resource level
✅ Encryption at rest (PostgreSQL TDE)

**SOC 2:**
✅ High availability via PostgreSQL zone redundancy

### Implementation Notes

```yaml
# Docker Compose
aidbox:
  image: healthsamurai/aidbox:edge
  environment:
    AIDBOX_LICENSE: ${LICENSE_KEY}
    PGHOST: postgres
    PGDATABASE: aidbox
```

### References

- [Aidbox Documentation](https://docs.aidbox.app/)
- [FHIR R4 Specification](https://hl7.org/fhir/R4/)

---

## ADR-005: DataDog for Observability

**Status:** Accepted
**Date:** 2025-10-27
**Deciders:** Architecture Team, SRE Team

### Context and Problem Statement

Need comprehensive observability platform for distributed tracing, log management, and security monitoring. Must support HIPAA audit log retention (7 years), integrate with OpenTelemetry, and provide PHI access anomaly detection.

### Decision Drivers

* HIPAA: 7-year audit log retention, PHI access monitoring
* Distributed Tracing: Track HL7 messages across microservices
* Team Expertise: Team prefers SaaS over self-hosted
* Cost: Predictable pricing model

### Considered Options

1. **DataDog**
2. Self-hosted ELK Stack + Jaeger
3. Azure Monitor + Application Insights

### Decision Outcome

**Chosen option:** "DataDog"

**Rationale:**
- HIPAA BAA available (compliance requirement)
- OpenTelemetry native support
- Security monitoring detects PHI access anomalies
- SaaS eliminates operational overhead
- Superior APM vs Azure Application Insights

### Consequences

**Positive:**
- Comprehensive observability (traces, metrics, logs) in one platform
- Security monitoring alerts on HIPAA violations
- 7-year log retention with compliance-friendly pricing

**Negative:**
- Cost: $1,500/month (vs $300 for Azure Monitor)
- Mitigation: Reduced SRE toil justifies premium
- Vendor lock-in for logs
- Mitigation: Export to Azure Blob for long-term archive

### Compliance Impact

**HIPAA:**
✅ 7-year log retention meets requirements
✅ PHI access logs with user, timestamp, resource
✅ BAA signed with DataDog

**SOX:**
✅ Financial transaction audit trail

**SOC 2:**
✅ Real-time security monitoring
✅ Anomaly detection for unauthorized access

### Implementation Notes

```yaml
# OTEL Collector Config
exporters:
  datadog:
    api:
      key: ${DATADOG_API_KEY}
    host_metadata:
      tags:
        - compliance:hipaa
        - data_classification:phi
```

### References

- [DataDog HIPAA Compliance](https://www.datadoghq.com/security/)
- [OpenTelemetry Integration](https://docs.datadoghq.com/tracing/setup_overview/open_standards/)

---

## ADR-006: Docker + Terraform for IaC

**Status:** Accepted
**Date:** 2025-10-27
**Deciders:** Architecture Team, Platform Team

### Context and Problem Statement

Need Infrastructure as Code strategy for reproducible environments and HIPAA-compliant change control. Must support local development, CI/CD pipelines, and multi-environment deployments (dev/staging/prod).

### Decision Drivers

* SOX: Change control and audit trail required
* Development Parity: Dev environment matches production
* Team Expertise: Team knows Docker and Terraform
* Cost: Open-source tools preferred

### Considered Options

1. **Docker Compose + Terraform**
2. Kubernetes Helm Charts only
3. Azure Bicep + ARM Templates

### Decision Outcome

**Chosen option:** "Docker Compose + Terraform"

**Rationale:**
- Docker Compose for local dev (easy onboarding)
- Terraform for Azure infrastructure (immutable, versioned)
- Both tools are team expertise and open-source
- Clear separation: Compose (services), Terraform (infra)

### Consequences

**Positive:**
- Git-versioned infrastructure provides audit trail
- Developers run identical services as production
- Terraform state tracks all changes (SOX compliance)

**Negative:**
- Duplication between Compose and Kubernetes manifests
- Mitigation: Generate K8s manifests from Compose with Kompose
- Terraform state management complexity
- Mitigation: Azure Storage backend with state locking

### Compliance Impact

**SOX:**
✅ Git commits provide change control audit trail
✅ Terraform plan approval before apply
✅ Infrastructure changes tracked in state file

**SOC 2:**
✅ Reproducible environments reduce configuration drift
✅ Automated testing in CI/CD pipeline

### Implementation Notes

```bash
# Local development
docker-compose up -d

# Production deployment
terraform plan -out=tfplan
terraform apply tfplan
```

### References

- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/)
- [Docker Compose Docs](https://docs.docker.com/compose/)

---

## ADR-007: OpenTelemetry for Observability

**Status:** Accepted
**Date:** 2025-10-27
**Deciders:** Architecture Team, SRE Team

### Context and Problem Statement

Need vendor-neutral telemetry collection for distributed tracing, metrics, and logs. Must integrate with DataDog, support PHI filtering, and provide HIPAA audit context in traces.

### Decision Drivers

* Vendor Neutrality: Avoid DataDog lock-in for instrumentation
* HIPAA: Filter PHI from traces before export
* Standards: CNCF standard preferred over proprietary
* Team Expertise: Team familiar with OpenTelemetry

### Considered Options

1. **OpenTelemetry**
2. DataDog APM Agent (proprietary)
3. Jaeger (tracing only)

### Decision Outcome

**Chosen option:** "OpenTelemetry"

**Rationale:**
- Vendor-neutral (can switch from DataDog if needed)
- OTEL Collector filters PHI before export
- Single instrumentation supports multiple backends
- CNCF standard with strong ecosystem

### Consequences

**Positive:**
- Flexibility to change APM vendors without re-instrumentation
- Collector filters PHI, reducing compliance risk
- Auto-instrumentation for common frameworks

**Negative:**
- Extra hop (app → collector → DataDog) adds latency
- Mitigation: <10ms overhead acceptable for compliance
- Collector ops overhead
- Mitigation: Run as sidecar in Kubernetes

### Compliance Impact

**HIPAA:**
✅ PHI filtering in collector before export
✅ Trace IDs link to audit logs for investigations

**SOC 2:**
✅ Security monitoring via trace analysis

### Implementation Notes

```typescript
// Auto-instrumentation
import { NodeSDK } from '@opentelemetry/sdk-node';
import { getNodeAutoInstrumentations } from '@opentelemetry/auto-instrumentations-node';

const sdk = new NodeSDK({
  instrumentations: [getNodeAutoInstrumentations()],
});
sdk.start();
```

### References

- [OpenTelemetry Docs](https://opentelemetry.io/docs/)
- [OTEL Collector](https://opentelemetry.io/docs/collector/)

---

## ADR Summary Table

| ID | Decision | Status | Compliance Impact | Monthly Cost |
|----|----------|--------|-------------------|--------------|
| 001 | Azure PostgreSQL | Accepted | HIPAA ✅ SOX ✅ | $600 |
| 002 | Confluent Kafka | Accepted | HIPAA ✅ SOX ✅ | $2,000 |
| 003 | Apollo GraphQL | Accepted | HIPAA ✅ | $0 (OSS) |
| 004 | Aidbox FHIR | Accepted | HIPAA ✅ | $2,000 |
| 005 | DataDog | Accepted | HIPAA ✅ SOX ✅ SOC2 ✅ | $1,500 |
| 006 | Docker + Terraform | Accepted | SOX ✅ SOC2 ✅ | $0 (OSS) |
| 007 | OpenTelemetry | Accepted | HIPAA ✅ SOC2 ✅ | $0 (OSS) |

**Total Monthly Cost (Medium Scale):** ~$6,100

---

**Document Version:** 1.0
**Last Updated:** October 2025
**Maintained By:** Healthcare Architecture Team
