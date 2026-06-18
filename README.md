# Open Learn — Workspace

**Einstiegspunkt für die gesamte [openlearnapp](https://github.com/openlearnapp)-Organisation.**

Dieses Repo ist der *Workspace-Bootstrap*: Du klonst nur dieses eine Repo, startest
Claude Code, und Claude richtet den restlichen Workspace ein — alle Org-Repos werden
in Unterordner geklont. Welche Repos es gibt, wofür sie sind und wie das Setup läuft,
steht hier.

## Quick Start

```bash
git clone git@github.com:openlearnapp/openlearnapp.git
cd openlearnapp
claude            # Claude Code starten
```

Dann in Claude Code:

> Richte den Workspace ein.

Claude liest `CLAUDE.md`, führt die `workspace-setup`-Skill aus (`.claude/skills/`)
und klont alle Org-Repos. Das Setup ist **idempotent** — schon vorhandene Repos werden
übersprungen, neue Org-Repos beim erneuten Lauf ergänzt.

Voraussetzungen: `git`, [`gh`](https://cli.github.com/) (authentifiziert: `gh auth login`),
SSH-Zugriff auf die Org.

## Workspace-Struktur

```
openlearnapp/                 # dieses Repo — Workspace-Bootstrap
  README.md                   # du bist hier
  CLAUDE.md                   # Anweisungen für Claude Code
  .claude/
    settings.json             # geteilte Claude-Config für alle
    skills/
      workspace-setup/        # Skill: klont alle Org-Repos
  <repo>/                     # je ein eigenständiger Git-Klon pro Org-Repo
                              # (vom Setup angelegt, hier git-ignoriert)
```

Jedes Org-Repo ist ein **eigenständiger Git-Klon** in einem Unterordner. Dieses
Bootstrap-Repo trackt nur die Workspace-Doku und `.claude/` — die Klone selbst werden
per Whitelist-`.gitignore` ignoriert (keine Submodule).

## Repos

| Repo | Zweck |
|------|-------|
| [`openlearnapp.github.io`](https://github.com/openlearnapp/openlearnapp.github.io) | Open Learn — Haupt-App (Vue 3, Vite, Tailwind), früher `open-learn` |
| [`content-engine`](https://github.com/openlearnapp/content-engine) | Werkzeug-Repo: automatisierte Bild-/Video-Produktion mit ComfyUI (lokal) |
| [`workshop-video-engine`](https://github.com/openlearnapp/workshop-video-engine) | Workshop-Video-Engine |
| [`concept-paid-workshops`](https://github.com/openlearnapp/concept-paid-workshops) | Konzept: bezahlte Workshops |
| [`team`](https://github.com/openlearnapp/team) | Team-/Org-Profil |
| [`workshop-english`](https://github.com/openlearnapp/workshop-english) | Workshop: Englisch aus dem Deutschen — 10 Verb-Lektionen, 30 Kernverben |
| [`workshop-spanish`](https://github.com/openlearnapp/workshop-spanish) | Workshop: Spanisch lernen |
| [`workshop-portugiesisch`](https://github.com/openlearnapp/workshop-portugiesisch) | Workshop: Portugiesisch |
| [`workshop-arabisch`](https://github.com/openlearnapp/workshop-arabisch) | Workshop: Arabisch |
| [`workshop-farsi`](https://github.com/openlearnapp/workshop-farsi) | Workshop: Farsi |
| [`workshop-milas-abenteuer`](https://github.com/openlearnapp/workshop-milas-abenteuer) | Workshop: Milas Abenteuer (Kinder-Lerngeschichte) |
| [`workshop-AI-im-Journalismus`](https://github.com/openlearnapp/workshop-AI-im-Journalismus) | Workshop: KI im Journalismus — KI-Tools in der journalistischen Praxis |
| [`workshop-linux-grundlagen`](https://github.com/openlearnapp/workshop-linux-grundlagen) | Workshop: Linux Grundlagen — 12 Lektionen |
| [`workshop-linux-grundlagen-preview`](https://github.com/openlearnapp/workshop-linux-grundlagen-preview) | Preview-Build für Linux-Grundlagen |
| [`workshop-docker`](https://github.com/openlearnapp/workshop-docker) | Workshop: Docker — Container-Grundlagen |
| [`workshop-k0rdent`](https://github.com/openlearnapp/workshop-k0rdent) | Workshop: k0rdent — Kubernetes Management (12 Lektionen, 4 Sprachen) |
| [`plugin-workshop-creator`](https://github.com/openlearnapp/plugin-workshop-creator) | Plugin: Workshop Creator für Claude Code |
| [`open-community`](https://github.com/openlearnapp/open-community) | Open Learn + Service Agent zu einer Open Community verbinden |

> Die Liste ist nicht hartcodiert: Das Setup zieht die aktuelle Repo-Liste live aus der
> Org (`gh repo list openlearnapp`), sodass neue Repos automatisch dazukommen.

## Konventionen

- **Klassische Klone** als Default. Worktrees nur, wo ein Repo das in seiner eigenen
  `CLAUDE.md` (`## Setup default`) empfiehlt.
- Klonen per **SSH**: `git clone git@github.com:openlearnapp/<repo>.git`
- **PR-basiert**, nie direkt auf `main`. Semantische Commits (`feat:`, `fix:`, `docs:`, `chore:`).
- Repo-Klone werden hier **nie** als Submodule oder verschachtelte Commits eingecheckt.
