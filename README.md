# CodeDelta for GitLab CI

`codedelta.gitlab-ci.yml` is a paste-in job for GitLab merge-request pipelines:
downloads the public engine bundle, runs churn + Agent Scan on the MR
(base..head), uploads the HTML/CSV/JSON reports as artifacts, and optionally
posts/updates a summary note on the MR.

Quick start: copy the job into your `.gitlab-ci.yml` (or `include:` this file
by URL). That's it — during the free-trial period (to 31 August 2026) no
licence variable is needed.

Variables (all optional):
- `CODEDELTA_LICENSE` — base64 of your codedelta.lic (masked CI/CD variable).
  Omit to use the bundled trial licence (valid to 2026-08-31).
- `CODEDELTA_GITLAB_TOKEN` — Project Access Token (Reporter+, scope `api`)
  to enable the MR note. Without it, reports are in the job artifacts.
- `CODEDELTA_ENGINE_URL` — pin an engine version or point at a self-hosted copy.
- `CD_MODE` (`churn_agent` default), `CD_THRESHOLD` (50).

Validated 26 Jul 2026: YAML parsed; bundle URL, extraction, licence fallback and
base-worktree steps exercised locally against the v1.8.9 release; the engine
invocation is identical to the GitHub Action's, which is live-tested end-to-end.
The MR-note API step is untested against a real GitLab instance — first run on
one should watch that step.
