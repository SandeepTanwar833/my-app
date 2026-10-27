# Claims Platform Project Notes

- Backend: ASP.NET Core 8 under `Chubb.Claims.Platform`; API, Application, Domain, Infrastructure, and Tests are separate projects. SQLite is the local source of truth.
- Frontend: Angular 20 standalone app under `chubb-claims-ui`; claimant and staff views share one application.
- Keep claim lifecycle transitions validated in the API. Record material changes in `ClaimActivity`.
- REST is used for interactive requests and queries. Kafka is intentionally not required to run the local assessment build; see `docs/architecture.md` for the eventing boundary.
- Update `AI-WORKING-JOURNAL.md` during material AI-assisted decisions and note what was accepted, challenged, or overridden.
- Validate API changes with `dotnet test` / `dotnet build`; validate frontend changes with `npm run build`.
