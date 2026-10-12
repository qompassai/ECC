# Patterns — ecc

## Validation

- Install: `npm ci --ignore-scripts` (matches upstream CI).
- Full local gate: `npm test` (validator chain + `node tests/run-all.js`).
- JS tests only: `node tests/run-all.js`. Python tests: `python3 -m pytest tests/ -q`.
- Primo is source of truth when a checkout disagrees with a stale record.

## Fork hygiene

- This fork's `main` tracks upstream affaan-m/ECC merges; local additions
  should be small, attributable commits on top, never rewrites of bundle
  content.
