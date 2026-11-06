# Betrieb und Installieren: Seitenprüfung vom 3. November 2026

## Änderungsbrief

Aufgabe: Elf vorhandene Seiten am aktuellen Produkt prüfen, zuerst verdichten,
danach Sprache und Darstellung überarbeiten. Leser sind Personen, die Einstellungen
verwalten oder Server und Geräte installieren; Host-/Docker-Wissen wird nur in den
entsprechenden Anleitungen vorausgesetzt. Das Ergebnis sind nachvollziehbare
Bedienwege mit Voraussetzungen, Folgen und unterscheidbaren Prüfergebnissen.

Bestehende URLs und Abschnittsüberschriften bleiben erhalten. Gute Anleitungen
bleiben inhaltlich stehen. Native Fumadocs-Callouts und Steps werden nur für
entscheidende Folgen beziehungsweise aufeinanderfolgende Installationsphasen
verwendet; vorhandene Tabellen bleiben Vergleichs- und Referenzmittel. Keine
Software-, API-, Metadaten- oder Übersetzungsänderungen.

Quellen: aktuelle Einstellungen, Setup-Wizard, CLI, Controller, Dienste,
Produktübersetzungen, Production-Compose und TLS-Hosting. Geprüft werden Code,
Format, Links und Anker; zentraler Consumer-Render und gegebenenfalls Screenshots
folgen beim Koordinator. Keine Installation, Kontoänderung, Wiederherstellung,
Provider-, Versand- oder Hardwareprüfung wird ausgeführt.

## Offene Produktgrenze

Der Setup-Portkonflikt bleibt nach Codeabgleich bestehen:
`deploy/production/docker-compose.prod.yml` setzt `KestrelOptions__HttpPort=8080`,
`web/components/setup/setup-wizard.tsx` baut den Apply-Request mit `httpPort: 5001`;
`api/Framework/Infrastructure/Configuration/Setup/SetupOrchestrator.cs` weist die
Abweichung über `EnsureLockedValueMatches` ab. Der sichtbare Warnhinweis bleibt
in der Installationsanleitung. Keine Reparatur im Dokumentationsauftrag.

## Seiten

### administration/server-einstellungen.mdx — geändert

- Leserfrage: Wo ändere ich Servervorgaben, welche Rechte brauche ich und wann
  gelten gespeicherte Werte? Einstieg Administration → Systemeinstellungen.
- Quellen: `web/components/layout/settings/settings-search.tsx`,
  `settings-sidebar.tsx`, `server-nav.config.ts`, `config-settings-page.tsx`,
  `settings-runtime-banner.tsx`; `web/hooks/use-settings-search-query.ts`;
  `web/app/[project]/dashboard/admin/server/{global-settings,auth-policy,certificates,monitoring-settings,error-reporting,tag-settings}/`;
  `web/locales/de/settings.json`; `api/Service/Admin/Settings/Boundary/HttpControllers/{GlobalAppSettingsController,AuthPolicySettingsController}.cs`;
  `api/Framework/Infrastructure/Settings/Boundary/Dto/SettingsSectionDataDtos.cs`;
  `api/Framework/Infrastructure/Certificates/{Boundary/CertificatesController.cs,Boundary/Dto/CertificateDtos.cs,Application/CertificateService.cs}`;
  `api/Service/Observability/Boundary/HttpControllers/{MetricsSettingsController,ErrorReportingSettingsController}.cs`;
  `api/Framework/Infrastructure/Telemetry/{MetricsSettings.cs,ErrorReporting/ErrorReportingSettings.cs}`.
- Verdichtet und korrigiert: Die Oberfläche hat einen Button und Suchdialog,
  kein direktes Suchfeld in der Bereichsnavigation. Entfernt wurden die nicht
  angebotene Inline-Trefferliste, deren Escape-Verhalten und „Suche leeren“.
  Tastatur, Mindestlänge, Bereichspfade, Rechtefilter und Entwurfswarnung bleiben.
  Verschlüsselte private PEM-Schlüssel beim Dateipasswort ergänzt;
  Ressourcen-Querverweis auf Heimat Administration berichtigt, trotz historischer
  URL unter Koordination. Löschfolge als nativer Callout hervorgehoben.
