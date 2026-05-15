# Cai Install XP - Steam 游戏清单获取与导入工具

**版本：v1.52b1 (GUI Edition-Final Vision)**  
**作者：pvzcxw**  
**许可证：MIT License**

> 一个用于 Steam 游戏的清单（manifest）和密钥（decryption key）获取、自动导入的桌面工具，同时支持 **SteamTools** 与 **GreenLuma** 两种解锁环境。

![Python](https://img.shields.io/badge/Python-3.9%2B-blue) ![License](https://img.shields.io/badge/License-GPLv3-green) ![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey)

本软件及cai install全系已完成停更，详细信息：

Cai install Official全系列于2026年6月停更

此次重建仓库是为了修改协议为MIT，即使软件里还是GPL3.0

人话：我不做软件了

停更通知：

从2023年，到现在，我们一起走过了3个春夏秋冬，但，落日终归海，入库圈的环境已经腻了，这个圈子固然是乌烟瘴气的，倒卖，恶俗，各家互斗，一次次的，对我来说，入库圈已不是我乐趣所在了，而是一种负担，折磨。从一次倒卖，被背刺，辱骂，都是对我的伤害。很多次，都是强行忍受，对我而言没有益处。

而且，清单下载器做久了也就那样，没什么新鲜感了，cai install走到现在，仅凭热爱，在25-26两年间，cai install xp,cai install gui,cai install web ui等，一共陆续更新了70多个版本，平均每5天更新一次，但现在这份热爱已消失了。

我已经想停更好久了，感觉继续下去没什么意思了，cai install这个工具能让大家喜欢，我也很开心，在入库圈有一定名誉，也是大家一齐的努力结果。

另一方面，步入高中，我也不想再把注意力放在这里。

Cai install全系（cai install xp,cai install GUI,cai install web ui,cai install reborn)将以MIT开源，欢迎大家二改！继承cai install的ip精神！

这次停更，也许是分离，但是我认为cai install这个IP会留在大家心里。


2023-2026                                                                                                         —pvzcxw

---

## ✨ 功能特点

- 🔍 **智能搜索** – 通过游戏名、AppID 或 SteamDB / Steam 商店链接自动识别游戏。
- 📦 **多源清单库** – 支持从以下仓库获取清单：
  - SWA V2 (printedwaste)
  - Cysaw
  - Furcate
  - CNGS (assiw)
  - SteamDatabase
  - 多个 GitHub 清单仓库（可自动搜索或指定）
- 🤖 **一键解锁** – 自动识别已安装的解锁工具（SteamTools / GreenLuma），并生成对应的解锁文件：
  - **SteamTools** → 生成 `stplug-in/<AppID>.lua`，同时复制清单到 `depotcache` 及 `config/depotcache`。
  - **GreenLuma** → 生成 `AppList/<AppID>.txt`，合并密钥到 `config.vdf`，复制清单到 `depotcache`。
- 🌐 **网络优化** – 自动检测国内/海外环境，使用相应镜像加速 GitHub 文件下载。
- 📝 **内置文件管理器** – 在 GUI 内直接浏览、编辑、删除已生成的 `.lua` 解锁文件。
- ⚙️ **可配置行为** – 支持 GitHub Personal Token、自定义 Steam 路径、SteamTools 仅生成 LUA 脚本模式。

---

## 🖥️ 系统要求

