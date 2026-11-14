# For evaluators

What a run of this action is evidence of. Not GA4GH certification. Not a statement that a server was started here.

## What a green run means

The composite action downloads the HelixTest release binary named by `version` (default `v0.1.3`), checks its `.sha256`, and, when `run` is not `false`, runs `helixtest`. The shell uses `set -euo pipefail`. A green step means that command exited 0.

Exit 0 means the suite met `--fail-level` (default `2`) for the mode, profile, and `--only` or `--all` you set. That is HelixTest's own exit rule, described in the HelixTest repository.

## What a green run does not mean

- It does not mean official GA4GH certification.
- It does not mean this action started Ferrum, ga4gh-infra, or any other server. The URLs in the environment have to be a stack the job already started, or a public URL you already trust.
- It does not mean HelixTest's default branch was tested. The default `version` is the release tag `v0.1.3`.
- It does not mean authentication was on, unless the stack you started has authentication on. The GHCR auth-on job is in HelixTest, not in this action.
- It does not issue Passports and it does not write HELIOS evidence.
- `run: false` only installs the binary. A green install-only step does not mean a suite ran.

The claims registry has no stage for this action. The GitHub repository description is not this file. This file's pin is `v0.1.3`, which is the default in `action.yml`.

## Contact

[contact@synapticfour.com](mailto:contact@synapticfour.com)
