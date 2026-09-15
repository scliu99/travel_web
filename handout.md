# 巷口咖啡館 CORNER CAFÉ — HTML/CSS 排版教學講義（草稿）

> 範例網站：[`mockups/index.html`](mockups/index.html)
> 這份講義只用得到基本 HTML 標籤與 CSS，**不使用 JavaScript**。

---

## 0. 課程資訊

| 項目 | 內容 |
|---|---|
| 課程時間 | 2.5 小時（150 分鐘） |
| 適合對象 | 已經學過基本 HTML 標籤（div、p、ul、img…）的初學者 |
| 範例主題 | 一頁式咖啡館網站，內含 header/nav、hero、about、店內相片牆、菜單、顧客評論、營業資訊、footer |
| 使用技術 | 語意標籤、box model、**float**、**position**、**flexbox**、**grid** |
| 額外亮點 | 同一份 HTML，換一行 CSS 連結就變出 3 種完全不同的風格 |

### 課程目標

上完這堂課，學生應該能夠：

1. 用語意標籤（`header`／`nav`／`main`／`section`／`footer`）取代到處都是 `div` 的寫法
2. 用 **float** 做出「文字繞著圖片排」的效果
3. 用 **position: relative / absolute** 把元素精準定位在指定位置
4. 用 **flexbox** 排出導覽列、資訊列、footer 這種「一整排」的排版
5. 用 **grid** 排出菜單卡片、相片牆這種「多欄多列」的排版
6. 理解「HTML 負責內容結構、CSS 負責外觀」——同一份 HTML 換一份 CSS 就能變成完全不同的網站

---

## 1. 教學流程時間分配

| 時間 | 主題 | 對應技術 |
|---|---|---|
| 00:00–00:15 | 開場：看成品、介紹今天要做的咖啡館網站 | — |
| 00:15–00:35 | 語意標籤骨架 + reset | `header`/`nav`/`main`/`section`/`footer`，`box-sizing` |
| 00:35–00:55 | Hero 區塊：定位徽章、CTA 按鈕 | `position: relative/absolute` |
| 00:55–01:20 | About 區塊：文繞圖 + 「我們的堅持」三欄 | `float`、`flexbox` |
| 01:20–01:30 | 休息 | — |
| 01:30–02:00 | 菜單卡片區、店內相片牆 | `grid`（`auto-fit` / `minmax`） |
| 02:00–02:20 | 導覽列、營業資訊列、footer | `flexbox` |
| 02:20–02:40 | 彩蛋：同一份 HTML 換 CSS 大變身 | 複習所有技術 + CSS/HTML 分離概念 |
| 02:40–02:50 | Q&A、作業說明 | — |

> 實際上課請依現場狀況彈性調整，上表僅供備課參考。

---

## 2. 語意標籤骨架

不要整頁都用 `<div>`，改用瀏覽器看得懂「這是什麼區塊」的標籤：

```html
<header id="header">...</header>   <!-- 網站頭：logo + 導覽列 -->
<section id="hero">...</section>   <!-- 主視覺 -->
<section id="about">...</section>  <!-- 內容區塊，可以有很多個 section -->
<footer id="contact">...</footer>  <!-- 網站尾 -->
```

**為什麼要用語意標籤？**
- 對搜尋引擎、螢幕報讀器更友善
- 光看標籤名稱就知道版面結構，不用每個都取 class 名字

搭配的 CSS reset（讓 padding/margin 從 0 開始，寬度計算比較好算）：

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

---

## 3. Position：把徽章精準定位

hero 區塊右上角有一個「☕ 每日新鮮烘焙」的徽章，它是用 `position` 做出來的：

```css
#hero {
    position: relative;   /* 讓子元素的絕對定位，以這個區塊為基準 */
}

.badge {
    position: absolute;   /* 脫離文件流，用座標精準定位 */
    top: 24px;
    right: 24px;
}
```

**觀念重點**：
- `position: relative` 本身不會讓元素移動，但會變成子元素 `absolute` 定位的「參考原點」
- `position: absolute` 的元素會脫離原本的排版位置，用 `top/right/bottom/left` 貼齊指定位置

---

## 4. Float：文字繞著圖片排

About 區塊的貓掌圖示，是用最經典的 float 文繞圖做出來的：

