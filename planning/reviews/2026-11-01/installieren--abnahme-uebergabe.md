# P36: Abnahme und Übergabe

## Änderungsbrief

Aufgabe: Die verborgene TODO-Seite zu einem nutzbaren Ablauf für die Prüfung einer
vorhandenen Installation und ihre Übergabe ausarbeiten. Leser sind Personen vor
Ort, die Geräte und Ressourcen zuordnen können, aber die Aussagegrenzen von
Dashboard, Protokoll und Gerätebestätigung kennen müssen. Ergebnis ist ein
manuell geführtes Prüfprotokoll je Zutrittspunkt, kein automatisch erstellter
Bericht und keine behauptete Hardwareabnahme. Heimat bleibt Installieren; URL
und die Anker `funktionsprüfung` und `protokoll-und-übergabe` bleiben erhalten.

Quellen: vorhandene Geräte-, Ressourcen-, Tag- und Betriebsanleitungen; Geräte-
Konfigurationsservice, Protokoll-/Bereitschaftstests, Zugriffsaktivität und deren
DTOs, UI und Übersetzungen. Nur die zugewiesene Seite und dieser Bericht werden
geändert. Statische Dokumentprüfungen lokal; Consumer-Rendering, Browser- und
Hardwareprüfung übernimmt der koordinierte Abschluss bzw. die Installation.

## Befund und Entscheidung

**Belegbare Teildokumentation / offene Prüfung.** Die Seite ist inhaltlich
ausgearbeitet und lokal statisch geprüft, jedoch weder im Consumer gerendert noch
an einer Anlage praktisch abgenommen. Leserfrage: Wie prüfe ich eine vorhandene
Zuordnung und den Zugriff je Zutrittspunkt und übergebe die Ergebnisse samt
offenen Mängeln an die Administration?

- Die bisherige Seite bestand aus einem Entwurfshinweis und Schreibaufträgen.
  Deren sinnvolle Themen bleiben erhalten: Prüfstand, positive/negative Fälle,
  optionale Bedingungen, Protokoll, Mängel, Rückbau und Übergabe.
- Neu sind ausführbare Schritte durch Geräte, Anschlüsse, Ressource und
  Zutrittsaktivität; sie unterscheiden Speicherung, Auftragsannahme,
  Gerätebestätigung, gemeldeten Hardwarezustand und Beobachtung an der Anlage.
- „Online“ wird auf eine eingegangene Meldung innerhalb von fünf Minuten begrenzt;
  „Betriebsbereit“ bestätigt nicht alle Anschlüsse. Fehlende Rückmeldung wird
  nicht als Geräteablehnung dargestellt.
- Normkonformität, physische Abnahme und ein allgemeines Offline-/Neustartverhalten
  werden nicht behauptet. Bedingungen, Übernahme und Unterbrechung sind optionale
  Prüffälle für die tatsächlich eingerichtete Variante.
- Eine administrativ beendete Backend-Sitzung ist vom bestätigten Endbefehl,
  der getrennten Leseraktualisierung und dem physischen Ergebnis unterschieden.
- Protokollvorlage und organisatorische Zuständigkeit sind manuelle Vorschläge;
  es wird kein Berichtsexport oder automatischer Prüfknopf erfunden. Der derzeit
  nicht freigegebene Datenbank-Backup-Bereich wird nicht als nutzbare Sicherung
  beschrieben.

## Quellen und relevante Stellen

Alle Softwarepfade beziehen sich auf die Repositorywurzel; Dokumentpfade auf
`web/content/docs/`.

