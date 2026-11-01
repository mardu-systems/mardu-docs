# Website-Consumerprüfung und lokale Kompatibilitätskorrektur

Stand: 1. November 2026. Die belegten Link- und Navigationsfehler sind lokal
korrigiert. Der installierte Website-Loader und die Navigationstests bestehen
sowohl mit dem alten Website-Content als auch mit der aktuellen gemeinsamen
Docsrevision. Eine gerenderte Website-/Browserabnahme ist damit nicht behauptet.

## Quellen und Grenzen

- Website: `/Users/lucaschoeneberg/Documents/GitHub/websites`, HEAD
  `b8036d4a8b9d72d096c8a3006177218b105300da`.
- Website-Docs unter `apps/mardu-de/content`: HEAD und Gitlink weiterhin
  `c3bbf49910c385276481fb63b00a7e6961bfe60d`; **50 MDX-Seiten**, älterer Inhalt.
  Die vorhandenen unversionierten `.DS_Store`-Dateien blieben unangetastet.
- Gemeinsame Quelle:
  `/Users/lucaschoeneberg/Documents/GitHub/mardu-rpi-api/web/content/docs`, HEAD
  `611fe8dcf45ffcd16d7f85e47accd242f78d4368` mit der aktuellen uncommitteten
  Revision; **69 MDX-Seiten** beim Abschluss dieser Prüfung.
- Geprüft wurden Root-/App-`AGENTS.md`, gemeinsame Dokumentationsregeln und
  Arbeitsweise, Websitepaket, Fumadocs-Quelle, MDX-Komponenten, Docs-Layout/-Seite,
  Bereichsfilter, Suchroute, Next-Konfiguration und Navigationstests.
- Installiert: Fumadocs Core/UI `16.17.9`, Fumadocs MDX `15.4.10`, Next `16.4.3`.
  Kein Build, Serverstart, Installationslauf, Commit, Push oder Submodule-Bump.

Websitepfade unten sind relativ zu `websites/apps/mardu-de`, gemeinsame
Quellpfade relativ zum oben genannten Docsrepository.

## Ausgangsbefunde und Umsetzung

### Virtuelle Operationslinks

`docs/entwickeln/http-api.mdx` enthielt 17 relative Links zu
`./API/.../*.mdx`. Der Software-Consumer erzeugt diese Seiten über
`web/lib/source.ts` und `openapi.staticSource({ baseDir: 'entwickeln/API' })`.
Website-`lib/source.ts` lädt ausschließlich MDX aus `content/docs`. Der
Website-Loader ließ alle 17 Operationslinks unverändert als `.mdx`-Dateiadresse
stehen; `createRelativeLink` der Seitenkomponente konnte sie nicht auflösen.

Die 17 Links wurden durch ausdrücklich genannte HTTP-Methoden/Pfade ersetzt,
abgeglichen gegen die tatsächlichen `operationId`-Einträge in
`web/contracts/backend-swagger-docs.json` des Software-Repositories. Beispiele:
`GET /api/v1/system/auth/capabilities`,
`POST /api/v1/passkeys/authentication/options`,
`GET /api/v1/auth/oidc/start` und
`POST /api/v1/managed-resources/{resourceId}/switch/state`.
Beispiele, Abläufe und vorhandene Anker bleiben erhalten.

`docs/entwickeln/api-integration.mdx` und `docs/entwickeln/index.mdx` begrenzen die
Anweisung **API** unter **Referenz** ausdrücklich auf die Dokumentation der
jeweiligen Softwareinstallation. Die Website bietet diese erzeugte Referenz
nicht an. `http-api.mdx` und `api-integration.mdx` nennen außerdem `/redoc` und
`/swagger/v1/swagger.json` an der eigenen API-Serveradresse **bei aktiviertem
Swagger**; Grundlage ist
`api/framework/Infrastructure/OpenApi/OpenApiExtensions.cs:126–144` des
Software-Repositories. Keine feste öffentliche Hostadresse wurde eingeführt.
Die Node-RED-Zeile der Integrationsauswahl führt zur vorhandenen Anleitung
`entwickeln/automationsfluesse.mdx`; die administrative Einrichtung bleibt im
anschließenden Text beschrieben.

### Navigation und Eigentum

Website-`lib/docs-roles.tsx` enthielt harte Sluglisten, in denen 20 nun kuratierte
Seiten fehlten. Außerdem gehörte `koordination/ressourcen` dort noch zur
Koordination; Ankerlinks wurden nicht normalisiert und native Separatoren
verworfen. Ein Filtern des gesamten Baums importierte teilweise zusätzliche
physische Bereichsordner.

Die vorhandenen Software-Patterns wurden ohne neue Dependency übernommen:

- Die 20 fehlenden Slugs sind ergänzt. Ressourcen und Monitoring gehören zur
  Administration; persönliche Profil-/Hilfeseiten gehören zum Benutzerbereich.
- Koordination erlaubt die ausdrücklich kuratierten Ressourcenquerverweise;
  Fragmentteile werden bei der Zuordnungsprüfung entfernt.
- Die Sidebar projiziert den eigenen Metadatenordner, zeigt dessen Start einmal
  und erhält native Separatoren nur für sichtbare Gruppen.
- Metadaten bestimmen Reihenfolge und Profilordner; alte physische Ordner werden
  nicht zusätzlich importiert. Fallbackbäume erscheinen nicht wieder, die
  bereichsspezifische `$id` bleibt erhalten. Website-Icons, Farben und übriges
  Design bleiben bestehen.

