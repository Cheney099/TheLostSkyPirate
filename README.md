# The Lost Sky Pirate

Private production repository for scripts, prompts, storyboards, asset registries, and project skills.

## Two-person collaboration

- `main` is the stable shared branch. Do not use it as a working branch.
- Cheney works on `sync/Cheney/<scope>` branches.
- Vincent works on `sync/Vincent/<scope>` branches.
- One branch and one pull request should cover one episode or one clearly named asset batch.
- Before starting, agree who owns the episode or asset batch. Do not edit the same episode or registry file at the same time.
- Merge through a pull request after reviewing the changed-file list and checklist.

Full operating rules are in [AGENTS.md](AGENTS.md).

## Daily workflow

```bash
git switch main
git pull --ff-only origin main
git switch -c sync/YourName/EPxx-short-task

# Work, then stage only the files belonging to this task.
git add prompts/EPxx.md storyboards/EPxx.md segment_mapping/EPxx.md
git commit -m "EPxx: short description"
git push -u origin HEAD
```

Open a pull request into `main`, have the other person review it, then merge. After merging, delete the task branch and start the next task from the updated `main`.

## Repository boundaries

- Git tracks text deliverables and project instructions.
- Local video renders remain outside Git under `/videos/`.
- Do not force-add ignored images, videos, temporary exports, credentials, or caches.
- Asset registry entries stay as one JSON file per asset; avoid combining them into a shared monolithic JSON file.

## GitHub plan limitation

This private repository's current GitHub plan does not expose branch protection or repository rulesets. Until the plan is upgraded (or the repository becomes public), the pull-request requirement is a team rule rather than a server-enforced restriction.
