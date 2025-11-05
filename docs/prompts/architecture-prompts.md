# Architecture Prompts

A collection of prompt templates for system design, architecture decisions, and technical planning.

---

## System Design

### 1. Design System Architecture

**Purpose:** Create a comprehensive system architecture for a new application.

**Prompt:**
```
Design a system architecture for [APPLICATION_NAME]:

Requirements:
- Purpose: [APPLICATION_PURPOSE]
- Scale: [EXPECTED_USERS/LOAD]
- Key features: [MAIN_FEATURES]
- Performance requirements: [LATENCY/THROUGHPUT]
- Availability requirements: [SLA]
- Data volume: [DATA_SIZE]
- Budget constraints: [COST_LIMITS]

Provide:
- High-level architecture diagram description
- Component breakdown with responsibilities
- Technology stack recommendations
- Data flow description
- Scalability strategy
- Security considerations
- Trade-offs and alternatives considered
```

**Example:**
```
Design a system architecture for a real-time collaborative document editing platform:

Requirements:
- Purpose: Google Docs alternative with real-time collaboration
- Scale: 1M users, 100k concurrent editors
- Key features: real-time sync, version history, comments, sharing
- Performance requirements: <100ms sync latency, 99.9% uptime
- Availability requirements: 99.9% SLA
- Data volume: 10TB documents, 1TB/month growth
- Budget constraints: Startup budget, cloud-based

Provide:
- High-level architecture diagram description
- Component breakdown with responsibilities
- Technology stack recommendations
- Data flow description
- Scalability strategy
- Security considerations
- Trade-offs and alternatives considered
```

---

### 2. Microservices Decomposition

**Purpose:** Break down a monolith into microservices.

**Prompt:**
```
Design a microservices architecture for this [MONOLITH_TYPE]:

Current system:
[SYSTEM_DESCRIPTION]

Decomposition goals:
- Identify service boundaries using [DOMAIN_MODEL]
- Define service responsibilities
- Specify inter-service communication patterns
- Design data ownership and isolation
- Plan migration strategy: [BIG_BANG/STRANGLER_FIG]
- Address cross-cutting concerns: [AUTH/LOGGING/CONFIG]

For each service provide:
- Service name and purpose
- API contracts
- Data models
- Dependencies
- Deployment considerations
```

**Example:**
```
Design a microservices architecture for this e-commerce monolith:

Current system:
Monolithic Rails app handling products, orders, payments, inventory, users, recommendations

Decomposition goals:
- Identify service boundaries using Domain-Driven Design
- Define service responsibilities clearly
- Specify inter-service communication (sync REST + async events)
- Design data ownership (each service owns its data)
- Plan migration strategy: Strangler Fig pattern
- Address cross-cutting concerns: API Gateway for auth, centralized logging, config service

For each service provide:
- Service name and purpose
- API contracts (REST endpoints)
- Data models
- Dependencies on other services
- Deployment and scaling considerations
```

---

### 3. Database Architecture Design

**Purpose:** Design database architecture and schema strategy.

**Prompt:**
```
Design database architecture for [APPLICATION]:

Requirements:
- Data types: [STRUCTURED/UNSTRUCTURED/BOTH]
- Query patterns: [READ_HEAVY/WRITE_HEAVY/BALANCED]
- Consistency requirements: [STRONG/EVENTUAL]
- Scale: [DATA_VOLUME], [QUERY_VOLUME]
- Relationship complexity: [SIMPLE/COMPLEX]
- Analytics needs: [OLTP/OLAP/BOTH]

Recommend:
- Database type(s) and justification
- Schema design approach
- Partitioning/sharding strategy
- Replication setup
- Indexing strategy
- Backup and recovery plan
- Migration and evolution strategy
```

**Example:**
```
Design database architecture for a social media platform:

Requirements:
- Data types: User profiles (structured), posts/media (unstructured), relationships (graph)
- Query patterns: Read-heavy (10:1 read/write), complex social graph queries
- Consistency requirements: Eventual consistency acceptable for feeds, strong for transactions
- Scale: 100M users, 1B posts, 10B relationships
- Relationship complexity: Complex (followers, friends, groups, mentions)
- Analytics needs: Both OLTP for app + OLAP for analytics

Recommend:
- Database type(s) and justification (polyglot persistence)
- Schema design approach for each data type
- Partitioning/sharding strategy by user ID
- Replication setup (multi-region)
- Indexing strategy for common queries
- Backup and recovery plan
- Migration and evolution strategy
```

