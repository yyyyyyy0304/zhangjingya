---
name: submit-github
description: Use when the user asks to 推送到GitHub, push to GitHub, commit and push to GitHub, or submit this coursework site to GitHub https://github.com/yyyyyyy0304/zhangjingya. Pushes to the github remote (already set up) in addition to Gitee origin.
---

# 推送到 GitHub (commit & push to GitHub)

Push the coursework site to `https://github.com/yyyyyyy0304/zhangjingya`. The repo keeps **two remotes**: `origin` → Gitee, `github` → GitHub.

## Current Remote Layout

```
origin  https://gitee.com/zjy115/zjy.git      (fetch/push)
github  https://github.com/yyyyyyy0304/zhangjingya.git  (fetch/push)
```

**Do NOT overwrite `origin`.**

## Steps

1. Check state first (from `D:\高级网页设计\site`):

   ```powershell
   git status --short
   git remote -v
   git log --oneline -5
   ```

2. If `github` remote is missing, add it:

   ```powershell
   git remote add github https://github.com/yyyyyyy0304/zhangjingya.git
   ```

   If it exists but points elsewhere, ask the user before rewriting.

3. Stage and commit (skip if nothing to commit):

   ```powershell
   git add -A
   git commit -m "提交网页设计练习到GitHub"
   ```

4. Push to GitHub (HTTPS, with SSL verification workaround for China network):

   ```powershell
   git -c http.sslVerify=false push github master
   ```

   > GitHub's SSL cert may fail verification on this network; the `-c http.sslVerify=false` flag skips that check for this single push command.

   If GitHub prompts for auth, complete it in the browser when Windows Credential Manager / GCM opens.

## Gotchas (Windows + PowerShell)

- Chinese filenames render as mojibake — display-only, not broken paths.
- **SSH (port 22) is blocked** on this network. HTTPS works with `sslVerify=false`.
- HTTPS push needs auth via GitHub's browser OAuth flow (GCM); the user must complete it when a browser window pops up.
- Never alter `origin` (Gitee). `github` is an **additional** remote.
- Nothing to commit → skip steps 3–4; report "无改动" instead of empty commits.
- Line endings: CRLF/UTF-8 without BOM.
