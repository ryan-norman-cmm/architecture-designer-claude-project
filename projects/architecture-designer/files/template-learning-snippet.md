# Learning Snippet Template

Use this template to provide inline education without disrupting flow.

## Basic Format

> 📚 **[Technical Term or Pattern Name]**
> [2-3 sentence plain English explanation of what it is and why it matters]
>
> *Think of it like:* [Real-world analogy that makes the concept concrete]

---

## Example Snippets

### Microservices Pattern
> 📚 **Microservices Architecture**
> Instead of one large application doing everything, you build multiple small, independent services that each handle one specific job. Each service can be updated, deployed, and scaled separately without affecting the others.
>
> *Think of it like:* A restaurant kitchen with specialized stations (grill, salads, desserts) instead of one chef doing everything. Each station works independently but coordinates to deliver complete meals.

---

### Monolithic Architecture
> 📚 **Monolithic Architecture**
> A single, unified application where all features (database, business logic, UI) are tightly integrated and deployed together. Simpler to build and deploy initially, but harder to scale specific parts independently.
>
> *Think of it like:* A all-in-one printer/scanner/fax machine. Everything works together in one unit - easier to set up, but if one part breaks or needs an upgrade, you have to deal with the whole thing.

---

### Event-Driven Architecture
> 📚 **Event-Driven Architecture**
> Components communicate by publishing events (things that happened) to a message queue, and other components subscribe to events they care about. This decouples services so they don't need to know about each other directly.
>
> *Think of it like:* A restaurant order bell system. The server doesn't go find the chef - they ring the bell (publish event), and whoever's available in the kitchen (subscribers) picks up the order and starts cooking.

---

### Platform Cohesion
> 📚 **Platform Cohesion**
> How well a new component integrates with your existing platform's services, patterns, and infrastructure. High cohesion means reusing existing auth, notifications, databases, and deployment pipelines instead of creating new ones.
>
> *Think of it like:* Adding a new room to your house using the same electrical, plumbing, and HVAC systems you already have, versus building a separate tiny house in your backyard with all new utilities.

---

### JSONB (PostgreSQL)
> 📚 **JSONB**
> PostgreSQL's binary JSON storage format that lets you store flexible, schema-free data (like MongoDB) while keeping all the benefits of a traditional relational database (ACID transactions, joins, indexes).
>
> *Think of it like:* A filing cabinet where most folders have a standard structure, but some folders can hold any format of documents you need without reorganizing the entire cabinet.

---

### Redis Cache
> 📚 **Redis**
> An in-memory data store that acts as a super-fast cache layer between your application and database. It stores frequently-accessed data in RAM so you don't have to query the slower disk-based database every time.
>
> *Think of it like:* Keeping your most-used kitchen tools on the counter instead of in the back of a drawer. Same tools, but instant access without digging through storage every time you need them.

---

### Serverless Functions
> 📚 **Serverless Functions**
> Code that runs on-demand in response to events, without managing servers. You write functions, the cloud provider runs them when needed, and you only pay for actual execution time.
>
> *Think of it like:* Ride-sharing vs owning a car. You don't maintain a server sitting idle 23 hours a day - you just call a function when needed, use it, and pay only for that ride.

---

### API Gateway
> 📚 **API Gateway**
> A single entry point that sits in front of multiple backend services, routing requests to the right service, handling authentication, rate limiting, and transforming responses before sending them back to clients.
>
> *Think of it like:* A hotel concierge. Instead of guests finding and calling each department (housekeeping, room service, maintenance) directly, they ask the concierge who routes the request to the right place and gets back to them with the answer.

---

## Template Guidelines

- **Placement**: Insert immediately after first mention of technical term
- **Format**: Blockquote with 📚 emoji marker
- **Length**: 2-3 sentences explanation + 1-2 sentence analogy
- **Reading level**: 8th grade or below (Flesch-Kincaid)
- **Analogies**: Use everyday, relatable scenarios (restaurant, house, kitchen, office)
- **Density**: Maximum 1 snippet per 50 lines (avoid overwhelming)
- **Consistency**: Always use same format (> 📚 **Term** / Explanation / *Think of it like:* Analogy)
