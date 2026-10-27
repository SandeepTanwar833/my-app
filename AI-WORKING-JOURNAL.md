# AI Working Journal

Running notes for the assessment. Add entries as the implementation evolves; this is intentionally a working log, not a polished narrative.

## 2026-10-27

- Asked AI to decompose the fragmented APAC claims process into a runnable sprint-sized platform. Accepted a backend-first, single-service direction so the domain transitions and data integrity could be implemented before broad UI coverage.
- Chose ASP.NET Core minimal API, EF Core + SQLite, and Angular. Upgraded the initial Angular 17 scaffold to Angular 20.3 after the runtime audit found high-severity advisories; aligned TypeScript and zone.js, and verified the production dependency audit is clean. Accepted the dependency reinstall cost for a safer baseline.
- Accepted REST for interactive intake, status checks, and staff actions. Kafka remains an event-delivery boundary for later integrations rather than a local prerequisite; see `docs/architecture.md`.
- Accepted an initial lifecycle of Submitted -> UnderReview -> InformationRequested -> UnderReview -> Approved/Rejected -> Settled. Rejected and settled are treated as closed. Added an activity timeline for consequential updates.
- Challenged the idea of requiring Kafka locally: it adds setup burden and does not improve the synchronous claim response contract in a short assessment. Would publish committed domain events through an outbox if downstream notifications/analytics become a production requirement.
- A local queue smoke test exposed SQLite's inability to translate `DateTimeOffset` in `ORDER BY`. Kept the assessment-scale filtered query and sorted its results in memory; with larger volumes, store sortable UTC ticks or use a provider-supported UTC timestamp mapping and database ordering.
- Restructured the backend into API, Application, Domain, Infrastructure, and Tests projects to match the solution structure requested for the walkthrough. Kept the API as one deployable service; the folder/project boundaries improve ownership without introducing distributed-service overhead. Enabled Swagger UI in Development for interactive API inspection.
- Updated monetary displays to derive currency from market (including MYR for Malaysia and HKD for Hong Kong). Challenged a single exposure total because adding balances in different currencies would be misleading; grouped dashboard reserves by market and officer-market instead.
- Overrode any assumption of a separate claimant/staff frontend: the brief requires one Angular codebase, so the role switch changes the working view while the API owns validation and state transitions.
- Known shortcuts to revisit: authentication/authorization is not implemented; staff identity is a demo selector; market currency is displayed in SGD; notifications and attachments are not integrated; current database initialization uses EnsureCreated for sprint speed.
