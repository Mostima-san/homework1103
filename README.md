# 茶事講義 (Tea Notes)

以繁體中文撰寫的**台灣茶入門講義網站**，純靜態 HTML + CSS，可直接部署到 GitHub Pages。

## 專案特色

- 規則集中在 [`CLAUDE.md`](./CLAUDE.md)，[`AGENTS.md`](./AGENTS.md) 指向它，讓任何 AI 代理都能依同一套規則繼續新增講義。
- 每課由 `templates/lesson-template.html` 複製而來，格式一致。
- 無框架、無外部依賴、支援手機與深色模式。

## 目錄結構

```
├── CLAUDE.md / AGENTS.md   # AI 規則
├── index.html              # 首頁（課程目錄）
├── assets/css/style.css    # 唯一樣式檔
├── lessons/                # 各課講義
└── templates/              # 新課模板
```

## 本機預覽

在專案根目錄執行：

```bash
python3 -m http.server 8000
```

然後開啟 <http://localhost:8000>。

## 上傳 GitHub 並公開網站

```bash
git init
git add .
git commit -m "Initial commit: 茶事講義"
git branch -M main
git remote add origin https://github.com/<你的帳號>/tea-notes.git
git push -u origin main
```

接著到 GitHub 儲存庫：**Settings → Pages → Build and deployment**，Source 選 **Deploy from a branch**，Branch 選 `main` / `/ (root)`，儲存。

約一分鐘後，網站會出現在 `https://<你的帳號>.github.io/tea-notes/`。

## 用 AI 新增下一課

對 AI 說：「請先讀 CLAUDE.md，然後新增第 3 課：台灣烏龍茶地圖。」
