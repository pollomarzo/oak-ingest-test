# fixture-paper-repo — the interim dogfood paper (repo=paper tier)

A **pushable** repo=paper skeleton whose only job is to exercise the frozen shim against a
live GitHub runner and close the two composite-action behavior spikes ([R18]). It is the
`test/fixture-paper/` unit fixture reshaped into a standalone repo, plus the frozen `.github/`
shim stamped in verbatim (design §1, [R2], [R55]).

## What this is

| Path | Role |
|---|---|
| `.github/actions/engine/action.yml` | frozen composite action: resolve ref → checkout ENGINE@ref → dispatch a verb (§1a) |
| `.github/actions/engine/pins.yml` | `engine_repo: pollomarzo/oaktree-sapling`, `instance_repo: pollomarzo/fixture-instance-config` (the trust boundary, dec. 21, [R37]) |
| `.github/workflows/{ci,preview-deploy,prepare,publish}.yml` | the four frozen workflows (§1b–1e) |
| `CODEOWNERS` | gates `.github/` + itself to `@pollomarzo` (personal repo → no org team, [R56]) |
| `myst.yml` | the paper; engine coordinate at `project.options.oaktree-sapling.{version,edition}` |
| `index.md`, `bib.bib` | minimal content (an `abstract` part + one section + one citation) |
| `thumbnails/thumbnail.png` | placeholder — the gallery/paper-base require this path |

## Engine coordinate (in `myst.yml`)

```yaml
project:
  id: fixture-2026-interim-paper          # matches instance id_pattern, ≠ id_sentinel
  options:
    youtube: https://youtu.be/dQw4w9WgXcQ # sibling option — proves compose never clobbers it ([R49])
    oaktree-sapling:
      version: v0.0.0-dev.1                # a dev release — CI runs released tags only ([R57])
      edition: fixture-edition
```

`version` is a **release** — a runnable engine ⟺ a release ([R57]): CI runs released tags only,
never a branch tip. Interim pins a dev pre-release (`vX.Y.Z-dev.N`, accumulate + prune —
`../../engine/RELEASING.md`); a non-release pin fails loud in the shim. **On canonical this
becomes a real `vX.Y.Z`.**

## Deliberately absent

- **No `paper-environment.yml`** — this paper executes no code. Its absence is load-bearing:
  it is exactly what makes the composite action's `if: hashFiles('paper-environment.yml') != ''`
  micromamba step **skip**, which is spike (i) of [R18].
- **No `extends:`** — compose injects the engine‹edition‹brand chain at build time.
- **No engine version *pin* in `extends:` or asset URLs** — the single coordinate above is it.

See `../PROVISIONING.md` for the push-the-engine prerequisite, the repo provisioning
checklist, and the exact [R18] test procedure.
