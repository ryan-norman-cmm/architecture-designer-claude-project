# Task 2: Test Scenarios - Pattern Selection & Diversity Algorithm

**Task:** Task 2 - Pattern Selection Engine & Diversity Algorithm
**Created:** 2025-10-27
**Purpose:** Validate pattern selection logic and diversity rules

---

## Pattern Diversity Validation Checklist

### Core Diversity Rules

- [ ] **Rule 1: Category Diversity** - No two patterns from same category
  - Categories: Monolithic, Microservices, Serverless, Event-Driven, Modular
  - Invalid: Microservices + Microservices Variant
  - Valid: Microservices + Serverless + Monolithic

- [ ] **Rule 2: Deployment Model Diversity** - Mix deployment approaches
  - Single-node vs Multi-node vs Serverless
  - Traditional hosting vs Cloud-native vs Hybrid

- [ ] **Rule 3: Scaling Characteristic Diversity** - Different scaling models
  - Vertical scaling (monolith)
  - Horizontal scaling (microservices)
  - Auto-scaling (serverless)

- [ ] **Rule 4: Complexity Level Diversity** - Range from simple to complex
  - Simple (monolith)
  - Moderate (modular monolith, serverless)
  - Complex (microservices, event-driven)

- [ ] **Rule 5: At Least One "Simpler" Option** - Always include lower-complexity approach
  - When team < 5: Must include monolithic option
  - When timeline < 3 months: Must include fastest-to-deploy option
  - When budget = limited: Must include low-cost option

---

## Test Scenario 1: Small Team, Short Timeline (Simplicity Favored)

### Input Constraints
```
Team: 2 engineers (Python/Django)
Scale: 500-1K users
Timeline: 3 months
Budget: Limited
```

### Expected Pattern Selection

**Approach 1: Monolithic (Django)**
- Category: Monolithic
- Fit: HIGH (perfect for constraints)
- Why: 2 engineers, 3 months = simplicity required

**Approach 2: Serverless (AWS Lambda + DynamoDB)**
- Category: Serverless
- Fit: MEDIUM (auto-scaling good, but learning curve)
- Why: Alternative deployment model, handles unknown scale

**Approach 3: Modular Monolith**
- Category: Modular
- Fit: MEDIUM-HIGH (balance simplicity + future flexibility)
- Why: Evolution path if growth exceeds expectations

### Diversity Validation
- ✅ 3 different categories (Monolithic, Serverless, Modular)
- ✅ Deployment models differ (single-node, serverless, single-node-modular)
- ✅ Complexity range (simple, moderate, moderate)
- ✅ Simplest option included (Django Monolith)

### Anti-Pattern Detection
- ❌ Should NOT include: Microservices (too complex for 2 engineers, 3 months)
- ❌ Should NOT include: Django Monolith + Flask Monolith (same category)
- ❌ Should NOT include: 3 serverless variations

---

## Test Scenario 2: High-Scale Platform (Complexity Justified)

### Input Constraints
```
Team: 10 engineers
Scale: 1M+ users, 100 TPS
Timeline: 6 months
Budget: Moderate
```

### Expected Pattern Selection

**Approach 1: Microservices**
- Category: Microservices
- Fit: HIGH (team size + scale justify complexity)
- Why: 10 engineers can own services, 1M+ users require independent scaling

**Approach 2: Event-Driven (Kafka + Services)**
- Category: Event-Driven
- Fit: HIGH (async patterns fit e-commerce workflows)
- Why: High throughput (100 TPS), decoupled services, audit trail

**Approach 3: Modular Monolith (Extract Later)**
- Category: Modular
- Fit: MEDIUM (faster to market, evolution path)
- Why: 6-month timeline achievable, can extract services at scale

### Diversity Validation
- ✅ 3 different categories (Microservices, Event-Driven, Modular)
- ✅ Scaling approaches differ (horizontal, event-based, vertical-then-horizontal)
- ✅ Complexity justified by constraints (10 engineers, 1M users)
- ✅ Includes simpler fallback (Modular Monolith rated MEDIUM, not recommended but presented)

### Anti-Pattern Detection
- ❌ Should NOT include: Microservices + Microservices with API Gateway (same category)
- ❌ Should NOT include: Microservices + SOA (too similar)
- ❌ Should NOT include: Simple monolith (underfit for 1M users)

---

