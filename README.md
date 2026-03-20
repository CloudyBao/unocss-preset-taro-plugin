# unocss-preset-taro-plugin

用于 **Taro Webpack 构建链路** 的 UnoCSS 插件，目标是提供和 `taro-plugin-tailwind` 类似的接入体验。

## 参考来源

- [taro-plugin-tailwind](https://github.com/pcdotfan/taro-plugin-tailwind)

## 功能

- 自动向 `mini/h5` 注入 `@unocss/postcss`
- 在 Webpack 链路中挂载 `@unocss/webpack`（默认跳过 `h5`，避免部分 h5 管线兼容问题）
- 可选向 `app.*ss` 注入 `@import "./uno.css";`（默认关闭）

## 安装

```bash
pnpm add -D unocss-preset-taro-plugin unocss @unocss/postcss @unocss/webpack
```

## 使用

在 `config/index.ts` 中添加插件：

```ts
plugins: [
  [
    'unocss-preset-taro-plugin',
    {
      // 默认 false，建议配合 src/app.ts 的 import 'uno.css' 使用
      injectCssEntry: false,
      // 可选：默认使用插件内置代理（兼容 Taro 对 CJS 函数插件的要求）
      postcssPluginName: '@unocss/postcss',
      // 透传给 @unocss/postcss
      postcss: {},
      // 透传给 unocss/webpack
      uno: {},
      // 默认 false（推荐），h5 下不挂载 @unocss/webpack
      // 如需 h5 强制启用可设为 true
      enableH5WebpackPlugin: false,
    },
  ],
],
```

默认（`enableH5WebpackPlugin: false`）建议在 `src/app.ts` 引入你自己的入口样式：

```ts
import './styles/uno.css'
```

并在 `src/styles/uno.css` 写入：

```css
@unocss all;
```

如果你设置了 `enableH5WebpackPlugin: true`，也可以继续使用：

```ts
import 'uno.css'
```

创建 `uno.config.ts`：

```ts
import { defineConfig } from 'unocss'
import { presetUno } from 'unocss'

export default defineConfig({
  presets: [presetUno()],
})
```

> 如果你使用 `unocss-preset-taro`，可在这里追加对应 preset。

## 选项

```ts
interface UnoPresetTaroPluginOptions {
  // 传给 unocss/webpack
  uno?: Record<string, unknown>
  // 传给 @unocss/postcss
  postcss?: Record<string, unknown>
  // 默认：插件内置 postcss 代理；传 @unocss/postcss / unocss/postcss 也会自动兼容
  postcssPluginName?: string
  // 默认 false
  injectCssEntry?: boolean
  // 指定注入文件，比如 app.wxss / app.jxss
  injectCssFile?: string
  // 默认 false，是否在 h5 构建也启用 @unocss/webpack
  enableH5WebpackPlugin?: boolean
}
```

## 开源信息

- License: MIT
- Changelog: [CHANGELOG.md](./CHANGELOG.md)
- Contributing: [CONTRIBUTING.md](./CONTRIBUTING.md)
- Code of Conduct: [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)
- Security: [SECURITY.md](./SECURITY.md)

## License

MIT
