# Changelog

## [0.2.0]

-   The file dialog API now uses [rfd](https://github.com/PolyMeilex/rfd). The filter option is now an array of `{ name: string, extensions: string[] }`.
    -   [2326bcd](https://www.github.com/tauri-apps/tauri/commit/2326bcd399411f7f0eabdb7ade910be473adadae) refactor(core): use `nfd` for file dialogs, closes [#1251](https://www.github.com/tauri-apps/tauri/pull/1251) ([#1257](https://www.github.com/tauri-apps/tauri/pull/1257)) on 2021-02-18
-   The HTTP API was improved with client caching and better payload and response types.
    -   [a7bc472](https://www.github.com/tauri-apps/tauri/commit/a7bc472e994730071f960d09a12ac85296a080ae) refactor(core): improve HTTP API, closes [#1098](https://www.github.com/tauri-apps/tauri/pull/1098) ([#1237](https://www.github.com/tauri-apps/tauri/pull/1237)) on 2021-02-15
-   The invoke function can now be called with the cmd as the first parameter and the args as the second.
    -   [427d170](https://www.github.com/tauri-apps/tauri/commit/427d170930ab711fd0ca82f7a73b524d6fdc222f) feat(api/invoke): separate cmd arg ([#1321](https://www.github.com/tauri-apps/tauri/pull/1321)) on 2021-03-04
-   Adds a global shortcut API.
    -   [855effa](https://www.github.com/tauri-apps/tauri/commit/855effadd9ebfb6bc1a3555ac7fc733f6f766b7a) feat(core): globalShortcut API ([#1232](https://www.github.com/tauri-apps/tauri/pull/1232)) on 2021-02-14
-   Added window management and window creation APIs.
    -   [a3d6dff](https://www.github.com/tauri-apps/tauri/commit/a3d6dff2163c7a45842253edd81dbc62248dc65d) feat(core): window API ([#1225](https://www.github.com/tauri-apps/tauri/pull/1225)) on 2021-02-13
    -   [641374b](https://www.github.com/tauri-apps/tauri/commit/641374b15343518cd835bd5ada811941c65dcf2e) feat(core): window creation at runtime ([#1249](https://www.github.com/tauri-apps/tauri/pull/1249)) on 2021-02-17
