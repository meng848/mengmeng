# AGENTS.md

## 项目规则 (user-mandated, always apply)
- **命名前缀**: 所有新的 CSS 类名、id 名、JS 变量名必须以 `mm_` 开头（如 `mm_card`、`mm_hero`、`mm_btn`）。既有页面（`index.html`、`11-1.html`–`14-1.html` 等）在本规则生效前使用的是 `meng_` 前缀，不要为套规则而批量重命名旧文件；新建或重构时一律使用 `mm_`。
- **页面头部注释**: 每个 HTML 页面的 `<head>` 内、`<meta charset>` 之后必须紧跟一条 HTML 注释，格式固定为：
  ```html
  <!-- 姓名：孟梦，日期：2026-10-22，功能名称：页面功能简述 -->
  ```
  日期以页面创建/主要修改日期为准；功能名称用一句话说清该页面做什么。
- **技术栈约束**: 全部使用**原生 HTML + CSS + JavaScript**（ES6+ 语法可），**不使用任何第三方库/框架**，**不使用 CDN**（包括 Font Awesome、Bootstrap、Lodash、Vue、React 等）。内联 `<style>` 和 `<script>` 即可，不引外部文件。
- **图标统一用 iconfont**: 所有页面需要图标时，从本地 `font/` 目录引用 iconfont（`font/font_5244875_7pxofbmupmt/iconfont.css` + `iconfont.ttf/woff/woff2`），用 `<i class="iconfont icon-xxx"></i>` 或 `<svg><use xlink:href="#icon-xxx"></use></svg>`，不再新建 Font Awesome / Lucide 等第三方图标目录。
- **数据请求**: 需从服务器获取数据时，统一使用原生 `fetch()` API，不要用 `XMLHttpRequest` 或 jQuery `$.ajax`。
- **提示词留痕**: 每次执行用户提示词**之前**，先以**追加**方式写入 `meng_prompt.md`（绝不覆盖/清空已有内容），每条记录包含三部分：时间（格式 `yyyy-mm-dd-hh-mm`）、使用的模型、提示词原文。格式见 `meng_prompt.md` 现有条目。
- **新页面必须入首页**: 每次新建 HTML 文件后，必须在 `index.html` 的作品网格中加一张 `<article class="card">` 超链接卡片（中文文件名的 href 要百分号编码），并把计数徽章 `共 N 个页面` +1。此规则适用于所有新 HTML，即使提示词没要求。

## What this is
Flat static-site repo: Chinese-language《高级网页设计》class exercises (student 孟梦). Plain HTML with inline `<style>` only — **no build, no package.json, no tests, no framework, no git repo**. Don't add tooling unless asked.

## Entry point
- `index.html` — navigation hub with 15 `<article class="card">` links and a count badge `共 15 个页面` (~line 229). The assignment prompt that generated it is embedded in a `<blockquote>` at the bottom; preserve it.
- **Unlisted pages**: `10-1 animation.html`–`10-4.html` (animation / media queries) and `meng.html` (standalone "美食节" page, referenced by nothing). When adding a page: add a card AND bump the count.

## Conventions that are easy to get wrong
- Filenames contain **Chinese characters and spaces**: `3-1 form.html`, `5-1 层叠与继承.html`. All `index.html` hrefs are percent-encoded (`3-1%20form.html`, `5-1%20层叠与继承.html`) — do the same for new links or they break. Never rename existing files (e.g. `6-1 fiex.html` is a typo but is linked under that name).
- Naming pattern for new exercise pages: `chapter-week[ topic].html` (e.g. `7-1 上图下文.html`).
- Every page is UTF-8 and declares `<meta charset="UTF-8">` — keep both when creating files.
- The PowerShell console here is GBK: Chinese names/content render as mojibake (`5-1 ???????.html`, `�����̳�`). On-disk names are correct Chinese — **do not rename files to the garbled text**. Read/verify content via UTF-8 decode or the Read tool.
- No CDN allowed (from the embedded prompt: 使用原生代码，不使用cdn): inline CSS/JS only, no external stylesheets/scripts. Fonts fall back to local `"Microsoft YaHei", "PingFang SC"`.
- Shared assets: `img/1.jpg`–`img/26.png`, referenced as either `img/x.jpg` or `./img/x.jpg` (both styles exist; both work). `css.css` is a tiny demo stylesheet used only by `5-1 层叠与继承.html` — styles otherwise live inline per page.

## Verifying
No lint/test/typecheck exists. Check changes by opening the page in a browser (`start index.html`); the main failure mode is broken links from un-encoded filenames.
