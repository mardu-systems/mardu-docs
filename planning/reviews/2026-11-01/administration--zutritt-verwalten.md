# P30: Zugangsmetriken lesen

## Änderungsbrief

Leserfrage: Wie lese ich die gespeicherten Zugangsentscheidungen und aktuellen
Sitzungszahlen einer Person oder eines Zutrittspunkts? Leser kennen das Öffnen
der jeweiligen Detailansicht; vorausgesetzt wird kein Wissen über UTC oder die
getrennten Sichtrechte für Protokolle und Sitzungen. Ziel ist eine belastbare
Einordnung von Zeitraum, Einheiten, leeren Werten und Aussagegrenzen.
Kanonische Heimat bleibt Administration unter der bestehenden URL
`administration/zutritt-verwalten`; vorhandene Anker und die ausgearbeitete
Metriktabelle bleiben erhalten. Plan: veraltete Gerätezuständigkeit und
Diagrammauswahl korrigieren, kurze Schritte/Rechte/Fehlerhilfe ergänzen, danach
nur die eigenen Dateien formatieren und Links/Anker statisch prüfen.
Keine Software- oder Vertragsänderung; Browser-/Consumerprüfung übernimmt der
Koordinator. Verwaltungsanleitungen werden als eigenständiger Bedarf belegt.

## Entscheidung und Befunde

**Verbessert; statisch belegte Metrik-Teildokumentation, keine praktische Abnahme.**

- Erhalten: Titel, historische URL, `zugangsmetriken`, alle fünf expliziten
  Altanker, UTC-Tagesfenster, fünf letzte Einträge ohne Begrenzung der Summen,
  Ausschluss ausstehender Entscheidungen/Sitzungsenden/-wechsel sowie die
  Grenzen gespeicherter Protokolle gegenüber einer physischen Gerätewirkung.
- Korrigiert: Die aktuelle Gerätediagnose verwendet nicht mehr die gemeinsame
  Sieben-Tage-Auswertung. Die Seite verweist auf die vorhandene Geräteanleitung.
- Korrigiert: Die feste Anzeige verwendet Linien; die Benutzer-Dashboardansicht
  erlaubt Balken, Linien und Fläche. Abweichende Kartentitel der Benutzeransicht
  werden als vorhandene Alternativen benannt.
- Ergänzt: Leseablauf für Benutzerdetails, Prozent als Einheit, Anzahlen statt
  Personen/Nutzungsdauer, Browserzeitzone der Einzelereignisse, getrennte
  Protokoll-/Sitzungsrechte und deren Folgen für Nullwerte, Ladefehler und
  stehengebliebene Werte des letzten erfolgreichen Abrufs.
- Der Schreibauftrag für umfassende Verwaltungsanleitungen wurde aus der
  Produktseite entfernt. Die bestehenden Altanker bleiben am knappen Verweis
  zur Ressourcenanleitung. Die Seite behauptet keine Abdeckung dieser Aufgaben.

## Quellen der Metrikbeschreibung

Pfadangaben beziehen sich auf das Software-Repository, Stand dieser Prüfung.

- `web/hooks/use-access-activity-metrics.ts:18–57`: `Accesses.View`, Abruf von
  `resourceAccessLogsMetrics`, Filter nach geöffnetem Benutzer/Zutrittspunkt;
  der Hook unterstützt weiterhin auch Gerätefilter, wird aber von der aktuellen
  Geräteansicht nicht mehr verwendet.
- `web/components/metrics/access-activity-metrics.tsx:18–24,97–129,174–219`:
  Zahlen-/Prozentdarstellung, Liniengrafik mit UTC, Leeranzeige, maximal fünf
  Einträge und Browserzeitzone der Einzelereignisse.
- `web/app/[project]/dashboard/user-management/users/dialog/user-metrics-tab.tsx:23–35,88–145`:
  Dashboard-Leserecht entscheidet über anpassbare Ansicht oder feste Anzeige;
  beide verwenden denselben Hook. Prozent, UTC-Verlauf und lokale Einzelzeiten.
- `api/Service/Observability/Application/UserMetricsDashboard.cs:18–25,57–61`:
  sechs Widgets und erlaubte Diagrammarten Balken/Linien/Fläche. UI-Titel:
  `web/locales/de/users.json:419–450` sowie
  `web/locales/de/access.json:465–487` für feste Anzeige/Fehler-/Leertexte.
- `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessActivityControllers.cs:153–175`:
  `GET /api/v1/resource-access-logs/metrics`, `Accesses.View`, dokumentierter
  Schutz und Ausschlüsse. Bestehende XML-/OpenAPI-Dokumentation wiederverwendet;
  kein API-/DTO-Vertrag wurde geändert.
