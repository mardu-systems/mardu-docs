# mardu-docs

Zentrale Produkt-Dokumentation für Website und Software aus einer Quelle
(Fumadocs-MDX). Dieses Repo wird als **Git-Submodule** in die
Consumer-Repos eingehängt – Inhalte hier pflegen, nie in den Consumern.

## Mount-Punkte

- Website: `mardu-systems/websites` → `apps/mardu-de/content`
- Software: Software-Repo → `content/docs` bzw. `content` (siehe dort)

Beide Mounts zeigen auf `docs/` in diesem Repo; die Consumer lesen ab
`content/docs` (Fumadocs `dir`).

## Struktur

```
./
  README.md          # diese Datei
  docs/
    meta.json        # Wurzel: listet nur index + Versionsordner
    index.mdx        # Landing (/docs) mit Versionswahl
    v2/meta.json     # { "title": "v2", "root": "version", "pages": [...] }
    v2/*.mdx         # aktuelle Inhalte
    v1/meta.json     # vorheriger Stand, nur noch bei Bedarf pflegen
    v1/*.mdx
```

Versionierung folgt dem Fumadocs-Prinzip **Root Type**: Jeder Ordner mit
`"root": "version"` ist eine austauschbare Version, die Website rendert
automatisch einen Versions-Switcher (`/docs/v1/...` ↔ `/docs/v2/...`).

## Neue Seite anlegen

1. `docs/vX/mein-thema.mdx` mit `title` + `description` im Frontmatter
   (kein `# H1` im Body – der Titel kommt aus dem Frontmatter).
2. Rolle als Sidebar-Icon setzen (`icon:` mit Lucide-Name):
   `ShieldCheck` (Administration), `Users` (Benutzer), `Wrench`
   (Installieren), `Code2` (Entwickeln), `CalendarClock` (Koordination),
   `BookOpen` (alle). Consumer färben danach ein.
3. Dateiname (ohne Endung) in `docs/vX/meta.json` unter `pages` eintragen.
4. Commit + Push hier, danach Submodule-Bump in den Consumern
   (Website zeigt die Seite automatisch in Sidebar, TOC und Suche).

## Neue Version anlegen (z. B. v3)

1. `docs/v2/` nach `docs/v3/` kopieren, Inhalte anpassen.
2. `title` in `v3/meta.json` auf `"v3"` setzen.
3. `v3` in Wurzel-`meta.json` **vor** `v2` in `pages` eintragen (neueste zuerst).
4. Tag setzen (`docs-v3.0.0`); Software-Release pinnt den passenden Tag,
   die Website zeigt alle Versionen an.

## Consumer-Update (Submodule-Bump)

```bash
# im Consumer-Repo, im Submodule-Ordner:
git fetch origin && git checkout docs-vX.Y.Z
# danach im Consumer:
git add <submodule-pfad> && git commit -m "chore(docs): bump ..."
```

## Hinweise

- Kein `README.md` (oder andere Nicht-Content-Dateien) unter `docs/`
  ablegen – jede `.md`/`.mdx`-Datei dort wird eine öffentliche Seite.
- UI-Strings der Doku-Oberfläche (Deutsch) liegen beim Consumer
  (Website: `apps/mardu-de/lib/docs-i18n.ts`), nicht hier.