## Test Scenario 3: Solo Developer, Unknown Scale (Risk Mitigation)

### Input Constraints
```
Team: 1 developer (JavaScript)
Scale: Unknown (MVP)
Timeline: 1 month
Budget: $0 (bootstrapped)
```

### Expected Pattern Selection

**Approach 1: Serverless (Vercel + Supabase)**
- Category: Serverless
- Fit: HIGH (zero DevOps, auto-scales, $0 starting cost)
- Why: Solo developer, 1-month timeline, unknown scale = serverless perfect fit

**Approach 2: Jamstack (Static + Functions)**
- Category: Static/Serverless Hybrid
- Fit: MEDIUM-HIGH (if content-heavy use case)
- Why: Ultra-fast, ultra-cheap, good for read-heavy apps

**Approach 3: Monolith (Railway/Render)**
- Category: Monolithic
- Fit: MEDIUM (traditional, but DevOps burden for solo dev)
- Why: Familiar mental model, easier debugging

### Diversity Validation
- ✅ 3 different deployment models (serverless, static+functions, traditional PaaS)
- ✅ Cost models differ ($0 scaling, $0-10, $5-20 fixed)
- ✅ DevOps overhead differs (zero, minimal, moderate)
- ✅ Risk mitigation for unknown scale (serverless auto-scales)

### Anti-Pattern Detection
- ❌ Should NOT include: Microservices (team too small)
- ❌ Should NOT include: Serverless AWS Lambda + Serverless Vercel (same category)
- ❌ Should NOT include: Complex patterns (event-driven, CQRS)

---

## Test Scenario 4: Enterprise Integration (Compliance Focus)

### Input Constraints
```
Team: 20 engineers
Scale: 50K users (internal)
Timeline: 12 months
Budget: Flexible
Compliance: HIPAA, SOX
```

### Expected Pattern Selection

**Approach 1: Service-Oriented Architecture (SOA)**
- Category: Service-Oriented
- Fit: HIGH (enterprise integration, stable patterns)
- Why: Legacy system integration, compliance audit trails, mature tooling

**Approach 2: Event-Driven (Event Sourcing)**
- Category: Event-Driven
- Fit: HIGH (compliance audit trails via immutable events)
- Why: SOX requires audit trail, event sourcing provides immutable log

**Approach 3: Modular Monolith (Domain-Driven Design)**
- Category: Modular
- Fit: MEDIUM-HIGH (faster delivery, clear boundaries)
- Why: 12-month timeline, can split later if needed

### Diversity Validation
- ✅ 3 different integration styles (SOA, event-driven, modular)
- ✅ Audit trail approaches differ (service logs, event sourcing, module boundaries)
- ✅ Compliance strategies differ (API contracts, immutable events, RBAC modules)
- ✅ Complexity range (high, high, moderate)

### Anti-Pattern Detection
- ❌ Should NOT include: Simple monolith (insufficient for compliance complexity)
- ❌ Should NOT include: SOA + Microservices (too similar for enterprise context)
- ❌ Should NOT include: Serverless (not typical for internal enterprise)

---

## Constraint Mapping Rules

### Team Size → Pattern Suitability

| Team Size | Suitable Patterns | Avoid Patterns |
|-----------|------------------|----------------|
| 1-2 | Monolithic, Serverless, Jamstack | Microservices, Event-Driven |
| 3-5 | Monolithic, Modular Monolith, Serverless | Microservices (too much overhead) |
| 6-10 | Modular Monolith, Microservices, Serverless | N/A (all patterns viable) |
| 10+ | Microservices, Event-Driven, SOA | Simple Monolith (team underutilized) |

### Scale → Pattern Suitability

| User Scale | Suitable Patterns | Avoid Patterns |
|-----------|------------------|----------------|
| <1K | Monolithic, Serverless, Jamstack | Microservices (premature) |
| 1K-10K | Monolithic, Modular Monolith, Serverless | Event-Driven (overkill) |
| 10K-100K | Modular Monolith, Microservices, Serverless | Simple Monolith (scaling limits) |
| 100K-1M | Microservices, Event-Driven, Modular (extract) | Simple Monolith |
| 1M+ | Microservices, Event-Driven, SOA | Monolithic |

### Timeline → Pattern Suitability

