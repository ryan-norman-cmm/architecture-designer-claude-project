# CMM Platform Services & Capabilities Inventory
# =============================================================================
# OPERATIONAL SERVICES
# =============================================================================

operational_services:
 universal_starting_platform:
   name: "Universal Starting Platform (USP)"
   type: "frontend_application"
   primary_purpose: "Single frontend platform for PA, Enrollment, and Affordability services"
   capabilities:
     - "SMART on FHIR launch from EHR systems"
     - "Patient import via EHR and batch processing"
     - "PA form search and initiation UI"
     - "Multi-service frontend foundation"
   use_for_requirements:
     - "Frontend PA workflow implementations"
     - "EHR-launched applications"
     - "Frontend provider experiences"


 ehr_connect:
   name: "EHR Connect Service"
   type: "service_api_fhir"
   primary_purpose: "EHR integration and interoperability"
   capabilities:
     - "iKnowMed EHR FHIR API integration"
     - "Epic EHR FHIR API integration"
     - "FHIR-compliant healthcare system connectivity"
   use_for_requirements:
     - "EHR data retrieval workflows"
     - "Patient data import"
     - "Insurance import from provider systems
     - "Clinical data import scenarios"

 form_capture_service:
   name: "Form Capture Service"
   type: "service_api_fhir"
   primary_purpose: "Render, complete, and submit healthcare forms"
   capabilities:
     - "Render, complete, and submit prior authorization forms"
     - "Render, complete, and submit enrollment forms"
     - "Structured Data Capture compliant"
   use_for_requirements:
     - "Completing healthcare forms"
     - "Submitting healthcare forms"
     - "Viewing healthcare forms"

 rbac_service:
   name: "Role-Based Access Control"
   type: "service_security"
   provider: "Health Samurai Aidbox"
   primary_purpose: "Healthcare-compliant access control and permissions"
   capabilities:
     - "Granular role-based permissions"
     - "Healthcare-specific access patterns"
     - "FHIR resource-level security"
     - "OAuth2 integration"
   use_for_requirements:
     - "User role definitions"
     - "Resource access control"
     - "Healthcare compliance security"

 audit_service:
   name: "Healthcare Compliant Audit Service"
   type: "service_compliance"
   provider: "Health Samurai Aidbox"
   primary_purpose: "Compliance and audit trail management"
   capabilities:
     - "HIPAA-compliant audit logging"
     - "Healthcare regulatory compliance tracking"
     - "Automated audit trail generation"
     - "User action tracking"
   use_for_requirements:
     - "Compliance audit trails"
     - "User activity monitoring"
     - "Regulatory reporting"

 secrets_management:
   name: "Azure Key Vault"
   type: "infrastructure_security"
   primary_purpose: "Secure secrets and credential management"
   capabilities:
     - "API keys and password storage"
     - "Certificate management"
     - "Secure credential distribution"
     - "Automated secret rotation"
   use_for_requirements:
     - "External system authentication"
     - "API key management"
     - "Certificate handling"

# =============================================================================
# SERVICES REQUIRING MODIFICATION
# =============================================================================

services_requiring_modification:
 user_service:
   name: "User Management Service"
   type: "service_api_fhir"
   primary_purpose: "User CRUD operations and profile management"
   capabilities:
     - "User profile management"
     - "Basic user CRUD operations"
     - "FHIR-compliant user resources"
   use_for_requirements:
     - "User management workflows"
     - "Profile customization features"
     - "User preference handling"

 provider_service:
   name: "Provider Management Service"
   type: "service_api_fhir"
   primary_purpose: "Provider and organization management"
   capabilities:
     - "Provider CRUD operations"
     - "Organization management"
     - "Basic provider data storage"
   use_for_requirements:
     - "Provider directory management"
     - "Provider-patient relationships"
     - "Organization hierarchies"

 patient_service:
   name: "Patient Management Service"
   type: "service_api_fhir"
   primary_purpose: "Patient and organization management"
   capabilities:
     - "Patient CRUD operations"
     - "Master patient identifier"
     - "Basic Patient data storage"
   use_for_requirements:
     - "Master patient management"
     - "Patient relationships"
     - "Organization hierarchies"

 communication_service:
   name: "Communication Service"
   aka: "Orca"
   type: "service_api_non_fhir"
   primary_purpose: "Unified communication facade over multiple vendors"
   capabilities:
     - "Email vendor integration"
     - "SMS vendor integration"
     - "Multi-channel communication"
     - "Template-based messaging"
   use_for_requirements:
     - "Patient notification workflows"
     - "Provider communication"
     - "Automated messaging scenarios"

