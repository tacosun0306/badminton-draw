# 羽球抽籤系統部署指南

## 部署到 GitHub Pages

### 步驟 1: 建立 GitHub 儲存庫

1. 前往 [GitHub](https://github.com) 並登入
2. 點擊右上角的 "+" 號，選擇 "New repository"
3. 填寫以下資訊：
   - Repository name: `badminton-draw` (或其他名稱)
   - Description: `羽球抽籤系統 - 16人羽球團體抽籤網頁應用`
   - 選擇 Public (必須是 Public 才能使用免費的 GitHub Pages)
4. **不要**勾選 "Initialize this repository with a README"
5. 點擊 "Create repository"

### 步驟 2: 推送程式碼到 GitHub

在你的本地專案資料夾中，執行以下指令（記得將 `YOUR_USERNAME` 替換成你的 GitHub 使用者名稱）：

```powershell
# 已完成：git init
# 已完成：git add .
# 已完成：git commit -m "Initial commit: 羽球抽籤系統"

# 新增遠端儲存庫（請替換 YOUR_USERNAME）
git remote add origin https://github.com/YOUR_USERNAME/badminton-draw.git

# 推送到 GitHub
git branch -M main
git push -u origin main
```

### 步驟 3: 啟用 GitHub Pages

1. 在 GitHub 儲存庫頁面，點擊 "Settings"
2. 在左側選單找到 "Pages"
3. 在 "Source" 下拉選單中選擇 "main" 分支
4. 點擊 "Save"
5. 等待幾分鐘後，你的網站就會在以下網址上線：
   `https://YOUR_USERNAME.github.io/badminton-draw/`

---

## 其他部署選項

### 選項 1: Netlify (推薦 - 最簡單)

1. 前往 [Netlify](https://www.netlify.com)
2. 註冊/登入帳號
3. 將整個 `badminton-draw` 資料夾拖曳到 Netlify 的上傳區域
4. 網站會自動部署，並給你一個網址（例如：`random-name-123.netlify.app`）
5. 可在設定中自訂網域名稱

**優點**：
- 最快速，拖曳即可完成
- 自動 HTTPS
- 可自訂網域
- 不需要 Git

### 選項 2: Vercel

1. 前往 [Vercel](https://vercel.com)
2. 註冊/登入帳號
3. 點擊 "Add New Project"
4. 匯入你的 GitHub 儲存庫，或直接上傳資料夾
5. 點擊 "Deploy"

**優點**：
- 快速部署
- 自動 HTTPS
- 與 GitHub 整合良好
- 自動部署更新

### 選項 3: GitHub Pages (如上述)

**優點**：
- 完全免費
- 與 GitHub 整合
- 適合開源專案

---

## 目前狀態

✅ Git 儲存庫已初始化  
✅ 檔案已提交到本地儲存庫  
⏳ 等待推送到遠端儲存庫（GitHub/Netlify/Vercel）

## 快速開始（最簡單方式）

**推薦使用 Netlify 的拖曳上傳：**
1. 前往 https://app.netlify.com/drop
2. 將 `C:\badminton-draw` 資料夾拖曳到網頁上
3. 等待幾秒鐘，完成！

你會立即獲得一個線上網址！
