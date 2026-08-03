# Self-hosted runner labels

This repository uses capability-based self-hosted GitHub Actions routing. Labels are case-sensitive and must describe capabilities that the runner actually provides.

## Canonical selectors

| Workload | Required selector | Intended use |
|---|---|---|
| General CI | `[self-hosted, fast]` | Checksums, metadata, lint, documentation and lightweight validation |
| Docker/Compose | `[self-hosted, docker]` | Docker builds, Compose integration and container workloads |
| Heavy tests | `[self-hosted, backtester]` | Long simulations, benchmarks and soak tests |
| Native Apple Silicon | `[self-hosted, macOS, ARM64]` | Jobs that genuinely require native macOS/ARM64 hardware |

GitHub default labels such as `Linux` and `X64` may be added only when operating system or architecture is a real hard requirement.

## Rules

1. Never use bare `self-hosted` or `[self-hosted]`; every self-hosted job needs a capability label.
2. Use `backtester`, not the legacy label `backtest`.
3. Docker, Compose, `container:`, `services:` and Docker actions require the `docker` capability.
4. Do not route jobs by individual machine names.
5. Multiple labels mean that one runner must satisfy every listed capability.
6. Runner-routing changes require review of tool availability, security boundaries, queue capacity and rollback.

The workflow `.github/workflows/self-hosted-runner-policy.yml` validates literal self-hosted selectors and fails closed on bare or legacy labels.
