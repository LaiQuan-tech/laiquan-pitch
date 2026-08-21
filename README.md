# laiquan-pitch

萊乾資訊 LaiQuan — **公司介紹簡報**（22 頁全螢幕互動簡報站）。

- 線上：<https://laiquan-pitch.vercel.app>
- 純靜態站（單一 `index.html`），無建置流程。
- **push 到 `main` → Vercel 自動部署**（Vercel 專案 `laiquan-pitch`，framework=static，原生 GitHub 整合）。

## ⚠️ 三條紅線（改內容前先讀）

**1. 投影片內容文字一律 ≥ 30px。**
擠不下就**刪字**，不要回頭改 `font-size`。CSS 裡的 `@media(max-height:800px)` 只收留白與間距、
不動字級，就是為了守這條。（頁碼、右側圓點、scroll 提示屬 UI 元件，不在此限。）

| 元素 | 最小 | 1920×1080 實際 |
|---|---|---|
| 正文 `.lead` | 30px | 38px |
| 卡片說明 `.cell .d` | 30px | 34px |
| 註腳 `.fine` | 30px | 30.7px |
| 眉標 `.eyebrow` / 客戶名 `.who` / 標籤 `.tags` | 30px | 32–34px |
| 項目標題 `.cell .k` / `.steps .bt` | 34px | 44px |
| 大標 `h2` | 44px | 92px |
| 封面 `h1` | 54px | 128px |

**2. 標題不用色塊。**
眉標是純文字＋字距（不是黑底黃字膠囊）、強調 `<em>` 是細底線（不是黃色螢光塊）、
客戶名 `.who` 是純文字（不是黃底藥丸）。新增元素請沿用這個規則。

**3. 斷行後不留兩字孤行。**
每個 `<br>` 前後至少四個實字。全簡報目前最短的一行是 4 字。改完用下方腳本重驗。

## 內容（22 張）

封面 → 這一年（24／7／12）→ 七種服務 → ①官網與後台 → ②電商交易 → ③營運系統
→ 案例·印刷收稿 → 案例·零售系統 → ④人資系統 → ⑤AI 應用 → 案例·AI 數位人 → 案例·AI 報價
→ ⑥行動 App → ⑦提案簡報 → 技術棧 → 服務過的產業
→ **風林火山 → 疾如風 → 徐如林 → 侵掠如火 → 不動如山** → 聯絡我們

最後五頁是收尾錨點：以風林火山四個字形容 AI，深色底＋巨大單字，
左右交錯排版（`.fs` / `.fs.flip`）。這段是簡報的記憶點，不要拿掉或縮短。

內容依據 `../LaiQuan-服務盤點-2026.md`（掃過 LaiQuan-tech 全部 24 個 repo 的 README、
路由結構與資料庫 migration 整理而成）。

## 對象是客戶，不是投資人

寫文案時注意立場：講客戶得到什麼，不要講我們的商業模式。
例：白標多租戶那頁講的是「系統掛你的招牌」「分店資料互不相通」，
**不是**「一套系統可以賣給很多家公司」——後者是投資人語言。

## 操作

滑鼠捲動 / 空白鍵 / ↑↓ / ←→ / PageUp·PageDown / Home·End 切頁；右側圓點跳頁；左下角頁碼。

## 改完內容後的驗證

本機起靜態伺服器，在 **1920×1080 / 1440×720 / 1366×768 / 1280×800** 各跑一次：

```js
(function(){document.querySelectorAll('.reveal').forEach(e=>e.classList.add('in'));
var r=[...document.querySelectorAll('.slide')].map(s=>{var i=s.querySelector('.inner'),c=getComputedStyle(s);
  return {id:s.id,over:Math.ceil(i.scrollHeight+parseFloat(c.paddingTop)+parseFloat(c.paddingBottom))-innerHeight};});
var min=999;['.lead','.cell .d','.steps .bs','.stats .l','.fine','.eyebrow','.cell .who','.tags span']
  .forEach(q=>document.querySelectorAll(q).forEach(e=>{var v=parseFloat(getComputedStyle(e).fontSize);if(v<min)min=v;}));
var blocks=[];['.eyebrow','em','.cell .who'].forEach(q=>document.querySelectorAll(q).forEach(e=>{
  var bg=getComputedStyle(e).backgroundColor;if(bg!=='rgba(0, 0, 0, 0)')blocks.push(q);}));
return JSON.stringify({minTextPx:min,colorBlockOnTitles:blocks,overflow:r.filter(x=>x.over>0)});})()
```

三個都要是空的／≥30 才算過。斷行檢查另用 `docs/` 無、直接看每個 `<br>` 兩側字數。

## 品牌

奶油底 `#fffbec`／墨黑 `#1a1a1a`／亮黃 `#ffce00`；深色頁 `#15130f`，巨大單字用亮黃。
Baloo 2 + Noto Sans TC 極粗圓體、⚡ 閃電識別、3px 黑框＋硬陰影。

## 未收錄（刻意）

- **客戶評價** — 官網 `lqtech-landing/content/data.ts` 那三則與實際客戶對不上，且「評價同意」
  仍列在 `DEPLOYMENT.md` §9 的上線前待辦，判定為示意稿。
- **電話** — `site.ts` 的 `02-1234-5678` 是佔位號碼。
- **費率表** — 這版定位是公司介紹，報價留給個案提案簡報。
