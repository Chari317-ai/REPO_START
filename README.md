# git-github-tutor

一個給 **Codex** 用的 skill：讓 Codex 變成你的 Git 家教，一步一步帶你完成：

1. 安裝 Git
2. 用 SSH 金鑰綁定你的 GitHub 帳號
3. 在電腦上開一個 repo
4. 在 GitHub 上開 repo，跟電腦連起來並推送上去
5. （選修）用 GitHub Pages 把網頁發布上線

Mac 和 Windows 都能用。每一步都會先用白話解釋在做什麼，需要你自己動手的地方（例如登入 GitHub）會停下來告訴你怎麼做。

## 開始前

先註冊一個 GitHub 帳號：https://github.com/signup

## 安裝

### 最簡單：請 Codex 幫你裝

在 Codex 裡輸入：

> 請幫我安裝這個 skill 到 ~/.agents/skills：https://github.com/Chari317-ai/git-github-tutor

### 自己貼指令安裝

**Mac**（打開「終端機」App 貼上）：

```
mkdir -p ~/.agents/skills && curl -L https://github.com/Chari317-ai/git-github-tutor/archive/refs/heads/main.tar.gz | tar -xz -C ~/.agents/skills --strip-components=2 git-github-tutor-main/skills/git-github-tutor
```

**Windows**（打開 PowerShell 貼上）：

```
$zip = "$env:TEMP\git-github-tutor.zip"
Invoke-WebRequest https://github.com/Chari317-ai/git-github-tutor/archive/refs/heads/main.zip -OutFile $zip
Expand-Archive $zip -DestinationPath "$env:TEMP\git-github-tutor" -Force
New-Item -ItemType Directory -Force "$HOME\.agents\skills" | Out-Null
Copy-Item "$env:TEMP\git-github-tutor\git-github-tutor-main\skills\git-github-tutor" "$HOME\.agents\skills\" -Recurse -Force
```

裝好後，**關掉再重開 Codex**。

## 使用

在 Codex 裡輸入以下任一種：

- `$git-github-tutor`（輸入 `$` 會跳出 skill 清單可以選）
- 或直接說：「教我裝 Git，然後把專案放上 GitHub」

接著跟著 Codex 的指示一步一步做就好。

## 檔案結構

```
skills/git-github-tutor/
├── SKILL.md                 主流程與教學原則
└── references/
    ├── mac.md               Mac 專用指令
    ├── windows.md           Windows 專用指令
    └── github-pages.md      選修：發布網頁
```
