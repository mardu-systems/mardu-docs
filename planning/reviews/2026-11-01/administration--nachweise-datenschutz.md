# Seitenrevision P29: Nachweise und Datenschutz

## Änderungsbrief

Die verborgene TODO-Seite `docs/administration/nachweise-datenschutz.mdx` soll
Administrierenden mit Kenntnis der Benutzer- und Zutrittsverwaltung erklären,
wie sie gespeicherte Verwaltungsänderungen suchen, lesen und exportieren und
welche Grenzen diese Daten für personenbezogene Auskünfte haben. Heimat bleibt
Administration; Kompetenzvergaben gehören in ihre bestehenden Anleitungen.
Ergebnis ist eine belegbare Teilanleitung, keine rechtliche Verfahrensvorgabe.

Plan: Auditoberfläche, Übersetzungen, Filter-/Exportvertrag und Löschfolgen
abgleichen; TODOs durch belegte Schritte und Grenzen ersetzen; alle vier
vorhandenen Abschnittsanker erhalten; nur Seite und diesen Bericht ändern.
Anschließend lokaler Format-/MDX-/Linkcheck. Gemeinsame Consumer- und
Browserprüfung erfolgt durch die Koordination.

## Entscheidung

**Belegbare Teildokumentation / offene Prüfung.** Statisch geprüfte Auditaufgaben
sowie Abgrenzung von Kontolöschung, Historie und öffentlichen Definitionen.
Keine praktische oder rechtliche Abnahme.

## Befunde und Umsetzung

- TODO-Entwurf durch Audit-Anleitung mit Leserecht, zusätzlichem Exportrecht,
  Benutzerleserecht für den Picker, Suchfiltern, Details und Fehlerhilfe ersetzt.
- Ausführende Person (`UserId`) von betroffenem Konto (`Entity=User`, `EntityId`)
  getrennt. Kombinierte Filter sind eine Schnittmenge, kein personenbezogener
  Gesamtexport.
- CSV in der UI, Excel nur API; Export über Tabellenseiten hinweg auf 10.000
  Ereignisse begrenzt. Der zugehörige Vorgang in der Detailansicht zeigt höchstens
  50 Einträge. Maskierte/gekürzte Werte und erhaltene Historie erklärt.
- Datenarten getrennt, keine gesetzliche Aufbewahrungsfrist behauptet. Nur
  technische Messwerte haben hier belegte einstellbare Fristen. Die im
  Benachrichtigungskatalog vorhandenen `RetentionDays` belegen für sich keinen
  ausgeführten Löschprozess und werden nicht als Löschgarantie beschrieben.
- Auskunftsgrenzen, API für Anmeldehistorie, Anbieterzuständigkeit für verwaltete
  Kontofelder und Kontolöschvorschau ergänzt. Keine vollständige Datenschutz- oder
  Sammellöschfunktion behauptet.
- Öffentliche Definitionen von persönlichen Vergaben und Auditdaten getrennt;
  vorhandene Anleitung für Veröffentlichung/Zurückziehen wiederverwendet.
- Alle vier ursprünglichen H2-Überschriften (damit ihre Anker) und URL erhalten.
  Es gab außer dem Titel, den Abschnittszuschnitten und der Aussage zu nicht
  automatisch festgelegten Fristen keine ausgearbeitete Anleitung zu bewahren.

## Quellen (statisch gelesen, Pfade ab Repositorywurzel)