- Browser: Globale Werte, nur lesbarer Installationsschlüssel, Aktiv/Hot Reload,
  Suche nach TLS samt Trefferwechsel zu Server-Zertifikaten und leerer
  Zertifikatsdialog praktisch geprüft; Uploaddialog ohne Eingabe geschlossen.
  Keine Einstellung gespeichert, kein Zertifikat hochgeladen/gewechselt/gelöscht.
- Bilder: `server-einstellungen-suche-aktuell.png` und
  `server-einstellungen-global-aktuell.png`, echte Oberfläche mit fiktiver
  Installation, Deutsch, helles Theme, 1440 × 1080; visuell geprüft, ImageZoom
  samt Alttext. Keine Änderung am dargestellten UI-Inhalt.
- Grenzen: Speichern, Fehlerzustände, externe Verbindungen und feldbezogene
  Betriebswirkung nur gegen Code geprüft, keine Neuabnahme aller Einstellungen.

### administration/sicherheit-betrieb.mdx — gezielt geändert

- Leserfrage: Wie vermeide ich Aussperrung und wie grenze ich Betriebsprobleme ein?
- Quellen: `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs`
  (Passwort-/2FA-Prüfung und erneute Prüfung der Anmeldesicherheit),
  `api/Framework/Infrastructure/Identity/Passkeys/PasskeyService.cs`
  (letzter Administrator-Passkey),
  `api/Framework/Infrastructure/Identity/Passwordless/PasswordlessLoginService.cs`,
  `api/Framework/Infrastructure/InfrastructureExtensions.cs`
  (Health-Predicates und 503 bei eingeschränktem Gesamtzustand),
  `api/Framework/Infrastructure/SetupModeExtensions.cs`,
  `web/app/[project]/dashboard/admin/server/database-backup/page.tsx`,
  `web/components/layout/settings/server-nav.config.ts`, CLI-Quellen unten.
- Inhaltlich passende Anmelde-, Sitzungs-, Rechte- und Störungsanleitungen erhalten.
  Fehlende Dashboard-/CLI-Sicherung als sichtbarer Callout; zum konkreten
  Update-Ablauf des Installationspakets verlinkt. Keine allgemeine
  Wiederherstellungsfähigkeit zugesagt.
- Grenzen: Keine neue Anmeldung unter geänderter Policy, keine Sitzung widerrufen,
  kein Backup, kein Update oder Wiederherstellungsversuch.

### administration/nachweise-datenschutz.mdx — geändert

- Leserfrage: Welchen Vorgang finde ich im Audit, wie exportiere ich ihn und
  welche weiteren Datenquellen muss ich getrennt berücksichtigen?
- Quellen: `web/app/[project]/dashboard/admin/server/audit-events/{audit-events-client.tsx,audit-event-details-sheet.tsx,use-audit-export.ts,use-audit-query-url.ts,data-table/audit-trail-data-table.tsx}`;
  `web/lib/audit/{audit-trail.ts,audit-trail-query.ts}`;
  `web/lib/stores/audit-trail-filter-url-serializer.ts`;
  `api/Framework/Infrastructure/Identity/Audit/{Boundary/AuditTrailController.cs,AuditService.cs,AuditTrailSpecifications.cs}`;
  `api/Framework/Infrastructure/Identity/Users/{Services/UserService.Delete.cs,UserDeletionImpactProvider.cs}`;
  `api/Framework/Infrastructure/Telemetry/MetricsSettings.cs`.
- Erhalten: UTC-Semantik, Personen-/Objektfilter-Unterschied, 10.000er-Grenze,
  getrennte Count-/Zeilenlesevorgänge, Historien- und Löschgrenzen.
  Korrigiert: Benutzer ist ein eigener Filterbutton; „Weitere Filter“ enthält
  Objekt-ID, Korrelations-ID und Client-IP. Exportdatei-Schutz als Callout;
  unbekannte Vollständigkeit an fehlende gültige Angaben statt an ein vermutetes
  Serveralter geknüpft.
