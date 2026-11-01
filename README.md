# mardu-docs

Produktdokumentation für Website und Software aus einer Quelle
(Fumadocs-MDX). Dieses Repository wird als Git-Submodule in die Consumer
eingehängt. Inhalte und Bilder werden hier gepflegt.

Die [Dokumentationsregeln](AGENTS.md) gelten auch für begleitende Dokumentation
im Software-Repository. [TODO.md](TODO.md) enthält Bestandsbewertung,
Prioritäten und den Arbeitsplan. Der
[Strukturvorschlag vom 1. November 2026](planning/2026-11-01-dokumentationsstruktur.md)
beschreibt den Zielbaum aller sechs Bereiche. Der erste nutzbare Stand der
Navigation und der neue Überblick sind im Software-Consumer umgesetzt.
Die [kritische Revision](planning/2026-11-01-dokumentationsstruktur-review.md)
begründet die korrigierte Aufgabenabdeckung. Weiterführende, noch nicht
ausgearbeitete Anleitungen bleiben geplant; die offenen Sachprüfungen bestehen weiter.
[BENUTZER-REVIEW.md](BENUTZER-REVIEW.md) hält den
Vergleich mit acht Dokumentationen und die Übernahme für Mardu fest. Der Auftrag vom 19. Oktober 2026 ergänzt die
Anleitungen zur Benutzeransicht des Webportals; die frühere Bestandsbewertung
und offene Aufgaben anderer Zielgruppen bleiben dort nachvollziehbar.

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

Der Bestand umfasst zum 1. November 2026 insgesamt 54 aktuelle MDX-Seiten und
die zwei historischen Einstiege, zusätzlich zur generierten API-Referenz des Consumers.
Der kuratierte Seitenbaum enthält davon 41 unterschiedliche handgeschriebene
Seiten einschließlich Wegweiser und Bereichsstarts. Das ist eine Navigationsauswahl,
keine vollständige Abnahme aller Produktfunktionen.
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
