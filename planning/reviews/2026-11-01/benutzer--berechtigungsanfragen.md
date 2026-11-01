# P05: Meine Berechtigungsanfragen

## Änderungsbrief

Die Seite beantwortet angemeldeten Nutzern ohne Verwaltungswissen, wie sie Zugriff
beantragen, ihren Bearbeitungsstatus lesen und eigene offene Anträge zurückziehen.
Heimatbereich und kanonische Quelle bleiben `benutzer/berechtigungsanfragen.mdx`.
Der vorhandene kurze Aufgabenablauf, Statusvergleich, Querverweis auf Freigaben
und Screenshot bleiben erhalten. Nötig sind die eindeutige Zuordnung der Rechte,
die optionale Begründung und präzisere Angaben zu Sperre, Ergebnis und Rückmeldung.
Quellen sind die Portal-Komponenten, deutsche Übersetzungen sowie Controller,
DTOs, Specifications und Katalogservice. Geprüft wird statisch und mit lokalen
Dokumentwerkzeugen; die gemeinsame Consumer- und Browserprüfung liegt beim
Koordinator. Es werden keine Softwarefunktionen oder API-Verträge geändert.

## Ergebnis: verbessert, zur Prüfung

- Die Seite war bereits knapp und deckte Antrag, Status, Rücknahme und
  Sendefehler ab. Diese Gliederung, alle vier Überschriften/Anker, der bestehende
  Freigaben-Link und das Bild bleiben erhalten; keine neue Komponente nötig.
- Die pauschalen „Anfragerechte“ sind nun dem Zugriffskatalog zugeordnet;
  dessen Leserecht als Voraussetzung für die eigene Liste ist ergänzt.
- Das vermeintliche Pflichtfeld Begründung ist als optional mit 1024 Zeichen
  beschrieben. Die exakte Aktion **Antrag senden** und das Ergebnis **Offen**
  sind ergänzt.
- Die vage Sperre weiterer Anfragen ist auf dieselbe Ressource präzisiert.
  Fehlende Anfrageaktion führt zu den Kataloggründen und Anfragerechten.
- **Alle Status**, optionale Nachricht/Rückmeldung und Bearbeitungsdatum sind
  erläutert. **Genehmigt** bedeutet eine erstellte Freigabe; ihre Gültigkeit und
  übrigen Nutzungsbedingungen bleiben über die Nachbarseite erschlossen.
