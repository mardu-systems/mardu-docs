# Agentenbrief: Doku-Punkte am aktuellen Produkt überarbeiten

Projekt: `/Users/lucaschoeneberg/Documents/GitHub/mardu-rpi-api`.
Eigene Seiten stehen beim zugewiesenen Besitzer in `2026-11-03-gesamtrevision.json`.
Arbeite sie einzeln ab, ohne andere Dateien als die zugewiesenen Produktseiten,
eindeutig eigene neue Bilder und deinen eigenen Prüfbericht zu ändern.

Lies `web/content/docs/AGENTS.md`, `ARBEITSWEISE.md`, den Gesamtplan und deine
aktuellen Seiten. Muster: `administration/freigaben-verwalten.mdx` und
`administration/ressourcen-buchbarkeit.mdx`. Root-/Web-Regeln gelten zusätzlich.

Pro Seite:

1. Leserfrage, Vorwissen, Ausgangspunkt und sichtbares Ergebnis bestimmen.
2. Aktuelle UI-Komponenten, Übersetzungen und Backend-Verträge lesen. Vergleiche
   besonders geänderte Menüs, Rollen, Felder, Folgen und Fehlermeldungen. Alte
   Reviewberichte sind Hinweise, keine neue Verhaltensprüfung.
3. Wiederholungen und Implementierungsdetails ohne Nutzen entfernen. Belegbare
   Lücken schließen. Gute, aktuelle Seiten dürfen unverändert bleiben.
4. Danach Sprache und Darstellung glätten: kurze konkrete Überschriften, exakte
   UI-Namen, nachvollziehbarer Ablauf mit Ergebnis. Native Steps für echte Phasen,
   Tabellen für Vergleiche, Callouts für konkrete Folgen, ImageZoom für informative
   aktuelle Bilder. Keine Pflichtkomponente und keine Wortquote. Keine neuen
   Akkordeons für notwendige Inhalte; kein CSS und keine eigene Komponente.
5. Bestehende URLs, Heading-IDs und Verweise erhalten. Bei geändertem Heading
   den alten Anker mit vorhandenem `span`-Muster erhalten. Source-Snapshots liegen
   unter `/tmp/mardu-docs-revision-20261103/before/`, gerenderte IDs in
   `/tmp/mardu-docs-revision-20261103/baseline-render.json`.
6. Prüfe eigene Dateien mit `bun x --bun prettier --ignore-path /dev/null --check`
   (aus `web/`) und scoped `git diff --check`. Keine Tests schreiben, die nur
   redaktionelle Formulierungen festschreiben.
7. Schreibe einen kompakten Bericht je Seite in deinem Paketbericht
   `planning/reviews/2026-11-03-gesamtrevision/<besitzer>.md`: Entscheidung,
   Quellen mit konkreten Pfaden, Änderungen, Prüfergebnisse und Grenzen.

Melde dem Koordinator früh höchstens drei besonders nützliche Screenshot-Motive
mit UI-Route, Zustand und Beispieldaten. Ein isolierter Browserzugang wird zentral
vorbereitet. Bis dahin Codeabgleich und Textarbeit erledigen. Behaupte keine
Browser-, Hardware- oder Anbieterprüfung, die du nicht ausgeführt hast.

Andere Agenten bearbeiten andere Dateien im selben Checkout. Keine Stashes,
Resets, Commits, Worktrees, Subagenten, Builds oder Serverstarts. Keine gemeinsam
genutzten Metadaten, Übersetzungen, Softwaredateien oder Inventarstände ändern.
Bestätigte Produktfehler getrennt melden. Vorhandene uncommittete Änderungen an
Geräte- und Ressourcenzustandsanleitung stammen teilweise aus paralleler Arbeit;
ihre aktuellen Inhalte sind der Ausgangspunkt und dürfen nicht zurückgesetzt werden.
