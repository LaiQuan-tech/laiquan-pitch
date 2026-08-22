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
- **並列項目的分隔符一律用 `．`（全形句號），不要用 `　·　`。**
  中間點加兩個全形空格佔三個字寬，在 30px 以上的字級會把一行撐開、也容易逼出孤行。
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

## 內容（15 張）

分兩段：**前九頁講承接的專案，後六頁講自己的產品。**

| # | 頁 | 底色 |
|---|---|---|
| 1 | 封面 | 深藍紫 |
| 2 | 這一年（24 專案／7 服務／12 產業）| 綠松石 |
| 3 | 七種服務（清單）| 淡紫 |
| 4 | 形象官網 ＋ 後台 | 深藍紫 |
| 5 | 產業營運系統．美強光廣告科技（印刷收稿）| 淡紫 |
| 6 | 產業營運系統．小時光書店（零售 POS）| 深藍紫 |
| 7 | 人資與內部管理（白標多租戶）| 葡萄紫 |
| 8 | 行動 App | 淡紫 |
| 9 | 技術棧 | 深藍紫 |
| 10 | **風林火山**（四個產品並排）| 綠松石 |
| 11 | 疾如風．線上客服報價 | 深藍紫 |
| 12 | 徐如林．語意標籤 App | 深藍紫 |
| 13 | 侵掠如火．業務助理 | 深藍紫 |
| 14 | 不動如山．數字人即時互動 | 深藍紫 |
| 15 | 聯絡我們 | 綠松石 |

### 風林火山 ↔ 四個產品

| | 特質 | 產品 | 為什麼是這個 |
|---|---|---|---|
| 風 | 極速反應 | 線上客服報價 | 客戶問完當場估價，不用等人回訊息 |
| 林 | 井然有序 | 語意標籤 App | 標籤把人事物歸位，資料多也找得到 |
| 火 | 生成與攻勢 | 業務助理 | 主動產出名單、開發信、跟進節奏 |
| 山 | 不為所動 | 數字人即時互動 | 護欄擋住越界內容，口徑始終如一 |

⚠️ **「數字人＝山」是刻意的，不要換成火。** 數字人最強的賣點不是會生成影音，
是**再怎麼被套話都不會亂答**——這直接接上婦權基金會那套三層護欄。
換成火之後，山就只剩「業務助理很穩」這種撐不起來的主張。

### 從 22 頁砍到 15 頁，砍掉的七頁與理由

| 砍掉 | 理由 |
|---|---|
| AI 應用（四種用法）| 完全被風林火山取代——那四頁現在就是四個具名產品 |
| 案例．AI 數位人 | 併入「山」 |
| 案例．AI 報價 | 併入「風」 |
| 營運系統（金句頁）| 兩個案例自己講得清楚，類別改由眉標帶出 |
| 服務過的產業（12 個標籤）| 第 2 頁的「12 個產業」已經講完 |
| 電商與交易 | 沒有具名客戶、只有功能列表，最弱的一頁；零售案例已涵蓋交易 |
| 提案與募資簡報 | meta 頁，改成結尾一句「你現在看的這份簡報，也是我們做的」|

⚠️ **眉標不要再加編號。** 砍頁之後 `01 → 04 → 06` 會斷號，看的人會以為漏了。
編號只留在第 3 頁的清單裡。

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
function L(c){var m=(c.match(/[\d.]+/g)||[0,0,0]).map(Number).slice(0,3).map(v=>{v/=255;
  return v<=0.03928?v/12.92:Math.pow((v+0.055)/1.055,2.4);});return .2126*m[0]+.7152*m[1]+.0722*m[2];}
function bgOf(el){var n=el;while(n&&n!==document.documentElement){var b=getComputedStyle(n).backgroundColor;
  if(b&&b!=='rgba(0, 0, 0, 0)')return b;n=n.parentElement;}return getComputedStyle(document.body).backgroundColor;}
var lowC=99;document.querySelectorAll('.slide .eyebrow,.slide h1,.slide h2,.slide .lead,.slide .fine,.slide .cell .k,.slide .cell .d,.slide .cell .who,.slide .steps .bt,.slide .steps .bs,.slide .stats .l,.slide .tags span,.slide em').forEach(el=>{
  if(!el.textContent.trim())return;var a=L(getComputedStyle(el).color),b=L(bgOf(el));
  var r=(Math.max(a,b)+.05)/(Math.min(a,b)+.05);if(r<lowC)lowC=+r.toFixed(2);});
