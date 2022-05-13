# shared-workflows

GitHub Actions workflows I use across multiple projects, stored in a single place for reusability.

## Contents

- [Rust](.github/workflows/test-rust-project.yml)
    - Runs checks across 3 operating systems (Linux, macOS, and Windows) and 3 Rust channels (Beta, Nightly, and Stable).
    - Validates source code formatting
    - Lints source code using Clippy
    - Runs tests using [cargo-nextest](https://nexte.st/)
    - Lints dependencies using [cargo-deny](https://github.com/EmbarkStudios/cargo-deny)
    - Can install packages on Linux runners using APT for crates that do dynamic linking
    - Publishes [LSIF](https://lsif.dev/) data to Sourcegraph for indexing the crate
    - Checks that the crate compiles against its MSRV (`1.57.0` by default)
