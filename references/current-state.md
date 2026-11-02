# 当前仓库盘点（2026-11-02）

以下是创建 skill 时的状态，不是永久规范。开始任务时重新读取对应仓库。

| 插件 | 实现 | 窗口高度 | Release workflow | 截图 workflow | packages 页面 |
| --- | --- | ---: | :---: | :---: | :---: |
| FunCalc | Vue/Vite | 620 | 有 | 无，CI 有 Playwright 截图 | 有 |
| FunCalendar | Vue/Vite | 620 | 有 | 有 | 有 |
| FunChat | Vue/Vite | 660 | 有 | 有 | 有 |
| FunDoc | Vue/Vite | 600 | 有 | 有 | 有 |
| FunImage | Vite/原生 JS | 720 | 有 | 有 | 有 |
| FunLink | Vue/Vite | 558 | 有 | 有 | 有 |
| FunOTP | Vue/Vite | 558 | 有 | 有 | 有 |
| FunQR | Vue/Vite | 660 | 有 | 有 | 有 |
| FunVideo | Vite/原生 JS | 720 | 有 | 有 | 有 |

9 个仓库的 `utools/logo.png` 都是 256×256 PNG，`plugin.json#main` 都指向 `dist/index.html`；`package.json` 与 `utools/plugin.json` 当前版本一致。9 个插件已进入 `utools-plugins`、组织 profile 和 `farfarfun/packages`。`utools-shots` 维护部分 Vue 插件的共享截图脚本，FunImage/FunVideo 使用组织 `.github` 的截图脚本。`utools-plugins` 是索引仓库，组织 `.github` 管主页与共享截图工作流，`farfarfun/packages` 管产品页与 Release 下载索引。
