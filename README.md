# mardu-docs

Produktdokumentation für Website und Software aus einer Quelle
(Fumadocs-MDX). Dieses Repository wird als Git-Submodule in die Consumer
eingehängt. Inhalte und Bilder werden hier gepflegt.

Die [Dokumentationsregeln](AGENTS.md) und die
[Arbeitsweise](ARBEITSWEISE.md) gelten auch für begleitende Dokumentation im
Software-Repository. Der [Ergebnisbericht der Seitenrevision](planning/2026-11-01-seitenrevision-ergebnis.md)
enthält den aktuellen Umfang, Einzelprüfungen und Grenzen. Die anschließende
[Textverdichtung](planning/2026-11-01-distill.md) hält den jüngsten Textstand fest.
[Sidebar-Hierarchie](planning/2026-11-01-sidebar-hierarchie.md) beschreibt die
Gruppenüberschriften und Unterseiten. Die sechs Bereiche
sind im Software-Consumer erschlossen; offene praktische Abnahmen stehen im
[abgeglichenen Backlog](planning/offene-dokumentationsaufgaben.md).

[TODO.md](TODO.md), der [ursprüngliche Strukturplan](planning/2026-11-01-dokumentationsstruktur.md)
und seine [kritische Revision](planning/2026-11-01-dokumentationsstruktur-review.md)
halten die vorherige Bestandsbewertung und Planung fest.
[BENUTZER-REVIEW.md](BENUTZER-REVIEW.md) dokumentiert den Vergleich mit acht
Dokumentationen. Diese älteren Bewertungen sind nicht der aktuelle
Erledigungsstand der Seitenrevision.

## Mount-Punkte und Quelle

- Website: `mardu-systems/websites` → `apps/mardu-de/content`.
- Software: `mardu-systems/web` → `content/docs`; im übergeordneten
  Software-Repository unter `web/content/docs`.

Die Mounts enthalten dieses Repository. Die veröffentlichte Inhaltsquelle ist
sein Unterordner `docs/`. Der Software-Consumer liest ihn über
`lib/source.ts` als `content/docs/docs`. Die Konfiguration weiterer Consumer
muss vor einer Änderung separat geprüft werden.

## Vorhandene Struktur

```text
AGENTS.md                 # Dokumentationsregeln, keine Produktseite
README.md                 # Ablage und Pflege
ARBEITSWEISE.md            # Prozess für bestehende Funktionen und neue Anleitungen
TODO.md                   # Bestandsbewertung und Arbeitsplan, keine Produktseite
docs/
  index.mdx               # Wegweiser
  meta.json               # Bereiche der Navigation
  ueberblick/
  administration/
  benutzer/
  koordination/
  installieren/
  entwickeln/
```

Die aktuellen Inhalte sind nach Zielgruppen und Aufgaben geordnet. Die früheren
Website-Adressen unter `v1/` und `v2/` bleiben als historische Einstiege erhalten
und verweisen auf die Dokumentationsübersicht. Sie bezeichnen keinen freigegebenen
Softwarestand und stehen nicht in der aktuellen Navigation. Eine spätere
Release-Versionierung wird erst nach Prüfung der Consumer eingeführt.

Der Bestand umfasst zum 1. November 2026 nach der Seitenrevision insgesamt
67 aktuelle MDX-Seiten und zwei historische Einstiege, zusätzlich zur generierten
API-Referenz des Consumers. Der kuratierte Seitenbaum erschließt alle 67 aktuellen
handgeschriebenen Seiten einschließlich Wegweiser und Bereichsstarts.
Das belegt die Inhaltsabdeckung dieser Seiten, keine vollständige praktische
Abnahme aller Produktfunktionen. Die
[Seitenrevision](planning/2026-11-01-seitenrevision.md) dokumentiert einzelne
Agentenaufträge, Quellenbelege, Änderungen und offene Prüfungen.
Die Benutzeranleitungen decken Einstieg,
Dashboard, Ressourcen und Freigaben, Berechtigungsanfragen, Buchungen,
Kalender, Qualifikationen, Posteingang und die persönlichen Profilbereiche ab.
Bestehende Profil-URLs unter `ueberblick/` bleiben erhalten. Im Software-Consumer
gehören sie zum Fokus **Benutzer** und stehen dort unter persönlichen Aufgaben
beziehungsweise im Zweig **Profil und Einstellungen**.
Die vorhandene Anleitung zu Systemmetriken gehört zum Verwaltungsfokus;
das persönliche Dashboard hat eine eigene Anleitung.

Jeder Bereich hat eine `index.mdx` und eine `meta.json`. Bilder liegen im
zugehörigen `bilder/`-Ordner. Der Software-Consumer ergänzt die API-Referenz
aus OpenAPI; generierte API-Seiten werden hier nicht von Hand gepflegt.

## Seite erstellen oder ändern

Die [Arbeitsweise](ARBEITSWEISE.md) beschreibt zwei Wege: vorhandene Funktionen
und Dokumentation überarbeiten oder eine neue Anleitung anlegen. Beide beginnen
mit Aufgabe, Ergebnis und Quellen und enden mit passenden Prüfungen.

Neue Entwürfe liegen außerhalb von `docs/`. `meta.json` listet nur nutzbare
Inhalte; reine Schreibaufträge bleiben außerhalb der Navigation. Bestehende,
ausgeblendete Seiten behalten ihre URLs. Im Software-Consumer berücksichtigt die
Veröffentlichungsliste auch Suche und LLM-Index. Relative Metadateneinträge und
`pagesIndex` ermöglichen andere Navigationsorte ohne neue Inhaltskopien.

Aus brauchbaren Anleitungen entfernte Schreibaufträge stehen unter
[offene Dokumentationsaufgaben](planning/offene-dokumentationsaufgaben.md).
Das Verschieben bedeutet keine Erledigung der Aufgabe.

## Consumer-Stände

Bei einer Änderung gehören die Inhalte ins Docs-Repository und bei einem
autorisierten Release der passende Submodule-Verweis in den Consumer. Software,
Website und Dokumentation müssen auf einen zueinander passenden Stand zeigen.

Eine Inhaltsänderung ist kein Auftrag für Commit, Push, Submodule-Bump oder
Veröffentlichung. Die Website wurde in der Bestandsaufnahme vom 10. Oktober 2026
nicht ausgeführt.

## Hinweise

- Planungsdateien, Agentenanweisungen und README bleiben außerhalb von
  `docs/`: Markdown/MDX darin wird als Produktinhalt geladen.
- UI-Texte der Doku-Oberfläche gehören zum jeweiligen Consumer.
- Noch fehlende Dokumentations- oder Linkprüfungen als Grenze nennen;
  keine nicht vorhandenen CI-Prüfungen behaupten.
