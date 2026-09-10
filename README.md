ONE PLUS旅遊網 — HTML/CSS 排版教學範例
======================================

單頁旅遊網站，只用基本 HTML 標籤與 CSS（不含 JavaScript），示範 float、flexbox、grid
三種排版技術如何在同一個頁面並存使用。搭配 git tag（step1 ~ step9）記錄每個教學階段，
可用 `git checkout <tag>` 切換到對應進度。

## Step 1：語意標籤骨架
用 header / nav / main / aside / footer 取代 div soup，nav 先放好頁內錨點連結，
CSS 做 reset + box-sizing，統一 UTF-8 編碼。此階段還沒排版，只給每個區塊底色看骨架。

## Step 2：五大區塊 float 巨集版型
用 float 排出 980px 置中的 wrapper，header / sidebar1 / content / sidebar2 / footer
左右並排。

## Step 3：header 完稿
logo 用「文字藏圖片」技巧呈現，標語用絕對定位；nav 選單改用 flexbox 排列，
對照原本 float 版 nav 的寫法。

## Step 4：sidebar1（本月出團）完稿
外層維持 float 巨集版型，清單內部改用 flexbox 對齊。

## Step 5：main content 完稿 + 熱門行程 Grid
歡迎詞與溫馨小叮嚀維持 float 排版；新增「熱門行程」卡片區，用 CSS Grid
（auto-fit / minmax）做響應式多欄卡片。

## Step 6：sidebar2（更多好康／國家區域）完稿
標題改用真文字＋CSS 排版樣式，和 sidebar1 的圖片標題手法對照。

## Step 7：footer 完稿
用 flexbox 排版權資訊與聯絡資訊。

## Step 8：全頁背景 + 錨點捲動
加上 body / wrapper 背景圖，nav 錨點加上平滑捲動效果。

## Step 9（final）：RWD 基礎
加上 viewport meta 與一個 media query，窄螢幕時 grid 卡片收成單欄、
sidebar 由左右浮動改為上下堆疊。
