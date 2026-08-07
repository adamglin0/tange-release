# tange-release

Tange 应用更新分发仓库。

| 用途 | 位置 |
|------|------|
| Release 清单 | [`release.json`](./release.json) · https://adamglin0.github.io/tange-release/release.json |
| RC 清单 | [`rc.json`](./rc.json) · https://adamglin0.github.io/tange-release/rc.json |
| Dev 清单 | [`dev.json`](./dev.json) · https://adamglin0.github.io/tange-release/dev.json |
| 安装包 | [Releases](https://github.com/adamglin0/tange-release/releases) |

## 模型

- **Channel**：`release` / `rc` / `dev`，各一份 JSON
- **Platform**：`macos-arm64` / `macos-x64` / `windows-x64` / `linux-x64`
- **版本按 platform 独立**：同一 channel 下不同平台可以是不同 version

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

1. 按当前 channel 请求 `/{channel}.json`
2. 取 `platforms[<platform>]`
3. 与本地 version 比较；需要更新时下载 `url` 并校验 `sha256`

## 发布

1. 上传构建产物到本仓库 Release
2. 更新对应 channel JSON 里**该平台**条目的 `version` / `url` / `sha256`
3. push `main` → Pages 自动更新
