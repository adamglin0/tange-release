# tange-release

Tange 应用更新分发仓库。

| 用途 | 位置 |
|------|------|
| 版本清单 | [`release.json`](./release.json) · https://adamglin0.github.io/tange-release/release.json |
| 安装包 | [Releases](https://github.com/adamglin0/tange-release/releases) |

## 模型

- **单一 manifest**：`release.json`
- **Platform**：`macos-arm64` / `macos-x64` / `windows-x64` / `linux-x64`
- **版本按 platform 独立**：不同平台可以是不同 version
- alpha / beta / rc / stable 都写进同一份 `release.json`；客户端始终取该平台最新 version

```json
{
  "platforms": {
    "macos-arm64": {
      "version": "1.2.0",
      "notes": "...",
      "publishedAt": "2026-08-07T00:00:00Z",
      "mandatory": false,
      "url": "https://github.com/adamglin0/tange-release/releases/download/...",
      "sha256": "...",
      "size": 0
    }
  }
}
```

## 客户端

1. 请求 `/release.json`
2. 取 `platforms[<platform>]`
3. 与本地 version 比较；需要更新时下载 `url` 并校验 `sha256`

## 发布

1. 上传构建产物到本仓库 Release
2. 更新 `release.json` 里**该平台**条目的 `version` / `url` / `sha256` / `size`
3. push `main` → Pages 自动更新
