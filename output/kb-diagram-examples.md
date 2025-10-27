# Knowledge Base: Diagram Examples & Best Practices

**Purpose:** Reference guide for generating high-quality Mermaid diagrams in architecture design workflows (REL-002 & REL-003)

**Diagrams Covered:** System Context (C4), Component Architecture, Sequence Diagrams, Entity-Relationship, Deployment Topology

---

## 1. System Context Diagrams (C4)

**Purpose:** Show system boundaries, external actors, and data flows

### ❌ BAD Example - Cluttered, unclear boundaries

```mermaid
graph LR
    User-->System
    System-->DB
    System-->API
    API-->Service
    Service-->Queue
```

**Problems:**
- No clear system boundary
- Generic labels ("System", "API")
- Missing protocols/data flows
- Flat structure (no hierarchy)

### ✅ GOOD Example - Clear boundaries, labeled flows

```mermaid
C4Context
    title System Context - Task Management Application

    Person(user, "User", "Team member managing tasks")
    System(app, "Task Management App", "Web application for task tracking")
    System_Ext(auth, "Auth0", "Authentication provider")
    System_Ext(email, "SendGrid", "Email notifications")

    Rel(user, app, "Uses", "HTTPS")
    Rel(app, auth, "Authenticates", "OAuth 2.0")
    Rel(app, email, "Sends notifications", "SMTP")
```

**Why Better:**
- C4Context syntax for proper boundaries
- Descriptive labels with roles
- Communication protocols specified
- External systems clearly marked (System_Ext)

### ⭐ GREAT Example - Comprehensive with data details

```mermaid
C4Context
    title System Context - E-Commerce Platform

    Person(customer, "Customer", "Purchases products online")
    Person(admin, "Administrator", "Manages inventory and orders")

    System(ecommerce, "E-Commerce Platform", "Product catalog, cart, checkout")

    System_Ext(payment, "Stripe", "Payment processing")
    System_Ext(shipping, "ShipStation", "Order fulfillment")
    System_Ext(email, "SendGrid", "Transactional emails")
    System_Ext(analytics, "Google Analytics", "User behavior tracking")

    Rel(customer, ecommerce, "Browse/purchase", "HTTPS/Web")
    Rel(admin, ecommerce, "Manage inventory", "HTTPS/Admin portal")

    Rel(ecommerce, payment, "Process payments", "REST API/JSON")
    Rel(ecommerce, shipping, "Create shipments", "REST API/XML")
    Rel(ecommerce, email, "Send receipts/updates", "SMTP")
    Rel(ecommerce, analytics, "Track events", "JavaScript SDK")

    UpdateRelStyle(customer, ecommerce, $offsetX="-50", $offsetY="-10")
    UpdateRelStyle(admin, ecommerce, $offsetX="50", $offsetY="-10")
```

**What Makes It Great:**
- Multiple user types with clear roles
- Data format in protocols (JSON, XML)
- Communication method details (REST API, SDK)
- Layout hints for readability (UpdateRelStyle)
- Covers all integration points

**Best Practices:**
- Use C4Context for proper system boundary representation
- Include Person() for users, System() for your app, System_Ext() for external dependencies
- Specify protocols (HTTPS, REST API, SMTP, gRPC)
- Add data formats when relevant (JSON, XML, Protobuf)
- Limit to 5-10 external systems (avoid clutter)

---

## 2. Component Diagrams

**Purpose:** Show internal structure and component relationships

### ❌ BAD Example - Box soup, unclear relationships

```mermaid
graph TD
    A[API] --> B[Service]
    B --> C[DB]
    D[Auth] --> A
    E[Queue] --> B
```

**Problems:**
- No component boundaries or layers
- Unclear what components do
- Missing dependency direction clarity
- No interface definitions

### ✅ GOOD Example - Layered with clear responsibilities

```mermaid
graph TB
    subgraph "API Layer"
        API[API Gateway<br/>REST endpoints, auth]
    end

    subgraph "Business Logic"
        TaskService[Task Service<br/>CRUD operations]
        NotifyService[Notification Service<br/>Email/SMS alerts]
    end

    subgraph "Data Layer"
        DB[(PostgreSQL<br/>Tasks, Users)]
        Cache[(Redis<br/>Session cache)]
    end

    API --> TaskService
    API --> NotifyService
    TaskService --> DB
    TaskService --> Cache
    NotifyService --> Queue[Message Queue]
```

**Why Better:**
- Clear layering (API → Business → Data)
- Component responsibilities described
- Subgraphs show architectural boundaries
- Technology choices specified

