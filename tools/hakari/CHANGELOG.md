# Changelog

## [0.13.1] - 2023-01-14

### Fixed

The default template for `hakari.toml` now specifies `dep-format-version = "4"`.

## [0.13.0] - 2023-01-14

### Added

Introduced a new `dep-format-version`, version 4, with a change to always sort outputs alphabetically. This
matches the order produced by [cargo-sort](https://crates.io/crates/cargo-sort) ([#65]).

[#65]: https://github.com/guppy-rs/guppy/issues/65

## [0.12.0] - 2023-01-08

### Added

Introduced a new `dep-format-version`, version 3, with these changes:

* Always elide build metadata from version strings (e.g. with the semver string `5.4.0+g7f361a3`, don't show the bit after the + sign). Thanks [Nikhil Benesch](https://github.com/guppy-rs/guppy/pull/57) for your first contribution!
* Remove private features from the workspace-hack's Cargo.toml. This should simplify the output greatly.

### Changed

- MSRV updated to Rust 1.62.
- target-spec updated to Rust 1.66.

## [0.11.1] - 2022-12-04

### Fixed

- Fixed a panic in rare circumstances ([#38]).

[#38]: https://github.com/guppy-rs/guppy/issues/38

## [0.11.0] - 2022-11-07

### Changed

- Updated guppy to 0.15.0.

## [0.10.2] - 2022-09-30

### Changed

- Repository location update.
- MSRV updated to Rust 1.58.

Thanks to [Carol Nichols](https://github.com/carols10cents) for her contributions to this release!

## [0.10.1] - 2022-05-29

### Changed

- Dependency updates: in particular, guppy updated to 0.14.2.

## [0.10.0] - 2022-03-14

### Added

Support for [weak dependencies and namespaced features].

[weak dependencies and namespaced features]: https://rust-lang.github.io/rfcs/3143-cargo-weak-namespaced-features.html

### Changed

- Public dependency version bump: `guppy` updated to 0.14.0.
- MSRV updated to Rust 1.56.

## [0.9.0] - 2022-02-06

### Added

- `doc_cfg`-based feature labels to rustdoc.

### Changed

- Public dependency bump: guppy updated to 0.13.0.

### Fixed

- A small fix to Cargo build simulations ([#596](https://github.com/facebookincubator/cargo-guppy/issues/596)). This is not a breaking change to the hakari output because it is a bugfix.

## [0.8.1] - 2021-12-08

- Reverted the changes in version 0.7.3 because of [#524](https://github.com/facebookincubator/cargo-guppy/issues/524).

## [0.8.0] - 2021-12-06

### Added

- Support for explaining why a crate is in the workspace-hack, used by `cargo hakari explain`.

### Changed

- `VerifyErrors` now prints out information in the same format as explain---as a result, some of its APIs have
  changed.

## [0.7.3] - 2021-11-28

- Internal dependency `guppy-workspace-hack` updated to [`workspace-hack`](https://crates.io/crates/workspace-hack).

## [0.7.2] - 2021-11-27

Internal updates for `cargo-hakari 0.9.8`.

## [0.7.1] - 2021-11-25

### Added

- Support for [publishing a dummy workspace-hack](https://docs.rs/cargo-hakari/latest/cargo_hakari/publishing). This is an
  alternate publishing method that integrates better with existing workflows.
- New config option `dep-format-version`, to control `workspace-hack = ...` lines in other `Cargo.toml`s.
  - Newly initialized workspaces have `dep-format-version = "2"`.
  - Version 2 is required for the alternate publishing method.

## [0.7.0] - 2021-11-23

### Fixed

- Updated example in `README.md` now that the `cargo-guppy` repository has a workspace-hack.

### Changed

- Updated to `guppy 0.12.0`.

## [0.6.2] - 2021-10-09

### Fixed

- Backed out the [algorithmic improvement](https://github.com/facebookincubator/cargo-guppy/pull/468) from earlier
  because it didn't handle some edge cases.
- Also simulate builds with dev-dependencies disabled.
- Remove empty sections from the output.

## [0.6.1] - 2021-10-06

### Added

- Support for alternate registries through the `[registries]` section in the config.
  - This is a temporary workaround until [Cargo issue #9052](https://github.com/rust-lang/cargo/issues/9052) is resolved.

### Fixed

- [Fixed some workspace-hack contents missing in an edge case.](https://github.com/facebookincubator/cargo-guppy/pull/476)

### Optimized

- An [algorithmic improvement](https://github.com/facebookincubator/cargo-guppy/pull/468) makes computation up to 33% faster.

## [0.6.0] - 2021-10-03

### Added

- A new `UnifyTargetHost::Auto` strategy, which uses the `ReplicateTargetOnHost` strategy
  if there are internal build dependencies or proc macros in the workspace, or the `UnifyIfBoth` strategy
  if not.

### Changed

- For `UnifyTargetHost`:
  - `Auto` is the new default strategy.
  - `ReplicateTargetAsHost` has been renamed to `ReplicateTargetOnHost`.
  - `UnifyOnBoth` has been renamed to `UnifyIfBoth`.

### Fixed

- Fixed some formatting issues with `WorkspaceOps`.

## [0.5.0] - 2021-10-01

### Added

- hakari now outputs packages corresponding to the intersection of all platforms, then outputs
  any other platform-specific packages left. This simplifies the output greatly and is also more
  correct.
- A new option `final_excludes` to remove packages from the result at the end of computation.
  - This is in constract to `traversal_excludes` (renamed from `omitted_packages`) which removes
    packages both during and after computation.
- A new `cli-support` feature contains several new structs used by `cargo-hakari`.
- In `HakariBuilderSummary`, `version = "v2"` etc has been renamed to `resolver = "2"` to align with
  cargo.
  - The old options will continue to work.
- In `HakariBuilderSummary`, `traversal-excludes` and `final-excludes` are now easier to describe while
  deserializing: they now take a `workspace-members` list of names, and a `third-party` list of specifiers such as
  `{ name = "serde", version = "1" }`.
  - The resolver will now also fail if any specifiers are unmatched.

### Changed

- `omitted_packages` renamed to `traversal_excludes`.
- Because of the changes to how excludes are represented, old-style `HakariBuilderSummary` instances
  may no longer parse correctly.
- Public dependency bump: `guppy` updated to 0.11.1.
- MSRV updated to Rust 1.53.

## [0.4.1] - 2021-09-13

### Changed

- Public dependency version bump: `guppy` updated to 0.10.1.
- MSRV updated to Rust 1.51.

## [0.4.0] - 2021-09-13

(This release was never published because it was based on `guppy 0.10.0`, which was yanked.)

## [0.3.0] - 2021-03-11

### Changed

- Public dependency version bump: `guppy` updated to 0.9.0.
- `HakariCargoToml` now uses `camino`'s UTF-8 paths.
  - `HakariCargoToml::new` now accepts `impl Into<Utf8PathBuf>` rather than `impl Into<PathBuf>`.
  - `HakariCargoToml::toml_path` returns `&Utf8Path` instead of `&Path`.

## [0.2.0] - 2021-02-23

### Changed

- `hakari` now uses [`camino`](https://crates.io/crates/camino) `Utf8Path` and `Utf8PathBuf` wrappers. These wrappers
  provide type-level assertions that returned paths are valid UTF-8.
- Public dependency version bumps:
  - `proptest` updated to version 1 and the corresponding feature renamed to `proptest1`.

## [0.1.1] - 2021-02-04

### Added

* Experimental Windows support. There may still be bugs around path normalization: please [report them](https://github.com/guppy-rs/guppy/issues/new).

### Fixed

* Fixed Cargo.toml output for path dependencies.
* Return an error for non-Unicode paths instead of silently producing incorrect paths.

## [0.1.0] - 2021-02-03

Initial release.

[0.13.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.13.1
[0.13.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.13.0
[0.12.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.12.0
[0.11.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.11.1
[0.11.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.11.0
[0.10.2]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.10.2
[0.10.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.10.1
[0.10.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.10.0
[0.9.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.9.0
[0.8.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.8.1
[0.8.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.8.0
[0.7.3]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.7.3
[0.7.2]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.7.2
[0.7.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.7.1
[0.7.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.7.0
[0.6.2]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.6.2
[0.6.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.6.1
[0.6.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.6.0
[0.5.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.5.0
[0.4.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.4.1
[0.4.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.4.0
[0.3.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.3.0
[0.2.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.2.0
[0.1.1]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.1.1
[0.1.0]: https://github.com/guppy-rs/guppy/releases/tag/hakari-0.1.0
