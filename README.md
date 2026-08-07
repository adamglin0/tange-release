# tange-release

Tange 应用更新分发仓库。

| 用途 | 位置 |
|------|------|
| 版本清单（Pages） | [`latest.json`](./latest.json) · https://adamglin0.github.io/tange-release/latest.json |
| 安装包 | [Releases](https://github.com/adamglin0/tange-release/releases) |

## 客户端流程

1. `GET https://adamglin0.github.io/tange-release/latest.json`
2. 与本地版本比较 `version`
3. 按平台取 `assets[<os>].url` 下载
4. 校验 `sha256` 后安装

## 发布

1. 上传构建产物到本仓库 **Release**（tag = 版本号，如 `1.0.0`）
2. 更新 `latest.json` 的 `version` / `notes` / 各平台 `url` 与 `sha256`
3. push `main` → Pages 自动更新

## Channel

- `latest.json` — stable
- 需要 beta 时再加 `beta.json`，结构相同
