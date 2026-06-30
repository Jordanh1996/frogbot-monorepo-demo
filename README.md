# frogbot-monorepo-demo

Private monorepo demo for **Frogbot V3** against `https://tokyoshiftleft.jfrog.io/`.

Two sub-projects, each with seeded CVEs on `main`:

| Project | Stack | Seeded vulnerability |
|---------|-------|----------------------|
| `frontend/` | npm | `minimatch@3.0.2` (ReDoS, CVE-2022-3517), `mpath@0.7.0` (prototype pollution) |
| `backend/` | pip | `pyjwt==1.7.1` (CVE-2022-29217), `urllib3==1.26.5` (multiple CVEs) |

**Pull-request scan:** open a PR that adds `axios@0.21.0` to `frontend/` — Frogbot should
report it as a newly introduced issue (PR scan only reports diff-introduced vulns).

## Frogbot

- `.frogbot/frogbot-config.yml` — monorepo project definitions (`frontend` + `backend`)
- `.github/workflows/frogbot-scan-repository.yml` — full-repo scan on `main`
- `.github/workflows/frogbot-scan-pull-request.yml` — diff scan on PRs

Scanner settings come from the repo-local config (not a central Config Profile), so the
monorepo `workingDirs` are respected.