---

### 4. API Design Strategy

**Purpose:** Design comprehensive API strategy.

**Prompt:**
```
Design an API strategy for [PLATFORM]:

Context:
- API consumers: [WEB/MOBILE/PARTNERS/PUBLIC]
- Use cases: [PRIMARY_USE_CASES]
- Scale expectations: [REQUEST_VOLUME]
- Data sensitivity: [PUBLIC/INTERNAL/CONFIDENTIAL]

Define:
- API style: [REST/GraphQL/gRPC/HYBRID] and rationale
- Authentication/authorization approach
- Versioning strategy
- Rate limiting and quotas
- Error handling conventions
- Documentation approach
- SDK strategy: [LANGUAGES]
- Monitoring and analytics
- Deprecation policy

Include example endpoint designs.
```

**Example:**
```
Design an API strategy for a payment processing platform:

Context:
- API consumers: Merchant web apps, mobile apps, backend integrations
- Use cases: Process payments, manage subscriptions, handle refunds, reporting
- Scale expectations: 10k requests/second peak
- Data sensitivity: Confidential (PCI-DSS compliance required)

Define:
- API style: REST for simplicity, webhooks for events
- Authentication: API keys + OAuth 2.0 for user context
- Versioning strategy: URL-based (/v1/, /v2/)
- Rate limiting: Tiered by plan (100/min basic, 1000/min premium)
- Error handling: RFC 7807 Problem Details
- Documentation: OpenAPI 3.0 with interactive docs
- SDK strategy: Official SDKs for JS, Python, Ruby, PHP, Java
- Monitoring: Request logging, error tracking, performance metrics
- Deprecation: 12-month notice, sunset headers

Include example endpoint designs for payment creation and retrieval.
```

---

## Architecture Decisions

### 5. Technology Stack Selection

**Purpose:** Choose appropriate technologies for a project.

**Prompt:**
```
Recommend a technology stack for [PROJECT_TYPE]:

Project requirements:
- Application type: [WEB/MOBILE/DESKTOP/EMBEDDED]
- Team expertise: [CURRENT_SKILLS]
- Performance needs: [REQUIREMENTS]
- Scalability needs: [GROWTH_EXPECTATIONS]
- Time to market: [DEADLINE_PRESSURE]
- Budget: [HOSTING/LICENSING_BUDGET]
- Maintenance expectations: [TEAM_SIZE/SUPPORT]

For each layer, recommend:
- Frontend: [FRAMEWORK/LIBRARY]
- Backend: [LANGUAGE/FRAMEWORK]
- Database: [TYPE/PRODUCT]
- Infrastructure: [CLOUD/ON_PREM]
- DevOps tools: [CI/CD/MONITORING]

Justify each choice with pros/cons and alternatives.
```

**Example:**
```
Recommend a technology stack for a startup SaaS analytics platform:

Project requirements:
- Application type: Web application with data dashboards
- Team expertise: 2 full-stack JS developers, learning curve acceptable
- Performance needs: Handle 1M data points, sub-second query responses
- Scalability needs: 0-10k users in first year
- Time to market: MVP in 3 months
- Budget: Cloud-based, $500/month initially
- Maintenance: Small team, need low ops overhead

For each layer, recommend:
- Frontend: Framework/library with rich visualization
- Backend: Language/framework with good async support
- Database: Time-series optimized or hybrid solution
- Infrastructure: Managed cloud platform
- DevOps tools: CI/CD pipeline, monitoring, error tracking

Justify each choice with pros/cons and alternatives.
```

---

### 6. Architecture Trade-off Analysis

**Purpose:** Evaluate architectural trade-offs for a decision.

**Prompt:**
```
Analyze trade-offs for [ARCHITECTURE_DECISION]:

Context:
[CURRENT_SITUATION]

Options:
1. [OPTION_1]
2. [OPTION_2]
3. [OPTION_3]

Evaluate each option across:
- Performance implications
- Scalability impact
- Development complexity
- Operational overhead
- Cost considerations
- Team expertise alignment
- Time to implement
- Future flexibility
- Risk factors

Provide recommendation with justification and migration path if changing from current approach.
```

