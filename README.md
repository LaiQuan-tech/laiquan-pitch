# laiquan-pitch

萊乾資訊 LaiQuan — **公司介紹簡報**（22 頁全螢幕互動簡報站）。

- **線上（對外用這個）**：<https://pitch.laiquan.co>
- 備用：<https://laiquan-pitch.vercel.app>（同一份，未綁網域時的原始網址）
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

## 三段斷點：投影／平板／手機

| 元素 | 投影＋桌機（≥641px）| 手機（≤640px）|
|---|---|---|
| **正文**（`.lead` / `.cell .d` / `.steps .bs` / `.stats .l`）| **30px** | 17–19px |
| 項目標題（`.cell .k` / `.steps .bt`）| 34px | 22px |
| 大標 `h2` | 44px | 31px |
| 封面 `h1` | 54px | 40px |
| 註腳 `.fine` | 30px | 16px |

⚠️ **手機（≤640px）是唯一可以低於 30px 的地方，而且是刻意的。**
30px 是**投影規格**——台下離螢幕好幾公尺才需要那麼大；手機拿在手上讀，距離 30 公分。
硬套 30px 的後果實測過：**7 頁溢出**（s4 最多 250px），第 10 頁的產品名被折成 5 行。
**≥641px 仍然是「擠不下就刪字，不准改字級」。**

| 斷點 | 做什麼 |
|---|---|
| `≤640px` | 手機字級 ＋ 底色與次要文字加深 |
| `≤900px` | **四產品 icon 列一律 2×2**（獨立於字級規則）|
| `641–900px` | 平板：字級維持投影規格，只收留白與間距 |

⚠️ **icon 列的 2×2 斷點要拉到 900px，不能只做手機。** 四欄需要約 800px 才排得開；
平板（768px）用的是投影字級，四欄一樣塞不下，會逼出「數字人即／時互動」這種孤行。

⚠️ **小字讓 WCAG 門檻從 3:1 跳到 4.5:1。** 手機字級變小之後，原本合格的中間調配色會整批不合格
（實測 16 處）。因此手機版把 `.slide.paris` 底色壓深到 `#5b4794`，並加深 `.eyebrow`、`.fine`
與粉底頁的次要文字，修完最低 4.74:1。**動手機字級時務必重跑對比檢查。**

### 封面閃電：高度不要寫死

`.bolt` 的形狀是 `clip-path` 的百分比畫出來的，**寬高比一變形狀就歪**。
正確比例是 `360/520`（0.692），由 `aspect-ratio` 從寬度算出高度，**不要再寫 `height`**。

原本寫 `height:min(520px,50vh)`，寬度用 `min(360px,27vw)`——兩者縮放速度不同，結果：

| 尺寸 | 錯誤比例 |
|---|---|
| 1280×800 | 0.864（略胖）|
| 375×812 | **0.249**（寬度剩 101px、高度還有 406px，被拉成細長條）|

改用 `aspect-ratio` 後全尺寸都是 0.692。**驗證腳本會把所有 `.bolt` 的寬高比去重，必須只有一個值。**

### 驗證要跑的尺寸

投影 1920×1080／筆電 1440×720、1280×800／平板 768×1024、1024×768／手機 375×812、360×740。

## 內容（15 張）

分兩段：**前九頁講承接的專案，後六頁講自己的產品。**

| # | 頁 | 底色 |
|---|---|---|
| 1 | 封面 | 深藍紫 |
| 2 | 這一年（24 專案／7 服務／12 產業）| 綠松石 |
| 3 | 七種服務（清單）| 淡紫 |
| 4 | 形象官網 ＋ 後台 | 深藍紫 |
| 5 | ERP 與營運系統．美強光廣告科技（**AI 強化既有 ERP**）| 淡紫 |
| 6 | ERP 與營運系統．小時光書店（零售 POS）| 深藍紫 |
| 7 | 人資與內部管理（白標多租戶）| 葡萄紫 |
| 8 | 行動 App | 淡紫 |
| 9 | 技術棧（**不列 AI 廠商**）| 巴黎粉 |
| 10 | **風林火山**（四個產品並排）| 綠松石 |
| 11 | 疾如風．線上客服報價 | 深藍紫 |
| 12 | 徐如林．語意標籤 App | 深藍紫 |
| 13 | 侵掠如火．業務助理 | 深藍紫 |
| 14 | 不動如山．數字人即時互動 | 深藍紫 |
| 15 | 聯絡我們 | 綠松石 |

### 第 9 頁：技術棧不要列 AI 廠商

那頁標題是「**主流、長期維護得下去**」，其餘九項都是活了十年、還會再活十年的基礎建設。
曾經列過 `Gemini`（他們確實只用 Gemini —— nina／liyuanzhen／sunny／interval-books／官網都是 `gemini.ts`），
已移除，三個理由：

