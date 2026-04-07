### Q:You need to handle file uploads from users — what’s your approach?

> Accept uploads via signed URLs (S3, Azure Blob). Scan for malware, store metadata in DB. Use async processing (queues) for resizing/conversion.

### Q: How do you prevent SQL injection in your applications?

> Always use parameterized queries or ORM query builders. Validate and sanitize inputs. Avoid concatenating strings into SQL.

### Q: How do you mentor a junior developer who frequently introduces DB performance bugs?

> Review their code patiently, explain query optimization basics. Provide examples of slow vs. indexed queries. Encourage them to use the query analyzer before deployment.

### Q: A production API endpoint suddenly becomes slow — what’s your approach?

> First, confirm the issue: metrics, logs, and latency alerts.
>
> Check infrastructure (CPU, memory, DB load) and application logs for slow queries or external API timeouts.
>
> Use APM tools (Application Insights, New Relic) to trace latency.
>
> If it’s database-bound, analyze query plans or add caching. If recent code was deployed, perform a quick rollback.

### Q: How would you design a scalable logging system for microservices?

> Each service writes structured logs (JSON) asynchronously. Logs flow to a centralized pipeline (e.g., Fluent Bit → Elasticsearch / CloudWatch).
>
> Use correlation IDs to trace requests across services. Add retention policies and dashboards (Grafana/Kibana).

### Q： Your new release caused 500-errors in production — what do you do first?

> Pause rollout, enable maintenance mode if critical. Check CI/CD logs for migration issues or config mismatches. Review error monitoring tools (Sentry, App Insights) for stack traces. Rollback if needed, then reproduce in staging.

### Q: You need to design a user authentication system — how would you approach it?

> Use industry standards: OAuth 2.0 / OpenID Connect. Store passwords hashed + salted (bcrypt). Issue JWTs for stateless APIs, refresh tokens for session renewal. Implement role-based authorization and MFA.

### Q： How do you handle a deadlock between two microservices?

> Identify circular dependencies (Service A → B → A). Break the cycle using event-driven design (publish/subscribe) or async queues. Implement timeouts and idempotency for retries.

### Q: A teammate’s PR significantly reduces readability for small performance gains — what do you do?

> Acknowledge the improvement, then discuss maintainability cost. Suggest measuring actual impact before merging. Propose clearer alternatives or inline documentation.

### Q: You’re asked to speed up page load times — where do you start?

> Measure using Lighthouse or Chrome DevTools. Optimize backend (DB queries, caching), then frontend (lazy loading, minified bundles). Use CDN and compression (gzip/Brotli).

### Q: How would you implement search in a large product catalog?

> Use full-text search (Elasticsearch / Azure Search). Store denormalized, indexed documents for quick retrieval. Implement pagination, filters, and relevance scoring.

### Q: How do you design APIs that evolve without breaking clients?

> Use versioning in URLs (/v1/users) or headers. Maintain backward compatibility; deprecate gradually. Provide clear API docs and changelogs.

### Q: How do you measure and improve database performance in production?

> Enable slow-query logs, review query plans, and track CPU/I/O. Add missing indexes and batch operations. Use monitoring dashboards (Datadog, CloudWatch).

### Q: How do you ensure data consistency across multiple databases?

> Use distributed transactions only if essential. Prefer eventual consistency with outbox patterns or message brokers (Kafka, RabbitMQ). Include version numbers and reconciliation jobs.

### Q: You must migrate millions of records to a new schema — how do you plan it?

> Perform dry-runs in staging. Migrate incrementally with background jobs, not blocking writes. Add dual-write compatibility during transition. Verify data integrity after each batch.

### Q: How do you design rate-limiting for an API?

> Track requests per user/IP using Redis counters. Enforce limits (e.g., 100 req/min). Return 429 Too Many Requests when exceeded. Use sliding-window or token-bucket algorithms.
