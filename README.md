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
  Omit to use the built-in evaluation licence (valid to 2026-10-31).
- `CODEDELTA_GITLAB_TOKEN` — Project Access Token (Reporter+, scope `api`)
  to enable the MR note. Without it, reports are in the job artifacts.
- `CODEDELTA_ENGINE_URL` — pin an engine version or point at a self-hosted copy.
- `CD_MODE` (`churn_agent` default), `CD_THRESHOLD` (50).

Validated 8 September 2026 against the v2.0.2 release: YAML parsed; the bundle URL resolves to v2.0.2 and extracts to the layout the job expects; the built-in evaluation licence verifies (valid to 31 October 2026); the base-worktree scan step run with the v2.0.2 CLI produced all artifacts and the MR comment. Not run inside the Ubuntu image itself; the MR-note API step is untested against a real GitLab instance.

---

CodeDelta is a deterministic code-churn measurement and AI-agent detection
engine — docs, technical papers and downloads at
[www.codedelta.app](https://www.codedelta.app) (CLI/CI guide:
[codedelta.app/cli.html](https://www.codedelta.app/cli.html)).
