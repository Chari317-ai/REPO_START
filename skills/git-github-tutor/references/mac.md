# Mac 指令參考

以下指令都在 Mac 的終端機（zsh）執行。

## 第 1 步：檢查／安裝 Git

```
xcode-select -p
git --version
```

- `xcode-select -p` 有印出路徑，而且 `git --version` 有版本號 → 已安裝。
- 沒有的話執行：
  ```
  xcode-select --install
  ```
  - 畫面會跳出「是否要安裝指令列開發者工具」的視窗，請學生按 **安裝**，再按 **同意**。
  - 下載加安裝大約 5～15 分鐘，等他回覆「裝好了」，再執行一次 `git --version`。
  - 說明：Mac 的 Git 包含在 Apple 的「指令列開發者工具」(Command Line Tools) 裡，所以裝的是這個。

## 第 3 步：SSH 金鑰

### 檢查現有金鑰

```
ls -la ~/.ssh
```

看到 `id_ed25519` 和 `id_ed25519.pub` 就表示已經有金鑰，直接沿用。

### 產生金鑰：不設密碼（你可以代為執行）

```
mkdir -p ~/.ssh && chmod 700 ~/.ssh
ssh-keygen -t ed25519 -C "他的 Email" -f ~/.ssh/id_ed25519 -N ""
```

### 產生金鑰：要設密碼（請學生自己執行）

請他打開 Mac 的「終端機」App（或在 Codex 的終端機裡），貼上：

```
ssh-keygen -t ed25519 -C "他的 Email"
```

- 問存放位置時，直接按 Enter
- 接著輸入兩次密碼（畫面上不會顯示字，是正常的）

產生後，請他再執行下面這行，把密碼存進 Mac 的鑰匙圈，之後就不用每次輸入：

```
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

### 讓 Mac 自動帶上這把鑰匙

先看 `~/.ssh/config` 是否存在、裡面有沒有 `Host github.com`：

```
cat ~/.ssh/config 2>/dev/null
```

沒有 `Host github.com` 的話，**附加**（不要覆蓋）以下內容：

```
cat >> ~/.ssh/config <<'EOF'

Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
EOF
chmod 600 ~/.ssh/config
```

### 複製公鑰到剪貼簿

```
pbcopy < ~/.ssh/id_ed25519.pub
cat ~/.ssh/id_ed25519.pub
```

## 刪除檔案

用 `trash 完整路徑` 移到垃圾桶（macOS 14 以後內建）。`which trash` 找不到這個指令的話，請學生自己在 Finder 把檔案拖到垃圾桶。

## 小技巧

- 在 Finder 顯示隱藏資料夾（例如 `.git`）：按 `Cmd + Shift + .`
- 「文件」資料夾的路徑是 `~/Documents`