**Example:**
```
Analyze trade-offs for data caching strategy:

Context:
E-commerce site with product catalog (50k products), user sessions, shopping carts.
Currently no caching, database under load.

Options:
1. In-memory application cache (Node.js)
2. Redis distributed cache
3. CDN + Redis hybrid

Evaluate each option across:
- Performance implications (latency, throughput)
- Scalability impact (horizontal scaling)
- Development complexity (code changes needed)
- Operational overhead (infrastructure management)
- Cost considerations (memory/hosting costs)
- Team expertise alignment (Redis experience)
- Time to implement
- Future flexibility (cache invalidation, multi-region)
- Risk factors (data consistency, cache stampede)

Provide recommendation with justification and migration path from no caching.
```

---

### 7. Scalability Planning

**Purpose:** Plan for application scalability.

**Prompt:**
```
Design a scalability strategy for [APPLICATION]:

Current state:
- Architecture: [CURRENT_ARCHITECTURE]
- Load: [CURRENT_METRICS]
- Bottlenecks: [KNOWN_ISSUES]

Growth projections:
- Target scale: [USERS/REQUESTS/DATA]
- Timeline: [GROWTH_TIMELINE]
- Peak load patterns: [TRAFFIC_PATTERNS]

Address:
- Horizontal vs vertical scaling strategy
- Stateless design requirements
- Load balancing approach
- Database scaling (read replicas, sharding)
- Caching strategy
- Async processing for heavy operations
- CDN usage
- Auto-scaling policies
- Performance testing plan

Provide phased implementation roadmap.
```

**Example:**
```
Design a scalability strategy for a video streaming platform:

Current state:
- Architecture: Monolithic app server + MySQL + object storage
- Load: 10k concurrent users, 1k videos
- Bottlenecks: Database queries, video processing

Growth projections:
- Target scale: 1M concurrent users, 100k videos
- Timeline: 18 months
- Peak load patterns: Evening hours 5-11pm, weekend spikes

Address:
- Horizontal scaling for app and streaming servers
- Stateless API design, sessions in Redis
- Load balancing with sticky sessions for streaming
- Database scaling (read replicas, eventual sharding by user)
- Caching strategy (video metadata, user profiles)
- Async video processing pipeline with queues
- CDN for video delivery and static assets
- Auto-scaling based on CPU and connection count
- Performance testing simulating 100k concurrent streams

Provide phased implementation: Phase 1 (months 1-6), Phase 2 (months 7-12), Phase 3 (months 13-18).
```

---

## Patterns and Best Practices

### 8. Design Pattern Application

**Purpose:** Apply appropriate design patterns to solve architectural problems.

**Prompt:**
```
Recommend design patterns for [PROBLEM]:

Problem description:
[DETAILED_PROBLEM]

System context:
- Language/framework: [TECHNOLOGY]
- Current architecture: [ARCHITECTURE_STYLE]
- Constraints: [LIMITATIONS]
- Quality attributes priority: [MAINTAINABILITY/PERFORMANCE/FLEXIBILITY]

For each recommended pattern:
- Pattern name and category
- Problem it solves
- Implementation approach in context
- Benefits and trade-offs
- Example structure/pseudocode
- Related patterns to consider

Focus on patterns that work well together.
```

**Example:**
```
Recommend design patterns for handling multiple payment gateway integrations:

Problem description:
Need to support multiple payment gateways (Stripe, PayPal, Square) with ability to easily add more.
Different gateways have different APIs, authentication, and capabilities.
Need to provide unified interface to rest of application.

System context:
- Language/framework: Node.js with TypeScript
- Current architecture: Layered architecture, dependency injection
- Constraints: Must support gateway-specific features while maintaining common interface
- Quality attributes priority: Flexibility (easy to add gateways), Maintainability

For each recommended pattern:
- Pattern name and category
- Problem it solves specifically
- Implementation approach with TypeScript
- Benefits and trade-offs
- Example structure/pseudocode
- Related patterns (Factory, Adapter, etc.)

Focus on patterns that work well together for this use case.
```

---

### 9. Event-Driven Architecture Design

**Purpose:** Design event-driven system architecture.

**Prompt:**
```
Design an event-driven architecture for [SYSTEM]:

Requirements:
- Events to handle: [EVENT_TYPES]
- Event volume: [EXPECTED_THROUGHPUT]
- Processing requirements: [SYNC/ASYNC/BOTH]
- Ordering guarantees: [STRICT/PARTITION/NONE]
- Delivery guarantees: [AT_LEAST_ONCE/EXACTLY_ONCE]
- Consumer patterns: [SINGLE/MULTIPLE/FANOUT]

Define:
- Event schema design and versioning
- Message broker choice: [KAFKA/RABBITMQ/SQS/PUBSUB]
- Topic/queue organization
- Event sourcing applicability
- CQRS pattern usage
- Saga pattern for distributed transactions
- Error handling and dead letter queues
- Monitoring and observability

Include event flow diagrams and example event schemas.
```

