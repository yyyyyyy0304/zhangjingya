---
name: submit-github
description: Use when the user asks to 推送到GitHub, push to GitHub, commit and push to GitHub, or submit this coursework site to GitHub https://github.com/yyyyyyy0304/zhangjingya. Adds a github remote alongside origin (Gitee), stages, commits, and pushes to the GitHub remote.
---

# 推送到 GitHub (commit & push to GitHub)

Push the coursework site to `https://github.com/yyyyyyy0304/zhangjingya` in **addition to** the existing Gitee remote.

## Important: Two-Remote Setup

The repo already has `origin` → Gitee (`https://gitee.com/zjy115/zjy.git`). **Do NOT overwrite `origin`.** Add a **separate** remote named `github`.

## Steps

1. Check state first (from the project root `D:\高级网页设计\site`):

   ```powershell
   git status --short
   git remote -v
   git log --oneline -5
   ```

2. Ensure the GitHub remote exists:

   ```powershell
   git remote add github git@github.com:yyyyyyy0304/zhangjingya.git
   ```

   If `github` already exists, **do NOT rewrite it** — ask the user first.

   The SSH URL is used because the user has already set up an SSH public key for GitHub authentication.

3. Stage everything (skip if `git status --short` shows nothing to commit):

   ```powershell
   git add -A
   ```

4. Commit only if there are staged changes:

   ```powershell
   git commit -m "提交网页设计练习到GitHub"
   ```

   If `user.name`/`user.email` are unset, set them locally (ask the user for values) — never edit global git config.

5. Push to GitHub:

   ```powershell
   git push github master
   ```

   The GitHub repo is empty and this will be the first push. If GitHub's default branch is `main`, retry with `git push github master:main` only after confirming with the user.

## Gotchas (Windows + PowerShell)

- Chinese filenames render as mojibake in the console — display-only, not broken paths. Do not "fix" encoding.
- SSH push relies on the user's SSH agent/key already configured; if push fails with SSH auth error, have the user run `ssh -T git@github.com` to verify, or push manually.
- Never alter the existing `origin` (Gitee) remote. The GitHub remote is **additional**.
- Nothing to commit → skip steps 3–4 and just run push if needed; report "无改动" instead of creating empty commits.
- Line endings: CRLF/UTF-8 without BOM; do not add `.gitattributes` unless asked.
