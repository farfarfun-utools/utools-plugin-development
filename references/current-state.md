# 当前仓库盘点（2026-11-02）

以下是创建 skill 时的状态，不是永久规范。开始任务时重新读取对应仓库。

| 插件 | 实现 | 窗口高度 | Release workflow | 截图 workflow | packages 页面 |
| --- | --- | ---: | :---: | :---: | :---: |
| FunCalc | Vue/Vite | 620 | 有 | 无，CI 有 Playwright 截图 | 有 |
| FunCalendar | Vue/Vite | 620 | 有 | 有 | 有 |
| FunChat | Vue/Vite | 660 | 有 | 有 | 有 |
| FunDoc | Vue/Vite | 600 | 有 | 有 | 有 |
| FunImage | 原生 HTML/JS | 720 | 无，CI 可打 UPXS | 无 | 无 |
| FunLink | Vue/Vite | 558 | 有 | 有 | 有 |
| FunOTP | Vue/Vite | 558 | 有 | 有 | 有 |
| FunQR | Vue/Vite | 660 | 有 | 有 | 有 |
| FunVideo | 原生 HTML/JS | 720 | 无，CI 可打 UPXS | 无 | 无 |

9 个仓库的 `utools/logo.png` 都是 256×256 PNG；`package.json` 与 `utools/plugin.json` 当前版本一致。FunImage/FunVideo 尚未进入 `utools-plugins` 和组织 profile 的插件总览，也未进入 `farfarfun/packages`；这是待补的现状，不表示它们不是插件。`utools-shots` 目前维护 FunChat、FunDoc、FunLink、FunOTP 的共享截图脚本。`utools-plugins` 是索引仓库，组织 `.github` 管主页与共享截图工作流，`farfarfun/packages` 管产品页与 Release 下载索引。
