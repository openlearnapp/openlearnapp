# Open Learn Platform — Workspace

GitHub Organisation: https://github.com/openlearnapp

Meta-Repo / Workspace für **alle** Repos der openlearnapp-Org. Jedes Repo ist ein
eigenständiger Git-Klon in einem Unterordner; dieses Meta-Repo trackt nur die
Workspace-Doku (CLAUDE.md, `*.md`, `docs/`) und git-ignoriert die Repo-Klone selbst
(Whitelist-`.gitignore`).

## Struktur

```
openlearnapp/
  .gitignore            # Whitelist — ignoriert alles, erlaubt Workspace-Doku
  CLAUDE.md             # diese Datei
  docs/                 # Workspace-übergreifende Notizen
  <repo>/               # je ein eigenständiger Git-Klon pro Org-Repo
```

## Repos

| Repo | Description |
|------|-------------|
| `openlearnapp.github.io` | Open Learn — Main app (Vue 3, Vite, Tailwind), formerly `open-learn` |
| `content-engine` | Werkzeug-Repo: automatisierte Bild-/Video-Produktion mit ComfyUI (lokal) |
| `workshop-video-engine` | Workshop-Video-Engine |
| `concept-paid-workshops` | Konzept: bezahlte Workshops |
| `team` | Team-/Org-Profil |
| `workshop-english` | Workshop: Learn English from German — 10 verb lessons, 30 core verbs |
| `workshop-spanish` | Workshop: Spanisch lernen |
| `workshop-portugiesisch` | Workshop: Portugiesisch |
| `workshop-arabisch` | Workshop: Arabisch |
| `workshop-farsi` | Workshop: Farsi |
| `workshop-milas-abenteuer` | Workshop: Milas Abenteuer (Kinder-Lerngeschichte) |
| `workshop-AI-im-Journalismus` | Workshop: KI im Journalismus — KI-Tools in der journalistischen Praxis |
| `workshop-linux-grundlagen` | Workshop: Linux Grundlagen — 12 Lektionen |
| `workshop-linux-grundlagen-preview` | Preview-Build für Linux-Grundlagen |
| `workshop-docker` | Workshop: Docker — Container Grundlagen |
| `workshop-k0rdent` | Workshop: k0rdent — Kubernetes Management (12 Lektionen, 4 Sprachen) |
| `plugin-workshop-creator` | Plugin: Workshop Creator für Claude Code |
| `open-community` | Combine Open Learn and Service Agent for an Open Community |

## Konventionen

- Repo-Klone sind eigenständige Git-Repos und werden hier git-ignoriert — nie als
  Submodule oder verschachtelte Commits einchecken.
- Klonen per SSH: `git clone git@github.com:openlearnapp/<repo>.git`
- Setup-Layout pro Repo: klassischer Klon (Default). Worktrees nur, wo ein Repo das
  in seiner eigenen CLAUDE.md (`## Setup default`) empfiehlt.
- Neue Org-Repos: hier klonen und in der Tabelle oben ergänzen.
