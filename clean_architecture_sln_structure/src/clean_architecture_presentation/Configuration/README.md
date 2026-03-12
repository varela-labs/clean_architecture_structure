# Configuration

## Purpose
Transport/hosting configuration: appsettings models, endpoint configuration, environment flags.

## Typical contents
- API settings POCOs
- CORS policy settings models
- Messaging endpoint settings models (broker URL, queues) — as data only

## Out of scope
- Hard-coded secrets
- Configuration reads inside Domain/Application

## Notes
Prefer strongly-typed configuration models. Bind and validate at startup.