- Browser: Auditliste, Objekttypfilter, UTC-Zeitraumdialog, weitere Filter und
  CSV-Download mit fiktiven Testdaten praktisch geprüft. Exportdatei mit
  erwarteten zehn Spalten und 36 Datenzeilen erhalten; durch parallele Testarbeit
  änderte sich die Trefferzahl gegenüber dem Listenstand. Der UI-Exportstatus
  meldete „Vollständigkeit ist unbekannt“, weil keine gültigen Exportangaben
  ankamen. Diese bereits dokumentierte Grenze bleibt sichtbar; Ursache des
  Headertransports nicht untersucht. Detailansicht nicht abschließend geprüft.
- Bild: `audit-trail-filter-aktuell.png`, gefilterte Auditliste mit geöffneten
  weiteren Filtern, Deutsch/hell/1440 × 1080, visuell geprüft und mit Alttext
  eingebunden. Nur Daten des isolierten Testsystems.
- Grenzen: Kein 10.000er-Lastfall, Excelabruf, vollständiges Auskunftsverfahren
  oder Löschvorgang. Keine rechtliche Prüfung oder Aussage zu gesetzlichen Fristen.

### administration/zertifikate-https.mdx — bewusst unverändert

- Leserfrage: Welche Komponente liefert das Zertifikat der verwendeten Adresse,
  und wie wird ein direkter API-Zertifikatswechsel vorbereitet und geprüft?
- Quellen: `api/Server/Program.cs` (Kestrel-Listener, Pfad und Passwort,
  Content-Root-Auflösung), `api/Server/Hosting/PersistentHttpsCertificateProvider.cs`,
  `docker-compose.https.yml`, `deploy/production/{docker-compose.prod.yml,Caddyfile}`,
  `api/Framework/Infrastructure/Certificates/Boundary/CertificatesController.cs`,
  `web/app/[project]/dashboard/admin/server/certificates/page.tsx`.
- Entscheidung: Die Tabelle trennt Listener, Caddy und Integrationsspeicher
  bereits verständlich; die Anleitung erhält Voraussetzungen, Neustartfolgen
  und getrennte Verbindungsprüfung. Weitere Steps oder Bilder würden dieselbe
  Unterscheidung wiederholen.
- Grenzen: Zertifikatsdialog lesend geöffnet; kein Zertifikats-/Dateiwechsel,
  API-Neustart, Proxytest oder Clientvertrauen geprüft.

### administration/wartungs-cli.mdx — bewusst unverändert

- Leserfrage: Wie prüfe ich lokal den Zustand oder stelle ein lokales Konto wieder her?
- Quellen: `tools/Mardu.Admin.Cli/{AdminCli.cs,Commands.cs,MaintenanceOperations.cs,MaintenanceClient.cs}`;
  `api/Framework/Infrastructure/Identity/Users/Services/UserService.Maintenance.cs`;
  `api/Server/Hosting/{LocalMaintenanceEndpoints.cs,LocalMaintenanceServer.cs,LocalMaintenanceHostingExtensions.cs}`;
  `api/Server/Dockerfile`, `deploy/production/docker-compose.prod.yml`.
- Entscheidung: Menü, Terminalvoraussetzung, temporäres/dauerhaftes Passwort,
  Bestätigung und verdeckte Eingabe entsprechen dem aktuellen Code. MFA,
  Aktivierung, E-Mail-Bestätigung und nicht unterstützte externe Konten sind
  getrennt erklärt. Die sichtbare Reihenfolge benötigt keine zusätzlichen Steps.
- Grenzen: Nur Codeabgleich; keine CLI-Kontoänderung oder Recovery ausgeführt,
  keine Aussage über einen praktisch bestandenen Reset.

### administration/wartungs-cli-referenz.mdx — bewusst unverändert

- Leserfrage: Welche Befehle, JSON-Felder, Rückgabewerte und Socket-Einstellungen gelten?
- Quellen: CLI- und Hostingdateien wie oben;
  `api/Framework/Core/Identity/{MaintenanceProtocol.cs,LocalMaintenanceOptions.cs,ILocalUserMaintenance.cs}`.
- Entscheidung: Optionen, englische Menüs, JSON nur für lesende Befehle,
  30-Sekunden-Timeout, Abbruchwert 130, private Socket-Rechte und Protokollprüfung
  sind zutreffend. Tabellen sind dafür das passende native Markdown-Mittel.