- `api/Service/Accesses/Application/Services/ResourceAccessActivityService.Metrics.cs:17–42`:
  UTC-Tagesbeginn vor sechs Tagen bis Beobachtungszeit, getrennte `ViewLogs` und
  `ViewSessions`, maximal fünf neueste Entscheidungen.
- `api/Service/Accesses/Gateway/ResourceAccessActivityMetricsQuery.cs:21–61`:
  persistierte Protokolle, nur erlaubte/abgelehnte Entscheidungen, sieben
  Tageswerte einschließlich Nullen, aktuelle offene Sitzungsabschnitte ohne
  Startzeitfilter. Zeitgrenzen/Filter:
  `api/Service/Accesses/Gateway/ResourceAccessActivitySpecifications.cs:228–356`.
- `api/Service/Accesses/Boundary/Dto/ResourceAccessActivityMetricsDto.cs:19–44`:
  Bedeutung von Gesamtzahl, aktuellen Sitzungen und UTC-Tageswerten.
- `web/hooks/use-access-collection.ts:77–100,121–136`:
  letzte Daten bleiben bei bestimmten Ladefehlern erhalten; bei 401/403 werden
  sie entfernt. Keine Aussage erfunden, dass eine Fehlermeldung aktuelle Daten
  bestätigt.
- `web/app/[project]/dashboard/device-management/device-settings/device-settings-sheet.tsx:213–227`
  und `device-monitoring-tab.tsx:26–107`: aktuelle Gerätediagnose lädt
  Dashboarddaten mit eigener Zeitraum-/Auflösungsauswahl. Die alte gemeinsame
  Gerätebeschreibung ist daher nicht mehr zutreffend.

## Bedarf für eigene kanonische Verwaltungsanleitungen

Diese Aufgaben gehören in spätere eigene Seiten, abgestimmt auf die vorhandene
Ressourcenanleitung. Keine vermuteten neuen Seiten verlinkt. Routenvorsatz aller
folgenden UI-Routen ist `/{project}`; `{resourceId}` bezeichnet eine verwaltete
Ressource, keinen zusätzlichen Scope-Datensatz.

| Aufgabe                                                             | Aktuelle Route und belegte Quellen für einen Folgeauftrag                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Zugriffsregel/ressourcenbezogenen Scope verstehen und konfigurieren | `/dashboard/resources`, Ressourcendetails **Nutzung & Zugriff**. `web/components/bookings/resource-details-sheet.tsx:305–333`, `web/components/access/resource-access-panel.tsx:244ff` und die dort verwendeten Regelkomponenten. API: `GET/PUT /api/v1/managed-resources/{resourceId}/access`, Controller `ResourceAccessController.cs:31–52`. An vorhandene Anleitung `koordination/ressourcen.mdx#nutzung-und-zugriff-nutzung-erlauben` anschließen, keine doppelte Einrichtung schreiben.                                                                                             |
| Verwaltungszuständigkeiten/Delegation und wirksame Rechte           | `/dashboard/access-management/scopes`; `page-client.tsx:194ff`, `web/components/access/responsibility-binding-dialog.tsx`, `access-scope-diagnostics-dialog.tsx`; API `/api/v1/access-scope-assignments`, `/profiles`, `/effective/{userId}`, `/check`, Controller `AccessScopeAssignmentsController.cs:17–78`. Benutzer-/Gruppen-/Rollenbezug, Zielressource versus Bereich, delegierbare Rechte und Widerruf praktisch prüfen.                                                                                                                                                          |
| Zutrittspunkte und Leser-/Aktorzuordnung                            | `/dashboard/resources`, Ressourcendetails **Technik**; `resource-details-sheet.tsx:333–355`, `resource-access-panel.tsx:32–234`, `web/components/access/access-point-editor.tsx`, `access-point-endpoint-bindings-panel.tsx`. API unter `/api/v1/managed-resources/{resourceId}/access`: `/hardware`, `/access-points`, `/access-points/{accessPointId}/endpoint-bindings`, `/{bindingId}/state`, `/{bindingId}/relocation`; `ResourceAccessController.cs:55–180`. Duplikate, Aktivierung, Umzug und physische Bestätigung getrennt prüfen.                                               |
| Freigaben anlegen, ändern und entziehen                             | `/dashboard/access-management/accesses?scope={resourceId}&user={userId}`; tatsächlich nutzbarer Ressourcenwähler und `ResourceGrantsPanel`, keine bloße Weiterleitung: `accesses/page.tsx:3–19`, `accesses-page-client.tsx:29–109`, `web/components/access/resource-grants-panel.tsx`, `access-grant-editor.tsx`, `access-grant-schedule.tsx`. API `GET/POST .../{resourceId}/access/grants`, `PUT/DELETE .../grants/{grantId}`, `ResourceAccessController.cs:184–230`. Empfänger, Zeitfenster/Zeitzone, Versionskonflikte und Wirkung bestehender Sitzungen brauchen eigene Prüfung.     |
| Katalog und Zugangsanträge verwalten                                | `/dashboard/access-management/requests`: `requests/requests-page-client.tsx:52–112`; `GET /api/v1/resource-access-requests`, `POST /{requestId}/approval` und `/rejection`, `ResourceAccessRequestsController.cs:19–56`. Katalog `/dashboard/access-catalog` und eigene Anträge: `ResourceAccessCatalogController.cs:19–65`, UI `access-catalog/page-client.tsx`. Sichtbar/beantragbar in der Ressourcenregel von tatsächlicher Freigabe unterscheiden; Benutzeranleitung `benutzer/zutritt.mdx` wiederverwenden.                                                                         |
| Protokolle, Sitzungsketten, Beenden und Gerätezustellung            | `/dashboard/access-management/logs` öffnet Sitzungsketten, `/dashboard/access-management/logs/events` Ereignisse. `logs-page-client.tsx:8–36`, `web/components/access/resource-activity-workspace.tsx:32–86`, `resource-session-details.tsx:296,426–474`. API `/api/v1/resource-access-logs`, `/resource-access-session-chains`, `/resource-access-sessions/{sessionId}/end`, `/{sessionId}/end-command`; `ResourceAccessActivityControllers.cs:19–125`. Gespeichertes Ende versus `Pending`/`Delivered`/`Failed`, Leser-/Aktorbestätigung und Wiederholung als eigene Aufgabe behandeln. |

