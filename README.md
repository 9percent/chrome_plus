# Chrome++ Next
[![LICENSE](https://img.shields.io/badge/License-GPL--3.0--only-blue.svg?style=for-the-badge&logo=github "LICENSE")](LICENSE) [![LAST COMMIT](https://img.shields.io/github/last-commit/9percent/chrome_plus?color=blue&logo=github&style=for-the-badge "LAST COMMIT")](https://github.com/9percent/chrome_plus/commits/main) [![STARS](https://img.shields.io/github/stars/9percent/chrome_plus?color=brightgreen&logo=github&style=for-the-badge "STARS")](https://github.com/9percent/chrome_plus/stargazers) ![SIZES](https://img.shields.io/github/languages/code-size/9percent/chrome_plus?color=brightgreen&logo=github&style=for-the-badge "SIZES")

English | [简体中文](README.zh-CN.md)

Chrome++ Next is a `version.dll` injection project for Google Chrome. It is loaded alongside `chrome.exe` and augments browser behavior at startup with tab, hotkey, portable, command-line, and policy-related features.

## Repository Recovery (2026-09-28)
The original `Bush2021/chrome_plus` repository is no longer accessible. This recovery preserves its commit identities, authorship, credits, and licenses. The recovered mainline baseline is `240777ff667f54baa2899291576f935a88b6b05d`, obtained from [nobug-project](https://github.com/nobug-project/chrome_plus) and corroborated by [ikly360](https://github.com/ikly360/chrome_plus) and [srhse5rh](https://github.com/srhse5rh/chrome_plus). The new recovery commit only updates repository/dependency links and these notes.

Additional public histories are preserved under `recovered/<owner>/<branch>` (with a repository component where needed), and source tags under `recovered/<owner>/...`. Verified original tag names are also retained without overwriting conflicting fork tags. These are historical snapshots, not merged enhancements: notably, `recovered/benzBrake/main` contains eight fork-only commits beyond the baseline. Historical branches retain their original dependency URLs; use `main` for the repaired recursive clone.

The [mini_gzip recovery](https://github.com/9percent/mini_gzip) preserves `master` at `2eee7df50ee8bda75070b5c40fe1e7022116503e`, recovered from [libsgh](https://github.com/libsgh/mini_gzip) and corroborated by [road0001-Forks-1](https://github.com/road0001-Forks-1/mini_gzip), with related [shuax](https://github.com/shuax/mini_gzip) history retained separately. Both gitlinks are unchanged: mini_gzip uses that exact commit, and [Microsoft Detours](https://github.com/microsoft/Detours) remains at `d644ce94e8c7f7f5a31591577c78134ea3ac1fae`.

```sh
git clone --recurse-submodules https://github.com/9percent/chrome_plus.git
```

After updating an existing checkout to the recovered mainline, refresh its cached submodule URLs:

```sh
git submodule sync --recursive
git submodule update --init --recursive
```

Recovery covers reachable public Git history, not deleted issues, pull-request discussions, Actions runs, or release binaries. The `1.18.2` tag was recovered from [smzhzy26](https://github.com/smzhzy26/chrome_plus) at the original version commit `232a2230d91496d40dcfafbcf40f11040ca36c91`; restoring a tag does not restore its release assets. Historical installer/setdll links and release automation are retained but may depend on unavailable upstream services.

## Overview
- Targets Google Chrome on Windows.
- Works by placing `version.dll` next to `chrome.exe`.
- Focuses on practical browser behavior changes instead of UI wrappers or extensions.
- Prioritizes capabilities that browser extensions cannot implement well, or that external tools do not solve cleanly.

## Support Policy
- Bug reports are accepted only for the latest stable Google Chrome.
- Other Chromium-based browsers may work, but they are not supported targets.
- Reporting requirements are enforced in the GitHub Issues templates.

## Download
- [Releases](https://github.com/9percent/chrome_plus/releases) (historical release binaries were not recovered).

## Installation
- Put `version.dll` in the same directory as `chrome.exe`.
- The recommended installation method is to use the [Chrome offline installer package](https://github.com/Bush2021/chrome_installer), extract it twice, and use the unpacked Chrome program files directly.
- The project is intended for portable Chrome deployments. If you keep updater components or other Chrome remnants on the system, you are responsible for the resulting environment-specific behavior.
- If `version.dll` is not loaded correctly, you can try [setdll](https://github.com/Bush2021/setdll/).

## Capability Overview
### Tab and bookmark behavior
- Double-click to close tabs.
- Right-click to close tabs, with `Shift` preserving the original menu.
- Keep the last tab from closing the browser window.
- Switch tabs with the mouse wheel over the tab strip.
- Switch tabs with the mouse wheel while holding the right mouse button.
- Activate a tab by resting the cursor on it.
- Open omnibox input or bookmarks in a new tab.
- Control new-tab detection through `new_tab_disable` and `new_tab_disable_name`.

### Hotkeys and input remapping
- Configure a boss key to hide and restore Chrome windows, and mute or restore audio along with those actions.
- Configure a translate hotkey.
- Remap hotkeys to other key combinations or Chrome command IDs through `keymapping`.

### Portable deployment and startup behavior
- Override `data_dir` and `cache_dir` for portable use.
- Append Chromium switches through `command_line`.
- Run commands or programs with `launch_on_startup` and `launch_on_exit`.

### Browser environment controls
- Ignore enterprise policies with `ignore_policies`.
- Enable the `win32k` fallback only when Chrome++ itself causes startup crashes.
- Suppress Chrome's false "out of date" upgrade notification on portable installs with `suppress_false_upgrade_notification`.
- Additional public options such as `show_password` remain documented in [`src/chrome++.ini`](src/chrome++.ini).

## Configuration Reference
- See [`src/chrome++.ini`](src/chrome++.ini) for the full public configuration surface.

## License
- Versions 1.5.4 and earlier are licensed under MIT, with all rights reserved by [Shuax](https://github.com/shuax/).
- Versions 1.5.5 through 1.5.9 are licensed under MIT, with modifications by contributors in this repository based on Shuax's version.
- Versions 1.6.0 and later are licensed under [GPL-3.0](LICENSE).

## Thanks
- All [contributors](https://github.com/Bush2021/chrome_plus/graphs/contributors)
- Original author [Shuax](https://github.com/shuax/)
- Revision code [provider](https://forum.ru-board.com/topic.cgi?forum=5&topic=51073&start=620&limit=1&m=1#1) for version 1.5.5
- [面向大海](https://github.com/mxdh/)
- [Ho Cheung](https://github.com/gz83/)
