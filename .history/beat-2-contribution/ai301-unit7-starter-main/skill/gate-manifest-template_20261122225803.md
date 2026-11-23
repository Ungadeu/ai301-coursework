# Ship manifest: EdgeTX/edgetx

## Must pass before a ship

| Check | Command | Source |
| --- | --- | --- |
| Build radio unit tests | `.venv/bin/cmake --build build/native --target gtests-radio` | `tools/commit-tests.sh` & `CLAUDE.local.md` |
| Run curve & mixer unit tests | `build/native/gtests-radio --gtest_filter='Curves.*'` | `tools/commit-tests.sh` & `CLAUDE.local.md` |

## Excluded, with a dated reason

| Check | Command | Date | Why it doesn't count against this PR |
| --- | --- | --- | --- |
| Full CI script (`commit-tests.sh`) | `tools/commit-tests.sh -btx16s` | 2026-11-22 | Requires Linux CI / Qt 6 for Companion targets and exceeds local macOS Intel setup; radio curve unit tests are run directly via `gtests-radio` above. |
