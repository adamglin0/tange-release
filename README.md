# tange-release

Tange 应用更新分发仓库。

| 用途 | 位置 |
|---|---|
| 版本清单 | [`release.json`](./release.json) · https://adamglin0.github.io/tange-release/release.json |
| 安装包 | [Releases](https://github.com/adamglin0/tange-release/releases) |

## 模型

- 单一 manifest：`release.json`
- Platform：`macos-arm64` / `macos-x64` / `windows-x64` / `linux-x64`
- 每个平台的 `releases` 保存多个频道候选，较新的预发布版本不会遮蔽稳定版。
- Channel 由版本名推导：
  - `x.y.z` → Release
  - `x.y.z-rcN` → Rc
  - `x.y.z-alphaN` / `betaN` → Dev
- 客户端从用户接受的最高频道中选择最新版本；`Auto` 跟随当前程序版本的频道。

```json
{
  "platforms": {
    "macos-arm64": {
      "releases": [
        {
          "version": "1.2.0-alpha01",
          "notes": "...",
          "publishedAt": "2026-08-07T00:00:00Z",
          "url": "https://github.com/adamglin0/tange-release/releases/download/...",
          "sha256": "...",
          "size": 123456
        }
      ]
    }
  }
}
```

## 客户端

1. 启动时请求 `/release.json`。
2. 读取 `platforms[<platform>].releases`。
3. 由版本名推导 channel，过滤出当前 max channel 接受的版本。
4. 选择比本地版本新的最高版本。
5. 下载 `url`，校验 `sha256`，等待用户确认重启后事务式覆盖安装。

## 发布

1. 上传静默更新产物到本仓库 Release：macOS Zip、Windows NSIS、Linux AppImage。
2. 在 `release.json` 对应平台的 `releases` 中追加或替换相同版本。
3. 保留其他频道的最新候选。
4. push `main`，由 Pages 自动更新。
