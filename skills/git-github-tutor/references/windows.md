# Windows 指令參考

Codex 在 Windows 上通常用 PowerShell 執行指令。SSH 相關的步驟統一透過 **Git Bash**（安裝 Git 時會一起裝好）執行，原因有兩個：

- PowerShell 傳「空字串」給 `ssh-keygen` 時，不同版本的行為不一樣，容易出錯
- Git 推送時用的就是 Git 內建的 SSH，用同一套最不容易出問題

以下用 `$bash` 代表 Git Bash：

```
$bash = "$env:ProgramFiles\Git\bin\bash.exe"
```

## 第 1 步：檢查／安裝 Git

```
git --version
```

有版本號 → 已安裝。沒有的話：

```
winget install --id Git.Git -e --source winget
```

- 過程中會跳出「是否允許此 App 變更你的裝置」的視窗，請學生按 **是**。
- 如果沒有 `winget`，或安裝失敗：請他到 https://git-scm.com/downloads/win 下載安裝檔，每個畫面都按 **Next**（全部使用預設值）就可以。
- 裝完後請他**關掉再重開 Codex**，再執行一次 `git --version`。

## 第 3 步：SSH 金鑰

### 檢查現有金鑰

```
Get-ChildItem "$HOME\.ssh" -Force
```

看到 `id_ed25519` 和 `id_ed25519.pub` 就表示已經有金鑰，直接沿用。

### 產生金鑰：不設密碼（你可以代為執行）

```
$bash = "$env:ProgramFiles\Git\bin\bash.exe"
& $bash -lc "mkdir -p ~/.ssh && ssh-keygen -t ed25519 -C '他的 Email' -f ~/.ssh/id_ed25519 -N ''"
```

### 產生金鑰：要設密碼（請學生自己執行）

請他從開始選單打開 **Git Bash**，貼上：

```
ssh-keygen -t ed25519 -C "他的 Email"
```

- 問存放位置時，直接按 Enter
- 接著輸入兩次密碼（畫面上不會顯示字，是正常的）

說明：Windows 上設了密碼，之後每次 push 都要輸入一次。嫌麻煩的話，可以選擇不設密碼。

### 複製公鑰到剪貼簿

```
Get-Content "$HOME\.ssh\id_ed25519.pub" | Set-Clipboard
Get-Content "$HOME\.ssh\id_ed25519.pub"
```

### 測試連線

```
& $bash -lc "ssh -o StrictHostKeyChecking=accept-new -T git@github.com"
```

（結果判讀見 SKILL.md 的 3-4。）

## 刪除檔案：移到資源回收筒

不要用 `rm`、`del`、`Remove-Item`，這些會直接把檔案抹掉。

先確認目標在本機硬碟：

```
[System.IO.DriveInfo]::new("C:\").DriveType
```

結果是 `Fixed` 才使用下面的方法：

```
Add-Type -AssemblyName Microsoft.VisualBasic
# 檔案
[Microsoft.VisualBasic.FileIO.FileSystem]::DeleteFile("完整路徑", "OnlyErrorDialogs", "SendToRecycleBin")
# 資料夾
[Microsoft.VisualBasic.FileIO.FileSystem]::DeleteDirectory("完整路徑", "OnlyErrorDialogs", "SendToRecycleBin")
```

如果目標在網路磁碟或隨身碟，或上面的指令失敗：不要改用其他刪除方式，把完整路徑列給學生，請他在檔案總管選取後按 Delete。

## 小技巧

- 檔案總管顯示隱藏資料夾（例如 `.git`）：上方「檢視」→「顯示」→ 勾選「隱藏的項目」
- 「文件」資料夾的路徑通常是 `$HOME\Documents`
- 換行符號警告（`LF will be replaced by CRLF`）是正常提示，不影響使用
