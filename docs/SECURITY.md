# Security

`feedbakkr-demo-base-astro` follows the [Feedbakkr org dependency-scanning
policy][org-policy]. This is a demo / reference project — not deployed.

[org-policy]: https://github.com/feedbakkr/feedbakkr/blob/main/docs/security-dependency-scanning.md

## Workflows

- **`security-pr.yml`** — runs `pnpm audit --audit-level high` on every PR
  against `master`. **Blocking.**
- **`security-scheduled.yml`** — nightly (04:15 UTC) + `workflow_dispatch`.
  Runs `pnpm audit --audit-level moderate` plus OSV-Scanner. Reporting-only.

## Local scans

```bash
pnpm run security:audit            # high+ — mirrors the PR gate
pnpm run security:audit:moderate   # moderate+ — mirrors the scheduled scan
pnpm run security:scan             # audit + osv-scanner
pnpm run security:scan:full        # audit:moderate + osv-scanner
```

Install osv-scanner locally (macOS): `brew install osv-scanner`.

## Snapshot at rollout

3 high advisories cleared via `pnpm.overrides`:
- `fast-uri >= 3.1.2`
- `devalue >= 5.8.1`