- Fehlerhilfe benennt die Lebensdauer des Texts im geöffneten Dialog und die
  vorhandenen Aktionen **Weiter bearbeiten**/**Änderungen verwerfen**. Keine
  Speicherung eines Entwurfs und kein automatischer Zugang werden versprochen.

## Code- und UI-Belege

Pfadangaben beziehen sich auf die Wurzel des Software-Repositories.

| Aussage                                                                           | Quelle und relevante Stellen                                                                                                                                                                                                                                        |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Portalabschnitt nur mit `AccessCatalog.View`                                      | `web/components/portal/portal-resources.tsx:55`; Portalroute `web/app/[project]/portal/resources/page.tsx:1`                                                                                                                                                        |
| Lesen eigener Anträge vs. Stellen/Rücknahme                                       | `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessCatalogController.cs:33–71`: Request-Recht für POST, View-Recht für eigene Liste; `web/components/portal/profile-access-requests.tsx:52–54`                                                            |
| Optionaler Kontext, Zeichenlimit                                                  | `api/Service/Accesses/Boundary/Dto/ResourceAccessCatalogDtos.cs:108–114`; `web/components/access/resource-catalog-workspace.tsx:137–151,345–365`: `null` bei leerer Begründung, `maxLength=1024`, Reset erst nach Erfolg                                            |
| Offener Antrag nur für aktuelle Person und dieselbe Ressource; Anlage als Pending | `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:142–190`: Prüfung auf anforderbare Ressource, vorhandenen Pending-Antrag und effektive Freigabe; `Note` normalisiert                                                                     |
| Alle Status, Pagination und sichtbare Metadaten                                   | `web/components/portal/profile-access-requests.tsx:34–39,55–65,94–140,164–191`; eigene Liste `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:193–199`, Filter in `api/Service/Accesses/Gateway/ResourceAccessSpecifications.cs:368–414`  |
| Rücknahme nur eigener offener, unveränderter Anträge; keine Freigabenänderung     | `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:221–240,390–401`; UI-Aktion `web/components/portal/profile-access-requests.tsx:193–214`; HATEOAS `api/Service/Accesses/Boundary/Hypermedia/ResourceAccessHypermediaEnrichers.cs:523–550` |
| Genehmigung erzeugt Nutzerfreigabe; Ablehnung hat Begründung                      | `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:242–310`; DTOs `api/Service/Accesses/Boundary/Dto/ResourceAccessCatalogDtos.cs:117–154`                                                                                                  |
| UI-Namen und Statuswerte                                                          | `web/locales/de/access.json:496–541`; persönliche Metadaten/Fehler `web/locales/de/resources.json:527–542`; Verwerfen-Aktionen `web/locales/de/devices.json:533–537`                                                                                                |
| Fehler lässt Text bestehen, Schließen kann verwerfen                              | `web/components/access/resource-catalog-workspace.tsx:115–151,322–365`; `web/components/profile/profile-draft-provider.tsx:76–108,259–265`: kein persistierter Entwurf, Bestätigung bei schmutzigem Formular; `web/hooks/use-access-mutation.ts:47–79`              |
| Kataloggründe sichtbar                                                            | `web/components/access/access-catalog-presentation.tsx:103,198–220`; `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:90–132`                                                                                                             |

Die benachbarte Anleitung `docs/benutzer/zutritt.mdx` bleibt die Quelle für Katalog,
Freigabengültigkeit und weitere Nutzungsbedingungen. Kein zusätzlicher
Seitenbedarf und keine Navigationserweiterung aus dieser Prüfung.

## Prüfungen und Grenzen

- Statischer Abgleich von UI, deutschen Übersetzungen, Controllerrechten, DTOs,
  Service, Specifications und Hypermedia-Aktionen durchgeführt.
- Vorhandenes PNG lokal angesehen: Statusfilter, Nachricht, Rückmeldung und
  Rücknahme sind lesbar. Das Bild wurde nicht neu aufgenommen; es belegt keine
  aktuelle angemeldete Praxisprüfung.
- Lokales Prettier aus `web/node_modules/.bin/prettier` mit `--ignore-path /dev/null`
  für genau die beiden eigenen Dateien ausgeführt; abschließendes `--check`
  erfolgreich. Die Ausnahme ist nötig, weil die Web-Ignore-Datei das gesamte
  Dokumentations-Submodule ausschließt.
- Produktseite mit vorhandenem `@mdx-js/mdx` nach Entfernen des Frontmatters
  erfolgreich kompiliert. Drei lokale Link-/Bildverwendungen auf vorhandene
  Dateien geprüft; alle vier ursprünglichen Überschriften erhalten.
- `git diff --check` für die beiden eigenen Dateien im Dokumentations-Submodule
  ohne Fehler. Keine globalen Tests oder Builds ausgeführt.
- Offen beim Koordinator: Rendering der geänderten Seite in Software- und
  Website-Consumer einschließlich mobiler Ansicht; angemeldeter Portalablauf mit
  View-only- und Request-Rechten, erfolgreichem Antrag und Rücknahme sowie
  Sendefehler/Verwerfen und konkurrierender Entscheidung. Es wurden hier weder
  Browserabläufe noch Hardware-/Provider-Verhalten praktisch geprüft.
- API-/DTO-Dokumentation nicht geändert: ausschließlich Produktanleitung und
  Prüfbericht; kein Software- oder Vertragsänderungsbedarf aus diesem Abgleich.

## Geänderte Dateien

- `web/content/docs/docs/benutzer/berechtigungsanfragen.mdx`
- `web/content/docs/planning/reviews/2026-11-01/benutzer--berechtigungsanfragen.md`