| Timeline | Suitable Patterns | Avoid Patterns |
|---------|------------------|----------------|
| <1 month | Serverless, Jamstack, Monolith (simple) | Microservices, Event-Driven |
| 1-3 months | Monolithic, Modular Monolith, Serverless | Microservices (setup takes 2-3 months) |
| 3-6 months | Modular Monolith, Microservices, Serverless | Event-Driven (2-3 month setup) |
| 6+ months | All patterns viable | N/A |

### Budget → Pattern Suitability

| Budget | Suitable Patterns | Avoid Patterns |
|--------|------------------|----------------|
| Limited ($0-$100/mo) | Serverless (pay-per-use), Jamstack, Monolith (PaaS) | Microservices (high infra cost) |
| Moderate ($100-$500/mo) | Monolithic, Modular Monolith, Serverless | Large-scale microservices |
| Flexible ($500+/mo) | All patterns viable | N/A |

### Expertise → Pattern Suitability

| Expertise | Suitable Patterns | Avoid Patterns |
|-----------|------------------|----------------|
| Backend only | Monolithic, Microservices | Jamstack (frontend-heavy) |
| Full-stack | All patterns viable | N/A |
| DevOps-heavy | Microservices, Event-Driven, Serverless | N/A |
| No DevOps | Serverless, PaaS Monolith, Jamstack | Microservices (high ops burden) |

---

## Pattern Selection Algorithm (Pseudo-Logic)

```typescript
function selectPatterns(requirements: Requirements): Pattern[] {
  // Step 1: Filter patterns by constraints
  const viable = allPatterns.filter(pattern => {
    return (
      pattern.minTeamSize <= requirements.teamSize &&
      pattern.minScale <= requirements.expectedScale &&
      pattern.minTimeline <= requirements.timeline &&
      pattern.minBudget <= requirements.budget
    );
  });

  // Step 2: Score patterns by fit
  const scored = viable.map(pattern => ({
    pattern,
    fitScore: calculateFitScore(pattern, requirements)
  }));

  // Step 3: Ensure diversity
  const selected: Pattern[] = [];

  // Always include best fit
  const bestFit = scored.sort((a, b) => b.fitScore - a.fitScore)[0];
  selected.push(bestFit.pattern);

  // Add 1-2 diverse alternatives
  const alternatives = scored.filter(s =>
    s.pattern.category !== bestFit.pattern.category &&
    s.fitScore > MEDIUM_THRESHOLD
  );

  selected.push(alternatives[0].pattern); // Different category

  if (alternatives.length > 1) {
    selected.push(alternatives[1].pattern); // 3rd option
  }

  // Step 4: Ensure simplicity option if applicable
  if (requirements.teamSize < 5 || requirements.timeline < 3) {
    const hasSimple = selected.some(p => p.complexity === 'simple');
    if (!hasSimple) {
      const simple = viable.find(p => p.complexity === 'simple');
      if (simple) selected[2] = simple; // Replace 3rd with simple option
    }
  }

  return selected;
}

function calculateFitScore(pattern: Pattern, req: Requirements): number {
  let score = 0;

  // Team size fit (40% weight)
  if (pattern.idealTeamSize === req.teamSize) score += 40;
  else if (Math.abs(pattern.idealTeamSize - req.teamSize) < 3) score += 30;
  else score += 10;

  // Scale fit (30% weight)
  if (pattern.idealScale === req.expectedScale) score += 30;
  else if (pattern.canScale(req.expectedScale)) score += 20;
  else score += 5;

  // Timeline fit (20% weight)
  if (pattern.setupTime < req.timeline) score += 20;
  else score += 0;

  // Budget fit (10% weight)
  if (pattern.cost <= req.budget) score += 10;
  else score += 0;

  return score; // 0-100
}
```

---

## Expected Test Results

### Test Scenario 1: Small Team, Short Timeline
- **Status:** ⏳ PENDING
- **Expected:** Monolithic (HIGH), Serverless (MEDIUM), Modular (MEDIUM-HIGH)
- **Diversity Check:** 3 categories ✓

### Test Scenario 2: High-Scale Platform
- **Status:** ✅ PASS (validated in test-results.md)
- **Actual:** Microservices (HIGH), Event-Driven (HIGH), Modular (MEDIUM)
- **Diversity Check:** 3 categories ✓

