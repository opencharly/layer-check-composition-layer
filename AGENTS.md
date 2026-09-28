# AGENTS.md — layer-check-composition-layer

Standalone candy repo for the `check-composition-layer` fixture — the marker
layer for the `from-composition-selftest` handwritten probe. It writes
`/etc/charly-composition-selftest` and carries **no `skill:` entity**.

Canonical files:

- `charly.yml` — the `check-composition-layer:` candy entity (`mkdir:` + `write:`
  run steps plus three `file:` `check:` probes; no `skill:` entity).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-check:check` — the owning family skill: the check plan authoring
  reference, the `from:` composition path, the disposable beds, and the R10
  change classes. Load before editing any `plan:` step.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, package sections, service declarations).
  Load before editing any entity field or plan step.
- **Missing owning skill:** this fixture has no `skill:` entity, so no
  `/charly-check-composition-layer:*` page is projected for it. The gap is
  recorded against the named batch
  [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291).

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has no
  per-repo candy gate. Its only workflow file is
  `.github/workflows/tag-on-merge.yml`.
- The candy's own proof is its `plan:` — the marker write plus the three `file:`
  `check:` probes (existence, mode `0644`, content) — exercised by the
  `from-composition-selftest` scenario.

## Modify this repo

- Keep the marker path, mode, and content stable: the `from-composition-selftest`
  scenario asserts all three, so a change here is a cross-repo change.
- The plan's `check:` probes are the acceptance test; keep at least one
  deterministic probe and never weaken it without a replacement.
- If an owning skill is authored, add the `skill:` entity here and update this
  signpost and the README in the same change.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
