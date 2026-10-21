# ECC overnight health pass (2026-10-11)

First .ai/memory note for this fork. Checkout created on primo this pass
(`git clone` into ~/.GH/Qompass/ECC); tree was clean and remains a straight
track of upstream affaan-m/ECC merges (HEAD at clone time: 4eb71d92).

## Gates run on primo (2026-10-11 night)

- Install: `npm ci --ignore-scripts` (matches upstream CI) — completed.
- Validators: `npm run test:validators` — exit 0 (catalog + command
  registry checks up to date).
- JS tests: `node tests/run-all.js` — exit 1; the runner's Final Results
  box reads: Total Tests 7305, Passed 7304, Failed 1; Files 347 passed,
  1 failed. The single failing file is
  `tests/hooks/pre-bash-commit-quality.test.js`, with exactly ONE failing
  case ("handles hash-prefixed python comments and string false-positives").
  (An earlier draft of this note cited an intermediate sub-summary —
  6976/9/164 — captured mid-run; the final tally above supersedes it and
  reconciles exactly with the one failed file and case.)
- Python tests: `python3 -m pytest tests/ -q` in a uv venv with the
  project's declared deps installed (anthropic, pyyaml, pytest-asyncio)
  — 285 passed, 3 skipped, 75 subtests passed, exit 0. With primo's
  system python the same run fails at collection (no anthropic module):
  an environment gap, not repo breakage.

## The one JS failure — root cause (proven, not patched)

The fixture stages a .py file whose line 5 is deliberately JavaScript
(`const str = "# TODO: ...";`) as a TODO-scanner false-positive probe.
The hook (scripts/hooks/pre-bash-commit-quality.js) runs pylint when it
is available; primo has pylint 4.0.7, which reports E0001 syntax-error
on line 5, and the hook blocks (exit 2). Upstream CI never installs
pylint, so the leg is skipped there and the test passes. The hook's
"pylint if available, nonzero blocks" behavior is upstream's design;
weakening it or editing the fixture would rewrite upstream behavior, so
this pass records the failure as environment-sensitive and changes
nothing. If Owner wants the local suite fully green, the lever is a
pylint-free PATH for the test run, not a code change.

## SCIP

Not produced. `npx -y @sourcegraph/scip-typescript index` at repo root:
"missing tsconfig.json — no files got indexed." The bundle is
JavaScript-first (798 tracked .js, 22 tracked .ts/.tsx); the only
tsconfig is .opencode/tsconfig.json (adapter config). Indexing that
subdir alone would misrepresent coverage, so no index.scip was placed.

## Memory / indexer

This .ai/memory/ tree was seeded this pass mirroring diver's layout
(INDEX.md, current.md, decisions.md, patterns.md, inbox/, archive/).
The repo becomes visible to Owner's memory indexer by having .ai/memory/
present in the checkout; the indexing mechanism itself is inventoried
separately in the 2026-10-11 overnight campaign record.

## Scanner allowlist thread (outside this repo)

The last two PRM-02 draft entries (line-lua-settings.json,
qonfig-build-settings.json) were drafted into the campaign record as
DRAFT ONLY (reason + expiry 2027-04-09); not installed, not applied.
