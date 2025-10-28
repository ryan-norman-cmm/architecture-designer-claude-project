# Progressive Questions Template

Use this template for one-question-at-a-time requirements gathering.

## Question Pattern

🤔 **Question [N] of ~[Total]**

**[Question in plain language?]**

*Why this matters:* [1-2 sentence explanation of how this impacts architecture decisions]

**Examples:**
- [Option A]: [description]
- [Option B]: [description]
- [Option C]: [description]
- Custom: [describe your specific situation]

Your answer:

---

## Example Questions

### Question 1: Project Type
🤔 **Question 1 of ~5**

**What are you building?**

*Why this matters:* Different project types (CRUD apps, real-time systems, data pipelines) have very different architectural needs. This helps me recommend patterns that fit your use case.

**Examples:**
- Web application (user-facing features)
- API service (backend integration)
- Data processing pipeline
- Real-time system (chat, notifications)
- Custom: [describe your project]

Your answer:

---

### Question 2: MVP Scope
🤔 **Question 2 of ~5**

**Is this an MVP/first release, or adding to an existing platform?**

*Why this matters:* MVPs can start simple and scale later. Existing platforms need to integrate with current architecture and maintain consistency.

**Examples:**
- New MVP: Start fresh, optimize for speed
- Existing platform: Integrate with current services
- Modernizing legacy: Replace existing system gradually

Your answer:

---

### Question 3: Platform Services
🤔 **Question 3 of ~5**

**What existing platform services can we leverage?**

*Why this matters:* Reusing existing services (auth, notifications, storage) maximizes platform cohesion and reduces build time.

**Examples:**
- Auth: OAuth service, user management
- Notifications: Email, SMS, push notifications
- Storage: File storage, object storage, CDN
- None: Greenfield project, build from scratch

Your answer:

---

### Question 4: Vendor Tooling
🤔 **Question 4 of ~5**

**What cloud provider or managed services are you using?**

*Why this matters:* Leveraging vendor-managed services (databases, caches, queues) reduces operational complexity and takes advantage of existing licenses.

**Examples:**
- Azure: App Service, PostgreSQL, Redis, Functions
- AWS: Lambda, RDS, ElastiCache, API Gateway
- GCP: Cloud Run, Cloud SQL, Memorystore
- Self-hosted: Docker, Kubernetes, on-premise
- Flexible: No current commitment

Your answer:

---

### Question 5: Expected Scale
🤔 **Question 5 of ~5**

**What's your expected user scale?**

*Why this matters:* Scale influences whether we need distributed architecture or can use simpler patterns.

**Examples:**
- Startup/POC: < 100 users
- Small business: 100-1,000 users
- Growth stage: 1,000-10,000 users
- Enterprise: 10,000-100,000 users
- Large scale: 100,000+ users

Your answer:

---

## Template Guidelines

- **One question per exchange**: Never batch multiple questions
- **Progress indicator**: Always show "Question N of ~Total"
- **Rationale**: Include "Why this matters" explanation (1-2 sentences)
- **Examples**: Provide 3-5 example answers with descriptions
- **Plain language**: 8th grade reading level, avoid jargon
- **Line limit**: Keep each question exchange under 20 lines total
- **Skip logic**: If answer can be inferred from previous responses, skip the question