**Example:**
```
Design an event-driven architecture for order processing system:

Requirements:
- Events: OrderPlaced, PaymentProcessed, InventoryReserved, OrderShipped, OrderCancelled
- Event volume: 1000 orders/minute peak
- Processing requirements: Async for most, some sync validations
- Ordering guarantees: Per-order ordering required
- Delivery guarantees: Exactly-once for payment events
- Consumer patterns: Multiple consumers (inventory, shipping, analytics)

Define:
- Event schema with versioning strategy
- Message broker: Kafka for high throughput and replay capability
- Topic organization (per aggregate or event type)
- Event sourcing for order state
- CQRS for order queries vs commands
- Saga pattern for distributed order fulfillment transaction
- Error handling, retries, and DLQ for failed events
- Monitoring event lag, processing time, error rates

Include event flow from OrderPlaced through fulfillment and example event schemas.
```

---

### 10. Security Architecture

**Purpose:** Design comprehensive security architecture.

**Prompt:**
```
Design a security architecture for [APPLICATION]:

Security requirements:
- Compliance: [GDPR/HIPAA/PCI-DSS/SOC2]
- Data classification: [SENSITIVITY_LEVELS]
- User types: [ROLES_AND_PERMISSIONS]
- Threat model: [KEY_THREATS]
- Risk tolerance: [RISK_APPETITE]

Address:
- Authentication strategy (SSO, MFA, etc.)
- Authorization model (RBAC, ABAC, etc.)
- Data encryption (at rest, in transit)
- Secrets management
- Network security (VPC, firewalls, etc.)
- API security
- Audit logging
- Incident response plan
- Security testing strategy
- Third-party security assessment

Provide layered defense approach.
```

**Example:**
```
Design a security architecture for healthcare patient portal:

Security requirements:
- Compliance: HIPAA, SOC 2 Type II
- Data classification: PHI (high), PII (medium), public data
- User types: Patients, doctors, admins with different access levels
- Threat model: Data breaches, unauthorized access, insider threats
- Risk tolerance: Very low (healthcare data)

Address:
- Authentication: SSO with hospital AD + MFA for all users
- Authorization: RBAC with attribute-based rules for PHI access
- Data encryption: AES-256 at rest, TLS 1.3 in transit, end-to-end for messages
- Secrets management: HashiCorp Vault
- Network security: VPC isolation, WAF, IDS/IPS
- API security: OAuth 2.0, rate limiting, input validation
- Audit logging: All PHI access logged with retention
- Incident response: Defined playbooks, breach notification procedures
- Security testing: Quarterly pentests, automated SAST/DAST
- Third-party: Annual security assessments

Provide defense in depth with layers from network to application.
```

---

## Migration and Modernization

### 11. Legacy System Migration

**Purpose:** Plan migration from legacy systems.

**Prompt:**
```
Design a migration strategy from [LEGACY_SYSTEM] to [TARGET_SYSTEM]:

Current system:
- Technology: [LEGACY_TECH_STACK]
- Data volume: [DATA_SIZE]
- Users/usage: [USER_BASE]
- Pain points: [ISSUES_TO_SOLVE]
- Dependencies: [INTEGRATIONS]

Migration approach:
- Strategy: [BIG_BANG/PHASED/STRANGLER_FIG]
- Risk mitigation: [ROLLBACK_PLANS]
- Data migration: [APPROACH]
- Downtime tolerance: [ALLOWED_DOWNTIME]
- Parallel running period: [DURATION]
- Testing strategy: [VALIDATION_APPROACH]

Provide:
- Detailed migration phases
- Rollback procedures
- Success criteria for each phase
- Resource requirements
- Timeline estimates
```

**Example:**
```
Design a migration strategy from legacy .NET Framework app to cloud-native .NET:

Current system:
- Technology: .NET Framework 4.5, WCF services, SQL Server 2012, IIS
- Data volume: 500GB database, 2TB file storage
- Users/usage: 5k daily users, 24/7 operations
- Pain points: Hard to scale, deployment complexity, old dependencies
- Dependencies: Third-party SOAP services, legacy reporting system

Migration approach:
- Strategy: Strangler Fig pattern (incremental)
- Risk mitigation: Feature flags, canary releases, automated rollback
- Data migration: Initial sync + CDC for live migration
- Downtime tolerance: Max 2 hours for cutover
- Parallel running period: 3 months overlap
- Testing strategy: Shadow traffic, A/B testing, comprehensive E2E tests

Provide:
- Migration phases (assess, pilot, incremental migration, cutover)
- Rollback procedures for each phase
- Success criteria (performance metrics, bug rates, user adoption)
- Resource requirements (team size, skills, tools)
- 12-month timeline with milestones
```

