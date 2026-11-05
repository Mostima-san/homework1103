# CLAUDE.md — 茶事講義 (Tea Notes)

> AI 助手請先完整閱讀本文件，再修改或新增任何內容。
> 目標：讓每一頁新講義都長得一致、寫法一致、能直接部署到 GitHub Pages。

## 1. 專案目的

「茶事講義」是一個以繁體中文撰寫的**台灣茶入門講義網站**。
讀者是完全沒有基礎、想認識茶的一般人。每一課聚焦一個主題，10 分鐘內讀完。

- 語言：繁體中文（台灣用語），專有名詞第一次出現時附英文或拼音。
- 語氣：親切、清楚、不賣弄術語；像一位泡茶的朋友在講解。
- 不做：商品銷售、醫療或保健功效宣稱、未經查證的數字。

## 2. 技術限制

- **純靜態網站**：HTML + CSS（必要時少量原生 JavaScript）。
- **不使用**：框架、打包工具、npm、後端、外部 CDN 腳本。
- 部署方式：GitHub Pages（從 `main` 分支根目錄發佈）。
- 所有連結使用**相對路徑**（例如 `../assets/css/style.css`），因為網站會放在子路徑 `/<repo-name>/` 底下。

## 3. 檔案結構

```
tea-notes/
├── CLAUDE.md              # 本文件（規則的唯一來源）
├── AGENTS.md              # 指向 CLAUDE.md
├── README.md              # 給人看的專案介紹與部署步驟
├── .nojekyll              # 讓 GitHub Pages 不做 Jekyll 處理
├── index.html             # 首頁：課程目錄
├── assets/
│   └── css/style.css      # 唯一的樣式檔
├── lessons/
│   ├── 01-tea-types.html
│   ├── 02-brewing-basics.html
│   └── 03-taiwan-oolong.html
└── templates/
    └── lesson-template.html   # 新增講義時複製這份
```

### 命名規則

- 講義檔名：`NN-英文-kebab-case.html`，NN 為兩位數序號（`03-taiwan-oolong.html`）。
- 全部檔名小寫、不用空白、不用中文檔名。
- 圖片放 `assets/img/`，檔名同樣用 kebab-case，且必須有 `alt` 文字。

## 4. 視覺風格

- 氣質：安靜、留白多、像茶館的紙本講義。
- 色彩一律透過 `style.css` 的 CSS 變數：`--bg`、`--ink`、`--accent`（茶綠）、`--muted`、`--card`。**不要在頁面內寫死色碼。**
- 字體：系統字體堆疊（含 `Noto Sans TC`、`PingFang TC`、`Microsoft JhengHei`），不載入外部字型。
- 版面：單欄置中，內文最大寬度約 `42rem`；手機優先（要能在 375px 寬度下正常閱讀）。
- 支援深色模式（`prefers-color-scheme: dark`），已在 `style.css` 內處理，新頁面不需另寫。
- **不要**在 HTML 內寫 inline style，需要新樣式請加到 `style.css` 並沿用既有 class 命名。

## 5. 講義頁面格式（必須遵守）

每一頁講義都由 `templates/lesson-template.html` 複製而來，並維持以下順序：

1. `<header>`：站名連結（回首頁）。
2. `<article>` 內：
   1. `<p class="kicker">` 課次，例如「第 3 課」。
   2. `<h1>` 標題（每頁只有一個 h1）。
   3. `<p class="lead">` 一句話摘要。
   4. `<div class="meta">` 閱讀時間、難度。
   5. `<div class="goals">` **學習目標**（2–4 點）。
   6. 內容章節：`<h2>` 為章節、`<h3>` 為小節，不跳級。
   7. 至少一個 `<div class="callout">` 小提醒或重點整理。
   8. `<section class="recap">` **本課重點**（3–5 點條列）。
3. `<nav class="pager">`：上一課 / 下一課連結（第一課沒有上一課，最後一課沒有下一課）。
4. `<footer>`。

`<head>` 必須包含：`charset`、`viewport`、唯一的 `<title>`（格式：`課名｜茶事講義`）、`meta description`、指向 `style.css` 的連結。

### 內容寫作規則

- 一段不超過 4 句；多用短句與條列。
- 數字、年份、溫度等事實要有依據；不確定就寫「約」或不寫。
- 比較資料用 `<table>`，並加 `<caption>`。
- 外部連結加 `rel="noopener"`，並說明連結內容。

## 6. 新增一課的標準流程

1. 複製 `templates/lesson-template.html` 到 `lessons/NN-slug.html`。
2. 依第 5 節填入內容。
3. 在 `index.html` 的課程清單 `<ol class="lesson-list">` 末端新增一個 `<li>`，沿用既有結構。
4. 更新**前一課**的 `pager`，加上「下一課」連結；新課的 `pager` 指回上一課。
5. 自我檢查（見第 7 節）後再 commit。

## 7. 完成前檢查清單

- [ ] 只有一個 `<h1>`，標題層級沒有跳級。
- [ ] 所有連結與資源都是相對路徑，且檔案真的存在。
- [ ] 沒有 inline style、沒有外部腳本。
- [ ] 圖片都有 `alt`。
- [ ] `index.html` 目錄、前後課 `pager` 都已更新。
- [ ] 手機寬度（375px）下沒有橫向捲軸。

## 8. AI 行為規則

- **先讀後改**：改動前先閱讀相關檔案，沿用現有寫法。
- **小步修改**：一次只做被要求的事，不順手重構或重新設計無關頁面。
- **不新增依賴**：不引入框架、套件或外部資源，除非使用者明確要求並更新本文件。
- **不亂改規則**：若認為本文件需要調整，先提出建議，經使用者同意後才修改。
- **不確定就問**：內容事實不確定時，標註「待確認」並告知使用者，不要編造。
- **回報方式**：完成後用 1–2 句說明改了哪些檔案，不需要逐步複述。

## 9. 目前課程進度

| 課次 | 檔案 | 主題 | 狀態 |
|---|---|---|---|
| 1 | `lessons/01-tea-types.html` | 茶的六大類 | 完成 |
| 2 | `lessons/02-brewing-basics.html` | 泡茶基本功 | 完成 |
| 3 | `lessons/03-taiwan-oolong.html` | 台灣烏龍茶地圖 | 完成 |
| 4 | （規劃中） | 台灣紅茶與蜜香紅茶 | 待寫 |
| 5 | （規劃中） | 茶具與器皿入門 | 待寫 |

> 新增或完成課程後，請同步更新此表。