| Beleg                                                     | Konkrete Quelle                                                                                                                                                                                                                                                                             |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Einstieg, Sichtbarkeit                                    | `web/components/layout/settings/server-nav.config.ts:211` (Audit-Menü mit View-Recht), `web/locales/de/navigation.json:84` (Audit-Ereignisse)                                                                                                                                               |
| UI-Lese-/Exportrechte, URL, CSV-Download                  | `web/app/[project]/dashboard/admin/server/audit-events/audit-events-client.tsx:76`, `:121`, `:195`; Dateiname `web/lib/audit/audit-trail.ts:93`                                                                                                                                             |
| Filter, lokale Tagesgrenzen und UI-Auswahl                | `web/app/[project]/dashboard/admin/server/audit-events/data-table/audit-trail-data-table.tsx:58`, `:66`, `:147`, `:273`; `web/lib/audit/audit-trail-query.ts:50` (24-h-Standard)                                                                                                            |
| Benutzerpicker und sein Leserecht                         | `web/app/[project]/dashboard/admin/server/audit-events/data-table/audit-user-filter.tsx:32`; `web/components/user/user-select-dialog.tsx:26`; `api/Framework/Infrastructure/Identity/Users/Boundary/UsersController.cs:36`                                                                  |
| UTC, Details und maximal 50 korrelierte Ereignisse        | `web/app/[project]/dashboard/admin/server/audit-events/data-table/columns.tsx:35`; `web/app/[project]/dashboard/admin/server/audit-events/audit-event-details-sheet.tsx:51`, `:158`                                                                                                         |
| Begriffe, Fehlermeldungen, Maskiert/Gekürzt               | `web/locales/de/access.json:918`; `api/Framework/Core/Audit/AuditTrailDto.cs:39`; `api/Framework/Infrastructure/Identity/Audit/AuditTrailSanitizer.cs:120`                                                                                                                                  |
| API-Rechte, CSV und Excel                                 | `api/Framework/Infrastructure/Identity/Audit/Boundary/AuditTrailController.cs:28`, `:87`; Filtervertrag `api/Framework/Core/Audit/AuditTrailFilter.cs:10`                                                                                                                                   |
| Benutzer ist Akteur, Objektfilter, Keyword-Felder         | `api/Framework/Infrastructure/Identity/Audit/AuditTrailSpecifications.cs:49`, `:105`; `api/Framework/Core/Audit/AuditTrailDto.cs:47`                                                                                                                                                        |
| Exportgrenze, flache Exportfelder, Sanitizing             | `api/Framework/Infrastructure/Identity/Audit/AuditTrailSpecifications.cs:160`; `api/Framework/Infrastructure/Identity/Audit/AuditService.cs:70`                                                                                                                                             |
| Fehlende/gelöschte Objektverknüpfung                      | `api/Framework/Infrastructure/Identity/Audit/AuditService.cs:43`; `web/app/[project]/dashboard/admin/server/audit-events/audit-event-details-sheet.tsx:186`                                                                                                                                 |
| Nicht jedes technische Update erzeugt Audit               | `docs/audit-persistence.md:3`; `api/Framework/Infrastructure/Persistence/Interceptor/AuditInterceptor.cs:51`                                                                                                                                                                                |
| Erhaltenes Login-/Zutritts-/Buchungsprotokoll             | `api/Framework/Infrastructure/Identity/Users/UserDeletionImpactProvider.cs:68`; `api/Service/Accesses/Infrastructure/DeletionImpact/AccessDeletionImpactContributor.cs:63`; `api/Service/Bookings/Application/Services/BookingDeletionImpactContributor.cs:23`                              |
| Audit bleibt unabhängig vom Konto                         | `api/Framework/Core/Audit/AuditTrail.cs:8` (historische IDs als Werte, keine Konto-Navigation); `api/Framework/Infrastructure/Identity/Users/Services/UserService.Delete.cs:15` (keine Audit-Löschung); Audit-Detail-Verfügbarkeitsprüfung oben                                             |
| Löschvorschau und Anbieterfelder                          | `api/Framework/Infrastructure/Identity/Users/Boundary/UserController.cs:131`; `api/Framework/Infrastructure/Identity/Users/Services/UserService.CreateUpdate.cs:481`; vorhandene Anleitung `web/content/docs/docs/administration/benutzer-rollen.mdx`                                       |
| Anmeldehistorie API; UI nur letzte erfolgreiche Anmeldung | `api/Framework/Infrastructure/Identity/Users/Boundary/UserController.cs:292`; `web/app/[project]/dashboard/user-management/users/dialog/edit-user-sheet.tsx:300` (höchstens zehn aktuelle Ereignisse ausgewertet)                                                                           |
| Messwertfristen, Vorgaben, Umsetzung                      | `api/Framework/Infrastructure/Telemetry/MetricsSettings.cs:18`, `:67`; `api/Service/Observability/Application/TimescaleRetentionPolicySynchronizer.cs:65`, `:83`; UI `web/app/[project]/dashboard/admin/server/monitoring-settings/page.tsx:51`; Labels `web/locales/de/settings.json:1505` |
| Benachrichtigungskatalog statt Löschgarantie              | `api/Service/Notifications/Application/Catalog/EventDefinition.cs:17`; Referenzsuche nach `RetentionDays` in `api/Service/Notifications` (Definitionen/DTO, kein belegter Cleanup)                                                                                                          |
| Öffentliche Definition und Rücknahme                      | `api/Service/Competencies/Boundary/HttpControllers/CompetencyPublicationsController.cs:15`, `:54`, `:64`; `api/Service/Competencies/Application/Services/PublicationService.cs:90`; vorhandene Badge-Anleitung                                                                              |

