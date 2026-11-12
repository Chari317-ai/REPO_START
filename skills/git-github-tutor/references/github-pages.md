# 選修：用 GitHub Pages 發布網頁

**比喻**：GitHub Pages 是 GitHub 送的免費「展示櫃」。把 repo 裡的網頁放進展示櫃，別人打開一個網址就能看到網頁畫面，而不是程式碼。

## 前置條件

- repo 是 **Public**（免費帳號只有 public repo 能用 Pages）。如果是 private，先跟他說明這個限制，讓他決定要不要改成 public。
- repo 最外層有一個名字剛好叫 `index.html` 的檔案，這是網站的首頁。
  - 沒有的話，問他想放什麼內容，幫他做一個簡單的 `index.html`，commit 並 push 上去。

## 步驟（學生在網頁上操作）

先提醒：「開啟後，網址會公開，任何人都能看到這個網頁。」他同意後：

1. 打開 `https://github.com/帳號/repo名稱/settings/pages`
2. **Source** 選 `Deploy from a branch`
3. **Branch** 選 `main`，旁邊的資料夾選 `/ (root)`
4. 按 **Save**

## 確認上線

- 部署大約需要 1～2 分鐘。可以到 `https://github.com/帳號/repo名稱/actions`，看到「pages build and deployment」出現綠色勾勾就是成功了。
- 網址格式：`https://帳號.github.io/repo名稱/`（帳號一律用小寫）
- 打開看到 404：多等 1～2 分鐘，再重新整理。
- 看到舊的畫面：強制重新整理（Mac 按 `Cmd + Shift + R`，Windows 按 `Ctrl + F5`）。

## 之後怎麼更新網站

修改 `index.html` → commit → push，大約 1 分鐘後網站就會自動更新，不用重新設定 Pages。
