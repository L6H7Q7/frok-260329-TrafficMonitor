# TrafficMonitor（本机改造版）

> 上游 [zhongyang219/TrafficMonitor](https://github.com/zhongyang219/TrafficMonitor) 的 fork：Windows 平台的网速/CPU/内存监控悬浮窗，可嵌入任务栏，支持换肤和历史流量统计。
> **本文件由 DSH 维护，每次项目告一段落时更新。**

最后更新：2026-11-26

## 现在什么状态：已提交并推送

- 分支：`master`
- 最后提交：`2026-11-26 feat(menu): 移除自动检查更新，改为「重启程序」菜单项`
- 远端：`https://github.com/L6H7Q7/frok-260329-TrafficMonitor.git`（注意仓库名是 `frok`，不是 fork）
- 上一个提交是 `2026-09-27 readme更新`，中间这一轮的改动（11-20 做的）已于 11-26 提交

**这轮改动做了什么**（12 个文件，`+24 / -144` 行）：

| 删掉 | 加上 |
|---|---|
| `CheckUpdate()` / `CheckUpdateInThread()` / `CheckUpdateThreadFunc()` | 菜单项「重启(&R)」（`ID_RESTART_APP`） |
| 启动时自动检查更新的调用 | `OnAppRestart()` 实现 |
| 设置页「启动时检查更新」复选框 + 「立即检查」按钮 | 中英文语言条目 `TXT_RESTART` |
| 右键菜单「检查更新」项 | |
| `m_checking_update` / `IsCheckingForUpdate()` | |

**动机**：不想被上游的自动更新检查打扰（和 DSH 那边「屏蔽版本更新」是同一套思路），同时给自己一个改完配置能立刻重启的入口。

## 技术栈

C++ / Win32 / MFC 风格，Visual Studio 工程（`.sln` 在 `TrafficMonitor\` 子目录）。

## 关键文件

| 路径 | 作用 |
|---|---|
| `TrafficMonitor\` | 主程序源码（`.cpp` / `.h`） |
| `include\` | 第三方头文件 |
| `lib\` | 预编译库 |
| `PluginDemo\` | 插件示例 |
| `OpenHardwareMonitorApi\` | 硬件监控（温度等） |
| `Bin\` | 编译产物 |
| `皮肤制作教程.md` | 换肤文档（中文） |
| `.dsh-backup-20261120-003528\` | 11-20 那次改动的备份，确认无用后可删 |

## 当时的决策 / 踩过的坑

- 这是**别人的项目**，本机是 fork 后自己改。改动要尽量集中在少数文件，方便以后同步上游。
- 上游 README 提到用了 Anti-996 License，二次分发要注意。

## 下次从哪接着做

这轮改动已**彻底完成**（功能移除 + 资源清理）。

**有意保留、不要删的东西**：

| 东西 | 为什么留着 |
|---|---|
| `CUpdateHelper` 类 | 仍被 `TrafficMonitor.cpp` 用来判断更新源（GitHub / Gitee），帮助菜单要靠它决定打开哪个站点 |
| `CPluginUpdateHelper` | 插件更新检查，和「程序更新检查」是两套独立机制 |
| `TXT_UPDATE_SOURCE` | 设置页「更新源」单选按钮还在用 |

要接着做，先 `git status` 确认干净，再谈新功能。

## 清理记录（2026-11-26）

| 提交 | 内容 |
|---|---|
| `0b23095` | 移除自动检查更新功能，新增「重启程序」菜单（14 个文件，+93/−144） |
| `9948e15` | 清除 19 个文件里的死条目：5 个 `IDS_*` 键、`TXT_CHECK_UPDATE`、`TXT_CHECK_NOW`（+6/−155），全项目 0 残留 |

`.dsh-backup-20261120-003528\` 是那轮改动的备份目录，已加入 `.gitignore`，确认无用后可删。

## 相关历史对话

```powershell
node D:\AI\WorkSpace\_会话存档\locate.mjs TrafficMonitor
node D:\AI\WorkSpace\_会话存档\locate.mjs 网速悬浮窗
```
