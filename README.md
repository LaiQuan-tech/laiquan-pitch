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

**2. 標題不用色塊，也不畫線。**
眉標是純文字＋字距（不是黑底黃字膠囊）、客戶名 `.who` 是純文字（不是黃底藥丸）、
強調 `<em>` **只換顏色**（`#8a6d00`；深色頁換亮黃）。

⚠️ `<em>` 曾經用過黃色底線，**踩過雷不要再加回來**：92px 的 CJK 標題行框很高，
底線會落在離字形很遠的位置，看起來像一條沒來由的橫線飄在標題下方。
黃底頁不要用 `<em>`——黃色上面沒有比黑字更醒目的顏色，強調在那裡本來就不成立。

驗證腳本裡的 `strayLines` 會掃全頁，把「細長色條」與「只有單邊 border 的寬元素」
一律抓出來，**必須是 0**。

### 版面一致性（同一件事只有一種畫法）

- **格線只有 `g2` 與 `g3`**，沒有 `g4`。
- **`.grid` 裡的 `.cell` 一律加 `.card`**，不要有的有框有的沒框。
- **風林火山四頁排版完全相同**（icon 在左、文字在右），不做左右交錯。
- **每頁結構固定**：眉標 → 標題 → 一個內容區塊 → 選配註腳。
  例外只有風林火山四頁：以 `.fs .zh`（疾如風…）取代眉標，那是收尾樂章的專用版型。
- **步驟副標一律七字、無標點、結構平行**（規則寫死不用猜／AI 引導改到對／直接列印不重打）。

### icon 規格（新增 icon 必須照抄）

風林火山四頁與開場的 icon 列，全部是同一組參數的線性 icon：

```
viewBox="0 0 24 24"  fill="none"  stroke="currentColor"
stroke-width="1.6"   stroke-linecap="round"  stroke-linejoin="round"
```

驗證腳本會把每個 `.icon svg` 的這五個屬性串起來比對，**必須只出現一種組合**。
火的 bbox 比其他三個窄（14 vs 20–22），那是火焰形狀本來就瘦長，不是規格不一致。

**3. 不留三字以內的孤行 —— 含自然換行。**
不只 `<br>` 強制斷行，**卡片裡自己折行的最後一行也算**（這是最容易漏掉的）。
驗證腳本會用 Range + getClientRects 量測實際渲染的行框，逐字判斷最後一行有幾個實字。
目前四種尺寸下孤行數皆為 0。

治本的三個手段，照這個順序用：
1. **加寬欄位** —— 全簡報只用 `g2`／`g3`，不要用 `g4`（四欄在 30px 字級下每行只剩約 6 字，必爆孤行）
2. **`text-wrap:balance`** —— 已套在 `.lead` / `.fine` / `.cell .d` / `.cell .k` / `.steps .bs`，行長自動均分
3. **刪字** —— 前兩項還救不了才動文案

## 內容（22 張）

封面 → 這一年（24／7／12）→ 七種服務 → ①官網與後台 → ②電商交易 → ③營運系統
→ 案例·印刷收稿 → 案例·零售系統 → ④人資系統 → ⑤AI 應用 → 案例·AI 數位人 → 案例·AI 報價
→ ⑥行動 App → ⑦提案簡報 → 技術棧 → 服務過的產業
→ **風林火山 → 疾如風 → 徐如林 → 侵掠如火 → 不動如山** → 聯絡我們

最後五頁是收尾錨點：以風林火山形容 AI，深色底，**用線性 icon 呈現、不用文字**
（開場頁四個 icon 並排先建立記憶，後面四頁各放大一個）。這段是簡報的記憶點，不要拿掉或縮短。

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
var PUNCT=/[，。、·　\s：；！？（）＋\+]/, orph=[];
document.querySelectorAll('h1,h2,.lead,.fine,.cell .d,.cell .k,.cell .who,.steps .bt,.steps .bs,.stats .l,.biglist li,.tags span,.fs .zh,.cbox .cv').forEach(el=>{
  var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),chars=[],n;
  while(n=w.nextNode()){for(var i=0;i<n.data.length;i++)chars.push({node:n,off:i,ch:n.data[i]});}
  if(!chars.length)return; var lines=[],cur=null,lt=null;
  chars.forEach(c=>{var r=document.createRange();r.setStart(c.node,c.off);r.setEnd(c.node,c.off+1);
    var q=r.getBoundingClientRect(); if(!q.width&&!q.height)return; var t=Math.round(q.top);
    if(lt===null||Math.abs(t-lt)>4){cur=[];lines.push(cur);lt=t;} cur.push(c.ch);});
  if(lines.length<2)return;
  if(lines[lines.length-1].filter(c=>!PUNCT.test(c)).length<=3)
    orph.push(el.closest('.slide').id+' ['+lines.map(l=>l.join('')).join(' / ')+']');});
var over=[...document.querySelectorAll('.slide')].map(s=>{var i=s.querySelector('.inner'),c=getComputedStyle(s);
  return {id:s.id,over:Math.ceil(i.scrollHeight+parseFloat(c.paddingTop)+parseFloat(c.paddingBottom))-innerHeight};});
var min=999;['.lead','.cell .d','.steps .bs','.stats .l','.fine','.eyebrow','.cell .who','.tags span']
  .forEach(q=>document.querySelectorAll(q).forEach(e=>{var v=parseFloat(getComputedStyle(e).fontSize);if(v<min)min=v;}));
var blocks=[];['.eyebrow','em','.cell .who'].forEach(q=>document.querySelectorAll(q).forEach(e=>{
  if(getComputedStyle(e).backgroundColor!=='rgba(0, 0, 0, 0)')blocks.push(q);}));
var stray=0;document.querySelectorAll('.slide *').forEach(el=>{var cs=getComputedStyle(el),r=el.getBoundingClientRect();
  if(r.width>=80&&r.height>0&&r.height<=14&&cs.backgroundColor!=='rgba(0, 0, 0, 0)')stray++;
  var bw=['Top','Right','Bottom','Left'].map(sd=>parseFloat(cs['border'+sd+'Width'])||0);
  if(bw.filter(v=>v>0).length===1&&Math.max(...bw)>=2&&r.width>=80)stray++;});
var spec={};document.querySelectorAll('.icon svg').forEach(sv=>{var k=[sv.getAttribute('viewBox'),
  sv.getAttribute('stroke-width'),sv.getAttribute('fill'),sv.getAttribute('stroke-linecap'),
  sv.getAttribute('stroke-linejoin')].join('|');spec[k]=(spec[k]||0)+1;});
return JSON.stringify({minTextPx:min,orphans:orph,overflow:over.filter(x=>x.over>0),
  colorBlockOnTitles:blocks,strayLines:stray,iconSpecs:spec});})()
```

孤行、溢出、icon 規格三項都要「只有一種／空陣列」，最小字級要 ≥30，才算過。

## 品牌

奶油底 `#fffbec`／墨黑 `#1a1a1a`／亮黃 `#ffce00`；深色頁 `#15130f`，巨大單字用亮黃。
Baloo 2 + Noto Sans TC 極粗圓體、⚡ 閃電識別、3px 黑框＋硬陰影。

## 未收錄（刻意）

- **客戶評價** — 官網 `lqtech-landing/content/data.ts` 那三則與實際客戶對不上，且「評價同意」
  仍列在 `DEPLOYMENT.md` §9 的上線前待辦，判定為示意稿。
- **電話** — `site.ts` 的 `02-1234-5678` 是佔位號碼。
- **費率表** — 這版定位是公司介紹，報價留給個案提案簡報。
