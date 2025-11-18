# Firebase 設定指南

## 如何啟用即時同步功能

目前系統使用本地模式，要讓所有人看到相同的賽程，需要設定 Firebase Realtime Database。

### 步驟 1: 建立 Firebase 專案

1. 前往 [Firebase Console](https://console.firebase.google.com)
2. 點擊「新增專案」或「Add project」
3. 輸入專案名稱，例如：`badminton-draw`
4. 按照指示完成專案建立

### 步驟 2: 啟用 Realtime Database

1. 在 Firebase Console 左側選單點擊「Realtime Database」
2. 點擊「建立資料庫」
3. 選擇資料庫位置（建議選擇 `asia-southeast1`）
4. 選擇安全性規則：
   - 開發階段：選擇「測試模式」（任何人都可讀寫）
   - 正式使用：選擇「鎖定模式」後手動設定規則

### 步驟 3: 設定安全性規則

在 Realtime Database 的「規則」頁籤，將規則改為：

```json
{
  "rules": {
    "game": {
      ".read": true,
      ".write": true
    }
  }
}
```

> ⚠️ 注意：這個規則允許所有人讀寫，適合小型私人使用。正式環境建議加入身份驗證。

### 步驟 4: 取得設定資訊

1. 在 Firebase Console 點擊專案設定（齒輪圖示）
2. 在「一般」頁籤向下捲動到「您的應用程式」
3. 點擊「</> Web」圖示新增網頁應用
4. 註冊應用後，複製設定物件

設定物件看起來像這樣：
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  authDomain: "badminton-draw-xxxxx.firebaseapp.com",
  databaseURL: "https://badminton-draw-xxxxx.firebaseio.com",
  projectId: "badminton-draw-xxxxx",
  storageBucket: "badminton-draw-xxxxx.appspot.com",
  messagingSenderId: "123456789012",
  appId: "1:123456789012:web:xxxxxxxxxxxxxx"
};
```

### 步驟 5: 更新程式碼

1. 開啟 `index.html`
2. 找到這段程式碼（約在第 394 行）：
```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT.firebaseio.com",
    projectId: "YOUR_PROJECT",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_ID",
    appId: "YOUR_APP_ID"
};
```

3. 將上面的內容替換成你從 Firebase 取得的設定

### 步驟 6: 測試

1. 儲存檔案並重新整理網頁
2. 右上角應該顯示「已連線」（綠色指示燈）
3. 開啟另一個瀏覽器視窗或使用手機開啟同一個網址
4. 在任一視窗進行操作，其他視窗應該會即時同步更新

## 功能說明

設定完成後，系統會提供：

✅ **即時同步** - 所有人看到相同的賽程
✅ **自動更新** - 一個人操作，所有人即時看到
✅ **持久化儲存** - 資料儲存在雲端，重新整理不會遺失
✅ **多人協作** - 多個裁判或管理員可同時管理

## 注意事項

- Firebase 免費方案每月有 1GB 下載量限制，對小型團體使用綽綽有餘
- 如果不設定 Firebase，系統仍可正常運作，但僅限單機使用
- 建議正式使用前測試同步功能是否正常

## 安全性建議

如果要加強安全性，可以：

1. 加入身份驗證（Firebase Authentication）
2. 修改資料庫規則，只允許特定使用者寫入
3. 設定網域白名單

詳細資訊請參考 [Firebase 官方文件](https://firebase.google.com/docs)。
