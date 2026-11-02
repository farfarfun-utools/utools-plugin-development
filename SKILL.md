---
name: utools-plugin-development
description: 开发或发布 farfarfun-utools 组织的 uTools 插件时，检查插件实现、名称图标、截图、GitHub Release、组织索引和 farfarfun/packages 的联动。适用于新插件及已有插件变更。
---

# farfarfun-utools 插件开发规范

用于 `farfarfun-utools` 的插件开发、改名和发布。先读目标仓库与工作区的 `AGENTS.md`、`README.md`、`utools/plugin.json`、CI/Release 工作流，再按本次变更选择下面的联动项。不要把某个插件的具体技术方案强加给其他插件；[当前仓库状态](references/current-state.md)只是盘点，实施前重新核对。

## 工作区与实现

- 插件仓库放在 `/home/bingtao/workspace/github/farfarfun-utools/<仓库名>`；新建或克隆前检查同名目录及远端。`.local-backups/` 不是开发目录。共享打包工具在相邻的 `farfarfun-action/utools-devtools`，不要重新克隆到本组织。
- 一插件一仓库，通常命名 `utools-fun<功能>`；对用户使用稳定的中文显示名及 `FunX` 英文名。仓库名、显示名、uTools 搜索词各有用途，改名时分别核对。
- 本地优先，核心操作尽量接入 uTools 主搜索框。`utools/plugin.json` 的 `features[].code`、`cmds`、文件/选中文字入口应与实际 `onPluginEnter` 路由一致；动态功能另检查 `setFeature`/`removeFeature` 的生命周期。
- `utools/` 是插件根目录：`plugin.json` 引用的 `main`、`logo`、可选 `preload` 和功能图标必须真实存在。需要宿主/Node 能力时通过 preload 暴露有限接口，在边界校验文件、URL 和外部数据。UI 依现有项目选 Vue 3/TypeScript/Vite 或原生 HTML/CSS/JS；不要为统一技术栈重写原生插件。
- 根据数据性质选择存储。`dbStorage` 参与 uTools 同步，不能把它称为“仅本机”；持久化格式变更要保留迁移与失败保护，避免空数据覆盖旧数据。涉及密钥、备份、外部服务时，在界面和 README 中写清同步、明文与联网行为。
- 调整 UI 时检查常用 uTools 窗口、窄窗口、浅色/深色、键盘与焦点。`pluginSetting.height` 是实际窗口高度，不存在全组织统一高度；截图视口与该值一致，默认内容不应无意溢出。

## 名称、图标与尺寸

- 新插件先在 `farfarfun/.github/brand/gen_logos.py` 增加主体，再由品牌生成流程产出素材；不要直接改生成的 `brand/svg/`、`brand/png/`、`brand/favicon/`。品牌规范见该仓库的 `brand/README.md`。
- `utools/logo.png` 使用 `brand/png/mark/<插件名>-256.png`：透明底、256×256 PNG。`plugin.json#logo` 指向它；额外功能图标按需配置并放在 `utools/`。若界面页眉、favicon、`public/logo.png` 或 README 引用同一品牌，也一并核对。
- 组织索引使用 `brand/png/mark/<插件名>-64.png`，即 64×64 PNG。品牌母版为 1024×1024；不要把 64 px 索引图拿来作插件的 256 px 图标。
- 窗口高度在 `plugin.json#pluginSetting.height` 按功能确定；当前项目为 558–720 CSS px，不能当成平台强制范围。截图通常以 800 CSS px 宽和实际窗口高度拍摄，并检查约 375 CSS px 的窄窗口；缩放倍率及最终 PNG 尺寸以项目截图脚本为准。`packages` 页面截图只认 PNG，没有统一宽高要求。

## 变更联动