| Aussage                                                                                               | Geprüfte Quelle                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Online-Schwelle, Lifecycle-Anzeigen                                                                   | `web/lib/device/device-status-utils.ts`, `isOnline`, `deviceLifecycleLabel`; `web/locales/de/devices.json`, `lifecycle`                                                                                                                                                                                                                                                                                                                                                                |
| Ein betriebsbereiter Anschluss genügt für Operational; vollständige Einrichtung prüft alle erwarteten | `api/Service/Devices/Application/Protocol/DeviceProtocolService.cs:237`, `UpdateReadinessAsync`; `service.Test/Devices/DeviceProtocolReadinessTests.cs:54`, `TwoReaders_MissingUnconfirmedOrFaultedSecondReader_FirstReaderRemainsUsable`; Zeile 81, `TwoReaders_BothReady_CompletesProvisioning`                                                                                                                                                                                      |
| Gespeicherte Sollwerte, bestätigte Werte und Auslesewerte getrennt; asynchroner Versand               | `api/Service/Devices/Application/Services/DeviceEndpointConfigurationService.cs:41`, `GetAsync`, `UpdateAsync`, `ReadbackAsync`; `service.Test/Devices/DeviceEndpointConfigurationServiceTests.cs:21`, `Update_TracksPendingAndAppliedWithoutPublishingBeforeCommit`; Zeile 44, `RejectedConfiguration_KeepsDesiredAndPreviousAppliedSeparate`; Zeile 81, `Readback_DoesNotChangeDesiredSettingsAndRetainsBothReceipts`                                                                |
| Bestehende Buttons und Anschlussstatus                                                                | `web/components/device/device-endpoints-panel.tsx:219`, `formatConfirmationBadgeLabel`; `reader-sensor-configuration.tsx:124`, Zuordnung zum aktuellen Auftrag, Pending und unsicherem Ergebnis; `web/locales/de/devices.json`, `actuators.status`, `endpointSettings`                                                                                                                                                                                                                 |
| Betrieb → Zutrittsaktivität, Sitzungen/Protokolle und Filter                                          | `web/components/layout/sidebar/dashboard-navigation.ts:43`; `web/locales/de/navigation.json:61`; `web/components/access/resource-activity-workspace.tsx:127`, Filter und Abfragen, Zeile 195, ViewSwitcher; `web/locales/de/resources.json`, `decisions`, `eventKinds`, `activityDetailsHint`                                                                                                                                                                                          |
| Protokolle und Sitzungen sind nach Ressourcenrechten begrenzt                                         | `api/Service/Accesses/Application/Services/ResourceAccessActivityService.cs:29`, `ViewSessions`; Zeile 261, `ViewLogs`; `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessActivityControllers.cs:25`, RequiredPermission View/Update Accesses                                                                                                                                                                                                                               |
| Administratives Backend-Ende und Hardwarezustellung getrennt                                          | `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessActivityControllers.cs:47`, XML-Vertrag zu End und GetEndCommand; `api/Service/Accesses/Boundary/Dto/ResourceAccessActivityDtos.cs:166`, End-Response; `web/components/access/resource-session-details.tsx:425`, Pending/Delivered/Failed; `web/locales/de/resources.json:260`, konkrete Meldungen; `service.Test/Accesses/ResourceAccessActivityServiceTests.cs:276`, `EndSessionCommitsAuditLogWhenDeviceDispatchFails` |
| Maschinenstart/-ende mit Aktorbestätigung; Impuls ohne Maschinensitzung                               | `service.Test/Devices/DeviceProtocolAccessIntegrationTests.cs:92`, `CardStartAndStop_RemoteActuator_ConfirmsExecutionAndPersistsSession`; Zeile 131, `CardStartAndStop_UsePersistedAccessSessionAndConfirmedActuatorResult`; Zeile 222, `UnlockScan_ExecutesBoundedPulseWithoutMachineSession`; Zeile 350, `UnconfirmedStop_LeavesSessionActiveForAnotherStopAttempt`                                                                                                                  |
| Gültige Buchung umgeht Kompetenzbedingung nicht; UND-Nachweise                                        | `service.Test/Accesses/ResourceAccessDecisionServiceTests.cs:57`, `BookingDoesNotBypassMissingCompetency`; Zeile 1088, `CombinedAuthorizationRequiresBothGrantAndBooking`; zu Aufsicht außerdem `RequiredSupervisionIsEnforcedEvenWithoutCompetencyRequirements`, `TwoReaderScansCreateOneSupervisedCanonicalDecision`                                                                                                                                                                 |
| Wiederkehrender Leser darf keinen pauschalen Neustart aller Aktoren implizieren                       | `service.Test/Devices/DeviceProtocolReaderReconnectionTests.cs:57`, `ReaderHello_RemoteActuatorSession_RestoresConfirmedSessionWithoutNewActuation`; daraus keine pauschale Hardwareaussage abgeleitet                                                                                                                                                                                                                                                                                 |
| Datenbank-Backup ist nicht freigegeben                                                                | `web/app/[project]/dashboard/admin/server/database-backup/page.tsx:12`, sichtbarer EmptyState ohne Backup-Aktion                                                                                                                                                                                                                                                                                                                                                                       |
| Kanonische Einrichtung und Übergabeinformationen                                                      | `docs/administration/geraete-verwalten.mdx`, `docs/koordination/ressourcen.mdx`, `docs/administration/tags-verwalten.mdx`, `docs/administration/benutzer-rollen.mdx`, `docs/administration/server-einstellungen.mdx`, `docs/administration/sicherheit-betrieb.mdx`                                                                                                                                                                                                                     |