1. **跟那頁的主張自相矛盾** —— 模型半年一換，是清單裡唯一會過期的東西。
2. **唯一的「某廠商產品」** —— 其餘全是框架與平台，混在一起格格不入。
3. **會把自己講小** —— 「我們用 Gemini」聽起來像「就是串個 API」，蓋掉真正的工夫
   （deterministic 驗證＋AI 只做潤飾、RAG 三層護欄、白名單查詢後才交給模型）；
   指名一家也等於邀請對方辯 Google／OpenAI／Anthropic。

AI 的份量由第 5 頁與第 10–14 頁承擔，技術棧那頁的任務是基礎建設可信度。

### 第 5 頁：講「強化」，不要講「重做」

現行文案：**「ERP 不用換，用 AI 讓它變強。」**
主檔匯進來（商品加工材質）→ 收稿自己驗（錯的當場不收）→ 工單自己開（商品名自動帶）
註腳：ERP 主檔 1,039 筆匯入比對，舊系統一行程式都不用動

⚠️ **不要寫成「整套 ERP 用 AI 重做」。** 兩個理由：

1. **對不上事實。** `LaiQuan-tech/nina` 的 ERP 是**唯讀比對**（`match_product` RPC 查商品名），
   系統不回寫 ERP；設計文件也明確排除「ERP 寫入」。
2. **「強化」比「重做」好賣。** 客戶最怕的就是被要求換掉 ERP——「不用換、AI 從旁邊讓它變強」
   風險低、門檻低，反而更容易點頭。

⚠️ **同樣不要提客戶知識庫／報價／回訪／後台 AI 小幫手。**
那四塊在 nina 是 **Demo 雛形、全虛構資料**（`is_demo=true` 隔離），AI 小幫手也只讀 demo 資料。
細節見 nina 的 README 開頭警語。

「1,039 筆」是真的：`supabase/erp_data/` 商品主檔 699 ＋ 子產品 161 ＋ 加工項目 149 ＋ 主產品 30。

⚠️ **nina 的 README 曾經停在舊版**（2026-08-23 已改寫），現在開頭就分清正式功能與 Demo。
判斷範圍時看那份，或直接看 `app/` 路由與 `supabase/` schema。

### 風林火山 ↔ 四個產品

| | 成語 | 產品 | 標語 | 為什麼是這個 |
|---|---|---|---|---|
| 風 | 疾如風 | 線上客服與即時報價 | 天下武功，唯快不破 | 毫秒級即時響應，黃金三秒內捕捉意圖完成報價 |
| 林 | 徐如林 | 語意標籤 | 化繁為簡，亂中有序 | 海量雜亂數據梳理成結構，是所有 AI 應用的地基 |
| 火 | 侵掠如火 | 數字人即時互動 | 視覺震撼，引爆情感 | 面向用戶的第一線，用視覺張力攻佔心智 |
| 山 | 不動如山 | 業務助理 | 行事沉穩，最強後盾 | 跨系統整合與商務跟進，穩健可靠、絕不出錯 |

四句標語都是 **4＋4 的八字結構**，四頁節奏完全一致，是這份簡報的記憶點。
換文案時請維持這個結構，不要寫成長短不一的句子。

⚠️ **火＝數字人、山＝業務助理，不要對調。**
數字人是**面向用戶的攻勢**（直播帶貨、商務接待、情境互動），屬火；
業務助理是**內部流程與跨系統整合**，講的是不能出錯的穩定度，屬山。
（曾經提過反過來的版本——數字人配山、強調護欄不亂答——已被否決。）

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

## 配色：兩個設計的融合（黃 × 紫 × 藍綠）

萊乾原本的**亮黃⚡**＋婦女館常設展的**深淺紫與藍綠**。
用巴黎奧運那種思路做活潑感：**多色並置**，而不是靠兩色堆對比。

| 角色 | 名稱 | 色碼 | 用在哪 |
|---|---|---|---|
| **主色** | 深藍紫 | `#1b0a3f` | 主要頁底（8 頁） |
| **主色** | 葡萄紫 | `#4a1b85` | 過渡頁底、卡片填色 `#2d1160` |
| **點綴** | **亮黃** | `#ffce00` | **萊乾品牌色回歸**：封面閃電、深底頁眉標、進度條、「這一年」整頁底、火 icon |
| 副色 | 綠松石 | `#2ad4cd` | 整頁底（2 頁）、風 icon |
| 副色 | 孔雀藍 | `#0a5f70` | 淡紫底的強調字 |
| 點綴 | 淺粉 | `#ff9ec0` | 山 icon、輪替輔色 |
| 點綴 | 淡紫 | `#e8dcf5` | 呼吸頁底（3 頁）、林 icon |

### 活潑感從哪來：多色輪替，不要整排同一色

這是跟前一版最大的差別。**同一頁裡的並列元素各給一個顏色**：