```css
.about-photo {
    float: left;
    width: 220px;
    height: 220px;
    margin: 0 40px 20px 0;
}
```

```html
<section id="about">
    <div class="about-photo">🐾</div>
    <div class="about-text">
        <h2>關於巷口</h2>
        <p>巷口咖啡館開在轉角已經五年了……</p>
    </div>
</section>
```

因為 `.about-photo` 浮動了，後面的文字會自動繞著它排，不會被它整個擋住——這是 float 最初被設計出來要解決的問題。

**別忘了清除浮動**，不然後面的區塊高度會算錯：

```css
#about::after {
    content: "";
    display: block;
    clear: both;
}
```

---

## 5. Flexbox：一排東西的排版

網站裡只要是「一整排、要對齊、要平均分配空間」的地方，幾乎都是用 flexbox，例如導覽列：

```css
#header {
    display: flex;
    justify-content: space-between;  /* logo 靠左、選單靠右 */
    align-items: center;             /* 垂直置中 */
}

#header nav ul {
    display: flex;
    gap: 32px;       /* 每個選單項目間距 */
    list-style: none;
}
```

其他用到 flexbox 的地方：
- 「我們的堅持」三欄小卡（`.commitment`）
- 營業資訊列（`#info`）
- 顧客評論（`.review-grid`）
- footer（`#contact`）

**flexbox 心法**：先想「這排東西要往哪裡對齊、間距怎麼分」，再決定 `justify-content`（水平）跟 `align-items`（垂直）怎麼設。

---

## 6. Grid：菜單卡片、相片牆

「多欄多列」的內容，改用 grid 比較好算，例如菜單卡片區：

```css
.menu-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 24px;
}
```

**這行在做什麼？**
- `repeat(auto-fit, ...)`：瀏覽器自己決定一列要放幾張卡片
- `minmax(220px, 1fr)`：每張卡片最小 220px，空間夠的話就平均撐開

視窗變窄的時候，欄數會自動變少——不用寫 media query 手動改欄數，這是 grid 相對 float 版型的一大優勢。

同樣的寫法也用在「店內一角」相片牆（`.gallery-grid`），只是 `minmax` 改成 `120px`。

---

## 7. 彩蛋：同一份 HTML，換 CSS 大變身

打開 [`mockups/index.html`](mockups/index.html)，`<head>` 裡有這幾行：

```html
<!-- <link rel="stylesheet" href="modern.css"> -->
<!-- <link rel="stylesheet" href="playful.css"> -->
<link rel="stylesheet" href="retro.css">
```

把註解拿掉、換另一個 `.css` 檔案取消註解，存檔重整頁面——**內容、結構完全沒改，但整個網站看起來像換了一個牌子**：

| 檔案 | 風格 |
|---|---|
| `modern.css` | 現代簡約：大留白、細線條、單一強調色 |
| `playful.css` | 活潑卡片風：大圓角、彩色陰影、hover 動畫 |
| `retro.css` | 混搭懷舊感：暖色調、襯線標題、虛線雙線框 |

**這個示範要讓學生帶走的觀念**：HTML 負責「有什麼內容、什麼結構」，CSS 負責「長什麼樣子」——兩者分開，才能讓同一份內容重複利用在不同外觀上。

---

## 8. 課後練習（討論用，先不寫死答案）

1. 把 `.menu-grid` 的 `minmax(220px, 1fr)` 改成 `minmax(300px, 1fr)`，欄數會怎麼變？為什麼？
2. 試著自己加一個「常見問題 FAQ」區塊，用 flexbox 或 grid 排出兩欄問答
3. 挑一個你喜歡的顏色，做出「風格 D」，只要改 CSS、不能動 HTML
4. 想一想：如果 `#hero` 沒有 `position: relative`，`.badge` 的絕對定位會發生什麼事？可以自己刪掉試試看

---

## 附錄：程式碼位置對照

| 技術 | 檔案位置（以 `modern.css` 為例） |
|---|---|
| `position: relative/absolute` | `mockups/modern.css` 第 94、288 行 |
| `float` | `mockups/modern.css` 第 164 行 |
| `flexbox` | `mockups/modern.css` 第 40、66、133、140、170、187、228、305、330、357、377 行 |
| `grid` | `mockups/modern.css` 第 222、256 行 |
