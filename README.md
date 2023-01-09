# shared-workflows [![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

GitHub Actions workflows I use across multiple projects, stored in a single place for reusability.

## Contents

### [Rust](.github/workflows/test-rust-project.yml)

- Runs checks across 3 operating systems (Linux, macOS, and Windows) and 3 Rust channels (Beta, Nightly, and Stable).
- Validates source code formatting
- Lints source code using Clippy
- Runs tests using [cargo-nextest](https://nexte.st/)
- Lints dependencies using [cargo-deny](https://github.com/EmbarkStudios/cargo-deny)
- Can install packages on Linux runners using APT for crates that do dynamic linking
- Checks that the crate compiles against its MSRV (`1.57.0` by default)

<details>
<summary>Usage</summary>

```yaml
on:
  push:
    branches:
      - main
      - renovate/**
  pull_request:
    branches:
      - main

name: Check Rust code
jobs:
  check:
    uses: msfjarvis/shared-workflows/.github/workflows/test-rust-project.yml@main
```

</details>

### [Nix Flakes](.github/workflows/test-flakes-project.yml)

- Sets up [Nix](https://nixos.org) on a Linux runner
- Sets up [Cachix](https://cachix.org/) with my own binary cache
- Runs `nix flake check` to run all default checks exposed by the Flake

<details>
<summary>Usage</summary>

```yaml
on:
  push:
    branches:
      - main
      - renovate/**
  pull_request:
    branches:
      - main

name: Check Rust code
jobs:
  check:
    uses: msfjarvis/shared-workflows/.github/workflows/test-flakes-project.yml@main
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
      cachix-token: ${{ secrets.CACHIX_AUTH_TOKEN }}
```

</details>
