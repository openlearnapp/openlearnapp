# Open Learn Workspace — Claude-Anweisungen

Dies ist der **Workspace-Bootstrap** für die [openlearnapp](https://github.com/openlearnapp)-Org.
Wer dieses Repo klont und Claude Code startet, erwartet, dass du den restlichen
Workspace einrichtest. Die menschenlesbare Struktur- und Repo-Übersicht steht im
[README](./README.md).

## Setup

Wenn der Nutzer den Workspace einrichten will ("Setup", "richte den Workspace ein",
"klone alle Repos") oder das offensichtlich ein frischer Klon ist:

→ Führe die Skill **`workspace-setup`** aus (`.claude/skills/workspace-setup/`).

Sie klont alle Org-Repos live aus `gh repo list openlearnapp` in Unterordner.
Idempotent: vorhandene Repos überspringen, das `openlearnapp`-Repo selbst nie klonen.

## Regeln

- Jedes Org-Repo ist ein **eigenständiger Git-Klon** in einem Unterordner und wird
  hier per Whitelist-`.gitignore` ignoriert — niemals als Submodule oder
  verschachtelten Commit einchecken.
- **Klassische Klone** als Default; Worktrees nur, wenn ein Repo das in seiner eigenen
  `CLAUDE.md` (`## Setup default`) empfiehlt.
- **PR-basiert**, nie direkt auf `main` pushen. Semantische Commits/PRs.
- Geteilte Skills/Configs liegen in `.claude/` und gelten für alle. Lokale, nicht zu
  teilende Einstellungen gehören in `.claude/settings.local.json` (git-ignoriert).
- Arbeit *innerhalb* eines geklonten Repos folgt dessen eigener `CLAUDE.md`.
