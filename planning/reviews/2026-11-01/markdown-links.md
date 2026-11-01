# Markdown-Links im Software-Consumer

Änderungsbrief: Die Markdown-Ausgaben für Leser und Agenten sollen interne
MDX-Seitenlinks als öffentliche `/docs/...`-URLs ausgeben. Der vorhandene
Fumadocs-Export erhält solche Links bisher als Quelltext, auch innerhalb von
Tabs und Callouts. Die vorhandenen APIs `replaceSource`,
`Stringifier.expression`, `applyMdxPreset` und `source.resolveHref` werden auf
einen kleinen Compiler-Hook geprüft. HTML, Codebeispiele, externe Ziele,
Bildimporte und virtuelle OpenAPI-Seiten müssen ihr Verhalten erhalten.
Die Prüfung erfolgt zunächst über gezielte fehlschlagende Vitest-Fälle und
anschließend lokale Tests/Lint. Die vollständige HTTP-/HTML-Abnahme übernimmt
die gemeinsame Consumer-Prüfung im Hauptauftrag.

## Ausgangsbefund

- `http://localhost:3400/docs/ueberblick.md` enthält zum Beispiel
  `[Ressourcen verwalten](../koordination/ressourcen.mdx)`.
- `remarkLLMs` serialisiert Markdown-Links als authored Strings. Die
  Komponentenbelegung von `getText('processed')` erreicht nur JSX-Komponenten;
  ein `a`-Override allein behebt den Fehler daher nicht.
- `remarkImage` nutzt bereits `replaceSource` und `Stringifier.expression`,
  um zur Laufzeit ausgewertete Bild-URLs in ansonsten erhaltenem Markdown
  auszugeben. Dieses bestehende Fumadocs-Pattern ist auch für Links geeignet.

## Umsetzung

- `web/lib/docs-markdown-links.ts` hinterlegt ausschließlich für relative
  Linkknoten und Referenzdefinitionen eine Markdown-Quellersetzung. Die
  Linkziele werden erst beim Export über den aktuellen Seitenkontext und
  `source.resolveHref` aufgelöst. Die MDX-/HTML-Knoten werden nicht verändert.
- `web/lib/source.ts` ergänzt diesen Remark-Hook über `applyMdxPreset`; die
  bestehenden Fumadocs-Plugins und Markdown-Komponenten bleiben im Einsatz.
  Dieselbe Ausgabe versorgt `.md` und `llms-full.txt`. OpenAPI-Operationen
  verwenden weiterhin den vorhandenen OpenAPI-Exporter.
- `web/tests/lib/docs-markdown-links.test.ts` kompiliert echte MDX-Fixtures
  mit Fumadocs und prüft direkte Links, Referenzlinks, Parent-/Sibling-Pfade,
  Custom Slugs, virtuelle API-Ziele, Anker, Tabs/Callouts sowie den Erhalt
  von Titeln, formatierten Labels, Bildern, externen Links und Codebeispielen.

## Prüfstand

- Reproduktion vor dem Patch: zwei gezielte Integrationstests schlagen wegen
  unveränderter `.mdx`-Linkziele fehl. Ein zusätzlicher Referenzlink-Test wurde
  ebenfalls vor seiner Umsetzung rot geprüft.
- `bun run test:run tests/lib/docs-markdown-links.test.ts
tests/lib/docs-markdown.test.tsx tests/lib/docs-source.test.ts
tests/lib/docs-roles.test.ts --coverage.enabled=false`: 63 Tests grün.
- Fokussierter TypeScript-Programmlauf für `lib/source.ts`, den Link-Hook und
  dessen Tests mit den Projektoptionen, `noEmit` und ohne inkrementelle
  Schreibausgabe: erfolgreich.
- ESLint und `bun fmt --check` für die geänderten Code-/Testdateien und diesen
  Bericht: erfolgreich.
- Eine Mutation, die Link- und Referenzknoten aus der Verarbeitung ausschließt,
  lässt die Integrationstests fehlschlagen; Produktionscode danach restauriert.
- HTML-Erhalt ist über den kompilierten Fixture-Baum geprüft. Vollständige
  HTTP-/HTML-Prüfungen des Software-Consumers, der globale Build und eine
  Prüfung des Website-Consumers sind hier nicht ausgeführt; die gemeinsame
  Software-Consumer-Abnahme erfolgt im Hauptauftrag.

## Grenzen

Die Auflösungsregeln stammen aus Fumadocs. Nicht vorhandene relative Ziele
bleiben unverändert; der Hook erfindet keine Zielseiten. API-/DTO-Verträge
wurden nicht verändert. Keine neuen Dependencies, Commits oder Serverstarts.