## Prüfungen und offene Grenzen

- Erfolgreich: Prettier auf ausschließlich den beiden eigenen Dateien, MDX-
  Syntaxkompilierung mit installiertem `@mdx-js/mdx`, relativer Link-/Fragmentcheck,
  Erhalt aller vier ursprünglichen Abschnittsüberschriften, TODO-Freiheit und
  `git diff --check` im Doku-Submodul für die Seite und diesen Bericht.
- Keine Software-/DTO-/OpenAPI-Änderung; bestehende API-Verträge erläutert.
  Keine globalen Builds, Serverstarts, echten Exporte oder personenbezogenen
  Datenabfragen ausgeführt.
- Offen für Koordination: Consumer-Rendering (Dashboard und Website), mobile
  Tabelle/Details, Tastaturbedienung und Rechtezustände mit fiktiven Daten prüfen.
  Einen kleinen synthetischen CSV-Export sowie Zeitzonenabgleich praktisch prüfen.
  Keine Behauptung über tatsächlich gespeicherte Installationsfristen oder
  erfolgreiche Timescale-Löschläufe.
- Außerhalb dieses Umfangs: vollständige Dateninventur aller Anbieter, Backups,
  Dateispeicher und Betriebslogs sowie rechtliche Verfahren.

## Hinweise an die Koordination und Publikationsvorschlag

- Bestätigte Text-/Codeabweichung: `web/locales/de/access.json:935` behauptet bei
  Zeitraum „Alle Zeitangaben werden in UTC angezeigt …“. Datumseingaben benutzen
  laut `dateBoundaryToUtc` jedoch lokale Kalendertage. Die Anleitung beschreibt
  den Code; Softwaretext nicht geändert. Praktisch mit Nicht-UTC-Browser prüfen.
- `web/docs/audit-trail-ui.md:13` nennt einen Benutzer-Aktivitätstab mit
  `auditTrailGetByUser`. Repositorysuche findet nur generierten Client, keinen
  UI-Aufrufer. Dieser Tab wird nicht dokumentiert; technische Bestandsdoku prüfen.
- Die Seite bleibt im Auftrag verborgen: `administration/meta.json` enthält sie
  nicht. `web/lib/docs-roles.tsx:141` ordnet die URL bereits Administration zu.
  Nach gemeinsamer Darstellungskontrolle als Teilanleitung unter **Betrieb**
  aufnehmen; nicht unter **Kompetenzen und Nachweise**. Vorhandener Link aus
  `sicherheit-betrieb.mdx` bleibt gültig. Keine neue Seite erforderlich.
- Navigation, Bereichsfilter und fremde Seiten unverändert.

## Geänderte Dateien

- `web/content/docs/docs/administration/nachweise-datenschutz.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--nachweise-datenschutz.md`
