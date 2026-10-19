# mardu-docs

Produktdokumentation für Website und Software aus einer Quelle
(Fumadocs-MDX). Dieses Repository wird als Git-Submodule in die Consumer
eingehängt. Inhalte und Bilder werden hier gepflegt.

Die [Dokumentationsregeln](AGENTS.md) gelten auch für begleitende Dokumentation
im Software-Repository. [TODO.md](TODO.md) enthält Bestandsbewertung,
Prioritäten und den Arbeitsplan. [BENUTZER-REVIEW.md](BENUTZER-REVIEW.md) hält den
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

Der Bestand umfasst 48 aktuelle MDX-Seiten und die zwei historischen Einstiege.
Die Benutzeranleitungen decken Einstieg,
Dashboard, Ressourcen und Freigaben, Berechtigungsanfragen, Buchungen,
Kalender, Qualifikationen, Posteingang und die persönlichen Profilbereiche ab.
Bestehende Profil-URLs unter `ueberblick/` bleiben erhalten. Im Software-Consumer
gehören sie zum Fokus **Benutzer** und bleiben aus **Überblick** erreichbar.
Die vorhandene Anleitung zu Systemmetriken gehört zum Verwaltungsfokus;
das persönliche Dashboard hat eine eigene Anleitung.

Jeder Bereich hat eine `index.mdx` und eine `meta.json`. Bilder liegen im
zugehörigen `bilder/`-Ordner. Der Software-Consumer ergänzt die API-Referenz
aus OpenAPI; generierte API-Seiten werden hier nicht von Hand gepflegt.

## Seite erstellen oder ändern

1. Vorhandene Seiten und die [Regeln](AGENTS.md) lesen; Zielgruppe und
   Hauptzweck festlegen.
2. Die Seite im passenden Bereich unter `docs/` mit `title` und
   `description` im Frontmatter pflegen. Kein zusätzliches H1 im Inhalt.
3. Neue Seite in der passenden `meta.json` und gegebenenfalls in der
   Rollen-/Slugliste des Consumers aufnehmen. Bestehende URLs erhalten.
4. Verhalten mit UI und Backend prüfen; vorhandene Begriffe, Verträge und
   Anleitungen wiederverwenden. Unfertige Inhalte als Entwurf kennzeichnen.
5. Links, Anker, Bilder, MDX und die gerenderte Consumer-Seite prüfen.
   Den Arbeitsplan erst nach Abnahme aktualisieren.

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
