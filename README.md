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

## 目录结构

```text
/
├── index.html
└── first-2d-game/
    ├── index.html
    ├── index.js
    ├── index.wasm
    └── index.pck
```