- Grenzen: Keine Ausführung eines CLI-Befehls; JSON-/Exitcode-Verhalten ist durch
  Implementierungslektüre und nicht durch einen neuen Prozesslauf belegt.

### installieren/abnahme-uebergabe.mdx — bewusst unverändert

- Leserfrage: Welche Beobachtungen brauche ich für einen nachvollziehbaren
  Funktionstest und eine Übergabe vor Ort?
- Quellen: `web/app/[project]/dashboard/device-management/device-settings/{device-settings-sheet.tsx,device-readers-settings.tsx}`;
  `web/locales/de/{devices,access}.json`; `web/lib/device/device-status-utils.ts`;
  `api/Service/Devices/Application/Protocol/DeviceProtocolService.cs`
  (ein betriebsbereiter Anschluss versus vollständige Konfiguration),
  `api/Service/Accesses/Application/Services/AccessSessionEndCommandService.cs`.
- Entscheidung: Positiv-/Negativtest, Ende eines Servervorgangs versus
  Befehlszustellung, getrennte Hardwarewirkung und Protokollvorlage sind bereits
  verständlich und zutreffend. Die Tabellen unterstützen den Vergleich.
- Grenzen: Keine Hardware, Tür, Maschine, Strom-/Netzunterbrechung oder
  Sicherheits-/Normprüfung. Die Seite gibt den Prüfauftrag vor, sie belegt keine
  Abnahme einer realen Installation.

### installieren/inbetriebnahme.mdx — bewusst unverändert

- Leserfrage: Wie nehme ich einen montierten Controller am vorhandenen Server auf
  und erkenne, welche Anschlüsse geprüft werden müssen?
- Quellen: `api/Service/Devices/Boundary/HttpControllers/{DevicesController,DeviceEnrollmentController}.cs`;
  `api/Service/Devices/Application/Services/DeviceService.CreationUpdate.cs`;
  `api/Service/Devices/Application/Protocol/{DeviceProtocolService.cs,DeviceProtocolService.Registration.cs}`;
  `web/app/[project]/dashboard/device-management/device-settings/{device-settings-sheet.tsx,device-readers-settings.tsx}`;
  `web/locales/de/devices.json`.
- Entscheidung: Bestehende Aufnahme- und Konfigurationsanleitung bleibt.
  Automatischer Schlüsselaustausch, Modell-/Anschlusskatalog, separate
  Ressourcen-/Regelzuordnung und Anschlussbereitschaft stimmen überein.
  Links bleiben auf die kanonischen Anleitungen gerichtet; Ressourcen gehören
  trotz historischer URL zur Administration.
- Grenzen: Kein Geräteimport, keine MQTT-Verbindung oder Konfigurationssendung,
  keine Montage-/Hardwareprüfung.

### installieren/index.mdx — bewusst unverändert

- Leserfrage: Beginne ich mit dem Serveraufbau, der Geräteaufnahme oder einem
  bestehenden Betriebsproblem?
- Quellen: Fünf aktuelle Installationsseiten sowie
  `web/lib/docs-roles.tsx` und `web/content/docs/docs/administration/ressourcen-anleitungen/meta.json`.
- Entscheidung: Der kurze aufgabenbezogene Einstieg verweist bereits auf die
  nutzbaren Anleitungen und die bekannte Erstsetup-Grenze. Keine zusätzliche
  Kartenebene oder wiederholte Inhaltszusammenfassung nötig.
- Grenzen: Navigation statisch abgeglichen; keine Installation durch diesen
  Seitenaufruf verifiziert.

### installieren/raspberry-pi.mdx — Darstellung gezielt geändert

- Leserfrage: Wie bereite ich das Installationspaket vor, richte den Server ein
  und übernehme spätere Releases ohne Datenvolumenverlust?
- Quellen: `deploy/production/{docker-compose.prod.yml,Caddyfile,.env.deploy.example}`;
  `.github/workflows/release-container.yml` und
  `web/.github/workflows/release-container.yml` (Archivinhalt, stabile Tags,
  ARM64-/AMD64-Images); `api/Server/Dockerfile`;
  `web/components/setup/setup-wizard.tsx` (Apply-Payload, Testschritte, Mindestpasswort);
  `api/Framework/Infrastructure/Configuration/Setup/{SetupOrchestrator.cs,SetupConfigurationDraftService.cs,SetupTokenService.cs}`;
  `api/Framework/Infrastructure/SetupModeExtensions.cs`.