### ⭐ GREAT Example - Detailed with interfaces and tech stack

```mermaid
graph TB
    subgraph "Client Layer"
        Web[Web App<br/>React/TypeScript]
        Mobile[Mobile App<br/>React Native]
    end

    subgraph "API Gateway Layer"
        Gateway[API Gateway<br/>Express.js<br/>Auth middleware, rate limiting]
    end

    subgraph "Service Layer"
        AuthSvc[Auth Service<br/>Node.js<br/>JWT validation, user sessions]
        TaskSvc[Task Service<br/>Node.js<br/>Task CRUD, assignments]
        NotifySvc[Notification Service<br/>Node.js<br/>Email/push notifications]
    end

    subgraph "Data Layer"
        PG[(PostgreSQL 14<br/>Primary database<br/>Tasks, Users, Teams)]
        Redis[(Redis 7<br/>Session cache<br/>Rate limit counters)]
    end

    subgraph "External Services"
        Email[SendGrid<br/>Email delivery]
        Push[FCM<br/>Push notifications]
    end

    Web -->|HTTPS/JSON| Gateway
    Mobile -->|HTTPS/JSON| Gateway

    Gateway -->|REST| AuthSvc
    Gateway -->|REST| TaskSvc
    Gateway -->|REST| NotifySvc

    AuthSvc -->|SQL| PG
    AuthSvc -->|GET/SET| Redis

    TaskSvc -->|SQL| PG
    TaskSvc -->|Pub/Sub| NotifySvc

    NotifySvc -->|SMTP| Email
    NotifySvc -->|HTTP| Push

    style Gateway fill:#f9f,stroke:#333,stroke-width:2px
    style PG fill:#bbf,stroke:#333,stroke-width:2px
    style Redis fill:#fbb,stroke:#333,stroke-width:2px
```

**What Makes It Great:**
- Complete tech stack specified (languages, versions)
- Interface protocols on every connection
- Component responsibilities clearly stated
- Color coding for emphasis (optional but helpful)
- Proper layering (Client → Gateway → Services → Data → External)

**Best Practices:**
- Use subgraphs to show architectural layers or modules
- Include technology stack (language, framework, version)
- Specify interfaces (REST, gRPC, SQL, Pub/Sub)
- Add component responsibilities (what each does)
- Show data flow direction clearly
- Limit to 8-12 components (split into multiple diagrams if needed)

---

## 3. Sequence Diagrams

**Purpose:** Show component interactions over time for specific workflows

### ❌ BAD Example - Missing details, no error handling

```mermaid
sequenceDiagram
    User->>API: Request
    API->>DB: Query
    DB->>API: Data
    API->>User: Response
```

**Problems:**
- No specific operation details
- Missing error scenarios
- No timing information
- Generic labels

### ✅ GOOD Example - Specific operations with errors

```mermaid
sequenceDiagram
    participant U as User
    participant A as API Gateway
    participant T as Task Service
    participant D as PostgreSQL

    U->>A: POST /api/tasks<br/>{title, description}
    A->>A: Validate JWT
    A->>T: createTask(userId, data)
    T->>D: INSERT INTO tasks

    alt Success
        D-->>T: taskId=123
        T-->>A: {id: 123, status: "created"}
        A-->>U: 201 Created
    else Validation Error
        T-->>A: {error: "Title required"}
        A-->>U: 400 Bad Request
    else Database Error
        D-->>T: Connection timeout
        T->>T: Log error
        T-->>A: {error: "Service unavailable"}
        A-->>U: 503 Service Unavailable
    end
```

**Why Better:**
- Specific API endpoint and payload
- Error scenarios covered (validation, database)
- HTTP status codes included
- Clear participant labels

### ⭐ GREAT Example - Complete with timing and notes