- **卡片外框**（深底頁）：亮黃 → 綠松石 → 淺粉，`nth-child(3n+1/2/3)` 輪替
- **步驟投影**（淺底頁）：亮黃 → 綠松石 → 淺粉
- **標籤外框**：亮黃 → 綠松石 → 淺粉 → 淡紫，四色循環
- **風林火山四個 icon 各一色**：風＝綠松石、林＝淡紫、**火＝亮黃**、山＝淺粉

⚠️ `.steps` 的格線是 `bx,箭頭,bx,箭頭,bx`，配色要用 **`nth-child(1/3/5)`**。
用 `nth-of-type` 會把箭頭也數進去，顏色順序會跑掉。

⚠️ **火＝亮黃是刻意的**：火本來就該是黃的，而亮黃又正好是萊乾的品牌色——
這是兩個設計的接點，不要換成別的顏色。

頁底共五種：深藍紫（8）／淡紫（3）／綠松石（2）／葡萄紫（1）／**亮黃（1）**。

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
| **這一版** | **5 種（全品牌色，含亮黃）** | — | — |

⚠️ 深底頁的文字對比要另外顧。全簡報最低 4.34:1，驗證腳本的 `lowestContrast` 會算。

### 導覽元件會跟著換色

頁碼、進度條、右側圓點浮在深淺兩種底上。`setActive()` 依當頁是不是 `.lilac`／`.turq`
在 `<body>` 寫入 `data-ground="light|dark"`，CSS 再據此換色。

⚠️ 用 `getComputedStyle` 驗這幾個元素時，記得 `.nav button::after` 有
`transition:border-color .35s`——改完屬性立刻讀會拿到**過場的起始值**，
看起來像沒生效。驗證時先塞一條 `transition:none !important` 再讀。

## 風林火山那一段是「能力」，不是「型錄」

第 10 頁的眉標是**「我們怎麼看 AI」**、標題是**「AI 有四種面貌」**，
收在 icon 列後面的是「四種面貌，我們都已經做成可以直接用的產品線」。

⚠️ **不要寫成「我們自己的產品」。** 那會把整段變成型錄。這段真正的訊息是
「我們懂 AI 懂到四種面向都做得出來」，四個產品是**能力的證據**，不是待售清單。
四頁內頁的成語行帶產品名（疾如風．線上客服與即時報價）也是同一個道理——
先講特質，產品名是佐證。

## 配色定案

**巴黎紫粉版**已定案（2026-08-23）。比色期間的三個版本（深藍紫＋亮黃、第一版紫綠、
最初黃黑）已從 repo 移除，需要時從 `329d8c1` 取回：

```bash
git show 329d8c1:compare/deep-gold.html > deep-gold.html
```

（另兩個檔名為 `purple-soft.html`、`yellow.html`。）

## 自訂網域

`pitch.laiquan.co` → Cloudflare CNAME 指向 `aea5620a01e77f13.vercel-dns-017.com`，**Proxy 必須是灰色雲朵（DNS only）**。
主站 `laiquan.co` / `www.laiquan.co` 仍綁在 `lqtech-landing`，兩者互不影響。

⚠️ **憑證不會總是自動簽。** 這次 DNS 生效後等了 3 分鐘仍未簽發，
用 `POST https://api.vercel.com/v3/certs` 帶 `{"cns":["pitch.laiquan.co"]}` 手動觸發後才拿到。
症狀是 **http 通、https 握手直接失敗**（`SSL_ERROR_SYSCALL`）。下次遇到同樣情況照這樣處理。

### 現行配色（巴黎紫粉版）的設計說明

拿第一版的**淺底柔和**當底子，換上巴黎奧運的紫與粉：

- **前九頁全是淺／中調**（紫白、白、淡紫、巴黎紫、巴黎粉、綠松石），
  風林火山那五頁才落到深紫——**輕盈在前，重擊在後**，跟現行版的深底主場相反。
- 七種頁底，是四個版本裡最多彩的：巴黎紫（3）／巴黎粉（2）／深紫（5）／
  白（2）／紫白（1）／淡紫（1）／綠松石（1）。
- 卡片、步驟、標籤的輔色輪替改成 **粉 → 綠松石 → 巴黎紫**。
- 綠松石保留當冷色制衡，亮黃只留在封面閃電（萊乾識別）。

⚠️ **`--paris` 不要調亮。** 巴黎跑道那種亮紫（`#8b7bc4` 一類）拿來做整頁底，
淺色眉標在上面只有 2.4:1，不合格。壓深到 `#7461ad` 才過。

## 未收錄（刻意）

- **客戶評價** — 官網 `lqtech-landing/content/data.ts` 那三則與實際客戶對不上，且「評價同意」
  仍列在 `DEPLOYMENT.md` §9 的上線前待辦，判定為示意稿。
- **電話** — `site.ts` 的 `02-1234-5678` 是佔位號碼。
- **費率表** — 這版定位是公司介紹，報價留給個案提案簡報。