- Erhalten: Befehle, Domain-/Registry-/Broker-Voraussetzungen, Paket-/Image-Tags,
  sensible Werte, Persistenz und Upgrade-/Migrationsgrenzen. Vier Installationsphasen
  mit nativen Steps gegliedert; sichtbarer Setup-Warnhinweis vor den Startbefehl
  gezogen. `.env`-Aufbewahrung und `down -v`-Datenverlust als Callouts. Alle fünf
  historischen nummerierten Abschnittsanker durch vorhandenes span-Muster erhalten.
- Browser: Consumer rendert Steps und Warnungen. Kein Setup-Screenshot, da die
  Laufzeit bereits eingerichtet ist; weder Setup zurückgesetzt noch angewendet.
- Grenzen: Kein Paketdownload, Registry-Login, Imagepull, Compose-Aufruf,
  DNS-/Caddy-Zertifikatstest, Erstsetup oder Release-Update. GHCR-Kontorechte und
  externe Registry-Regeln nicht neu praktisch geprüft.

### installieren/stoerung-vor-ort.mdx — bewusst unverändert

- Leserfrage: Wie trenne ich Server-, Netzwerk-, Konfigurations- und
  Zugangsprobleme, bevor ich Änderungen an Geräten auslöse?
- Quellen: `web/lib/device/device-status-utils.ts` (fünf Minuten),
  `web/app/[project]/dashboard/device-management/device-settings/{device-settings-sheet.tsx,device-readers-settings.tsx}`;
  `web/locales/de/{devices,access}.json`;
  `api/Service/Devices/Application/Protocol/DeviceProtocolService.cs`;
  `api/Service/Devices/Boundary/HttpControllers/DeviceEnrollmentController.cs`;
  Health- und CLI-Quellen wie oben.
- Entscheidung: Ablauf, Vergleichstabelle und Eskalationsangaben sind bereits
  klar. Unbestätigt/abgelehnt/physisch wirksam bleiben getrennte Aussagen.
  Erneute Aufnahme bleibt an die korrekten Voraussetzungen gebunden.
- Grenzen: Keine Störung erzeugt oder behoben, kein Hardware-/Wiederanlauftest.

## Ausgeführte gemeinsame Dokumentprüfungen

- Prettier: `bun x --bun prettier --ignore-path /dev/null --check` mit genau den
  elf Paketdateien aus `web/`: erfolgreich.
- `git -C web/content/docs diff --check` scoped auf die elf Seiten und diesen
  Paketbericht: erfolgreich.
- Read-only Link-/Ankerprüfung mit vorhandenem `github-slugger`: alle elf Seiten,
  91 relative MDX-Verweise sowie alle bisherigen IDs aus
  `/tmp/mardu-docs-revision-20261103/baseline-render.json`: kein Fehler.
- Consumer-Render im bereitgestellten Testsystem, eigene Playwright-Session
  `docs-revision-betrieb`: alle elf Seiten bei 1440 × 900 und 390 × 900 mit
  HTTP 200 und ohne horizontalen Seitenoverflow. Die drei neuen Bilder auf den
  geänderten Seiten wurden geladen und dekodiert, kein defektes Bild. RPi-Steps,
  alten Anker `#4-starten-und-einrichten` und Warnhinweis zusätzlich bei 390 px
  visuell geprüft. Protokolle:
  `/tmp/mardu-docs-revision-20261103/render-betrieb.txt` und
  `/tmp/mardu-docs-revision-20261103/render-betrieb-erhalten.txt`.
- Native Komponenten aus der installierten Fumadocs-Version geprüft:
  `web/node_modules/fumadocs-ui/dist/components/steps.d.ts` und bestehende
  `web/mdx-components.tsx`-Einbindung für Callout/ImageZoom. Keine neuen Komponenten,
  Styles oder Dependencies.
- Keine API-/DTO-Verträge verändert; daher keine generierte API-Dokumentation
  oder XML-/OpenAPI-Datei angepasst. Keine Softwaredatei verändert.

