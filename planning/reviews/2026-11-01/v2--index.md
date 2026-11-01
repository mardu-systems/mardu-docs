# P49: Historischer Einstieg v2

**Entscheidung: unverändert gut.**

Leserfrage: Was bedeutet die alte Adresse `/docs/v2`, und wo stehen die aktuellen
Anleitungen? Vorwissen ist nicht erforderlich. Die Seite dient als historischer
Einstieg außerhalb der sichtbaren Aufgabennavigation und beantwortet diese Frage
bereits klar. Kein Produktpatch nötig.

## Befunde und Quellen

- `web/content/docs/docs/v2/index.mdx:1–8`: Titel und Beschreibung kennzeichnen
  den historischen Einstieg. Der Text schließt einen veröffentlichten Softwarestand
  ausdrücklich aus und verweist mit `../index.mdx` auf die aktuelle Übersicht.
  URL, Frontmatter und Text bleiben erhalten. Keine zusätzlichen Überschriften,
  expliziten Anker oder Bilder vorhanden.
- `web/content/docs/docs/index.mdx`: Das Linkziel erschließt die sechs
  Aufgabenbereiche und erklärt deren Bedeutung als Lesereinstiege.
  `web/content/docs/docs/v1/index.mdx` verwendet denselben historischen Hinweis.
- `web/content/docs/docs/meta.json:3–10`: Die ausdrückliche Veröffentlichungsliste
  führt die Übersicht und sechs Aufgabenbereiche, keinen Eintrag `v2`.
  `web/content/docs/docs/v2/meta.json:2–4` enthält das historische
  `root: "version"`; der native Loader zeigt diesen Zweig nicht im Seitenbaum.
  Beide Metadatendateien nur gelesen; keine neue Versionsnavigation.
- `web/lib/source.ts:13–14,36–51`: Der vorhandene Fumadocs-Loader liest die
  Dokumentationsquelle unter `/docs`, erzeugt keinen Fallback-Baum und begrenzt
  Suche/LLM-Index auf die Veröffentlichungsliste.
  `web/app/docs/[[...slug]]/page.tsx` verwendet `source.getPage` für direkte
  Aufrufe und `createRelativeLink` für MDX-Verweise. Metadaten übernehmen Titel
  und Beschreibung aus der Seite.
- `web/tests/lib/docs-roles.test.ts:16–44`: Das vorhandene Muster zum Einlesen
  der MDX-Dateien und Metadaten wurde für die begrenzte Loader-Prüfung verwendet.
  Der offene Dokumentationsbacklog enthält keinen Auftrag zu `v2`.

## Eigene Checks und Grenzen

- Read-only-Prüfung mit Bun und dem installierten `fumadocs-core`: Alle
  MDX-Dateien und Metadaten wie im vorhandenen Navigationstest geladen.
  `/docs/v2` wird mit dem Titel „Übersicht v2“ aufgelöst. `/docs` ist vorhanden
  und im Seitenbaum sichtbar. `resolveHref('../index.mdx', page)` ergibt exakt
  `/docs`. Weder die v2-Seite noch ein v2-Ordner erscheinen im sichtbaren Baum.
- Dateibezogene Formatprüfung mit vorhandenem Prettier und
  `--ignore-path /dev/null`; dateibezogenes `git diff --check`.
- Ausschließlich statische und native Loader-Prüfung. Kein Browser, Build,
  Hardware- oder Anbietercheck; keine praktische Abnahme behauptet.
  Der Koordinator übernimmt die gemeinsame Consumer-Prüfung der alten URL,
  des Übersichtslinks und der Navigation. Der Website-Consumer wurde nicht
  ausgeführt.

Kein weiterer Seitenbedarf oder Navigationspatch. Keine API-/DTO-Änderung und
keine entsprechende Dokumentationsanpassung. Offene Grenze bleibt die gemeinsame
Browserprüfung beider Consumer; kein belegter Produktfehler.

Geänderte Datei: ausschließlich
`web/content/docs/planning/reviews/2026-11-01/v2--index.md`.
Die Produktseite `web/content/docs/docs/v2/index.mdx` bleibt unverändert.