# =============================================================================
# SERVICES IN DEVELOPMENT
# =============================================================================

services_in_development:
  consent_service:
   name: "Consent Service"
   type: "service_api_fhir"
   primary_purpose: "Patient, provider, and user consent management"
   capabilities:
     - "FHIR-compliant consent tracking"
     - "Patient authorization workflows"
     - "Consent lifecycle management"
     - "RxLightning integration"
   use_for_requirements:
     - "Patient consent workflows"
     - "Authorization management"
     - "Consent tracking scenarios"
     - "FHIR-compliant consent events"

 prior_authorization_service:
   name: "Prior Authorization Service"
   type: "service_api_fhir"
   primary_purpose: "PA lifecycle management using Da Vinci ePA Implementation Guide"
   capabilities:
     - "FHIR-compliant PA request handling"
     - "Da Vinci ePA Implementation Guide adherence"
     - "PA workflow orchestration"
     - "Multi-payer PA processing"
   use_for_requirements:
     - "Prior authorization workflows"
     - "PA status tracking"
     - "Multi-payer PA scenarios"
     - "FHIR-compliant pharmacy and medical PA events"

 benefits_service:
   name: "Benefits Service"
   type: "service_api_fhir"
   primary_purpose: "Patient coverage benefit information retrieval"
   capabilities:
     - "Coverage verification requests"
     - "Benefit information retrieval"
     - "Insurance eligibility checking"
     - "Real-time benefit validation"
   use_for_requirements:
     - "Benefits verification workflows"
     - "Coverage validation scenarios"
     - "Eligibility checking processes"
     - "FHIR-compliant benefits events"

 notification_service:
   name: "Notification Service"
   type: "service_api_fhir"
   primary_purpose: "Event-triggered notification delivery"
   capabilities:
     - "FHIR-compliant notification management"
     - "Multi-channel notification delivery"
     - "Event-driven messaging"
     - "Real-time notification processing"
   use_for_requirements:
     - "Real-time notification workflows"
     - "Event-triggered communications"
     - "Multi-channel messaging scenarios"
     - "FHIR-compliant communication events"

# =============================================================================
# PLATFORM INFRASTRUCTURE
# =============================================================================

