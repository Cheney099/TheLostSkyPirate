# AGENTS.md - Collaboration contract

This repository is maintained by Cheney and Vincent, often through Codex or other coding agents. Every person and agent must read this file before editing, generating, deleting, committing, or pushing files.

## 1. Branch and pull-request rule

- Treat `main` as stable and read-only for daily work.
- Create branches from the latest `origin/main`:
  - `sync/Cheney/<scope>`
  - `sync/Vincent/<scope>`
- Keep one episode or one clearly named asset batch per branch and pull request.
- Do not push ordinary production changes directly to `main`.
- The person who did not author the pull request reviews it before merge.
- Pull-request title: `EPxx: <work>` or `Assets: <batch>`.

Because GitHub branch protection is unavailable for this private repository on the current plan, these rules are enforced by the two maintainers and the pull-request checklist.

## 2. Ownership and parallel work

- Before work starts, Cheney and Vincent agree who owns each episode or asset batch.
- Only the owner edits that episode's files across `prompts/`, `storyboards/`, and `segment_mapping/` until the pull request is merged.
- Do not make drive-by edits to the other person's episode.
- If a task crosses episode boundaries, split it into separate pull requests whenever practical.
- If both people need the same file, choose one temporary owner; the other person sends notes instead of editing it concurrently.

## 3. Shared-file conflict rules

- Prefer one file per episode and one JSON file per asset. This is the repository's main conflict-avoidance mechanism.
- Never reformat, reorder, or mechanically rewrite unrelated registry files.
- For future `*.jsonl` logs, append one complete JSON object per line; never reorder or pretty-print the file. `.gitattributes` uses Git's union merge driver so independent appended lines are retained.
- Ordinary `*.json` files are not append-only and do not use union merge. If both branches changed the same JSON file, stop and review it manually.
- Before committing registry changes, validate every changed JSON file.

PowerShell validation example:

```powershell
$files = git diff --name-only --cached -- '*.json'
foreach ($file in $files) { Get-Content -LiteralPath $file -Raw | ConvertFrom-Json | Out-Null }
Write-Output 'JSON OK'
```

## 4. Safe sync sequence

Before opening or updating a pull request:

```bash
git fetch origin
git merge origin/main
```

- Resolve conflicts only in files owned by the current task.
- Never resolve a conflict by blindly choosing all local or all remote files.
- Preserve both sides when two contributors appended independent records.
- After syncing, inspect `git status` and the pull-request file list again.

## 5. Files that must not be committed

- Video renders and other ignored binary outputs
- Credentials, tokens, login state, or local configuration containing secrets
- Temporary exports, caches, debug logs, and machine-specific files
- Unrelated changes from another episode or another contributor's task

Do not use force-add to bypass `.gitignore` unless both maintainers explicitly agree that the file belongs in Git.

## 6. Pull-request merge checklist

The reviewer confirms:

- Scope matches one episode or one asset batch.
- No unrelated files are included.
- Changed JSON files parse successfully.
- No media, cache, temporary output, or secret is included.
- Prompt, storyboard, segment mapping, and registry references remain consistent.
- Any same-file conflict was manually reviewed.

Use squash merge for normal task branches so `main` keeps one clear commit per pull request.
