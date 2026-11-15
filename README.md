# XSec Desktop Releases

XSec Desktop 的安装包、更新清单和更新包发布在本仓库的 [Releases](https://github.com/xsec-labs/xsec/releases) 页面。本仓库只放发布产物和这份说明，源码不在这里。

本仓库原名 `xsec-labs/xsec-desktop-releases`，2026-11-15 改名为 `xsec-labs/xsec`。旧链接由 GitHub 跳转，仍然有效。

## 版本

- 标为 **Latest** 的 release 是正式版。应用只读取它，草稿和预发布都不会被应用读取。
- 每个版本的 tag 是 `v<版本>`，例如 `v0.3.7`。
- 每个 release 都附带 `SHA256SUMS`，列出每个文件的 SHA-256 摘要。

## 安装

**macOS**：打开 `XSec-<版本>-arm64.dmg`（Apple 芯片）或 `XSec-<版本>-amd64.dmg`（Intel），把 XSec 拖进「应用程序」。应用只做了临时签名，没有公证，首次打开会被 Gatekeeper 拦截：

- macOS 15 及以上：双击后出现「无法打开 XSec」，点「完成」。到「系统设置 → 隐私与安全性」，下滑到「安全性」，点 XSec 旁的「仍要打开」，输入密码后再确认。
- macOS 14 及以下：在 Finder 里右键 XSec.app，选择「打开」，再点一次「打开」。

**Windows**：运行 `XSec-Setup-<版本>-amd64.exe`。它为当前用户安装到 `%LOCALAPPDATA%\Programs\XSec`，不需要管理员权限。安装包没有签名，SmartScreen 可能提示「Windows 已保护你的电脑」，点「更多信息」，再点「仍要运行」。

**Linux**（x64）：任选一种。

- 用户级安装，不需要 root：`sh install.sh xsec-<版本>-linux-amd64.tar.gz`，装到 `~/.local/xsec.app`。
- Debian 或 Ubuntu：`sudo apt install ./xsec_<版本>_amd64.deb`，装到 `/opt/xsec`。

## 应用内更新

- macOS 应用和 Windows 当前用户安装可以在应用内检查并更新。
- Linux 目前不支持应用内更新，需要下载新版本重新安装。

应用读取 `releases/latest/download/update-<平台>.json`，平台有 `darwin-arm64`、`darwin-amd64`、`windows-amd64` 和 `linux-amd64`。清单列出版本、更新包地址、大小和签名，也列出从前几个版本升级用的增量包（`xsec-<旧版本>-to-<版本>-<平台>.delta`）。

清单和更新包都有更新签名，应用用内置公钥验证。版本、大小或摘要对不上时，更新会被拒绝。应用不会安装不高于当前版本的更新。

检查和下载更新需要能访问 `github.com`，以及 GitHub 存放 release 文件的域名。受管网络需要放行它们。

## 校验下载

```sh
sha256sum -c SHA256SUMS --ignore-missing
```

`SHA256SUMS` 只能发现下载损坏，不能证明文件真实，因为能替换安装包的人也能替换它。应用内更新的真实性靠更新签名。

## 旧版本

早于 Go 版的 Tauri 版不再收到应用内更新，需要手动下载安装最新版本。Bundle ID 仍是 `com.xsec.desktop`，用户数据目录沿用。