### Test Scenario 3: Solo Developer, Unknown Scale
- **Status:** ✅ PASS (validated in test-results.md)
- **Actual:** Serverless (HIGH), Jamstack (MEDIUM-HIGH), Monolith (MEDIUM)
- **Diversity Check:** 3 deployment models ✓

### Test Scenario 4: Enterprise Integration
- **Status:** ⏳ PENDING
- **Expected:** SOA (HIGH), Event-Driven (HIGH), Modular (MEDIUM-HIGH)
- **Diversity Check:** 3 integration styles ✓

---

## Anti-Pattern Validations

### ❌ Scenario: 3 Microservice Variations (FAIL)

**Invalid Output:**
1. Microservices with API Gateway
2. Microservices with Service Mesh
3. Microservices with Event Bus

**Why Invalid:** All 3 are same category (Microservices), violates diversity rule

**Correct Output:**
1. Microservices
2. Event-Driven
3. Modular Monolith

---

### ❌ Scenario: No Simple Option for Small Team (FAIL)

**Invalid Output for 2-person team:**
1. Microservices (LOW fit)
2. Event-Driven (LOW fit)
3. SOA (LOW fit)

**Why Invalid:** Team size = 2, must include simple option (monolith or serverless)

**Correct Output:**
1. Monolithic (HIGH fit)
2. Serverless (MEDIUM fit)
3. Modular Monolith (MEDIUM fit)

---

### ❌ Scenario: Overfit for Unknown Scale (FAIL)

**Invalid Output for unknown scale:**
1. Microservices (planned for 1M users)
2. Event-Driven (planned for high throughput)
3. SOA (enterprise integration)

**Why Invalid:** Scale unknown = risk of premature optimization

**Correct Output:**
1. Serverless (auto-scales 0-100K)
2. Monolithic (simple start, evolve later)
3. Modular Monolith (balance simplicity + flexibility)

---

## Integration with Knowledge Base

### Pattern Query Process

1. **Load Pattern Library:** Read `output/kb-architecture-patterns.md`
2. **Extract Pattern Metadata:**
   - Pattern name
   - Category (monolithic, microservices, serverless, etc.)
   - Ideal team size range
   - Ideal scale range
   - Setup timeline
   - Cost range
   - Complexity level

3. **Filter by Constraints:** Apply constraint mapping rules
4. **Score by Fit:** Calculate fit score (0-100)
5. **Ensure Diversity:** Select from different categories
6. **Validate Rules:** Check all 5 diversity rules pass

### Knowledge Base References

**Patterns to Query:**
- Monolithic Architecture
- Modular Monolith
- Microservices Architecture
- Event-Driven Architecture
- Serverless Architecture
- Service-Oriented Architecture (SOA)
- Jamstack Architecture
- CQRS + Event Sourcing

**Selection Priority:**
1. Constraint viability (must fit team/scale/timeline/budget)
2. Fit score (highest scores preferred)
3. Category diversity (different categories required)
4. Simplicity rule (if team < 5 or timeline < 3 months)

---

## Manual Validation Test: High-Scale E-Commerce (Task 2 Requirement)

### Test Input
"1M+ users, 100 TPS, 10-person team, 6-month timeline"

### Expected Behavior
1. Agent queries kb-architecture-patterns.md
2. Agent filters: Microservices, Event-Driven, Modular Monolith (viable for scale)
3. Agent scores: Microservices (HIGH), Event-Driven (HIGH), Modular (MEDIUM)
4. Agent selects: 3 different categories (not microservice variations)
5. Agent presents with fit scores

### Validation Checklist
- [ ] No two patterns from same category
- [ ] Microservices included (HIGH fit for 10 engineers, 1M users)
- [ ] Event-Driven included (HIGH fit for 100 TPS, async workflows)
- [ ] Modular Monolith included as simpler fallback (MEDIUM fit, 6-month timeline achievable)
- [ ] Simple monolith NOT included (LOW fit for 1M users)
- [ ] Serverless NOT primary recommendation (not typical for high-scale e-commerce with 10-person team)

### Test Status
✅ **VALIDATED** - Already tested in test-results.md, confirmed pattern diversity

---

## Notes

Pattern selection logic should be embedded in:
- `workflow-architecture-exploration.md` (Phase 3: Architecture Exploration)
- Agent uses constraint mapping rules automatically
- Knowledge base queried dynamically during conversation

**Next Step:** Integrate pattern selection rules into workflow file