Stand: **zur Prüfung**. Abschließende Consumer-Prüfung einschließlich beider
Consumer, Markdown-/Agentenausgabe und zentraler Navigationstests durch den
Koordinator; nicht als umfassende Betriebs- oder Hardwareabnahme zu verstehen.

## Ergänzung: fokussierte Serveraufgaben

Nach dem unabhängigen Strukturreview wurden drei Aufgaben aus dem Servereinstieg
in eigene kanonische Anleitungen verschoben. `server-einstellungen.mdx` erklärt
weiterhin Suche, gemeinsames Speichermodell und Global App. Die bisherigen neun
Anker der ausgegliederten Themen sind als `span` erhalten und führen zu sichtbaren
Zielverweisen. Die zusätzliche DESFire-Serverreferenz bleibt einschließlich der
Schlüssel-TTL in **Sekunden** erhalten; sie ist nicht die Enrollment-Laufzeit.

### administration/anmeldevorgaben.mdx — neue kanonische Anleitung

- Leserfrage: Wie lege ich Selbstregistrierung und Anmeldebedingungen fest, ohne
  betroffene Konten unvorbereitet auszusperren?
- Quellen: `web/app/[project]/dashboard/admin/server/auth-policy/page.tsx`,
  `web/locales/de/settings.json`,
  `api/Service/Admin/Settings/Boundary/HttpControllers/AuthPolicySettingsController.cs`,
  `api/Framework/Core/Auth/AuthPolicySettings.cs`,
  `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs`,
  `api/Framework/Infrastructure/Identity/Passkeys/PasskeyService.cs` sowie der
  vorhandene Passwortlos-/OIDC-Vertrag aus dem ersten Quellenabgleich.
- Aus Servereinstellungen verschoben: Registrierungsmodi, Standardrolle,
  Linkgültigkeit, Verfahren und Wiederherstellung, Passwort-/Sperrregeln,
  Token-Laufzeiten. Die konkrete Wirkung der Admin-/Passkey-/2FA-Schalter und
  die neue Anmeldeprüfung stehen jetzt hier; `sicherheit-betrieb.mdx` verweist
  darauf und behält Kontowiederherstellung und Sitzungsbetrieb.
- Ergänzt: nachvollziehbarer Ablauf zum Speichern, erneuten Laden und Prüfen
  mit getrenntem Testkonto sowie Fehlerhilfe. Rechte, vorhandene Kontoverfahren,
  Neustartfolgen und Grenzen des Passwort-Resets bleiben sichtbar.
- Darstellung: nummerierte Handlungen, native Markdown-Tabellen und Callout vor
  dem Speichern neustartpflichtiger Tokenänderungen. Kein zusätzlicher Screenshot,
  der gegenüber den konkreten Feldnamen und Abläufen keinen Nutzen belegt.
- Grenze: Keine Auth Policy gespeichert, kein neues Konto angelegt, kein
  zweiter Faktor oder externer Anbieter geändert.

### administration/integrationszertifikate.mdx — neue kanonische Anleitung

- Leserfrage: Wie hinterlege, ersetze oder lösche ich Zertifikatsmaterial für
  eine Integration, und welchen Verbindungstest brauche ich danach?
- Quellen: `web/app/[project]/dashboard/admin/server/certificates/page.tsx`,
  `web/components/server/certificates-card.tsx`,
  `api/Framework/Infrastructure/Certificates/Boundary/CertificatesController.cs`,
  `api/Framework/Infrastructure/Certificates/Boundary/Dto/CertificateDtos.cs`,
  `api/Framework/Infrastructure/Certificates/Application/CertificateService.cs`.
- Aus Servereinstellungen verschoben: Bestand/Suche, PEM-/PFX-Upload, Schlüssel,
  Passwort, Selbstsignaturfreigabe, Austausch mit erhaltener ID und Löschung.
  Ersetzen und Löschen erhalten je einen eigenen Ablauf mit Ergebnisprüfung.
- Deutlich getrennt: Speicher und Dienstzuordnung ändern nicht das Browser-
  HTTPS-Zertifikat. Der HTTPS-Leitfaden bleibt für Kestrel/Proxy kanonisch und
  verlinkt für den Speicherwechsel direkt hierher. Sicherheit und Betrieb
  verweist bei gespeichertem Integrationsmaterial ebenfalls auf diese Seite.
