# Lickba Godot Web Games

这个仓库只保存可直接发布的 Godot Web 导出成品，与 Hugo 主站源码分离。

## 已发布游戏

- [第一个 2D 游戏（Dodge the Creeps）](./first-2d-game/)

## 发布约定

- 每个游戏使用独立目录，入口统一命名为 `index.html`。
- Godot 4 Web 默认使用 Compatibility 渲染器和单线程导出。
- 不修改同批导出的 `.html`、`.js`、`.wasm`、`.pck` 文件之间的相对引用。
- GitHub Pages 对 WASM 等资源进行动态 gzip；仓库保留原始文件，由浏览器透明接收并解压压缩响应。
- Hugo 主站只保存游戏元数据、封面和此仓库的试玩地址，不复制大型运行时。

## Cloudflare Pages 测试线路

- `main` 分支继续供 GitHub Pages 使用，保留原有发布内容。
- `cloudflare-pages` 分支供 Cloudflare Pages 使用，发布裁切版 Godot 4.7 Web 模板导出。
- Cloudflare Pages 项目使用仓库根目录作为静态输出目录，不运行额外构建命令。
- 首个裁切版将 `first-2d-game/index.wasm` 从 39,509,339 字节降至 22,977,963 字节，以满足单文件 25 MiB 的部署限制。

## Cloudflare R2 大文件测试

- R2 存储桶为 `godot-web-games-assets`，游戏资源使用 `游戏目录/版本目录/` 结构保存。
- `first-2d-game-r2-original/` 是独立测试外壳，Pages 只发布 HTML、JavaScript 和加载图片。
- 未裁剪的 `index.wasm`、`index.pck` 和音频 Worklet 保存到 R2 的 `first-2d-game/original-v1/`。
- 测试阶段使用受限速的 `r2.dev` 公开地址；正式使用前应绑定可缓存的自定义域，并替换测试外壳中的资源基址。
- R2 CORS 当前允许 `godot-web-games.pages.dev`、`lickba.cn` 与 `www.lickba.cn` 发起 `GET`、`HEAD` 请求。
- 当前优化版 `first-2d-game/` 保持不变，R2 测试失败时直接停止使用测试目录即可回退。

## 目录结构

```text
/
├── index.html
├── first-2d-game/
    ├── index.html
    ├── index.js
    ├── index.wasm
    └── index.pck
└── first-2d-game-r2-original/
    ├── index.html
    ├── index.js
    └── 加载图片与图标
```