return JSON.stringify({minTextPx:min,orphans:orph,overflow:over.filter(x=>x.over>0),
  colorBlockOnTitles:blocks,strayLines:stray,iconSpecs:spec,lowestContrast:lowC});})()
```

孤行／溢出／色塊／多餘線條要全空，`iconSpecs` 只能有一種，`minTextPx` ≥ 30，`lowestContrast` ≥ 3。

## 配色：深藍紫主場 × 綠松石重擊

取自台灣國家婦女館年度常設展主視覺，並把紫與藍綠的對比再拉深一階。

| 角色 | 名稱 | 色碼 | 用在哪 |
|---|---|---|---|
| **主色** | 深藍紫 | `#1b0a3f` | **主要頁底（10 頁）**、淺底頁的文字與外框 |
| **主色** | 葡萄紫 | `#4a1b85` | 過渡頁底（2 頁）、卡片填色 `#2d1160` |
| 副色 | 孔雀藍 | `#0a5f70` | 淡紫底頁的強調字與清單編號 |
| 副色 | 藍綠 | `#10a5a0` | 備用 |
| 副色 | 綠松石 | `#2ad4cd` | **整頁底（5 頁）**、深底頁的外框／眉標／icon／封面閃電 |
| 點綴 | 淺粉 | `#ff9ec0` | 深底頁的 `<em>` 強調、風林火山的成語標、封面閃電疊層 |
| 點綴 | 淡紫 | `#e8dcf5` | 呼吸頁底（5 頁） |

### 對比是怎麼拉深的

**1. 沒有白底頁。** 白底會把紫綠對比稀釋成「白紙上印彩色」。淺色頁一律用淡紫，
白色只出現在卡片填色。四種頁底全是品牌色。

**2. 深藍紫從點綴變主場。** 前一版 22 頁裡有 11 頁是白或淡紫，紫只是文字顏色；
這版 10 頁深藍紫 ＋ 2 頁葡萄紫，紫是「地」不是「字」。

**3. 綠松石整頁下重手。** 從 2 頁增為 5 頁，且飽和度拉高（`#3fc7c2` → `#2ad4cd`）。

**4. 啟用淺粉。** 前一版標「保留備用」，這版用在深藍紫底上的強調字與成語標——
淺粉配深藍紫是這組色裡張力最高的一對。

客觀量測（相鄰頁底色的對比跳動，數字越大切頁越有斷點）：

| | 頁底種類 | 平均跳動 | 平坦切換 |
|---|---|---|---|
| 前一版 | 6 種（含白） | 4.55 | 11 次 |
| **這一版** | **4 種（全品牌色）** | **7.23（＋59%）** | **7 次** |

⚠️ 深底頁的文字對比要另外顧。全簡報最低 4.34:1，驗證腳本的 `lowestContrast` 會算。

### 導覽元件會跟著換色

頁碼、進度條、右側圓點浮在深淺兩種底上。`setActive()` 依當頁是不是 `.lilac`／`.turq`
在 `<body>` 寫入 `data-ground="light|dark"`，CSS 再據此換色。

⚠️ 用 `getComputedStyle` 驗這幾個元素時，記得 `.nav button::after` 有
`transition:border-color .35s`——改完屬性立刻讀會拿到**過場的起始值**，
看起來像沒生效。驗證時先塞一條 `transition:none !important` 再讀。

## 比色用的舊版

- [`compare/yellow.html`](compare/yellow.html) — 最初的黃黑版
- [`compare/purple-soft.html`](compare/purple-soft.html) — 第一版紫綠（淺底為主）

線上路徑同名。**都是凍結快照，不同步更新**，配色定案後可以整個 `compare/` 刪掉。

## 未收錄（刻意）

- **客戶評價** — 官網 `lqtech-landing/content/data.ts` 那三則與實際客戶對不上，且「評價同意」
  仍列在 `DEPLOYMENT.md` §9 的上線前待辦，判定為示意稿。
- **電話** — `site.ts` 的 `02-1234-5678` 是佔位號碼。
- **費率表** — 這版定位是公司介紹，報價留給個案提案簡報。