## Praxisgrenzen und Koordinatorhinweise

- Keine eigene Browser-, Hardware-, Gerätebefehls- oder Providerprüfung.
  Zahlen, leere Ereignisse, unterschiedliche Sichtrechte, Ladefehler mit alten
  Werten, lokale Zeitzone/UTC-Tagesgrenze und die Benutzer-Diagrammvarianten im
  Consumer noch prüfen. Website-Consumer wurde ebenfalls nicht ausgeführt.
- **Zutrittspunkt-Metriken: Erreichbarkeit offen.**
  `web/app/[project]/dashboard/device-management/access-points/access-point-settings/access-point-settings-sheet.tsx:648–651`
  rendert weiterhin `AccessActivityMetrics`. Aufrufer dieses Sheets sind die
  älteren AccessPoint-Tabellen-RowActions und `DeviceReadersGraph`; eine Suche
  nach deren Namen findet keine aktuellen Aufrufer außerhalb ihrer Definitionen.
  Die heutige Ressourcen-Technik nutzt den anderen `AccessPointEditor`, ohne
  Metrik-Tab. Das belegt eine vorhandene Implementierung, keinen nutzbaren
  Navigationsweg. Deshalb nur die Benutzeransicht als Öffnungsschritt beschrieben;
  die bestehende Erklärung der Zutrittspunktwerte erhalten. Koordinator soll
  entscheiden, ob nach Browserprüfung ein eigener Produktbefund nötig ist.
- `administration/geraete-verwalten.mdx#diagnose-lesen` nannte bei Beginn dieser
  Prüfung noch „Zugangsmetriken“ im Diagnoseumfang. Den zuständigen Agenten auf
  den neuen `DeviceMonitoringTab` hinweisen; fremde Seite nicht geändert.
- URL und sämtliche Altanker bleiben. Die früheren Verwaltungsanker führen
  weiterhin zum knappen Ressourcenverweis; bei späteren kanonischen Seiten die
  Verweisziele gezielt ergänzen. Navigation nicht verändert.

## Ausgeführte Checks

- Vorhandenes Prettier 3.9.10 direkt aus `web/node_modules/.bin/prettier`
  mit `--ignore-path /dev/null` auf genau diese zwei Dateien angewendet und
  anschließend mit `--check` geprüft: erfolgreich. Das explizite Ignore-Override
  ist nötig, weil der Software-Consumer das Dokumentationssubmodule ausnimmt.
- Produktseite mit dem installierten `@mdx-js/mdx` kompiliert (Frontmatter vorab
  ausgeblendet): erfolgreich; kein Consumer-Rendering behauptet.
- Alle vier lokalen Seitenlinks einschließlich Fragmentzielen anhand der
  aktuellen Dateien und des installierten `github-slugger` geprüft: erfolgreich.
- Alle acht bisherigen expliziten/aus Überschriften erzeugten Anker gegen
  `HEAD:docs/administration/zutritt-verwalten.mdx` verglichen: erhalten.
- `git -C web/content/docs diff --check --` beschränkt auf die beiden eigenen
  Pfade: erfolgreich. Keine Softwaretests, globalen Builds, Commits oder
  Änderungen außerhalb der zwei zugewiesenen Dateien.

## Geänderte Dateien

- `web/content/docs/docs/administration/zutritt-verwalten.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--zutritt-verwalten.md`
