# Postgres as the job queue

Ingestion and Research jobs run from a queue table in Postgres, claimed with `SELECT ... FOR UPDATE SKIP LOCKED`, instead of Celery with Redis. The app runs on Railway's usage-billed Hobby plan, where every always-on service costs RAM. Redis and a Celery broker would add services that the expected load (a beta of 30–50 users) does not need. Postgres already holds all job state, so a job and its results commit in one transaction. The same table also enforces the global arXiv rate limit shared by all Research jobs.

## Consequences

- Retries, timeouts, and stuck-job recovery are our own code, not a library's.
- If throughput ever outgrows Postgres, the queue sits behind one small interface and can be swapped out.