```mermaid
sequenceDiagram
    participant U as User
    participant A as API Gateway
    participant Auth as Auth Service
    participant Task as Task Service
    participant DB as PostgreSQL
    participant Cache as Redis
    participant Queue as Message Queue

    Note over U,Queue: Create Task Workflow (P95: <300ms)

    U->>+A: POST /api/tasks<br/>{title, description, assignee}
    Note right of A: Rate limit check:<br/>100 req/min per user

    A->>+Auth: validateToken(jwt)
    Auth->>Cache: GET session:{userId}
    Cache-->>Auth: {userId: 123, roles: ["user"]}
    Auth-->>-A: {valid: true, userId: 123}

    A->>+Task: createTask(userId=123, data)
    Note right of Task: Validate: title length,<br/>assignee exists

    Task->>+DB: BEGIN TRANSACTION
    Task->>DB: INSERT INTO tasks
    Task->>DB: INSERT INTO activity_log
    DB-->>-Task: taskId=456, COMMIT

    Task->>Queue: PUBLISH task.created<br/>{taskId: 456, assignee: 789}

    alt Success Path
        Task-->>-A: {id: 456, status: "created", createdAt}
        A-->>-U: 201 Created<br/>X-Response-Time: 187ms
    else Validation Error (40ms)
        Task-->>A: {error: "Title too long", code: "INVALID_INPUT"}
        A-->>U: 400 Bad Request
    else Database Constraint Violation (50ms)
        DB-->>Task: ROLLBACK (assignee_fk violation)
        Task-->>A: {error: "Assignee not found", code: "INVALID_ASSIGNEE"}
        A-->>U: 400 Bad Request
    else Database Timeout (2000ms)
        DB-->>Task: Connection timeout
        Task->>Task: Log: ERROR - DB timeout
        Task->>Task: Increment metric: db_errors_total
        Task-->>A: {error: "Service temporarily unavailable"}
        A-->>U: 503 Service Unavailable<br/>Retry-After: 30
    end

    Note over U,Queue: Async: Notification service consumes<br/>task.created and sends email
```

**What Makes It Great:**
- Performance target in title (P95: <300ms)
- Request/response payloads shown
- Multiple error scenarios with timing
- Notes explain business logic
- Async operations documented
- Metrics and logging mentioned
- HTTP headers included (X-Response-Time, Retry-After)
- Database transactions shown (BEGIN, COMMIT, ROLLBACK)

**Best Practices:**
- Use participant aliases (U, A, T) for brevity
- Show request/response payloads
- Include HTTP methods and status codes
- Add timing notes for performance targets
- Use alt/else for error scenarios (at least 2-3 error paths)
- Add notes for business logic or validation rules
- Show async operations (message queues, background jobs)
- Limit to 5-7 participants (split complex flows)

---

## 4. Entity-Relationship Diagrams

**Purpose:** Show data model, entities, and relationships

### ❌ BAD Example - Missing constraints and keys

```mermaid
erDiagram
    USER ||--o{ TASK : creates
    TASK }o--|| PROJECT : belongs_to
```

**Problems:**
- No attributes shown
- Missing data types
- No primary/foreign key indicators
- Unclear cardinality

### ✅ GOOD Example - Attributes and keys specified

```mermaid
erDiagram
    USER ||--o{ TASK : creates
    USER ||--o{ PROJECT : owns
    TASK }o--|| PROJECT : belongs_to

    USER {
        uuid id PK
        string email UK
        string password_hash
        timestamp created_at
    }

    PROJECT {
        uuid id PK
        uuid owner_id FK
        string name
        timestamp created_at
    }

    TASK {
        uuid id PK
        uuid project_id FK
        uuid created_by FK
        string title
        text description
        enum status
        timestamp due_date
        timestamp created_at
    }
```

**Why Better:**
- Primary keys (PK) and foreign keys (FK) marked
- Data types specified
- Unique keys (UK) shown
- Timestamps included

### ⭐ GREAT Example - Complete with constraints and indexes

```mermaid
erDiagram
    USER ||--o{ TASK : "creates (created_by)"
    USER ||--o{ TASK : "assigned_to (assignee_id)"
    USER ||--o{ PROJECT : "owns (owner_id)"
    USER }o--o{ TEAM : "member_of"
    PROJECT ||--o{ TASK : "contains (project_id)"
    TEAM ||--o{ PROJECT : "has_projects"

    USER {
        uuid id PK "gen_random_uuid()"
        string email UK "NOT NULL, INDEX"
        string password_hash "NOT NULL, bcrypt"
        string full_name "INDEX for search"
        timestamp created_at "DEFAULT NOW()"
        timestamp last_login "INDEX for activity"
        boolean is_active "DEFAULT true"
    }

    PROJECT {
        uuid id PK
        uuid owner_id FK "REFERENCES user(id)"
        uuid team_id FK "REFERENCES team(id)"
        string name "NOT NULL, INDEX"
        text description
        enum status "active|archived|deleted"
        timestamp created_at "DEFAULT NOW()"
        timestamp updated_at "DEFAULT NOW()"
    }

    TASK {
        uuid id PK
        uuid project_id FK "ON DELETE CASCADE"
        uuid created_by FK "REFERENCES user(id)"
        uuid assignee_id FK "REFERENCES user(id), NULL"
        string title "NOT NULL, length 1-200"
        text description "NULL, length 0-5000"
        enum status "todo|in_progress|done"
        enum priority "low|medium|high|urgent"
        timestamp due_date "NULL, INDEX for sorting"
        timestamp created_at "DEFAULT NOW()"
        timestamp updated_at "DEFAULT NOW(), INDEX"
        int position "DEFAULT 0, for drag-drop ordering"
    }

    TEAM {
        uuid id PK
        string name "NOT NULL, UK"
        timestamp created_at
    }

    USER_TEAM {
        uuid user_id FK "REFERENCES user(id)"
        uuid team_id FK "REFERENCES team(id)"
        enum role "member|admin|owner"
        timestamp joined_at
        PK "user_id, team_id"
    }
```

