---
name: workspace-setup
description: Set up the Open Learn workspace by cloning every openlearnapp org repo into a subfolder. Use when bootstrapping a fresh clone of the openlearnapp workspace, or when the user asks to "set up the workspace", "bootstrap", "clone all repos", or add newly created org repos. Idempotent — skips repos already present.
---

# Workspace Setup

Clones every repo of the [openlearnapp](https://github.com/openlearnapp) org into a
subfolder of this workspace, so all projects sit side by side. Safe to re-run: existing
clones are skipped, newly added org repos are picked up.

## Preconditions

- `gh` is authenticated — verify with `gh auth status`. If not, tell the user to run
  `gh auth login` (interactive — they must do it; suggest the `! gh auth login` prefix).
- SSH access to the org (clones use `git@github.com:` URLs).

## Steps

1. Confirm you are at the workspace root (the folder containing this repo's `README.md`
   and `.claude/`). Run all clones from there with absolute paths.

2. Clone every org repo except the `openlearnapp` workspace repo itself, skipping any
   that already exist (classic clones, SSH). Each repo that ends up in the workspace
   must also be listed in `.gitignore` — append it if missing, so the clones are never
   accidentally tracked:

   ```bash
   cd <workspace-root> || exit 1
   touch .gitignore
   gh repo list openlearnapp --limit 200 --json name --jq '.[].name' \
   | while read -r repo; do
       [ "$repo" = "openlearnapp" ] && continue          # never clone the workspace into itself
       if [ -d "$repo/.git" ]; then
         echo "SKIP $repo (exists)"
       else
         git clone -q "git@github.com:openlearnapp/$repo.git" "$repo" \
           && echo "OK   $repo" || { echo "FAIL $repo"; continue; }
       fi
       # ensure the repo is git-ignored by this workspace
       grep -qxF "/$repo/" .gitignore || echo "/$repo/" >> .gitignore
     done
   ```

3. If new entries were appended to `.gitignore`, keep them tidy (they belong under the
   "Cloned org repos" section). Committing the updated `.gitignore` is a normal docs/chore
   PR — the cloned repos themselves stay ignored and are never staged.

4. Report a short summary: how many repos cloned, skipped, failed, and whether
   `.gitignore` was updated. If anything failed, show the repo names and the likely cause
   (auth, SSH, network) — do not silently drop failures.

## Notes

- **Layout:** classic clones by default. Only use a worktree layout for a repo if that
  repo's own `CLAUDE.md` declares `## Setup default: worktree`.
- The cloned repos are independent git repos and are git-ignored by this workspace —
  never stage or commit them here.
- Re-run this skill any time to pull in repos added to the org since the last setup.
