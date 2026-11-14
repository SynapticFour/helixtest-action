# helixtest-action

helixtest-action downloads a published HelixTest program and runs it against an HTTP service the job already started.

For someone who wants that check in GitHub Actions without building HelixTest in the job.

**Status: No public status is recorded.** The claims registry has no stage for this action.

The program is the HelixTest release `v0.1.3`. Results are not GA4GH certification. The action does not start Ferrum, ga4gh-infra, or any other server. Signed evidence stays in [HELIOS](https://github.com/SynapticFour/HELIOS).

## What it does

- It downloads the `helixtest` binary for the runner from the HelixTest GitHub Release named by `version`, and checks the `.sha256` file.
- It runs `helixtest --mode` with `--report json` and `--fail-level`. Empty `only` means `--all`.
- The default mode is `ferrum`. `ferrum+infra` expects the broker stack to be up already.

## Limits

- A green run means `helixtest` exited 0 at the fail level you set. It does not mean GA4GH certification, and it does not mean a server was started by this action. See [docs/FOR-EVALUATORS.md](docs/FOR-EVALUATORS.md).
- The default binary pin is HelixTest `v0.1.3`, which is the default of `version` in `action.yml`. The GitHub description of this repository still says `v0.1.1`. That description is not this file. The tag `v0.1.3` is not HelixTest's default branch. This action does not build that branch.
- Release assets exist for linux-gnu x86_64, linux-gnu aarch64, and darwin aarch64. Other runners fail with that list. There is no Windows binary.
- This action does not turn authentication on, does not issue Passports, and is not HELIOS.

## Quick start

Point the environment at a service you already started.

```yaml
- uses: SynapticFour/helixtest-action@SHA
  with:
    version: v0.1.3
    mode: ferrum
    only: beacon
    fail-level: "2"
  env:
    GATEWAY_BASE: http://127.0.0.1:8080
    BEACON_URL: http://127.0.0.1:8080/ga4gh/beacon/v2
    DRS_URL: http://127.0.0.1:8080/ga4gh/drs/v1
```

Replace `SHA` with the 40-character commit you have read. Do not use `@main` as the pin. Empty `only` runs `--all`. `run: "false"` only installs the binary.

You should see the step run `helixtest` and exit 0 when the suite met the fail level. A missing binary for the runner prints the published asset list and exits 1.

## Inputs

| Input | Required | Default | What it does |
|-------|----------|---------|--------------|
| `version` | no | `v0.1.3` | HelixTest GitHub Release tag |
| `mode` | no | `ferrum` | `helixtest --mode`. `ferrum` or `ferrum+infra`. Does not start servers. |
| `profile` | no | empty | Optional `--profile`, for example `ferrum-infra-pilot` |
| `only` | no | empty | Optional `--only` surface, for example `beacon`. Empty means `--all`. |
| `fail-level` | no | `2` | `--fail-level`. The process exits non-zero at this HelixTest level. |
| `extra-args` | no | empty | Extra arguments appended to `helixtest`. They are split on spaces. Do not put secrets here. |
| `run` | no | `true` | `false` only installs the binary. This repository's CI uses that. |
| `github-token` | no | `${{ github.token }}` | Optional token for the public release download |

Modes, the `ferrum+infra` example, and runners: [docs/REFERENCE.md](docs/REFERENCE.md).

## Documentation

Every file under `docs/` is listed in [docs/README.md](docs/README.md).

### Tutorial

The usage example above is the tutorial. There is no separate getting-started page.

### How-to guides

- [Modes and runners](docs/REFERENCE.md)

### Reference

- [For evaluators](docs/FOR-EVALUATORS.md)
- [Who it is for](docs/IDENTITY.md)
- [Changelog](CHANGELOG.md)
- [Security](SECURITY.md)

### Explanation

The checks live in [HelixTest](https://github.com/SynapticFour/HelixTest). This repository only downloads a published binary and runs it.

## Licence

Apache License 2.0. The file is [LICENSE](LICENSE). GitHub reports this repository's licence as Other. The licence file in the tree is Apache-2.0. There is no separate licence claim in the registry.

## Cite

Use [CITATION.cff](CITATION.cff). Prefer that file over a hand-copied line.

## Website

- Open tools: [https://synapticfour.com/en/offene-werkzeuge/](https://synapticfour.com/en/offene-werkzeuge/)
- Technical profile: [https://synapticfour.com/en/technical/code/](https://synapticfour.com/en/technical/code/)

The same pages exist in German (`/de/offene-werkzeuge/`, `/de/technik/code/`) and in French (`/fr/offene-werkzeuge/`, `/fr/technique/code/`).

The map of repositories: [profile/README.md](https://github.com/SynapticFour/.github/blob/main/profile/README.md).

Contact: [contact@synapticfour.com](mailto:contact@synapticfour.com)