platform_infrastructure:
 aidbox_fhir_server:
   name: "Health Samurai Aidbox"
   type: "infrastructure_data"
   primary_purpose: "FHIR R4 resource storage and retrieval"
   capabilities:
     - "FHIR REST and GraphQL APIs"
     - "RBAC integration with OAuth2"
     - "PostgreSQL-based FHIR data storage"
     - "Event broker integration for FHIR events"
     - "FHIR Implementation Guide support"
     - "Resource validation and profiling"
   use_for_requirements:
     - "FHIR resource storage and retrieval"
     - "Healthcare data standardization"
     - "API-based data access patterns"
     - "Audit needs"
     - "Authorization needs"

 confluent_kafka:
   name: "Confluent Kafka"
   type: "infrastructure_messaging"
   primary_purpose: "Event streaming and message persistence"
   capabilities:
     - "Real-time event processing"
     - "Message durability and replay"
     - "Event-driven architecture support"
     - "Stream processing capabilities"
   use_for_requirements:
     - "Event-driven architectures"
     - "Real-time data streaming"
     - "Asynchronous processing workflows"

 apollo_graphql:
   name: "Apollo GraphQL Router"
   type: "infrastructure_api"
   primary_purpose: "Supergraph hosting for federated service integration"
   capabilities:
     - "REST API connectors for quick integration"
     - "Developer studio for graph exploration"
     - "Subgraph deployment pipeline"
     - "Federated GraphQL architecture"
     - "Query optimization and caching"
   use_for_requirements:
     - "Federated API architectures"
     - "Service composition scenarios"
     - "Developer-friendly API exploration"

 mulesoft_gateway:
   name: "MuleSoft API Gateway"
   type: "infrastructure_api"
   primary_purpose: "API management, routing, and security"
   capabilities:
     - "Request routing and load balancing"
     - "Rate limiting and throttling"
     - "Authentication and authorization"
     - "API lifecycle management"
     - "Analytics and monitoring"
   use_for_requirements:
     - "API gateway patterns"
     - "External system integrations"
     - "API security and management"

 okta_identity:
   name: "Okta Identity Provider"
   type: "infrastructure_identity"
   primary_purpose: "Enterprise SSO and user provisioning"
   capabilities:
     - "OAuth2 scopes management"
     - "OIDC capabilities"
     - "Enterprise identity integration"
     - "User provisioning and deprovisioning"
     - "Multi-factor authentication"
   use_for_requirements:
     - "Enterprise authentication workflows"
     - "OAuth2-based authorization"
     - "Identity federation scenarios"

 datadog_apm:
   name: "DataDog Application Performance Management"
   type: "infrastructure_monitoring"
   primary_purpose: "Infrastructure and application monitoring"
   capabilities:
     - "Performance monitoring and alerting"
     - "Error tracking and analysis"
     - "Infrastructure metrics collection"
     - "Application observability"
     - "Custom dashboard creation"
   use_for_requirements:
     - "Performance monitoring requirements"
     - "Error handling and alerting"
     - "System observability needs"

 pendo_analytics:
   name: "Pendo User Analytics"
   type: "infrastructure_analytics"
   primary_purpose: "User behavior tracking and product insights"
   capabilities:
     - "User interaction analytics"
     - "Product usage metrics"
     - "Behavioral insights and reporting"
     - "Feature adoption tracking"
   use_for_requirements:
     - "User behavior analysis"
     - "Product usage tracking"
     - "Feature adoption measurement"

 ibm_bamoe:
   name: "IBM BAMOE"
   type: "infrastructure_workflow"
   primary_purpose: "Business process and decision management"
   capabilities:
     - "Business process modeling (BPMN)"
     - "Decision management (DMN)"
     - "Workflow orchestration"
     - "Rule-based automation"
     - "Process monitoring and analytics"
   use_for_requirements:
     - "Complex workflow orchestration"
     - "Business rule management"
     - "Multi-step process automation"

# =============================================================================
# EXTERNAL INTEGRATIONS
# =============================================================================

external_integrations:
 fastauth:
   name: "FastAuth"
   type: "acquired_integration"
   primary_purpose: "Medical PA processing and submission"
   capabilities:
     - "Medical PA initiation and submission"
     - "Real-time medical PA status updates"
     - "Medical PA routing decisions"
   use_for_requirements:
     - "Medical  PA submission workflows"
     - "Medical PA status tracking scenarios"
     - "Medical PA routing"

 cmm_epa:
   name: "CoverMyMeds ePA"
   aka: "CMM ePA"
   type: "legacy_integration"
   primary_purpose: "Pharmacy PA processing system"
   capabilities:
     - "PharmacyPA initiation via messaging"
     - "PharmacyPA form search and retrieval"
     - "Status updates via events"
     - "Pharmacy PA access management"
   use_for_requirements:
     - "Pharmacy PA system integration"
     - "Pharmacy PA form search and retrieval"

 cmm_benefits:
   name: "CoverMyMeds Benefits"
   aka: "Benefits Module"
   type: "legacy_integration"
   primary_purpose: "Benefits verification and investigation"
   capabilities:
     - "Benefits verification requests"
     - "Coverage investigation workflows"
     - "Real-time verification status"
     - "Insurance eligibility validation"
   use_for_requirements:
     - "Benefits verification workflows"
     - "Coverage investigation processes"
     - "Insurance eligibility validation"

 rxlightning:
   name: "RxLightning Enrollment & Patient Consent"
   type: "acquisition_integration"
   primary_purpose: "Patient enrollment and consent management"
   capabilities:
     - "Patient enrollment workflows"
     - "Consent management processes"
     - "Enrollment form search and handling"
   use_for_requirements:
     - "Patient enrollment workflows"
     - "Consent management processes"
     - "Enrollment form handling"
     - "Specialty hub integrations"
