# Changelog

## [0.2.0]

-   You can now run `cargo tauri build -t none` to speed up the build if you don't need executables.
    -   [4d507f9](https://www.github.com/tauri-apps/tauri/commit/4d507f9adfb26819f9d6406b191fdaa6188145f4) feat(cli/core): add support for building without targets ([#1203](https://www.github.com/tauri-apps/tauri/pull/1203)) on 2021-02-10
-   The `dev` and `build` pipeline is now written in Rust.
    -   [3e8abe3](https://www.github.com/tauri-apps/tauri/commit/3e8abe376407bb0ca8893602590ed9edf7aa71a1) feat(cli) rewrite the core CLI in Rust ([#851](https://www.github.com/tauri-apps/tauri/pull/851)) on 2021-01-30
-   Fixes `<a target="_blank">` polyfill.
    -   [4ee044a](https://www.github.com/tauri-apps/tauri/commit/4ee044a3e662a0ac2be98f7e1286088d721c3307) fix(cli): use correct arg in `_blanks` links polyfill ([#1362](https://www.github.com/tauri-apps/tauri/pull/1362)) on 2021-03-17
