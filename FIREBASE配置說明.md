# Firebase 配置說明

## 步驟 1：建立 Firebase 專案

1. 前往 [Firebase Console](https://console.firebase.google.com/)
2. 點擊「新增專案」
3. 輸入專案名稱（例如：badminton-game）
4. 完成建立流程

## 步驟 2：啟用 Firestore Database

1. 在左側選單選擇「Firestore Database」
2. 點擊「建立資料庫」
3. 選擇「以測試模式啟動」（或稍後設定安全規則）
4. 選擇資料庫位置（建議選 asia-east1 或 asia-southeast1）

## 步驟 3：設定安全規則

在 Firestore 的「規則」頁籤，貼上以下規則：

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /badminton/{document=**} {
      allow read, write: if true;  // 允許所有人讀寫
    }
  }
}
```

> ⚠️ 這是最簡單的設定，所有人都可以存取。如果需要更安全的設定，請參考進階設定。

## 步驟 4：取得 Firebase 配置

1. 點擊左上角齒輪圖示 → 「專案設定」
2. 在「一般」頁籤往下滑，找到「你的應用程式」
3. 點擊「</>」（網頁）圖示
4. 複製 `firebaseConfig` 物件中的資訊

## 步驟 5：更新 index_v2.html 配置

打開 `index_v2.html`，找到以下程式碼：

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

替換成你從 Firebase Console 複製的配置。

## 步驟 6：部署網站

### 選項 A：Firebase Hosting（推薦）

```powershell
# 安裝 Firebase CLI
npm install -g firebase-tools

# 登入 Firebase
firebase login

# 初始化專案
firebase init hosting

# 選擇剛才建立的專案
# public directory: 選擇當前目錄 .
# Configure as single-page app: No
# Set up automatic builds: No

# 部署
firebase deploy
```

部署完成後會得到一個網址，例如：`https://badminton-game.web.app`

### 選項 B：Netlify（簡單快速）

1. 前往 [Netlify](https://www.netlify.com/)
2. 拖曳 `index_v2.html` 到部署區域
3. 完成！會得到一個 `.netlify.app` 網址

### 選項 C：GitHub Pages

1. 將檔案上傳到 GitHub repository
2. 在 repository 設定中啟用 GitHub Pages
3. 選擇分支和資料夾
4. 完成！會得到一個 `.github.io` 網址

## 步驟 7：測試多裝置同步

1. 在瀏覽器開啟部署的網址
2. 用手機或另一台電腦也開啟同一個網址
3. 在任一裝置登記球員或操作
4. 觀察其他裝置是否即時同步更新

## 驗證 Firebase 連線

打開瀏覽器的開發者工具（F12），在 Console 中應該看到：
- ✅ Firebase 已連線
- 📡 資料已同步
- 💾 資料已儲存

## 常見問題

### Q: 顯示「Firebase 初始化失敗」
A: 檢查 firebaseConfig 是否正確替換，確認網路連線正常

### Q: 資料沒有同步
A: 檢查 Firestore 安全規則是否設定正確，確認已啟用 Firestore Database

### Q: 本地測試無法連線
A: 本地檔案（file://）無法使用 Firebase，需要部署到網路伺服器

## 進階：更安全的規則設定

如果想要增加安全性，可以使用以下規則：

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /badminton/{document=**} {
      // 只允許讀取和更新 gameState 文件
      allow read: if true;
      allow write: if request.resource.data.keys().hasAll(['players', 'playerMatchCount']);
    }
  }
}
```

## 需要協助？

如果遇到問題，請檢查：
1. Firebase Console 的 Firestore 是否有資料寫入
2. 瀏覽器 Console 是否有錯誤訊息
3. 網路連線是否正常