### Erhalt des tatsächlich eingebundenen Altstands

Der alte Website-Content hat noch keinen Profilzweig unter Benutzer und keine
Ressourcen-/Monitoringquerverweise unter Administration. Eine ausschließliche
Projektion des eigenen Bereichs hätte deshalb bereits nutzbare Seiten aus den
passenden Sidebars entfernt. Die Aufgabenentscheidung verlangt, den alten
Content-Gitlink ohne Inhalts- oder Metadatenänderung weiter zu unterstützen.

Nach der Bereichsprojektion werden daher nur bereits in
`flattenTree(tree.children)` veröffentlichte, dieser Rolle gehörende und dort
noch fehlende Seiten **flach** ergänzt. Kanonische URLs ohne Fragment verhindern
Dopplungen. Die Ergänzung verwendet weder `source.getPages()` noch Dateien oder
Fallbackbäume und veröffentlicht keine ausgeblendeten Inhalte. `/docs` bleibt
der bereichsübergreifende Einstieg, keine ergänzte Unterseite eines Bereichs.

Der reale Loaderdurchlauf zeigt:

| Quelle                       | Ergänzungen                                                                             | Fehlende veröffentlichte Anleitungen im Eigentümerbereich |
| ---------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Alter Website-Content        | Neun Profil-/Hilfeseiten unter Benutzer; Ressourcen und Monitoring unter Administration | Keine                                                     |
| Aktuelle gemeinsame Revision | Keine; alle Seiten stehen bereits in den kuratierten Metadaten                          | Keine                                                     |

## Prüfungen

- Neue Fehlfälle zuerst gegen den alten Filter ausgeführt: 31 fehlgeschlagene
  Tests mit altem Content, 32 mit der aktuellen Quelle, darunter der unaufgelöste
  virtuelle API-Link. Die zusätzliche Altstand-Erhaltung wurde anschließend mit
  zwei gezielt fehlschlagenden Tests vor ihrer Umsetzung belegt.
- `bun test apps/mardu-de/lib/docs-roles.test.ts apps/mardu-de/lib/docs-structure.test.ts`:
  **49 bestanden** mit dem unveränderten Website-Docscheckout.
- `MARDU_DOCS_TEST_ROOT=/Users/lucaschoeneberg/Documents/GitHub/mardu-rpi-api/web/content/docs/docs bun test apps/mardu-de/lib/docs-roles.test.ts`:
  **45 bestanden** mit der aktuellen gemeinsamen Quelle, nur im Speicher geladen.
  Das Test-Override verändert den Gitlink nicht.
- Vollständiges Website-`bun test`: **145 bestanden, 0 fehlgeschlagen**.
- Website-App-Typecheck, ohne inkrementelle Ausgabe:
  `bun check --project apps/mardu-de/tsconfig.json --incremental false`:
  **523 Dateien ohne Typfehler**. Ein zuvor gefundener Testtypfehler bei
  `readdirSync` wurde durch die explizite vorhandene UTF-8-Option korrigiert.
- Scoped ESLint für beide Website-Dateien: Exit **0**. Das bestehende
  shadcn-Lint-Setup meldet zusätzlich seinen Konfigurationshinweis zu
  `animate-fade-in`; keine neue Lintdiagnose der geänderten Dateien.
- Formatierung mit vorhandenem Bun-Formatter für die Website-Dateien und
  vorhandenem Prettier für die drei MDX-Seiten; `git diff --check` geprüft.
- Alle regulären relativen MDX-Links lösen mit dem installierten Website-Loader
  in beiden Quellen auf. Die neuen API-Methoden/Pfade wurden mit dem tatsächlichen
  Software-OpenAPI-Vertrag abgeglichen.
- `/docs/v1` und `/docs/v2` bleiben in beiden Quellen adressierbar und verlinken
  auf `/docs`. Weitere historische Unterseiten oder Weiterleitungen sind damit
  nicht nachgewiesen.

## Weiterhin offene Darstellungs- und Veröffentlichungsgrenzen

Kein Komponentenimport-Konflikt festgestellt: Framework-`Image`, `ImageZoom`,
`Steps` und `Tabs` existieren in den installierten Paketen; die Website stellt
Fumadocs-Standardkomponenten einschließlich `Callout` bereit. Der vorhandene
`RootProvider` aus `fumadocs-ui/provider/next` liefert über den NextProvider auch
`next/image`; alle relativen Bildimporte der aktuellen Quelle existieren.
Darstellung, Zoom-Bedienung und mobile Lesbarkeit wurden hier nicht im Browser
geprüft. Browser und Builds übernimmt die übergeordnete Aufgabe.

Die Website-Suche verwendet weiterhin die vollständige Quelle aus
`app/api/search/route.ts`, nicht die Veröffentlichungsliste des Software-Consumers.
Es wurde keine Änderung der Websitequelle, OpenAPI-Pipeline, Suche, Pakete oder
Metadaten vorgenommen. Ein späteres Veröffentlichen der neuen Texte benötigt
weiterhin den passenden Docsstand im Consumer; der alte Content-Gitlink wurde
nicht verändert.

Geänderte Dateien: die drei genannten gemeinsamen Entwicklungsseiten, dieser
Bericht sowie Website-`lib/docs-roles.tsx` und `lib/docs-roles.test.ts`. Es wurde
kein API-/DTO-Vertrag verändert; die vorhandene OpenAPI-Referenz wurde für die
Anleitungs- und Linkkorrektur wiederverwendet.
