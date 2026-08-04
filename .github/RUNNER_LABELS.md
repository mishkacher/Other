# Canonical runner selectors

Every GitHub Actions job must use exactly one selector:

```yaml
runs-on: [self-hosted, fast]
runs-on: [self-hosted, docker]
runs-on: [self-hosted, backtester]
runs-on: [self-hosted, macOS, ARM64]
```

No extra labels are permitted. Bare `self-hosted`, GitHub-hosted runners, dynamic or multiline selectors, machine names, `Linux`, `X64`, combined capabilities and legacy `backtest` are forbidden.

The workflow `.github/workflows/self-hosted-runner-policy.yml` executes `.github/scripts/check_runner_selectors.py` and fails closed on every other selector.
