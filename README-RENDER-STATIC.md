# Spec/Plan Bulk Downloader — Render Static Site

这是无需 Blueprint 的 **静态站点**版本。用于在 Render 里通过 **Create → Static Site** 直接部署。

## 部署步骤（Render 仪表盘）
1. 把本仓库推到 GitHub（根目录就是这两个文件：`index.html`、`README-RENDER-STATIC.md`）。
2. Render → New → **Static Site**
3. 选择仓库与分支
4. **Build Command**：留空
5. **Publish Directory**：`.`
6. 创建后等待发布完成，打开域名即可。

## 可选：服务端打包（推荐，绕过 CORS）
- 如果你已部署“打包代理”（Express/Flask 版的 `/zip` 接口）：
  - 访问页面时在 URL 后加：`?zipapi=https://你的代理域名/zip`
  - 页面右上角徽标会显示“服务端打包模式”。

## 使用方法
- 在文本框粘贴从 Excel 复制的车架号列（支持换行/逗号/Tab 分隔；自动去重并忽略表头 “Chassis / Chassis Number”）。
- 页面会从 Firebase RTDB 的 `spec_plan` 读取对应的 Plan/Spec 链接。
- 可选择“打包 ZIP（全部）/只 Plan/只 Spec”。
- 如目标链接禁止跨域，前端打包会生成 `failed_links.txt` 和 `open_failed_links.html` 以便手动下载。

## 配置说明
- Firebase 配置已内嵌到 `index.html`（与你现有网站一致）。
- 如需更换代理地址，可在访问 URL 末尾加 `?zipapi=...` 动态覆盖；也可直接在 `index.html` 顶部 `window.ZIP_API_URL` 写死。

