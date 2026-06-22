# agentaudit-action

GitHub Action for [**agentaudit**](https://github.com/mujinlabs/agentaudit) — audit
AI-agent extensions (Claude Code skills, MCP servers, plugins) for security & quality
risks in CI, with results in GitHub's **Code scanning** tab.

## Usage

```yaml
# .github/workflows/extension-audit.yml
name: extension-audit
on: [push, pull_request]

permissions:
  contents: read
  security-events: write     # required to upload SARIF

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: mujinlabs/agentaudit-action@v1
        with:
          path: ./skills       # what to scan (default: .)
          fail-on: high        # critical | high | medium | low | none (default: high)
```

## Inputs

| Input | Default | Description |
|---|---|---|
| `path` | `.` | File or directory to scan |
| `fail-on` | `high` | Minimum severity that fails the job |
| `version` | pinned | `mujin-agentaudit` version to install |
| `upload-sarif` | `true` | Upload SARIF to GitHub code scanning |

Findings appear under **Security → Code scanning** and as inline PR annotations.
The job fails if any finding meets `fail-on`, blocking the merge.

MIT · built by [Mujin Labs](https://github.com/mujinlabs).
