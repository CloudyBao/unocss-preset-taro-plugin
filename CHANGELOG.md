# Changelog

All notable changes to this project will be documented in this file.

## [0.1.5] - 2026-03-20

### Added

- Re-export `presetUno` from `unocss-preset-taro-plugin` so business projects can import preset from the same plugin package.

## [0.1.4] - 2026-03-20

### Fixed

- Support Taro 4 `modifyRunnerOpts` config shape where `opts` is the config object itself (not only `{ config }` wrapper).
- Patch `ctx.initialConfig` in addition to runner opts so Uno PostCSS injection is consistently visible in h5/mini builds.

## [0.1.3] - 2026-03-20

### Fixed

- Add built-in CJS proxy for Uno PostCSS so Taro can execute plugin via `require(name)(config)`.
- Normalize `@unocss/postcss` and `unocss/postcss` to the built-in proxy path, fixing h5 Uno directive transform not taking effect.

## [0.1.2] - 2026-03-20

### Fixed

- Normalize `postcssPluginName` from `@unocss/postcss` to `unocss/postcss` for Taro postcss runtime compatibility.
- Set default postcss plugin name to `unocss/postcss` so Uno directives are actually transformed in h5/mini builds.

## [0.1.1] - 2026-03-20

### Fixed

- Skip `@unocss/webpack` on `h5` by default to avoid webpack loader parse issues in some Taro h5 pipelines.

### Added

- New option `enableH5WebpackPlugin` to explicitly enable `@unocss/webpack` for h5 when needed.

## [0.1.0] - 2026-03-20

### Added

- Initial release of `unocss-preset-taro-plugin`.
- Taro webpack plugin integration for UnoCSS via `@unocss/webpack`.
- Auto injection for `@unocss/postcss` into `mini/h5` config.
- Optional CSS entry injection (`injectCssEntry`, default `false`).
