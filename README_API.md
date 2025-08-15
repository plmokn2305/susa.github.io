# 議會監督網站（單一端點即時發佈版）

## 「全部整合在一起」怎麼做？
使用 Google Apps Script **Web App** 將同一份試算表內的兩個分頁合併成**一個 JSON 端點**：
- `匯出`（統計 8 欄）
- `提案清單`（議員、日期、標題、類型、連署名單）

前端網址只帶一個參數：
`?api=https://script.google.com/macros/s/<DEPLOY_ID>/exec`

頁面每 60 秒輪詢一次，達到即時更新。

### 步驟
1. 在你的 Google 試算表（建議用我們的 `backend_master.xlsx` 轉成雲端試算表）新增 Apps Script，將 `sheets/apps_script_webapp.gs` 程式貼上。
2. 部署 → 新部署 → 類型選「網路應用程式」，存取權設「任何知道連結的人」。複製 URL。
3. 將 `index.html` 上傳到 GitHub Pages，造訪：
   `https://<你>.github.io/<repo>/?api=<上一步的URL>`

> 備援：若沒用 Web App，也可照舊用 `?sheet=` + `?proposals=`。

本專案檔案：
- `index.html`（支援 `?api=`）
- `sheets/apps_script_webapp.gs`（Web App 程式碼）
