# 五張命盤，一張人生地圖

一個把八字、紫微斗數、西洋占星、吠陀占星、人類圖放在同一個出生時刻上交叉分析的網站。輸入生日，五套系統各自排盤，再整合成一份依生活領域分類的解讀。

**線上版本：** https://emmatttsao.github.io/fatenlife/

---

## 為什麼做這個

我自己長期在看命理，過程中一直有個困擾：每一套系統都自成一個世界，各講各的，看得越多越容易鑽牛角尖。單看一套，你很難分辨哪些訊號是真的、哪些只是那套系統的語言習慣。

但如果同一個出生時刻被五套系統同時描述，那些**重複出現的訊號**就有意義了。八字說你的命帶變動，紫微說你三方是殺破狼，人類圖說你是 6/3 前期試錯型——這三句話用完全不同的語言，指向同一件事。這種交叉驗證，才是我想要的東西。

市面上的工具都是單一系統，而且多半要付費、要註冊、要把生日交出去。所以我自己做了一個。

## 產品決策

**一頁綜合分析，四張完整命盤。** 首頁不是丟一堆星曜術語給你，而是按照財務、事業、家庭、人際、健康、感情這些真正會被拿來做決定的領域來組織。想深入看原始盤面的人，再從選單進去看紫微、西洋、吠陀、人類圖的完整圖。給不懂的人一個入口，也給懂的人足夠的資訊量。

**盲讀原則。** 系統只從盤面結構推導，不會因為知道使用者是誰而調整說法。這是刻意的自我限制——如果分析會受已知資訊影響，那它就失去了驗證的價值。

**資料不離開裝置。** 所有計算都在使用者自己的瀏覽器完成，沒有後端、沒有資料庫，生日不會被傳出去也不會被記錄。命理資料很私密，這件事沒有妥協空間。

## 視覺與文案

主標「五張命盤，一張人生地圖」——五對一的收束，把散落的系統收攏成一個東西。副標把五套系統列出來，負責把話講清楚，讓主標可以留一點空間。

視覺參考傳統星圖與星盤儀：純黑底、髮絲級線條、多層同心環、發光的行星點。配色收在古金、咖啡、淡金三色，只有需要被指認的東西才發光——命宮、上升、已定義的通道。四張命盤形狀完全不同，但共用同一套線條語彙與留白節奏，看起來像同一組儀器上的四個刻度盤。

## 技術上的選擇

**天文計算是自己寫的，零外部依賴。** 瀏覽器不能跑 Python，而可靠的天文函式庫壓縮後也有 116KB，不適合內嵌。所以我用 JavaScript 重寫了一套計算核心，涵蓋儒略日、太陽月亮與各行星黃經、上升與中天、Lahiri 歲差、合朔與節氣。

**精度是驗證出來的，不是估計的。** 每一項都拿瑞士星曆表逐一比對：太陽 3 角秒、月亮與內行星 1 角分內、天海冥 2 角分內，最差的土星約 10 角分。過程中修正了三個實質錯誤——行星缺少 J2000 到當日的歲差轉換（系統性偏差約 29 角分）、混用了兩套不相容的軌道根數修正項、合朔搜尋的步進啟發式會跳過整個朔望月導致農曆算出 34 天。

**有一個很尖銳的邊界案例。** 測試用的那張盤，太陽剛好落在人類圖閘門的邊界上，差 0.001 度。原本的太陽公式精度不足，把人生角色算成 1/3；換成 VSOP87 截斷級數後才回到正確的 6/3。這種盤不多，但遇到就會整份判讀跑掉。

**單一 HTML 檔案，約 100KB。** 沒有建置流程、沒有相依套件、沒有伺服器成本。丟到任何靜態空間都能跑，離線也能用。

## 成果

- 造訪次數：_（待填）_
- 排盤次數：_（待填）_
- 最多人看的分頁：_（待填）_

## 已知限制

命理提供的是傾向與節奏，不是判決。這個網站的分析由規則引擎推導，深度不及人工細讀，準確度也受限於規則涵蓋的範圍。

計算方面，土星最大誤差約 0.16 度，對星座與宮位判定無影響，但在極少數落於閘門邊界的盤上可能有差異。時區採固定偏移，若出生當地當時實施日光節約時間，需自行調整。

---

## Summary in English

A single-page web app that reads one birth moment through five divination systems at once — Chinese BaZi, Zi Wei Dou Shu, Western astrology, Vedic astrology, and Human Design — then cross-references them into one synthesised reading organised by life area.

The premise: any single system is easy to over-read. Signals that appear independently across five different frameworks are the ones worth paying attention to.

Built as a single self-contained HTML file with a hand-written, zero-dependency astronomical engine in JavaScript, validated position by position against the Swiss Ephemeris. No backend, no API calls, no data collection — every calculation runs in the visitor's own browser, so birth data never leaves the device.

Concept, copywriting, art direction, and build: Emma Tsao.

---

## 統計設定（給我自己看的）

要開啟造訪統計，在 `index.html` 裡找到 `const GC_CODE='';`，把 GoatCounter 代碼填進引號中。留空則完全不載入統計。統計只記錄造訪次數與來源，不接觸使用者輸入的任何內容。
