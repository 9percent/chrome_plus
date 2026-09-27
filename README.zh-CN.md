# Chrome++ Next
[![LICENSE](https://img.shields.io/badge/License-GPL--3.0--only-blue.svg?style=for-the-badge&logo=github "LICENSE")](LICENSE) [![LAST COMMIT](https://img.shields.io/github/last-commit/9percent/chrome_plus?color=blue&logo=github&style=for-the-badge "LAST COMMIT")](https://github.com/9percent/chrome_plus/commits/main) [![STARS](https://img.shields.io/github/stars/9percent/chrome_plus?color=brightgreen&logo=github&style=for-the-badge "STARS")](https://github.com/9percent/chrome_plus/stargazers) ![SIZES](https://img.shields.io/github/languages/code-size/9percent/chrome_plus?color=brightgreen&logo=github&style=for-the-badge "SIZES")

简体中文 | [English](README.md)

Chrome++ Next 是一个 `version.dll` 注入项目，会与 `chrome.exe` 一同加载，在浏览器启动时增强标签页、快捷键、便携化、命令行参数以及策略相关行为。

## 仓库恢复说明（2026-09-28）
原 `Bush2021/chrome_plus` 仓库已无法访问。本次恢复保留原提交 SHA、作者信息、致谢与许可证。主线基准为 `240777ff667f54baa2899291576f935a88b6b05d`，来自 [nobug-project](https://github.com/nobug-project/chrome_plus)，并由 [ikly360](https://github.com/ikly360/chrome_plus) 和 [srhse5rh](https://github.com/srhse5rh/chrome_plus) 交叉核对。新增的恢复提交只更新仓库及依赖链接和这些说明。

其它公开历史保存在 `recovered/<owner>/<branch>` 分支下（必要时增加仓库名），来源标签隔离在 `recovered/<owner>/...` 下；已核实的原始标签也保留原名，不覆盖有冲突的 fork 标签。这些是历史快照，不代表已合并增强功能：例如 `recovered/benzBrake/main` 比基准多八个 fork 自有提交。历史分支保留原依赖地址；需要已修复的递归克隆时请使用 `main`。

[mini_gzip 恢复仓库](https://github.com/9percent/mini_gzip) 的 `master` 保持为 `2eee7df50ee8bda75070b5c40fe1e7022116503e`，来源为 [libsgh](https://github.com/libsgh/mini_gzip)，并经 [road0001-Forks-1](https://github.com/road0001-Forks-1/mini_gzip) 核对；相关的 [shuax](https://github.com/shuax/mini_gzip) 历史单独保留。两个子模块的 gitlink 均未修改：mini_gzip 使用上述精确提交，[Microsoft Detours](https://github.com/microsoft/Detours) 仍为 `d644ce94e8c7f7f5a31591577c78134ea3ac1fae`。

```sh
git clone --recurse-submodules https://github.com/9percent/chrome_plus.git
```

已有检出更新到恢复后的主线后，请同步缓存的子模块地址：

```sh
git submodule sync --recursive
git submodule update --init --recursive
```

恢复范围是可达的公开 Git 历史，不包括已删除的 Issues、PR 讨论、Actions 记录及 Release 二进制附件。`1.18.2` 标签来自 [smzhzy26](https://github.com/smzhzy26/chrome_plus)，指向原版本提交 `232a2230d91496d40dcfafbcf40f11040ca36c91`；恢复标签不代表恢复了 Release 附件。历史安装器、setdll 链接及发布流程仍保留，可能依赖已不可用的上游服务。

## 项目简介
- 面向 Windows 下的 Google Chrome。
- 通过将 `version.dll` 放在 `chrome.exe` 同目录的方式工作。
- 重点是对浏览器原生行为做增强，而不是做额外的界面壳层或扩展。
- 优先处理扩展难以实现、或外部方案无法很好解决的能力。

## 支持策略
- 只接受最新版稳定版 Google Chrome 的问题反馈。
- 其它 Chromium 分支浏览器能用则用，但不属于正式支持目标。
- 具体反馈要求以 GitHub Issues 页面和表单为准。

## 获取
- [Releases](https://github.com/9percent/chrome_plus/releases)（历史 Release 二进制附件未恢复）。

## 安装
- 请确保将 `version.dll` 放在 `chrome.exe` 同一目录。
- 推荐使用 [Chrome 离线安装包](https://github.com/Bush2021/chrome_installer)，解压两次后直接使用解包得到的 Chrome 程序文件。
- 本项目面向便携式 Chrome 部署场景。如果系统中保留了 updater 组件或其它 Chrome 遗留项，由此产生的环境问题需要自行处理。
- 如果 `version.dll` 没有被正确加载，可以尝试 [setdll](https://github.com/Bush2021/setdll/)。

## 功能概览
### 标签页与书签行为
- 双击关闭标签页。
- 右键关闭标签页，按住 `Shift` 保留原始菜单。
- 保留最后一个标签页，避免关闭整个浏览器窗口。
- 鼠标悬停标签栏时滚轮切换标签页。
- 按住右键时滚轮切换标签页。
- 鼠标在标签页上停留后自动激活该标签页。
- 将地址栏输入内容或书签在新标签页中打开。
- 通过 `new_tab_disable` 和 `new_tab_disable_name` 控制新标签页判定。

### 快捷键与按键映射
- 配置老板键以隐藏和恢复 Chrome 窗口，并随之静音与恢复静音。
- 配置网页翻译快捷键。
- 通过 `keymapping` 将按键映射到其它快捷键或 Chrome 命令 ID。

### 便携化与启动行为
- 通过 `data_dir` 和 `cache_dir` 控制便携化数据路径。
- 通过 `command_line` 追加 Chromium 启动参数。
- 通过 `launch_on_startup` 和 `launch_on_exit` 在启动或退出时执行程序或命令。

### 浏览器环境控制
- 通过 `ignore_policies` 忽略企业策略。
- 仅在 Chrome++ 自身导致启动崩溃时再考虑启用 `win32k` 兜底选项。
- 通过 `suppress_false_upgrade_notification` 抑制便携版上错误的“已过期”升级提示。
- `show_password` 等其它公开选项仍以 [`src/chrome++.ini`](src/chrome++.ini) 为准。

## 配置说明
- 完整公开配置请参见 [`src/chrome++.ini`](src/chrome++.ini)。

## 许可证
- 1.5.4 及以前版本使用 MIT 许可证，版权所有者为 [Shuax](https://github.com/shuax/)。
- 1.5.5 到 1.5.9 版本使用 MIT 许可证，由本仓库贡献者基于 Shuax 版本进行修改。
- 1.6.0 及以后版本使用 [GPL-3.0](LICENSE)。

## 致谢
- 所有 [贡献者](https://github.com/Bush2021/chrome_plus/graphs/contributors)
- 原作者 [Shuax](https://github.com/shuax/)
- 1.5.5 修改代码 [提供者](https://forum.ru-board.com/topic.cgi?forum=5&topic=51073&start=620&limit=1&m=1#1)
- [面向大海](https://github.com/mxdh/)
- [Ho Cheung](https://github.com/gz83/)
