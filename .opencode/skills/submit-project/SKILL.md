---
name: submit-project
description: Use when the user asks to 提交项目, 提交/上传/推送代码, commit and push, or submit this coursework site to Gitee https://gitee.com/zjy115/zjy. Stages everything, commits, and pushes to the Gitee remote.
---

# 提交项目 (commit & push to Gitee)

Push the whole coursework site to `https://gitee.com/zjy115/zjy`.

## Steps

1. Check state first (from the project root `D:\高级网页设计\site`):

   ```powershell
   git status --short
   git remote -v
   git log --oneline -5
   ```

2. Ensure the remote exists (repo has zero commits and may have no remote yet):

   ```powershell
   git remote add origin https://gitee.com/zjy115/zjy.git
   ```

   If `origin` already exists but points elsewhere, do NOT rewrite it — ask the user first.

3. Stage everything (the site is coursework, nothing secret lives in it):

   ```powershell
   git add -A
   ```

   Never stage credentials or keys; re-check `git status` if any unexpected file appears.

4. Commit. Write a short Chinese message; include the prompt-log rule compliance (`zhang_prompt.md` is committed along with everything else):

   ```powershell
   git commit -m "提交网页设计练习"
   ```

   If the commit fails because `user.name`/`user.email` are unset, set them locally (ask the user for the values) — never edit global git config.

5. Push. First push of an unborn `master` branch:

   ```powershell
   git push -u origin master
   ```

   If the remote default branch is `main` and rejects the push, retry with `git push -u origin master:main` only after confirming with the user.

## Gotchas (Windows + PowerShell)

- Chinese filenames render as mojibake in the console (`core.quotepath` unset); that is display-only, not broken paths. Do not "fix" encoding or rename files.
- HTTPS push to Gitee needs credentials; if the push fails with auth error, tell the user to enter their Gitee username/token when Windows Credential Manager prompts, or run `git push -u origin master` themselves. Never hardcode tokens into any file.
- Re-running the skill when there is nothing to commit is fine — report "无改动" instead of creating empty commits.
- Line endings: repo files are CRLF/UTF-8 without BOM; do not add `.gitattributes` or renormalize unless asked.
