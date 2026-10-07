Hi! I'd like to work on this. Here is my plan.

**What I found (current behavior):**
On `main` (`f89c06f`), I ran the existing extractor on this repo's own `.github/workflows/ci.yml`:

```bash
python3 -c "from pathlib import Path; from ingestion.parsers.skill_extractor import SkillExtractor; p=Path('.github/workflows/ci.yml'); print(sorted(s.name for s in SkillExtractor().extract_skills(p.read_text(), filename=str(p))))"
```

It prints `['Postgresql', 'Redis']`. That file uses `actions/checkout` and `actions/setup-python` and runs `pytest`, but neither `GitHub Actions` nor `pytest` is detected. `SkillExtractor.extract_skills()` in `ingestion/parsers/skill_extractor.py` only does substring matching against its `FRAMEWORKS`/`DATABASES`/`TOOLS` tables. Nothing in it recognizes a workflow file, and `pytest` isn't in any table.

**What I'll do:**
- Add `ingestion/parsers/workflow_parser.py` with a `WorkflowParser` that reads `uses:`, `run:` and `name:` lines from a `.github/workflows/*.yml` file and returns `GitHub Actions`, `Docker`, `pytest` and `Deployment` skills, with the matching lines as evidence.
- Add a `_detect_workflow()` step to `SkillExtractor.extract_skills()` that only runs when `filename` is a workflow path. Other inputs behave exactly as they do today.
- Add `tests/unit/test_workflow_parser.py` and one new test in `tests/unit/test_skill_extractor.py`.
- Out of scope: fetching workflow files or wiring them into `ingestion/pipeline.py`, other CI systems (GitLab, CircleCI, Travis), `agent/tools/skill_extractor.py`, and adding a YAML dependency. PyYAML isn't in `pyproject.toml`, so I'll use line-based regex.

**How I'll prove it:**
- Re-run the command above on the same `ci.yml`: it currently prints `['Postgresql', 'Redis']` and after the change should print `['GitHub Actions', 'Postgresql', 'Redis', 'pytest']`.
- `pytest tests/unit/test_workflow_parser.py tests/unit/test_skill_extractor.py -v` passes, along with `make lint`, `make typecheck` and `make test-unit`.

**Open question:** nothing calls `SkillExtractor` with workflow files yet, so these skills won't show up on a profile until something passes them in. Would you like that wiring as a separate follow-up issue?

*(Note: Prepared with AI assistance via Claude Code.)*