Die genannten Tests wurden gelesen, nicht ausgeführt. Sie sind Codebelege für
die abgebildeten Verträge und keine Funktionsprüfung der installierten Hardware.

## Ausgeführte Prüfungen

- Prettier aus vorhandenen `web/node_modules`: Die Consumer-Ignorierliste schließt
  das Doku-Submodul aus. Deshalb ausschließlich die beiden eigenen Dateien mit
  `--ignore-path /dev/null --write` formatiert und anschließend mit
  `--ignore-path /dev/null --check` geprüft, erfolgreich.
- MDX-Kompilierung der Seite mit dem bereits installierten `@mdx-js/mdx`,
  erfolgreich; kein Gesamtbuild gestartet.
- Lokaler statischer Check: alle zwölf relativen Seitenverweise einschließlich
  vorhandener Zielanker aufgelöst; beide ursprünglichen Überschriften erhalten;
  Frontmatter vorhanden; keine TODO-Aufträge im Produkttext.
- `git diff --check` im Doku-Submodul für die beiden eigenen Dateien, erfolgreich.
- Keine Software-, Navigations- oder API-/DTO-Änderung. Keine Hardwareaktion,
  Serveraktion, Browserprüfung oder Normprüfung durchgeführt.

## Offene Prüfungen und Publikationsvorschlag

Die ausgearbeitete Seite kann nach Consumer-Rendering und redaktioneller Prüfung
als Anleitung zur **Durchführung** einer Prüfung veröffentlicht werden. Ihre
Veröffentlichung würde keine konkrete Installation abnehmen. Die spezifischen
Prüfergebnisse entstehen erst vor Ort mit passenden Hardware-/Firmwareunterlagen.

Koordinator: Desktop-/Mobilansicht und Markdown-/Agentenausgabe im Consumer prüfen.
Die Seite ist derzeit in `docs/installieren/meta.json` nicht enthalten; dort steht
nur `raspberry-pi`. Für eine Aufnahme die gemeinsame Navigation und Consumer-
Bereichsfilter prüfen. Im Seitenauftrag wurde nichts daran geändert.

Die vorhandenen Nachbarseiten `installieren/inbetriebnahme` und
`installieren/stoerung-vor-ort` waren beim Lesen noch Teilentwürfe. Der Verweis auf
„Störung vor Ort“ bleibt wie beauftragt erhalten; seine Nutzbarkeit muss der
Koordinator nach der parallelen Überarbeitung beurteilen. Es werden keine
LED-Codes oder Reset-Anweisungen aus diesen Entwürfen übernommen.

Für eine praktische Abnahme fehlen weiterhin gerätespezifische Montage-/
Sicherheitsunterlagen und Mess-/Beobachtungsergebnisse je Installation. Die
Anleitung schreibt deshalb keine feste Neustartdauer, Offlinewirkung oder
physische Abschaltgarantie vor. Kein neuer Seitenthemenbedarf und kein bestätigter
Softwarefehler aus dieser Prüfung.

## Geänderte Dateien

- `docs/installieren/abnahme-uebergabe.mdx`
- `planning/reviews/2026-11-01/installieren--abnahme-uebergabe.md`
