# CodeDelta for GitLab CI

`codedelta.gitlab-ci.yml` is a paste-in job for GitLab merge-request pipelines:
downloads the public engine bundle, runs churn + Agent Scan on the MR
(base..head), uploads the HTML/CSV/JSON reports as artifacts, and optionally
posts/updates a summary note on the MR.

Quick start: copy the job into your `.gitlab-ci.yml` (or `include:` this file
by URL). That's it — until 31 December 2026 the built-in evaluation licence
is used, so no licence variable is needed.

Variables (all optional):
- `CODEDELTA_LICENSE` — base64 of your codedelta.lic (masked CI/CD variable).
  Omit to use the built-in evaluation licence (valid to 2026-12-31).
- `CODEDELTA_GITLAB_TOKEN` — Project Access Token (Reporter+, scope `api`)
  to enable the MR note. Without it, reports are in the job artifacts.
- `CODEDELTA_ENGINE_URL` — pin an engine version or point at a self-hosted copy.
- `CD_MODE` (`churn_agent` default), `CD_THRESHOLD` (50).

Validated 7 October 2026 on GitLab.com with a pre-release build of v2.3.0: the job ran in a real merge-request pipeline and produced the reports, with CodeDelta's own output kept out of the scan. The MR-note API step is untested against a real GitLab instance (it needs a Project Access Token).

---

CodeDelta is a deterministic code-churn measurement and AI-agent detection
engine — docs, technical papers and downloads at
[www.codedelta.app](https://www.codedelta.app) (CLI/CI guide:
[codedelta.app/cli.html](https://www.codedelta.app/cli.html)).
