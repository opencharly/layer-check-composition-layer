# layer-check-composition-layer

A from-composition check fixture: the marker layer for the
`from-composition-selftest` handwritten probe.

The `check-composition-layer` candy writes `/etc/charly-composition-selftest`,
satisfying the `composition-handwritten-probe` scenario in
`from-composition-selftest`. It exercises the `from:` composition path — a box
composed from another image rather than from a base — with a hand-written probe.

The candy is a **fixture**: it ships no user-facing service and has no `skill:`
entity. Its acceptance steps live in its `plan:` (an `mkdir:` step, a `write:`
step, and three `file:` `check:` probes) and are baked into the
`ai.opencharly.description` OCI label. The owning family skill is
`/charly-check:check`; the missing owning `skill:` entity is tracked by
[opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291).

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `check-composition-layer` |
| Effect | writes `/etc/charly-composition-selftest` (mode `0644`, content `charly composition selftest marker`) |
| Plan | `mkdir:` + `write:` run steps plus three `file:` `check:` probes |
| Owns | 0 `skill:` entities (fixture) |
| Service / port | none |

## How to use it

Compose it as a layer ref in a box's nested `candy:` list (the composition list).
A box is a `candy:` node carrying the box's `base:` image and a nested `candy:`
list of layer refs (the nested `candy:` is the composition list; the outer
`candy:` is the box body):

```yaml
my-box:
  candy:                  # the box body (an IMAGE is a `candy:` node carrying `base:`)
    from: fedora          # compose FROM another image (the `from:` path)
    candy:                # the box's composition list
      - '@github.com/opencharly/layer-check-composition-layer:v2026.239.1620'
```

The fixture is driven by the `from-composition-selftest` scenario, not by a user
box.

## Layout

- `charly.yml` — the `check-composition-layer:` candy entity (no `skill:` entity).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning family skill: `/charly-check:check`
- Missing `skill:` entity: [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291)
- Authoring reference: `/charly-image:layer`
- [`opencharly/marketplace`](https://github.com/opencharly/marketplace) — the projected corpus
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