---

### 12. Cloud Migration Strategy

**Purpose:** Plan migration to cloud infrastructure.

**Prompt:**
```
Design a cloud migration strategy for [APPLICATION]:

Current state:
- Infrastructure: [ON_PREM_SETUP]
- Applications: [APP_INVENTORY]
- Data storage: [STORAGE_SYSTEMS]
- Network architecture: [NETWORK_SETUP]
- Compliance requirements: [REGULATORY_NEEDS]

Cloud strategy:
- Target cloud: [AWS/AZURE/GCP/MULTI]
- Migration approach: [REHOST/REPLATFORM/REFACTOR]
- Workload prioritization: [WHICH_FIRST]
- Networking: [HYBRID/FULL_CLOUD]
- Disaster recovery: [DR_REQUIREMENTS]

Address:
- Application assessment and 6Rs (retire, retain, rehost, replatform, refactor, replace)
- Cloud architecture design
- Cost optimization strategy
- Security and compliance
- Migration waves and dependencies
- Performance testing
- Training and change management
```

**Example:**
```
Design a cloud migration strategy for retail company infrastructure:

Current state:
- Infrastructure: 3 data centers, 200 physical servers
- Applications: E-commerce (Java), ERP (SAP), inventory management (custom)
- Data storage: Oracle DB, file servers, backup systems
- Network: MPLS connecting stores, VPN for remote
- Compliance: PCI-DSS for payments

Cloud strategy:
- Target cloud: AWS primary, Azure for disaster recovery
- Migration approach: Mixed (rehost for ERP, refactor e-commerce, replace inventory)
- Workload prioritization: Dev/test first, then non-critical, finally production
- Networking: Hybrid cloud with Direct Connect for transition period
- Disaster recovery: Multi-region active-passive

Address:
- 6Rs assessment for each application
- AWS Well-Architected Framework design
- Reserved instances and savings plans for cost optimization
- Shared responsibility model, PCI compliance in cloud
- 4 migration waves over 18 months with dependency mapping
- Performance comparison testing vs on-prem baselines
- Cloud skills training program for ops team
```

---

## Integration Architecture

### 13. Third-Party Integration Design

**Purpose:** Design integration with external systems.

**Prompt:**
```
Design integration architecture for [EXTERNAL_SYSTEMS]:

Integration requirements:
- Systems to integrate: [LIST_SYSTEMS]
- Data to exchange: [DATA_TYPES]
- Frequency: [REAL_TIME/BATCH/SCHEDULED]
- Volume: [DATA_VOLUME]
- Reliability needs: [SLA_REQUIREMENTS]
- Direction: [INBOUND/OUTBOUND/BIDIRECTIONAL]

Design:
- Integration patterns: [API/ETL/MESSAGE_QUEUE/FILE]
- API management strategy
- Data transformation approach
- Error handling and retry logic
- Rate limiting and throttling
- Authentication/authorization
- Monitoring and alerting
- Testing strategy (mocking external systems)
- Versioning and backward compatibility

Consider failure scenarios and provide fallback strategies.
```

**Example:**
```
Design integration architecture for CRM and marketing automation platforms:

Integration requirements:
- Systems: Salesforce CRM, HubSpot Marketing, custom billing system
- Data to exchange: Contacts, leads, opportunities, invoices
- Frequency: Real-time for leads, daily batch for reporting
- Volume: 10k contacts/day, 1k leads/day
- Reliability needs: 99.9% success rate, no data loss
- Direction: Bidirectional (CRM ↔ Marketing), outbound (billing → CRM)

Design:
- Integration patterns: REST APIs for real-time, ETL for batch
- API management with rate limiting and caching
- Data transformation with schema mapping and enrichment
- Error handling with exponential backoff, DLQ, manual review queue
- Respect vendor rate limits (Salesforce: 100k API calls/day)
- OAuth 2.0 for authentication
- Monitoring sync status, latency, error rates with alerts
- Integration testing with mock servers and contract tests
- API versioning strategy, handle schema evolution

Provide fallback for API outages (queue and replay) and data conflict resolution.
```