**What Makes It Great:**
- Default values specified (gen_random_uuid(), NOW())
- Constraints documented (NOT NULL, length limits)
- Indexes identified for performance
- ON DELETE behavior specified
- Join tables for many-to-many (USER_TEAM)
- Enum values listed (status, priority, role)
- Multiple FK relationships clarified in relationship labels
- Business logic hints (position for drag-drop)

**Best Practices:**
- Always mark PK (primary key) and FK (foreign key)
- Specify data types (uuid, string, text, enum, timestamp, int, boolean)
- Show unique constraints (UK)
- Add index hints for frequently queried fields
- Include default values and constraints (NOT NULL, length limits)
- Document enum values inline
- Show many-to-many via join tables
- Limit to 6-8 entities per diagram (split if needed)

---

## 5. Deployment Topology Diagrams

**Purpose:** Show infrastructure layout, tiers, and connections

### ❌ BAD Example - Flat, unclear tiers

```mermaid
graph LR
    LB[Load Balancer]
    App[App Server]
    DB[Database]

    LB --> App
    App --> DB
```

**Problems:**
- No environment context
- Missing instance counts
- No network boundaries
- Unclear what runs where

### ✅ GOOD Example - Tiered with instance counts

```mermaid
graph TB
    subgraph "Internet"
        Users[Users]
    end

    subgraph "DMZ"
        LB[Load Balancer<br/>ALB - Auto-scaling]
    end

    subgraph "Application Tier"
        App1[App Instance 1<br/>t3.medium]
        App2[App Instance 2<br/>t3.medium]
        App3[App Instance 3<br/>t3.medium]
    end

    subgraph "Data Tier"
        DB[(PostgreSQL<br/>db.t3.large<br/>Primary)]
        DBR[(PostgreSQL<br/>db.t3.medium<br/>Read Replica)]
        Cache[(Redis<br/>cache.t3.small)]
    end

    Users -->|HTTPS| LB
    LB --> App1
    LB --> App2
    LB --> App3
    App1 --> DB
    App1 --> DBR
    App1 --> Cache
    App2 --> DB
    App2 --> DBR
    App2 --> Cache
    App3 --> DB
    App3 --> DBR
    App3 --> Cache
    DB -.Replication.-> DBR
```

**Why Better:**
- Clear network tiers (DMZ, App, Data)
- Instance types specified (t3.medium, db.t3.large)
- Load balancing shown explicitly
- Replication relationships (dotted lines)

### ⭐ GREAT Example - Production-ready with monitoring