- Darstellung: sichtbare Voraussetzungen und Folgen, nummerierte Abläufe,
  zwei native Callouts und symptombezogene Fehlerhilfe. Vorheriger lesender
  Browserabgleich von leerer Liste und Uploaddialog bleibt der praktische Beleg;
  keine künstlichen Zertifikatsdaten und kein weiterer Screenshot nötig.
- Grenze: Kein Upload, Wechsel, Löschen, API-Neustart oder externer TLS-Test.

### administration/monitoring-einrichten.mdx — neue kanonische Anleitung

- Leserfrage: Wie lege ich lokale Messwerterfassung und Alarmgrenzen fest, und
  wie entscheide ich getrennt über die Übertragung von Diagnosedaten?
- Quellen: `web/app/[project]/dashboard/admin/server/monitoring-settings/page.tsx`,
  `web/app/[project]/dashboard/admin/server/error-reporting/page.tsx`,
  `web/components/layout/settings/server-nav.config.ts`,
  `api/Service/Observability/Boundary/HttpControllers/MetricsSettingsController.cs`,
  `api/Service/Observability/Boundary/HttpControllers/ErrorReportingSettingsController.cs`,
  `api/Framework/Infrastructure/Telemetry/MetricsSettings.cs`,
  `api/Framework/Infrastructure/Telemetry/ErrorReporting/ErrorReportingSettings.cs`,
  `api/Framework/Infrastructure/Telemetry/ErrorReporting/ErrorReportingExtensions.cs`,
  `api/Framework/Infrastructure/Telemetry/ErrorReporting/ErrorReportingService.cs`.
- Aus Servereinstellungen verschoben: Sammlung, Fristen, HTTP-/Speicheralarme,
  Bestätigungssamples sowie separate Fehlerberichtsfreigabe, Sampling,
  Laufzeitangaben, Transportvoraussetzung und Widerrufsfolge. Die Fristen und
  ihre Defaults stehen jetzt hier; die Datenschutzanleitung verlinkt darauf.
- Ergänzt: Zweckvergleich lokale Metriken versus Sentry-kompatible
  Fehlerberichterstattung, Speicher-/Prüfschritte, getrennte Verbindung zur
  Benachrichtigungszustellung und symptombezogene Fehlerhilfe. Folgen des
  Abschaltens stehen **vor** der betroffenen Aktion. Keine Zusage über einen
  externen Empfang und kein erfundener Dashboard-Versandtest.
- Darstellung: native Markdown-Tabellen für Zweck und Fristen, nummerierte
  Handlungen und ein Callout für die Widerrufsfolge. Kein zusätzliches Bild nötig.
- Grenze: Keine Messwert-/Alarmkonfiguration geändert und kein Fehlerbericht,
  Performance-Ereignis oder Zustelltest erzeugt.

### Prüfungen der Strukturkorrektur

- Read-only Prüfung mit vorhandenem `github-slugger`: 14 Paketdateien,
  106 relative Verweise sowie alle bisherigen IDs aus dem Baseline-Render:
  kein fehlendes Ziel und kein verlorener Anker.
- Navigation, gemeinsame Querverweise und Inventar werden wie beauftragt durch
  den Koordinator ergänzt. Keine Meta-/Software-/Übersetzungsdatei geändert.
- Prüfgrenzen und Status **zur Prüfung** bleiben bestehen; die neue Struktur
  ersetzt keine praktische Auth-, Zertifikats- oder Anbieterverifikation.
- Prettier für die sieben betroffenen/neuen MDX-Seiten und den Paketbericht:
  erfolgreich; scoped `git diff --check`: erfolgreich.
- Browser-Render der sieben betroffenen/neuen Seiten bei 1440 × 900 und
  390 × 900: alle 14 Aufrufe HTTP 200, kein horizontaler Seitenoverflow,
  keine defekten Bilder. Alle bisherigen IDs dieser Bestandsseiten sind auch
  im gerenderten DOM erhalten. Protokoll:
  `/tmp/mardu-docs-revision-20261103/render-betrieb-struktur.txt`.
