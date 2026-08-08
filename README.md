# tange-release

Tange 应用更新分发仓库。

| 用途 | 位置 |
|------|------|
| 版本清单 | [`release.json`](./release.json) · https://adamglin0.github.io/tange-release/release.json |
| 安装包 | [Releases](https://github.com/adamglin0/tange-release/releases) |

## 模型

- **单一 manifest**：`release.json`
- **Platform**：`macos-arm64` / `macos-x64` / `windows-x64` / `linux-x64`
- **Channel 由版本名推导**（不是单独的 JSON）：
  - `x.y.z` → Release
  - `x.y.z-rcN` → Rc
  - `x.y.z-alphaN` / `betaN` → Dev
- 客户端用用户设置的 **max channel** 过滤是否接受该版本

```json
{
  "platforms": {
    "macos-arm64": {
      "version": "1.2.0-alpha01",
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
3. 由 `version` 推出 channel；若超出用户 max channel 则忽略
4. 与本地 version 比较；需要更新时下载 `url` 并校验 `sha256`

## 发布

1. 上传构建产物到本仓库 Release
2. 更新 `release.json` 里**该平台**条目
3. push `main` → Pages 自动更新
