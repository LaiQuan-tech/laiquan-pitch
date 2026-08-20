# laiquan-pitch

萊乾資訊 LaiQuan — **公司介紹簡報**（Apple 風全螢幕 pitch deck，沿用 `LaiQuan-tech/nina-pitch`、`LaiQuan-tech/aster-pitch` 的版型）。

- 線上：<https://laiquan-pitch.vercel.app>
- 純靜態站（單一 `index.html`），無建置流程。
- **push 到 `main` → Vercel 自動部署**（Vercel 專案 `laiquan-pitch`，framework=static，原生 GitHub 整合）。

## 內容（12 張投影片）

封面 → 我們是誰 → 數字 → 三大服務 → AI 系統（差異化）→ 作品案例 → 案例亮點一·AI 收稿（美強光）→ 案例亮點二·公司數位化（亞斯特）→ 合作流程 → 技術與資安 → 參考費率 → 聯絡我們。

## 內容來源

全部取自 `LaiQuan-tech/lqtech-landing`（官網 laiquan.co）：

| 投影片 | 來源 |
|---|---|
| 封面標語、數字 50+/98%/12 年 | `components/Hero.tsx` |
| 三大服務、作品六件、合作流程五步、FAQ 文案 | `content/data.ts` |
| 公司名稱、Email、服務區域、技術棧 | `content/site.ts` |
| 參考費率表 | `lib/pricing.ts` → `DEFAULT_RATE_CARD` |
| 案例亮點一（AI 收稿） | `LaiQuan-tech/nina-pitch` |
| 案例亮點二（公司數位化） | `LaiQuan-tech/aster-pitch` |

⚠️ **官網的 `reviews`（客戶評價）刻意未收錄** —— 那三則與 `works` 的實際客戶對不上，且 `DEPLOYMENT.md` §9 把「評價同意」列為上線前待辦，判定為示意稿。要放客戶評價請先取得當事人同意再補上。

⚠️ **官網的 `site.phone`（02-1234-5678）為佔位號碼，未收錄。** 要在簡報上放電話，請改成真實號碼再加。

## 品牌

色彩與字體取自官網 <https://laiquan.co>：奶油底 `#fffbec` ＋ 墨黑 `#1a1a1a` ＋ 亮黃 `#ffce00`，Baloo 2 + Noto Sans TC 極粗圓體、⚡ 閃電識別、黑色膠囊按鈕與硬陰影。封面／結尾的大閃電形狀直接沿用官網 Hero 的 `clip-path`。

## 版面注意

`#s6`（作品，6 張卡）與 `#s11`（費率，7 列）是最密的兩頁，已針對筆電高度加 `@media(min-width:900px) and (max-height:900px)` 的壓縮規則。**改動這兩頁的內容後，務必在 1280×800 與 1920×1080 各確認一次仍單屏容納。**

## 操作

滑鼠捲動 / 空白鍵 / ↑↓ / PageUp·PageDown / Home·End 切頁；右側圓點可直接跳頁。
