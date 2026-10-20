# arXiv as the only Research source, full text kept privately

Research searches only arXiv. Every paper it adds is stored as full text, whatever its license, but only inside the requesting user's own Workspace and never shown to anyone else. This works like a personal reference manager downloading a freely available PDF. Most arXiv papers use arXiv's default non-exclusive licence rather than CC. Storing only CC-licensed full text would leave most researched papers abstract-only and sharply lower answer quality after research. Each Document shows its license and a link to the original. OpenAlex was considered for broader coverage but dropped to keep a single integration.

## Consequences

- Everything outside arXiv (most journal-only papers, non-CS/physics/math fields) cannot be found by Research. Users can still upload such papers themselves.
- arXiv allows one request every 3 seconds, so Research jobs share a global rate limiter and may queue (see ADR-0001).
- Workspaces must never become shareable without revisiting this decision.
