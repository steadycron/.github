# SteadyCron

**The reliable cron platform — schedule, run, and monitor your jobs in one place. EU-hosted, infrastructure-as-code first.**

SteadyCron unifies the two halves of scheduled work that teams usually bolt together from crontabs, cloud schedulers, and a separate uptime monitor:

- **HTTP execution** — we run your scheduled HTTP jobs with retries, timeouts, and a full audit trail.
- **Heartbeat monitoring** — watch jobs already running on your own infrastructure and alert on missed or failed runs.
- **Cron as code** — define every job, channel, and alert rule in a version-controlled manifest and reconcile it from CI.

## Cron as code

```yaml
version: 2
namespace: prod
jobs:
  - id: weekly-digest
    kind: http
    method: POST
    url: https://api.myapp.com/jobs/digest
    schedule: "0 9 * * 1"
    timezone: Europe/Berlin
    retries: 3
    rules:
      - { channel: ops-email, trigger: on_failure }
```

```bash
croncli sync ./jobs.yaml
```

Get a plan diff on every pull request via the SteadyCron GitHub Action; apply on merge. Renames preserve heartbeat tokens, signing secrets, and execution history — reconcile updates in place, it never recreates.

## Why SteadyCron

- **EU-hosted, GDPR-native** — German entity, Hetzner infrastructure, clean DPA. No data leaves the EU.
- **Execution and monitoring in one product** — one dashboard, one alerting pipeline, instead of two tools that don't talk to each other.
- **Built for teams that version-control their infra** — clean REST API, CLI, a generic webhook channel, and a public status badge per job.

## Links

- Website — https://steadycron.com
- Documentation — <https://steadycron.com/docs>
- Sign up — https://app.steadycron.com
- CLI — `steadycron` on NuGet
- GitHub Action — <https://github.com/steadycron/...>
