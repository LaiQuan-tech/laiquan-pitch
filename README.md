# laiquan-pitch

萊乾資訊 LaiQuan — **公司介紹簡報**（18 頁全螢幕互動簡報站）。

- 線上：<https://laiquan-pitch.vercel.app>
- 純靜態站（單一 `index.html`），無建置流程。
- **push 到 `main` → Vercel 自動部署**（Vercel 專案 `laiquan-pitch`，framework=static，原生 GitHub 整合）。

## 這是簡報，不是文件

第一版是照 pitch deck 排的（正文 14–17px、資訊密度高），適合「讀」不適合在台上「講」。
現在這版是**站在台上用的規格**：每頁只講一件事、最多 4 個並列項目，字級如下。

### ⚠️ 排版紅線

| 元素 | 最小字級 | 1920×1080 實際 |
|---|---|---|
| **正文**（`.lead` / `.cell .d` / `.steps .bs` / `.stats .l`）| **30px** | 33.6–40px |
| 項目標題（`.cell .k` / `.steps .bt`）| 34px | 44px |
| 大標 `h2` | 44px | 94px |
| 封面 `h1` | 54px | 132px |
| 註腳 `.fine` | 24px | 28px |

**內容擠不下時，刪字，不要改字級。** CSS 裡有一段 `@media(max-height:800px)` 只收留白與間距、
不動 `font-size`，就是為了守住這條線。改完內容請重跑下方驗證。

## 內容（18 張）

封面 → 這一年（24 專案／7 服務／12 產業）→ 七種服務 → ①官網+CMS → ②電商交易 → ③營運系統
→ 案例·印刷收稿 → 案例·零售 POS → ④人資 SaaS → ⑤AI 四種用法 → 案例·AI 數位人 → 案例·AI 自動報價
→ ⑥行動 App → ⑦提案簡報 → 技術棧 → 服務過的產業 → 為什麼找萊乾 → 聯絡我們

內容依據 `../LaiQuan-服務盤點-2026.md`（掃過 LaiQuan-tech 全部 24 個 repo 的 README、
路由結構與資料庫 migration 整理而成）。

## 操作

滑鼠捲動 / 空白鍵 / ↑↓ / ←→ / PageUp·PageDown / Home·End 切頁；右側圓點跳頁；左下角顯示頁碼。

## 改完內容後的驗證

本機起一個靜態伺服器，在 **1920×1080 / 1440×720 / 1366×768 / 1280×800** 各跑一次，
確認「無溢出」且「最小正文 ≥ 30px」：

```js
(function(){document.querySelectorAll('.reveal').forEach(e=>e.classList.add('in'));
var r=[...document.querySelectorAll('.slide')].map(s=>{var i=s.querySelector('.inner'),c=getComputedStyle(s);
  return {id:s.id,over:Math.ceil(i.scrollHeight+parseFloat(c.paddingTop)+parseFloat(c.paddingBottom))-innerHeight};});
var min=999;['.lead','.cell .d','.steps .bs','.stats .l'].forEach(sel=>
  document.querySelectorAll(sel).forEach(e=>{var v=parseFloat(getComputedStyle(e).fontSize);if(v<min)min=v;}));
return JSON.stringify({minBodyPx:min,overflow:r.filter(x=>x.over>0)});})()
```

## 品牌

奶油底 `#fffbec`／墨黑 `#1a1a1a`／亮黃 `#ffce00`，深色頁用 `#1a1a1a` 反白。
Baloo 2 + Noto Sans TC 極粗圓體、⚡ 閃電識別、3px 黑框＋硬陰影。

## 未收錄（刻意）

- **客戶評價** — 官網 `lqtech-landing/content/data.ts` 那三則與實際客戶對不上，且「評價同意」
  仍列在 `DEPLOYMENT.md` §9 的上線前待辦，判定為示意稿。
- **電話** — `site.ts` 的 `02-1234-5678` 是佔位號碼。
- **費率表** — 這版定位是公司介紹（講能力），報價留給個案提案簡報。
