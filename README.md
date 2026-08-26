# 📋 發票管理系統

莫蘭迪藍色系發票管理系統，資料存放於 Google 試算表，支援多裝置同步。

---

## 檔案結構

```
├── index.html       ← 主程式
├── manifest.json    ← PWA 設定
├── icon-192.png     ← App 圖示
├── icon-512.png     ← App 圖示（大）
├── favicon.ico      ← 瀏覽器標籤圖示
└── README.md
```

> `Code.gs` 為後端程式，部署於 Google Apps Script，**不上傳至 GitHub**。

---

## 部署步驟

### 1. 建立 Google Apps Script

1. 開啟 [script.google.com](https://script.google.com)
2. 新增專案，命名為「發票管理系統」
3. 將後端程式碼貼入編輯器
4. 執行 `initialize()` 函式，自動建立試算表分頁
5. 執行 `createDailyBackupTrigger()` 函式，建立每日自動備份排程
6. 部署 → 新增部署作業 → 類型選「Web 應用程式」
   - 執行身分：**我**
   - 存取權：**任何人**
7. 複製 Web App 網址備用

### 2. 設定 index.html

開啟 `index.html`，找到以下這行（約第 360 行），將網址替換為步驟 1 取得的 Web App 網址：

```javascript
const API_URL = 'YOUR_APPS_SCRIPT_URL_HERE';
```

### 3. 上傳到 GitHub Pages

1. 在 GitHub 建立新 repository
2. 上傳所有檔案（**不含** `Code.gs`）
3. Settings → Pages → Source 選 **main branch / root**
4. 等待約 1 分鐘即可透過 GitHub Pages 網址存取

---

## 功能說明

| 功能 | 說明 |
|------|------|
| 登入驗證 | 密碼於後端設定，前端完全看不到 |
| 登入時效 | 4 小時自動登出 |
| 暴力破解保護 | 連續錯誤達上限後自動鎖定 |
| 自動備份 | 每天午夜過後，有異動時自動備份至指定雲端資料夾 |
| 手動備份 | 工具列「☁️ 雲端備份」→「立即備份」 |
| 本機備份 | 工具列「💾 備份」，下載 JSON 檔案至本機 |
| 備份還原 | 可從雲端備份清單還原，或上傳本機 JSON |
| 付款日計算 | 台幣：10／25 日制；外幣：14／28 日制 |

## 試算表結構

| 分頁名稱 | 說明 |
|----------|------|
| 發票資料 | 所有發票記錄 |
| 廠商資料 | 廠商代碼、名稱、稅別、付款天數、幣別 |
| 假日設定 | 台灣國定假日清單 |
