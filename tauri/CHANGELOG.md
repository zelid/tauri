# Changelog

## [0.12.0]

-   Now Tauri commands always returns Promise<T>.
    -   [ea73325](https://www.github.com/tauri-apps/tauri/commit/ea7332539d100bd63f93396101ffa01ff73c924b) refactor(core): all API are now promise based ([#1239](https://www.github.com/tauri-apps/tauri/pull/1239)) on 2021-02-16
-   The Tauri files are now read on the app space instead of the `tauri` create.
    Also, the `AppBuilder` `build` function now returns a Result.
        - [e02c941](https://www.github.com/tauri-apps/tauri/commit/e02c9419cb8c66f4e43ed598d2fc74d4b19384ec) refactor(tauri): support for building without environmental variables ([#850](https://www.github.com/tauri-apps/tauri/pull/850)) on 2021-02-09
-   Tauri now uses explicit Error variants with `thiserror` instead of relying on `anyhow`.
    -   [156a0ad](https://www.github.com/tauri-apps/tauri/commit/156a0ad5cb0a152eaa0dd038a6b3dba68f03eb21) refactor(tauri): use explicit error types instead of anyhow ([#1209](https://www.github.com/tauri-apps/tauri/pull/1209)) on 2021-02-10
-   Replace `\` with `\\` in css assets that are lazy loaded. Since these are injected in a template literal, backslashes must be escaped. Backslashes are sometimes used for octal sequences in CSS.
    -   [4491c70](https://www.github.com/tauri-apps/tauri/commit/4491c707907a6a931fd8c057c2baeb0b9e6db1d8) fix(tauri/asset): escape octal sequences in css ([#1166](https://www.github.com/tauri-apps/tauri/pull/1166)) on 2021-01-30
-   Replaces the embedded-server mode with Wry's custom protocol feature. This allows assets to be transferred to the webview directly, instead of through a localhost server.
    -   [0c691f4](https://www.github.com/tauri-apps/tauri/commit/0c691f40a338be184a4dd2c84d6e5d0b0ed6ee4b) feat(core): Use Wry custom protocol instead of embedded server ([#1296](https://www.github.com/tauri-apps/tauri/pull/1296)) on 2021-02-25
-   Refactor the event callback payload and return an unlisten function on the `listen` API.
    -   [b670ec5](https://www.github.com/tauri-apps/tauri/commit/b670ec55f2b7389b8a2f8c965d4fe1e0cb46e6dc) refactor(core): add `unlisten`, `once` APIs to the event system ([#1359](https://www.github.com/tauri-apps/tauri/pull/1359)) on 2021-03-16
-   Adds `unlisten` and `once` APIs on the Rust event system.
    -   [b670ec5](https://www.github.com/tauri-apps/tauri/commit/b670ec55f2b7389b8a2f8c965d4fe1e0cb46e6dc) refactor(core): add `unlisten`, `once` APIs to the event system ([#1359](https://www.github.com/tauri-apps/tauri/pull/1359)) on 2021-03-16
-   The `tauri::event` module has been moved to a Webview manager API.
    -   [07208df](https://www.github.com/tauri-apps/tauri/commit/07208dff6c1e8cff7c10780f4f7f8cee9de44a2e) feat(core): add mult-window support ([#1217](https://www.github.com/tauri-apps/tauri/pull/1217)) on 2021-02-11
-   Tauri now emits events on file drops on the webview window.
    -   [2db901e](https://www.github.com/tauri-apps/tauri/commit/2db901e744f51cd4296ddec4352d7a51c859b85b) feat(core): add file drop handler ([#1352](https://www.github.com/tauri-apps/tauri/pull/1352)) on 2021-03-12
-   Fixes `resource_dir` resolution on AppImage.
    -   [bd1df5d](https://www.github.com/tauri-apps/tauri/commit/bd1df5d80431f5de4cd905ffaf7f3f2628d6b8ab) fix: get correct resource dir in AppImge (fix [#1308](https://www.github.com/tauri-apps/tauri/pull/1308)) ([#1333](https://www.github.com/tauri-apps/tauri/pull/1333)) on 2021-03-12
-   The HTTP API was improved with client caching and better payload and response types.
    -   [a7bc472](https://www.github.com/tauri-apps/tauri/commit/a7bc472e994730071f960d09a12ac85296a080ae) refactor(core): improve HTTP API, closes [#1098](https://www.github.com/tauri-apps/tauri/pull/1098) ([#1237](https://www.github.com/tauri-apps/tauri/pull/1237)) on 2021-02-15
-   Added support to multiple windows.
    -   [07208df](https://www.github.com/tauri-apps/tauri/commit/07208dff6c1e8cff7c10780f4f7f8cee9de44a2e) feat(core): add mult-window support ([#1217](https://www.github.com/tauri-apps/tauri/pull/1217)) on 2021-02-11
-   Plugins are now configurable through a `tauri.conf.json > "plugins" > $pluginName` object.
    -   [2058cc3](https://www.github.com/tauri-apps/tauri/commit/2058cc39c9ac9d9d442802db2c2f3be34a85acc4) feat(tauri): add plugin `initialize` (with config) API, run in parallel ([#1194](https://www.github.com/tauri-apps/tauri/pull/1194)) on 2021-02-10
-   Renamed the `Plugin` trait `init_script` to `initialization_script`.
    -   [5c5d8f8](https://www.github.com/tauri-apps/tauri/commit/5c5d8f811fc094cca1b441ff966f15c7bf5d2e90) refactor(tauri): rename `init_script` to `initialization_script` ([#1200](https://www.github.com/tauri-apps/tauri/pull/1200)) on 2021-02-10
-   The plugin instance is now mutable and must be `Send + Sync`.
    -   [fb607ee](https://www.github.com/tauri-apps/tauri/commit/fb607ee97a912d1e23f6d7dd6dd3c28aac9b4527) refactor(tauri): plugin trait with mutable references ([#1197](https://www.github.com/tauri-apps/tauri/pull/1197)) on 2021-02-10
-   Fixes the event system usage on the plugin `ready` hook.
    -   [23132ac](https://www.github.com/tauri-apps/tauri/commit/23132acf765ab8b6a37b74151a4c175b68390657) fix(tauri): run plugin::ready without webview.dispatch ([#1164](https://www.github.com/tauri-apps/tauri/pull/1164)) on 2021-01-29
-   The `allowlist` configuration now has one object per module.
    -   [e0be59e](https://www.github.com/tauri-apps/tauri/commit/e0be59ea26df17fe2e31224759f21fb1d0cbdfd3) refactor(core): split allowlist configuration per module ([#1263](https://www.github.com/tauri-apps/tauri/pull/1263)) on 2021-02-20
-   The Tauri script is now injected with the webview `init` API, so it is available after page changes.
    It will no longer be injected on `${distDir}/index.tauri.html`, but we will add a `${distDir}/__tauri.js` file to read it at app compile time.
    You should add that to your `.gitignore` file.
        - [4412b7c](https://www.github.com/tauri-apps/tauri/commit/4412b7c438c2b10e519bf8b696e3ef827e9091f2) refactor(tauri): inject script with webview init API ([#1186](https://www.github.com/tauri-apps/tauri/pull/1186)) on 2021-02-05
-   Removed the `no-server` mode, the `inliner`, the `dev` server proxy and the `loadAsset` API.
    -   [84d7cda](https://www.github.com/tauri-apps/tauri/commit/84d7cdae632eeb02a66f8d1d7577adfa65917a34) refactor(core): remove `no-server` and its APIs ([#1215](https://www.github.com/tauri-apps/tauri/pull/1215)) on 2021-02-11
-   Adds a global shortcut API.
    -   [855effa](https://www.github.com/tauri-apps/tauri/commit/855effadd9ebfb6bc1a3555ac7fc733f6f766b7a) feat(core): globalShortcut API ([#1232](https://www.github.com/tauri-apps/tauri/pull/1232)) on 2021-02-14
-   Added `async` support to the Tauri Rust core on commit [#a169b67](https://github.com/tauri-apps/tauri/commit/a169b67ef0277b958bdac97e33c6e4c41b6844c3).
    -   [2bf55f8](https://www.github.com/tauri-apps/tauri/commit/2bf55f80564f5c31d89384bd4a82dd55307f8c75) chore: add changefile on 2021-02-03
    -   [e02c941](https://www.github.com/tauri-apps/tauri/commit/e02c9419cb8c66f4e43ed598d2fc74d4b19384ec) refactor(tauri): support for building without environmental variables ([#850](https://www.github.com/tauri-apps/tauri/pull/850)) on 2021-02-09
-   The Tauri integration with Webview was refactored to use traits, which allows custom implementations by developers and simplifies changes on the webview implementation.
    -   [b9ce7b9](https://www.github.com/tauri-apps/tauri/commit/b9ce7b94c4eb027bcbbd4ee600b75a7407f108ca) refactor(tauri): Webview traits ([#1183](https://www.github.com/tauri-apps/tauri/pull/1183)) on 2021-02-05
-   Added window management and window creation APIs.
    -   [a3d6dff](https://www.github.com/tauri-apps/tauri/commit/a3d6dff2163c7a45842253edd81dbc62248dc65d) feat(core): window API ([#1225](https://www.github.com/tauri-apps/tauri/pull/1225)) on 2021-02-13
    -   [641374b](https://www.github.com/tauri-apps/tauri/commit/641374b15343518cd835bd5ada811941c65dcf2e) feat(core): window creation at runtime ([#1249](https://www.github.com/tauri-apps/tauri/pull/1249)) on 2021-02-17
-   Use [WRY](https://github.com/tauri-apps/wry) as Webview interface, thanks to @wusyong.
    -   [99ecf7b](https://www.github.com/tauri-apps/tauri/commit/99ecf7bb3e8da6e611b57c6680a14b65179f8a35) feat(tauri): use WRY as webview engine ([#1190](https://www.github.com/tauri-apps/tauri/pull/1190)) on 2021-02-08

## [0.11.1]

-   Update webview-official dependency which fix compatibility on macOS.
    -   [692312a](https://www.github.com/tauri-apps/tauri/commit/692312a0f51a05dd418d9cad553a695f3347b943) chore(deps) Update webview-official ([#1152](https://www.github.com/tauri-apps/tauri/pull/1152)) on 2021-01-24

## [0.11.0]

-   Match writeBinaryFile command name between js and rust
    -   [486bd92](https://www.github.com/tauri-apps/tauri/commit/486bd920f899905bec0f690092aa1e3cac2c78f3) Fix: writeBinaryFile to call the correct command (fix [#1133](https://www.github.com/tauri-apps/tauri/pull/1133)) ([#1136](https://www.github.com/tauri-apps/tauri/pull/1136)) on 2021-01-06

## [0.10.0]

-   Adds missing APIs features from `allowlist` to the tauri crate's manifest file.
    -   [2c0f09c](https://www.github.com/tauri-apps/tauri/commit/2c0f09c85c8a60c2fa304fb25174d5020663f0d7) fix(tauri) add missing API features, closes [#1023](https://www.github.com/tauri-apps/tauri/pull/1023) ([#1052](https://www.github.com/tauri-apps/tauri/pull/1052)) on 2020-10-17
    -   [72996be](https://www.github.com/tauri-apps/tauri/commit/72996be1bd3eb878c4cf30bfec79058071c26d7a) apply version updates ([#1024](https://www.github.com/tauri-apps/tauri/pull/1024)) on 2020-10-21
-   Adds a path resolution API (e.g. getting the download directory or resolving a path to the home directory).
    -   [771e401](https://www.github.com/tauri-apps/tauri/commit/771e4019b8cfd1973015ffa632c9d6c6b82c5657) feat: Port path api to js ([#1006](https://www.github.com/tauri-apps/tauri/pull/1006)) on 2020-09-24
    -   [72996be](https://www.github.com/tauri-apps/tauri/commit/72996be1bd3eb878c4cf30bfec79058071c26d7a) apply version updates ([#1024](https://www.github.com/tauri-apps/tauri/pull/1024)) on 2020-10-21
-   Update minimum Rust version to 1.42.0 due to a dependency update.
    -   [d13dcd9](https://www.github.com/tauri-apps/tauri/commit/d13dcd9fd8d30b1db147a78cecb878e924382274) chore(deps) Update Tauri Bundler ([#1045](https://www.github.com/tauri-apps/tauri/pull/1045)) on 2020-10-17
    -   [72996be](https://www.github.com/tauri-apps/tauri/commit/72996be1bd3eb878c4cf30bfec79058071c26d7a) apply version updates ([#1024](https://www.github.com/tauri-apps/tauri/pull/1024)) on 2020-10-21
-   Minimum Rust version updated to 1.47.0. Run `$ rustup update` to update to the latest version.
    -   [b4544b6](https://www.github.com/tauri-apps/tauri/commit/b4544b63f268dc6f3f47a4bfbad5d72cceee8698) chore(deps) Update Tauri API ([#1072](https://www.github.com/tauri-apps/tauri/pull/1072)) on 2020-11-07

## [0.9.2]

-   Bump all deps as noted in #975, #976, #977, #978, and #979.
    -   [06dd75b](https://www.github.com/tauri-apps/tauri/commit/06dd75b68a15d388808c51ae2bf50554ae761d9d) chore: bump all js/rust deps ([#983](https://www.github.com/tauri-apps/tauri/pull/983)) on 2020-08-20

## [0.9.1]

-   Adjust payload formatting to handle multibyte characters in front-end message
    payloads.
        - [df70ca5](https://www.github.com/tauri-apps/tauri/commit/df70ca51965665952a74161cc6eb1ff19eae45e2) Fix [#912](https://www.github.com/tauri-apps/tauri/pull/912) multibyte character breaks message ([#914](https://www.github.com/tauri-apps/tauri/pull/914)) on 2020-08-01

## [0.9.0]

-   Make sure CSS content loaded with the `loadAsset` API is inside a template string and not injected raw.
    -   [e3e2e39](https://www.github.com/tauri-apps/tauri/commit/e3e2e3920833627400ee7a5b000dc6e51d8d332b) fix(tauri) ensure css content is loaded inside a string ([#884](https://www.github.com/tauri-apps/tauri/pull/884)) on 2020-07-22
    -   [b96b1fb](https://www.github.com/tauri-apps/tauri/commit/b96b1fb6b8a4f565fb946847bb9a29d9d939e2cb) inject css with template string to allow for line breaks ([#894](https://www.github.com/tauri-apps/tauri/pull/894)) on 2020-07-25
-   Pin the `tauri-api` dependency on the `tauri` crate so updates doesn't crash the build.
    -   [ad717c6](https://www.github.com/tauri-apps/tauri/commit/ad717c6f33b4d6e20fbb13cbe30e06946dbb74f6) chore(tauri) pin tauri-api dep version ([#872](https://www.github.com/tauri-apps/tauri/pull/872)) on 2020-07-21
-   Fixes the Webview initialization on Windows.
    -   [4abd12c](https://www.github.com/tauri-apps/tauri/commit/4abd12c2a42b5ace8527114ab64da38f4486754f) fix(tauri) webview initialization on windows, fixes [#879](https://www.github.com/tauri-apps/tauri/pull/879) ([#885](https://www.github.com/tauri-apps/tauri/pull/885)) on 2020-07-23

## [0.8.0]

-   Use native dialog on `window.alert` and `window.confirm`.
    Since every communication with the webview is asynchronous, the `window.confirm` returns a Promise resolving to a boolean value.
        - [0245833](https://www.github.com/tauri-apps/tauri/commit/0245833bb56d5462a4e1249eb1e2f9f5e477592d) feat(tauri) make `window.alert` and `window.confirm` available, fix [#848](https://www.github.com/tauri-apps/tauri/pull/848) ([#854](https://www.github.com/tauri-apps/tauri/pull/854)) on 2020-07-18
        - [dac0ae9](https://www.github.com/tauri-apps/tauri/commit/dac0ae976ea1b419ed5af078d00106b1476dee04) chore(changes) add tauri-api to JS dialogs changefile on 2020-07-19
-   The notification's `body` is now optional, closes #793.
    -   [dac1db3](https://www.github.com/tauri-apps/tauri/commit/dac1db39831ecbcf23c630351d5753af01ccd500) fix(tauri) notification body optional, requestPermission() regression, closes [#793](https://www.github.com/tauri-apps/tauri/pull/793) ([#844](https://www.github.com/tauri-apps/tauri/pull/844)) on 2020-07-16
-   Fixes a regression on the storage of requestPermission response.
    ß
        - [dac1db3](https://www.github.com/tauri-apps/tauri/commit/dac1db39831ecbcf23c630351d5753af01ccd500) fix(tauri) notification body optional, requestPermission() regression, closes [#793](https://www.github.com/tauri-apps/tauri/pull/793) ([#844](https://www.github.com/tauri-apps/tauri/pull/844)) on 2020-07-16
-   Plugin system added. You can hook into the webview lifecycle (`created`, `ready`) and extend the API adding logic to the `invoke_handler` by implementing the `tauri::plugin::Plugin` trait.
    -   [78afee9](https://www.github.com/tauri-apps/tauri/commit/78afee9725e0e372f9de7edeaac523011a1c02a3) feat(tauri) add plugin system for rust ([#494](https://www.github.com/tauri-apps/tauri/pull/494)) on 2020-07-12
-   Renaming `whitelist` to `allowlist` (see #645).
    -   [a6bb3b5](https://www.github.com/tauri-apps/tauri/commit/a6bb3b59059e08a844d7bb2b43f3d1192954d890) refactor(tauri) rename `whitelist` to `allowlist`, ref [#645](https://www.github.com/tauri-apps/tauri/pull/645) ([#858](https://www.github.com/tauri-apps/tauri/pull/858)) on 2020-07-19
-   Moving the webview implementation to [webview](https://github.com/webview/webview), with the [official Rust binding](https://github.com/webview/webview_rust).
    This is a breaking change.
    IE support has been dropped, so the `edge` object on `tauri.conf.json > tauri` no longer exists and you need to remove it.
    `webview.handle()` has been replaced with `webview.as_mut()`.
        - [cd5b401](https://www.github.com/tauri-apps/tauri/commit/cd5b401707d709bf8212b0a4c34623f902ae40f9) feature: import official webview rust binding ([#846](https://www.github.com/tauri-apps/tauri/pull/846)) on 2020-07-18

## [0.7.5]

-   Fixes Edge blank screen on Windows when running tauri dev (Tauri crashing window due to Edge reloading app because of missing Content-Type header).
    -   Bumped due to a bump in tauri-api.
    -   [fedee83](https://www.github.com/tauri-apps/tauri/commit/fedee835e36daa4363b91aabd43143e8033c9a5c) fix(tauri.js) windows Edge blank screen on tauri dev ([#808](https://www.github.com/tauri-apps/tauri/pull/808)) on 2020-07-11

## [0.7.4]

-   Ignoring non UTF-8 characters on the loopback command output.
    -   [f340b29](https://www.github.com/tauri-apps/tauri/commit/f340b2914dc9c3a94ca8606f4663964fa87b95ea) fix(tauri) addition to the previous commit on 2020-07-10

## [0.7.3]

-   Properly run the loopback command on Windows.
-   Properly ignore the ${distDir}/index.html asset from the asset embbeding. Previously every asset with name matching /(.+)index.html$/g were ignored.

## [0.7.2]

Bumped due to dependency.

## [0.7.1]

-   Fixes the assets embedding into the binary.

## [0.7.0]

-   The execute_promise and execute_promise_sync helpers now accepts any tauri::Result<T> where T: impl Serialize.
    This means that you do not need to serialize your response manually or deal with String quotes anymore.
    As part of this refactor, the event::emit function also supports impl Serialize instead of String.

## [0.6.2]

-   Fixes the Windows build with the latest Windows SDK.

## [0.6.1] - (Not Published)

## [0.6.0]

-   Adds a command line interface option to tauri apps, configurable under tauri.conf.json > tauri > cli.
-   Fixes no-server mode not running on another machine due to fs::read_to_string usage instead of the include_str macro.
    Build no longer fails when compiling without environment variables, now the app will show an error.
-   Adds desktop notifications API.
-   Properly reflect tauri.conf.json changes on app when running tauri dev.
