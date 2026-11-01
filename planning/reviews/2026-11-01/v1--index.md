# P48: Historischer Einstieg v1

**Entscheidung: unverändert gut.**

Leserfrage: Was bedeutet die alte Adresse `/docs/v1`, und wo finde ich die
aktuellen Anleitungen? Vorwissen ist nicht erforderlich. Die Seite bleibt ein
historischer Einstieg außerhalb der sichtbaren Aufgabennavigation. Ergebnis der
Prüfung: Hinweis und Verweis erfüllen diesen Zweck; kein Produktpatch nötig.

## Befunde und Quellen

- `web/content/docs/docs/v1/index.mdx:1–8`: Titel und Beschreibung kennzeichnen
  den historischen Einstieg. Der Text schließt einen veröffentlichten Softwarestand
  ausdrücklich aus und verlinkt mit `../index.mdx` die aktuelle Übersicht.
  URL, Text und Link bleiben erhalten. Es gibt keine zusätzlichen Überschriften,
  expliziten Anker oder Bilder.
- `web/content/docs/docs/index.mdx:6–22`: Das Linkziel erschließt die sechs
  Aufgabenbereiche und bezeichnet sie als Lesereinstiege.
- `web/content/docs/docs/meta.json:3–10`: Die ausdrückliche Veröffentlichungsliste
  enthält die Übersicht und sechs Aufgabenbereiche, keinen Eintrag `v1`.
  `web/content/docs/docs/v1/meta.json:2–4` trägt zwar das historische
  `root: "version"`, ist aber kein sichtbarer Hauptnavigationszweig. Keine
  Versionsnavigation ergänzen; beide Metadatendateien nur gelesen.
- `web/lib/source.ts:13–14,36–51`: Der bestehende Loader liest alle Seiten,
  erzeugt keinen Fallback-Baum und begrenzt Suche/LLM-Index auf die Navigation.
  `web/app/docs/[[...slug]]/page.tsx:48–51,91–95` löst direkte Seitenaufrufe über
  `source.getPage` und relative MDX-Verweise über `createRelativeLink` auf.
- `web/lib/docs-roles.tsx` und `web/components/docs-shell.tsx:21–30`: Die sechs
  bestehenden Bereiche und die Baumfilter werden wiederverwendet. Für `v1`
  wird kein neuer Bereich eingeführt.

## Eigene Checks und Grenzen

- Mit Bun und dem installierten `fumadocs-core` die vorhandene
  Metadaten-/Seitenquelle wie im Navigationstest geladen: `/docs/v1` wird
  aufgelöst, erscheint nicht im sichtbaren Seitenbaum; `/docs` wird aufgelöst
  und erscheint im Seitenbaum. Der relative Link zeigt auf die vorhandene
  Datei `docs/index.mdx`.
- Formatprüfung beider eigenen Dateien mit dem vorhandenen Prettier und
  `--ignore-path /dev/null`; dateibezogenes `git diff --check`.
- Ausschließlich statische und Loader-Prüfung. Keine Browserabnahme, kein Build,
  keine Hardware-/Anbieterprüfung. Der Koordinator übernimmt die gemeinsame
  Consumer-Prüfung: alte URL öffnen, Übersicht verlinken, keine sichtbare
  Versionsauswahl. Der Website-Consumer wurde hier nicht ausgeführt.

Kein weiterer Seitenbedarf oder Navigationspatch. Keine API-/DTO-Änderung und
keine entsprechende Dokumentationsanpassung. Offene Grenze bleibt die gemeinsame
Browserprüfung beider Consumer; kein belegter Produktfehler.

Geänderte Datei: ausschließlich
`web/content/docs/planning/reviews/2026-11-01/v1--index.md`.
Die Produktseite `web/content/docs/docs/v1/index.mdx` bleibt unverändert.