---

## Performance Architecture

### 14. High-Performance System Design

**Purpose:** Design architecture optimized for performance.

**Prompt:**
```
Design a high-performance architecture for [USE_CASE]:

Performance requirements:
- Latency target: [P50/P95/P99]
- Throughput target: [REQUESTS_PER_SECOND]
- Concurrency: [CONCURRENT_OPERATIONS]
- Data size: [WORKING_SET_SIZE]
- Consistency needs: [STRONG/EVENTUAL]

Optimize for:
- CPU-bound operations: [STRATEGIES]
- I/O-bound operations: [STRATEGIES]
- Network latency: [STRATEGIES]
- Database queries: [STRATEGIES]
- Memory usage: [STRATEGIES]

Include:
- Architecture diagram optimized for data flow
- Caching strategy at multiple layers
- Async processing where applicable
- Resource pooling
- Performance budgets
- Load testing strategy
- Performance monitoring and SLOs
```

**Example:**
```
Design a high-performance architecture for real-time bidding ad system:

Performance requirements:
- Latency target: p95 < 50ms, p99 < 100ms
- Throughput: 100k bid requests/second
- Concurrency: 10k simultaneous auctions
- Data size: 100GB user profiles in hot cache
- Consistency: Eventual consistency acceptable

Optimize for:
- CPU-bound: Parallel bid calculations, compiled languages (Go/Rust)
- I/O-bound: Connection pooling, async I/O, batch reads
- Network: Edge deployment, protocol buffers, HTTP/2
- Database: Denormalized reads, materialized views, partitioning
- Memory: In-memory caching (Redis), efficient data structures

Include:
- Multi-tier architecture (edge → app → data) with data flow
- L1 (app memory), L2 (Redis), L3 (database) caching
- Async bid scoring and notification
- Connection pooling for all external services
- 10ms budget per layer (network, app, cache, database)
- Load testing with gradual ramp to 150k RPS
- Track p50/p95/p99 latency, error rate, throughput as SLOs
```

---

### 15. Cost Optimization Architecture

**Purpose:** Design architecture optimized for cost efficiency.

**Prompt:**
```
Design a cost-optimized architecture for [APPLICATION]:

Current costs:
- Infrastructure: [BREAKDOWN]
- Services: [BREAKDOWN]
- Data transfer: [BREAKDOWN]
- Total: [MONTHLY_COST]

Optimization goals:
- Target reduction: [PERCENTAGE/AMOUNT]
- Cannot compromise: [CRITICAL_REQUIREMENTS]
- Willing to trade-off: [ACCEPTABLE_COMPROMISES]

Analyze and recommend:
- Right-sizing resources
- Reserved capacity vs on-demand
- Serverless opportunities
- Storage tiering
- Data transfer optimization
- Auto-scaling policies
- Spot instances for appropriate workloads
- Multi-cloud cost arbitrage
- Monitoring and cost allocation

Provide cost-benefit analysis and implementation priority.
```

**Example:**
```
Design a cost-optimized architecture for data analytics platform:

Current costs:
- Compute (EC2): $8k/month (over-provisioned)
- Database (RDS): $5k/month
- Data transfer: $3k/month
- Storage (S3): $2k/month
- Total: $18k/month

Optimization goals:
- Target reduction: 40% ($7k/month savings)
- Cannot compromise: Query performance, data durability
- Willing to trade-off: Some cold-start latency for batch jobs

Analyze and recommend:
- Right-size EC2 instances based on actual CPU/memory usage
- 1-year reserved instances for baseline load (60% savings)
- Move batch processing to Lambda/Fargate Spot (70% savings)
- S3 Intelligent-Tiering for infrequently accessed data
- VPC endpoints to eliminate NAT gateway costs
- Scale down/up based on hourly patterns
- Spot instances for non-critical ETL jobs
- Consider BigQuery for analytics vs self-managed
- CloudWatch dashboards for cost per team/project

Prioritize: 1) Right-sizing (quick win), 2) Reserved instances, 3) Serverless migration.
Estimated savings: $2k right-sizing, $3k reserved, $2k serverless = $7k total.
```

---

## Additional Resources

- **Related:** See [prompt-engineering-guide.md](./prompt-engineering-guide.md) for writing effective architecture prompts
- **Implementation:** See [coding-prompts.md](./coding-prompts.md) for implementing architectural decisions
- **DevOps:** See [devops-prompts.md](./devops-prompts.md) for infrastructure implementation