| 变更 | 必须核对的地方 |
| --- | --- |
| 新插件 | 仓库与 README、品牌图、`utools/plugin.json`、入口实现、测试/CI、截图、身份配置与发布链路、两个组织索引、`packages` 清单及页面 |
| 显示名/功能/唤起词变化 | `pluginName`、`description`、`features`、入口路由、界面文字、README、截图文案、组织索引、`packages` 的 `app` 与页面文案 |
| 图标或界面变化 | 品牌源及导出图、`utools/` 图标、界面与 README 引用、截图脚本/PNG、`packages` 页面截图链接与说明 |
| 存储/联网变化 | 数据迁移与恢复测试、权限与校验、README 隐私说明、组织索引“数据在哪”、包页相关文案 |
| 版本/正式发布 | `package.json` 与 `plugin.json` 版本、锁文件（依仓库工具）、`vX.Y.Z` tag、CI/Release、UPXS 文件名、`SHA256SUMS`、Release 说明及页面下载状态 |

按变化核对即可；纯内部改动不必重做品牌、截图或包页。新增插件和首次公开发布须完成完整链路，不能以已有仓库尚缺某项为理由省略。

## 截图、索引与包页

- 将实际界面 PNG 放在插件仓库 `docs/screenshots/`，用可复现的演示数据生成；不要含真实密钥、API Key 或私人资料。视觉变更后更新受影响截图和 README 引用。现有 Vue 插件多用 `scripts/screenshots.mjs` 与共享截图工作流；可复用 `utools-shots` 的既有脚本，原生插件按自己的页面制作真实截图。
- 新增、删除、改名或调整插件职责时，同步 `farfarfun-utools/utools-plugins/README.md` 索引表和 `farfarfun-utools/.github/profile/README.md` 插件总览。检查显示名、唤起方式、数据位置、品牌 64 px 图 URL、产品页链接；这两个表当前仍漏列 FunImage/FunVideo，不能把它们当作完整清单。
- 在 `farfarfun/packages/packages.toml` 添加 `[[source]]`，`repo = "farfarfun-utools/<仓库名>"`、`keep = 3`、`[source.utools]` 的 `app` 和英文 `desc`。`app` 对应 uTools 显示名；仅在确实上架插件市场时设置 `store = true`。uTools 插件不进入 APT/Homebrew。
- 在 `farfarfun/packages/site/pages/<仓库名>.toml` 写中英名称、标语、简介、功能点、安装说明，以及指向插件仓库 PNG 的 `[[shots]]`（含中英 `alt`）。页面文件不是站点展示的技术前提，但组织现有 7 个包页都维护了它；新插件按这条产品展示约定补齐。字段和自检以 `farfarfun/packages/docs/package-spec.md` 为准。
- 包站点只索引正式 GitHub Release 的附件，不复制插件源码，也不替插件打包。首次接入和发版后在 `packages` 工作流中检查页面、截图和 `.upxs` 下载；站点定时扫描新 Release，需立刻刷新可手动触发其 `build.yml`。

## CI 与发布

- `identity.json` 只存官方 `pluginId`；`mid`、`uid`、`cellphone` 从组织 Secrets `UTOOLS_MID`、`UTOOLS_UID`、`UTOOLS_CELLPHONE` 注入。不要编造 ID、提交身份私密字段或把普通 ZIP 改名为 `.upxs`。新仓库还需确认组织 Secrets 对它开放。
- PR 的 CI 检查实际项目的语法/类型/测试、构建产物及清单资源；有浏览器截图流程时检查截图任务。正式发布验证版本与 tag 一致，调用固定版本的 `farfarfun-action/utools-devtools` 打包 `<仓库名>-<版本>.upxs`，生成 `SHA256SUMS`，发布非草稿、非预发布的 GitHub Release。构建、测试和打包遵守当前工作区 `AGENTS.md` 的执行位置要求。
- 检查 Release 附件、校验和、README 下载说明及 `packages` 页面是否一致。uTools 的实机安装、文件选择、剪贴板和宿主扩展等能力，不能仅靠浏览器或包站 CI 证明；若未实机验收，要明确记录。
