# 議會監督網站（GitHub Pages + Google 試算表後台）

這個專案包含：
- `index.html`：前端單檔，支援 `?sheet=` 參數連線 Google 試算表（CSV）做**即時更新**。
- `data/councilors.csv`、`data/councilors.json`：離線備援資料（在沒有 `?sheet=` 時使用）。
- `sheets/匯出工作表_公式.txt`：Google 試算表的**自動計算版匯出工作表**公式，從你的原始分頁（出席率／質詢率／連署次數／提案次數／議員名冊）自動彙整成前端吃的 8 欄。

## 部署（方案 A：Google 試算表當後台）

1. 把 `index.html` 放到你的 GitHub Pages repo 根目錄並啟用 Pages。
2. 開一個 Google 試算表，將 `data/councilors.csv` 匯入為新工作表（或用你的自動計算「匯出」表）。
3. 在 Google 試算表：**檔案 → 發佈到網路 → 選『目前的工作表』＋『逗號分隔值 (.csv)』**，取得公開 CSV 連結：
   `https://docs.google.com/spreadsheets/d/e/<PUB_ID>/pub?gid=<GID>&single=true&output=csv`
4. 造訪你的網站時在網址加上：
   ```
   ?sheet=https://docs.google.com/spreadsheets/d/e/<PUB_ID>/pub?gid=<GID>&single=true&output=csv
   ```
   頁面右上角會顯示「即時資料（輪詢中）」，預設每 60 秒重抓一次。

## 後台資料欄位（8 欄）
請確保你對外匯出的 CSV 第一列標題為：

```
姓名, 系級/單位, 職稱, 照片URL, 出席率, 質詢率, 連署數, 提案數
```

- **出席率、質詢率**：0–1 的小數（例如 0.6 = 60%）
- **連署數、提案數**：整數
- **照片URL**：可使用 Google Drive 共享連結（本前端會自動轉換 `file/d/<ID>/view` 為可顯示的直連）

## 離線模式（備援）
若網址未加 `?sheet=`，前端會優先讀取 `data/councilors.csv`；若不存在，改讀 `data/councilors.json`；最後使用內建示範資料。

---

© 2025 議會監督網站