- **操作系统**：Windows 10 / 11（理论支持 Windows 7，未严格测试）
- **Python 版本**：3.9 或更高
- **Steam 客户端**：已安装并登录
- **解锁工具**（任选其一）：
  - [SteamTools](https://steamtools.net/)（推荐）
  - [GreenLuma 2025](https://cs.rin.ru/forum/viewtopic.php?f=29&t=71837)

---

## 📦 安装与依赖

### 1. 克隆或下载源码

```bash
git clone https://github.com/pvzcxw/cai-install_stloader.git
cd cai-install_stloader
```

### 2. 安装 Python 依赖

建议使用虚拟环境（venv）避免冲突。

```bash
pip install ttkbootstrap httpx aiofiles vdf
```

- **ttkbootstrap** – 现代化 GUI 主题  
- **httpx** – 异步 HTTP 请求（用于 API 和文件下载）  
- **aiofiles** – 异步文件操作  
- **vdf** – Valve VDF 格式解析

> 注：标准库 `asyncio`, `tkinter`, `zipfile`, `json`, `pathlib` 等无需额外安装。

### 3. 运行程序

```bash
python frontend_gui.py
```

首次启动会自动生成 `config.json` 和 `settings.json`（用于记录“不再显示启动提示”的状态）。

---

## 🚀 使用说明

### 1. 初始配置

程序启动后会尝试自动检测：
- Steam 安装路径（通过注册表或自定义路径）
- 已安装的解锁工具（SteamTools / GreenLuma）

若无法自动检测，将弹出手动选择对话框，请根据你实际使用的工具选择。

> ⚠️ 请勿同时安装 SteamTools 和 GreenLuma，否则程序会报“环境冲突”并禁用处理按钮。

### 2. 主界面

- **输入区**：输入 Steam 游戏 AppID 或商店链接（支持逗号分隔多个，如 `730, 570`）。
  - 也可以使用“搜索”按钮通过游戏名称查找 AppID 并自动填入。
- **模式选择**：
  - **从指定库安装** – 从下拉列表中选择一个固定的清单库。
  - **搜索所有 GitHub 库** – 在所有已知仓库中自动搜索该游戏的清单。
- **开始处理** – 执行获取清单、密钥并生成解锁文件。
- **入库管理** – 打开右侧面板，查看/编辑/删除 `stplug-in` 目录下的 `.lua` 文件。

### 3. 高级设置（菜单栏 → 设置 → 编辑配置）

| 选项 | 说明 |
|------|------|
| GitHub Personal Token | 可选，用于提高 GitHub API 请求限额（每小时 5000 次 vs 未认证 60 次）。[获取方法](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) |
| 自定义 Steam 路径 | 当自动检测失败时，手动指定 Steam 安装目录（例如 `D:\Steam`）。 |
| 使用 SteamTools 进行清单更新 (仅下载 LUA) | 勾选后，对于 SteamTools 用户将 **仅生成 LUA 脚本**，不下载 `.manifest` 文件，适合只想自动更新解锁脚本而无需本地清单的场景（注意：可能影响 D 加密游戏）。 |

### 4. 入库管理面板

点击“入库管理”按钮展开右侧面板，可以：
- **刷新** – 重新读取 `stplug-in` 目录下的 `.lua` 文件。
- **查看/编辑** – 用内置记事本打开选中的 `.lua` 文件（支持保存）。
- **删除** – 删除选中的解锁文件。
- **右键菜单** – 支持定位文件、在 Steam 库中查看详情。

---

## ⚙️ 配置文件说明

### `config.json`

存放用户配置，位于程序同目录。示例：

```json
{
    "Github_Personal_Token": "ghp_xxxxxxxxxxxx",
    "Custom_Steam_Path": "D:\\Steam",
    "steamtools_only_lua": false,
    "QA1": "温馨提示...",
    "QA2": "温馨提示..."
}
```

### `settings.json`

仅用于记录启动提示的显示状态：

```json
{
    "show_notification": false
}
```

---

## 🧩 支持的清单仓库

| 名称 | 标识符 | 说明 |
|------|--------|------|
| SWA V2 | `swa` | https://printedwaste.com |
| Cysaw | `cysaw` | https://cysaw.top |
| Furcate | `furcate` | https://furcate.eu |
| CNGS | `cngs` | https://assiw.cngames.site |
| SteamDatabase | `steamdatabase` | S3 存储 |
| GitHub - Auiowu/ManifestAutoUpdate | `Auiowu/ManifestAutoUpdate` | 仓库路径 |
| GitHub - SteamAutoCracks/ManifestHub | `SteamAutoCracks/ManifestHub` | 仓库路径 |

程序会自动从这些仓库下载 `.zip` 包或直接读取 GitHub 分支内容，提取 `.manifest` 文件和 `key.vdf` 密钥。

---

## ❓ 常见问题

### 1. 启动时提示 `ttkbootstrap` 未安装？

```bash
pip install ttkbootstrap
```

### 2. 报错“Steam 路径未找到”？

- 确保 Steam 已安装并至少运行过一次。
- 尝试在“设置”中手动填写 Steam 路径（如 `C:\Program Files (x86)\Steam`）。

### 3. 为什么有些游戏处理失败？

可能原因：
- 该游戏在所选清单库中不存在（可以尝试“搜索所有 GitHub 库”模式）。
- 网络问题导致下载失败（尝试配置 GitHub Token 或使用代理）。
- 游戏使用了自定义分支或第三方 DRM（如 Denuvo），单纯清单可能不足以解锁。

### 4. SteamTools 模式下生成的 `.lua` 文件为什么 `setManifestid` 行被注释了？

- 当启用“使用 SteamTools 进行清单更新（仅下载 LUA）”且 **未锁定清单版本** 时，程序默认使用浮动版本，因此注释掉 `setManifestid`，让 SteamTools 自动获取最新清单。
- 若需要固定清单版本，请关闭该选项重新处理。

### 5. 如何卸载已导入的游戏？

- **SteamTools**：删除 `config/stplug-in/<AppID>.lua`，并可选删除 `depotcache` 中对应的 `.manifest`。
- **GreenLuma**：删除 `AppList/<AppID>.txt`，并从 `config/config.vdf` 的 `depots` 节点中移除相关条目（建议手动备份）。

### 6. 程序是否支持 macOS 或 Linux？

GUI 基于 Tkinter，理论上可在支持 Tk 的平台上运行，但解锁工具 SteamTools/GreenLuma 均为 Windows 专用，因此本工具 **实际仅在 Windows 上有意义**。

---

## 📄 开源协议

本项目基于 **MIT License** 开源。  
您可自由使用、修改、分发，但任何衍生作品也 **必须使用相同许可证** 并公开源代码。

---

## 🙏 致谢与联系

- **作者**：pvzcxw  
- **官方 QQ 群**：993782526  
- **Bilibili**：[@菜Games-pvzcxw](https://m.bilibili.com/space/49307545)  

> 本项目完全免费，请勿用于商业用途。如有问题请在 GitHub 仓库提交 Issue 或加入 QQ 群反馈。

---

**Enjoy unlocking! 🎮**