```mermaid
graph TB
    subgraph "Users"
        Web[Web Browsers]
        Mobile[Mobile Apps]
    end

    subgraph "CDN Layer - CloudFront"
        CDN[CDN<br/>Global edge locations<br/>Static assets, API gateway]
    end

    subgraph "AWS Region: us-east-1"
        subgraph "Public Subnet - DMZ"
            ALB[Application LB<br/>Target: 3 instances<br/>Health check: /health]
            Bastion[Bastion Host<br/>t3.micro<br/>SSH access only]
        end

        subgraph "Private Subnet - Application Tier"
            ASG[Auto Scaling Group<br/>Min: 2, Desired: 3, Max: 10<br/>Scale on CPU >70%]
            App1[App Server 1<br/>t3.medium<br/>2 vCPU, 4GB RAM<br/>Node.js 18]
            App2[App Server 2<br/>t3.medium]
            App3[App Server 3<br/>t3.medium]
        end

        subgraph "Private Subnet - Data Tier"
            RDS[RDS PostgreSQL 14<br/>db.t3.large Primary<br/>4 vCPU, 16GB RAM<br/>100GB SSD<br/>Multi-AZ: Yes]
            RDSR[Read Replica<br/>db.t3.medium<br/>Same AZ as apps]
            ElastiCache[ElastiCache Redis 7<br/>cache.t3.small<br/>1 vCPU, 1.5GB RAM<br/>Cluster mode: No]
        end

        subgraph "Monitoring & Logging"
            CW[CloudWatch<br/>Metrics, Logs, Alarms]
            XRay[X-Ray<br/>Distributed tracing]
        end
    end

    subgraph "External Services"
        SendGrid[SendGrid<br/>Email delivery]
        Stripe[Stripe<br/>Payment processing]
    end

    Web -->|HTTPS| CDN
    Mobile -->|HTTPS| CDN
    CDN -->|HTTPS| ALB

    ALB -->|HTTP| App1
    ALB -->|HTTP| App2
    ALB -->|HTTP| App3

    App1 -->|SQL:5432| RDS
    App2 -->|SQL:5432| RDS
    App3 -->|SQL:5432| RDS

    App1 -->|Read:5432| RDSR
    App2 -->|Read:5432| RDSR
    App3 -->|Read:5432| RDSR

    App1 -->|Redis:6379| ElastiCache
    App2 -->|Redis:6379| ElastiCache
    App3 -->|Redis:6379| ElastiCache

    RDS -.Async replication.-> RDSR

    App1 -.Logs/Metrics.-> CW
    App2 -.Logs/Metrics.-> CW
    App3 -.Logs/Metrics.-> CW
    RDS -.Metrics.-> CW

    App1 -.Traces.-> XRay
    App2 -.Traces.-> XRay
    App3 -.Traces.-> XRay

    App1 -->|SMTP| SendGrid
    App2 -->|HTTPS| Stripe

    Bastion -.SSH tunnel.-> App1
    Bastion -.SSH tunnel.-> RDS

    style CDN fill:#f9f,stroke:#333,stroke-width:2px
    style ALB fill:#ff9,stroke:#333,stroke-width:2px
    style RDS fill:#9cf,stroke:#333,stroke-width:2px
    style CW fill:#cfc,stroke:#333,stroke-width:2px
```

**What Makes It Great:**
- Complete AWS architecture with region specified
- Auto-scaling configuration shown (min/max, trigger)
- Network boundaries (Public/Private subnets)
- Instance specifications (vCPU, RAM, disk)
- Protocols and ports specified (SQL:5432, Redis:6379)
- Monitoring and logging integrated
- Health checks mentioned
- Multi-AZ configuration specified
- Bastion host for secure access
- External service integrations
- Color coding for visual emphasis

**Best Practices:**
- Use subgraphs for network boundaries (DMZ, private subnets)
- Specify cloud provider and region
- Include instance types and sizes
- Show auto-scaling configuration
- Add monitoring/logging systems
- Specify protocols and ports
- Mark replication (dotted lines)
- Include security components (bastion, NAT gateway)
- Limit to 15-20 nodes per diagram
- Use color coding sparingly for emphasis

---

## Quick Reference: When to Use Each Diagram

| Diagram Type | Use When | Key Info to Include |
|--------------|----------|---------------------|
| **System Context (C4)** | Showing external interactions | System boundary, external actors, protocols, data formats |
| **Component** | Showing internal architecture | Layers, tech stack, interfaces, responsibilities |
| **Sequence** | Showing workflow/interaction | Operations, payloads, errors, timing, async flows |
| **ER Diagram** | Showing data model | PKs, FKs, types, constraints, indexes, enums |
| **Deployment** | Showing infrastructure | Tiers, instance types, auto-scaling, monitoring, networks |

---

## Common Mermaid Pitfalls to Avoid

1. **Too Many Nodes** - Limit to 12-15 per diagram, split if needed
2. **Missing Labels** - Every connection should be labeled (protocol, relationship)
3. **Generic Names** - "Service", "API" → "Task Service", "REST API Gateway"
4. **No Error Paths** - Sequence diagrams need alt/else blocks
5. **Flat Hierarchies** - Use subgraphs to show layers/boundaries
6. **Missing Tech Stack** - Include language, framework, version
7. **Unclear Direction** - Arrows should show data/control flow clearly
8. **No Specifications** - Instance types, data types, ports should be specified

---

**Version:** 1.0 (REL-003)
**Last Updated:** 2025-10-27
**Usage:** Reference when generating diagrams in Phase 3 (REL-002) and Phase 6 (REL-003)
