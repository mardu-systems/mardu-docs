# P27 – Servereinstellungen

## Änderungsbrief

- Seite: `docs/administration/server-einstellungen.mdx`.
- Leserfrage: Wie lese und ändere ich vorhandene Servereinstellungen, und wann werden sie wirksam?
- Vorwissen: angemeldetes Konto; Bedienung des Dashboards, keine Kenntnis von DTOs vorausgesetzt.
- Ergebnis: nutzbare Anleitung mit belegten Formularen, Rechten, Grenzen und Folgen. Heimatbereich Administration.
- Bestehende gute Inhalte: sieben Abschnittsanker, Verweise auf Benachrichtigungen/Systemstatus und MCP erhalten. Platzhalteraufträge aus dem Produkttext entfernen.
- Quellen: vorhandene Servernavigation, gemeinsames Einstellungsformular, deutsche Übersetzungen, zuständige Controller, Verträge und konsumierende Dienste.
- Plan: gemeinsame Bedienung verdichten; Global/Auth/Zertifikate/Monitoring/Tags anhand vorhandener Felder erklären; fehlende Backup-/Updateverfahren nicht ersetzen; lokale Format-/Link-/MDX-Prüfung. Consumer- und Praxisprüfung beim Koordinator.
- Prüfgrenzen: ausschließlich statische Quellenprüfung; keine Konfigurationsänderung, Provider-, Hardware- oder Browserprüfung.

## Entscheidung und Umsetzung

**Verbessert – belegbare Teildokumentation / offene Prüfung.** Die versteckte
TODO-Seite enthält jetzt eine verwendbare Anleitung für die vorhandenen
Einstellungsformulare. Sie beansprucht keine vollständige Betriebs- oder
Integrationsanleitung.

- Gemeinsamen Ablauf mit Laden, Bereichssuche, Entwurf, Verwerfen, Validierung,
  Speichern, Fehlerhilfe, ENV-/dotenv-Sperren, Quellen- und Laufzeitstatus beschrieben.
- Rechte nach Menü und Backend unterschieden: Monitoring/Fehlerberichte im Menü
  nur mit `Settings.Update`, APIs lesen mit `Settings.View`; Zertifikatmutationen
  benötigen ebenfalls `Settings.Update` (kein separates Delete-Recht).
- Global-Felder, drei Registrierungsmodi, Anmeldeschutz und Einheiten/Grenzen
  dokumentiert. Direkte Registrierung nicht pauschal an E-Mail-Bestätigung gebunden;
  hierfür ist `RequireConfirmedAccount` maßgeblich. Keine Startwerte aus
  `EMPTY_FORM` als Serverdefaults übernommen.
- Zertifikat hinzufügen/ersetzen/löschen mit Folgen, Gültigkeit, optionalem
  CA-Schlüssel und separater Integrationszuordnung erklärt. Keine automatische
  Erneuerung, Abhängigkeitsansicht oder HTTP-/Proxy-Aktivierung behauptet.
- Tatsächlich vorhandene Metrikalarme (Systemzustand, HTTP 5xx, Speicherplatz),
  Aufbewahrung und Bestätigungssamples aufgenommen. Fehlerberichte als Opt-in,
  Performance-Sampling und Server-Queue-Löschung mit Client-Neuladen beschrieben.
- Tags auf drei sichtbare Eingaben begrenzt. Keine Schlüssel-/Versionsverwaltung
  aus dem Seitentitel abgeleitet. Integrations-/Aufgabenanleitungen verlinkt.
- Gute vorhandene Links zu Benachrichtigungen, Systemstatus und MCP sowie alle
  sieben alten H2-Überschriften/Anker erhalten. Keine neuen Assets/Komponenten.
- Dashboard-Backup ist aus der Navigation auskommentiert. Kein Sicherungs-,
  Export-, Update- oder Wiederherstellungsverfahren erfunden.

## Quellen und fachliche Belege

Pfade sind relativ zum Software-Repository, sofern nicht anders angegeben.

| Aussage                                      | Geprüfte Quelle / relevante Stelle                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Menüs, Rechte, Suche und verstecktes Backup  | `web/components/layout/settings/server-nav.config.ts:46` (Bereichsliste und auskommentierter Backup-Eintrag); `settings-sidebar.tsx:104` (Berechtigungsfilter); `web/app/[project]/dashboard/admin/server/layout.tsx` (Suchprovider).                                                                                                                                                                                                                                                                                                                                 |
| Gemeinsame Formularbedienung                 | `web/components/layout/settings/config-settings-page.tsx:154` (Laden), `:216` (Speichern, Erfolg/Fehler), `:266` (Validierung), `:326` (Verwerfen); `settings-field-renderer.tsx:47` (Metadatenhinweise), `:222` (Feldsperren); `settings-runtime-banner.tsx` und `web/lib/settings/utils.ts` (Statuswörter).                                                                                                                                                                                                                                                         |
| Deployment-Sperren                           | `api/Framework/Infrastructure/Settings/SettingsEnvironmentLock.cs` (`GetLockInfo`, `.env`-Quellen und `RejectLockedChange`); feldweise Verwendung in Global/Auth/Tag/ErrorReporting-Controllern. Keine pauschale Sperre aller Bereiche behauptet.                                                                                                                                                                                                                                                                                                                     |
| Globale Felder und Grenzen                   | `web/app/[project]/dashboard/admin/server/global-settings/page.tsx:33`; `api/Service/Admin/Settings/Application/GlobalAppSettings.cs`; `.../Boundary/HttpControllers/GlobalAppSettingsController.cs` (GET/PUT, Rechte, HotReload); `api/Framework/Infrastructure/Settings/Boundary/Dto/SettingsSectionDataDtos.cs:10`.                                                                                                                                                                                                                                                |
| Wartung/Cloud und Sitzungslimit              | `api/Service/Admin/Settings/Application/SettingsService.cs:116` (`GetSystemConfigurationAsync`) und `:159` (Cloud-Getter); repositoryweite Suche nach Konsumenten von `MaintenanceMode`/`EnableCloudCommunication` ohne Beleg einer Anmeldesperre oder eingerichteter Cloud-Anbindung; `api/Service/Accesses/Application/Services/ResourceAccessDecisionService.cs:272` und `ResourceAccessDecisionService.Transfers.cs:117` (Sitzungslimit).                                                                                                                         |
| Auth-Felder, abhängige Eingaben und Neustart | `web/app/[project]/dashboard/admin/server/auth-policy/page.tsx:23` und `restartRequiredFields`; `api/Framework/Core/Auth/AuthPolicySettings.cs:8` (Felder und Validierung); `api/Service/Admin/Settings/Boundary/HttpControllers/AuthPolicySettingsController.cs:30` (GET-Metadaten), `:78` (PUT-Vertrag); `api/Framework/Infrastructure/Identity/SelfRegistration/Services/SelfRegistrationService.cs:537` (Rolle), `:557` (Anfangsstatus).                                                                                                                          |
| Zertifikate und Folgen                       | `web/app/[project]/dashboard/admin/server/certificates/page.tsx:250` (Validierung/Upload/Rotation), `:307` (Löschen); `web/components/server/certificates-card.tsx` (Tabelle, Suche/Filter, Bestätigung); `api/Framework/Infrastructure/Certificates/Boundary/CertificatesController.cs:22`; `.../Application/CertificateService.cs:42` (Upload), `:69` (Rotation), `:104` (Entfernen), `:128` (Parsing und Ablehnungen).                                                                                                                                             |
| Metriken und Alarme                          | `web/app/[project]/dashboard/admin/server/monitoring-settings/page.tsx`; `api/Framework/Infrastructure/Telemetry/MetricsSettings.cs:7` (Bereiche, Einheiten und feldübergreifende Validierung); `api/Service/Observability/Boundary/HttpControllers/MetricsSettingsController.cs`; `.../Application/MetricsAlertEvaluator.cs:26` sowie `:96`, `:137`, `:151` (HTTP, OR bei Verletzung, AND bei Erholung).                                                                                                                                                             |
| Fehlerberichte, Status und Testgrenze        | `web/app/[project]/dashboard/admin/server/error-reporting/page.tsx` (drei editierbare Werte, sonst Anzeige, Bestätigung, kein Testbutton); `api/Service/Observability/Boundary/HttpControllers/ErrorReportingSettingsController.cs:54` (PUT/Queue-Löschung) und `:90` (API-Test); `api/Framework/Infrastructure/Telemetry/ErrorReporting/ErrorReportingScrubber.cs:33`; `web/lib/error-reporting/client-consent.ts:39`; `web/instrumentation-client.ts`; `web/components/error-reporting/error-reporting-consent-bootstrap.tsx:17` (Abruf je Sitzung/Projekt/Server). |
| Tag-Eingaben und Schlüsselgrenzen            | `web/app/[project]/dashboard/admin/server/tag-settings/page.tsx:29`; `api/Service/Tags/Boundary/HttpControllers/TagSettingsController.cs:37` (PUT: automatische URL, atomare Änderung und Erhalt Schlüsselmaterial), `:104` (Metadaten); `api/Framework/Infrastructure/Settings/Boundary/Dto/SettingsSectionDataDtos.cs` (`TagSettingsDataDto`/`UpdateTagSettingsDto`).                                                                                                                                                                                               |
| Exakte deutsche Bezeichnungen                | `web/locales/de/settings.json` (settings/globalApp/authPolicy/metrics/errorReporting/tag, serverSettings/certificates, MCP); `web/locales/de/navigation.json` (Servernavigation).                                                                                                                                                                                                                                                                                                                                                                                     |

## Produktwidersprüche / Prüfbedarf

1. **Leere Tag-Adresse wird vom Frontend abgelehnt.**
   `tag-settings/page.tsx:41` führt auch bei leerer Eingabe `new URL('')` aus und
   liefert einen Fehler. Feldhilfe und Backend erlauben leer/null für automatische
   Ermittlung (`TagSettingsController.cs:51`). Deshalb keine Anleitung zum
   Zurücksetzen auf automatische Ermittlung veröffentlicht. Vor der Ergänzung UI
   mit leerem Ausgangswert/Leeren prüfen und Produktfehler separat bearbeiten.
2. **Neustarthinweise Auth sind nicht deckungsgleich.**
   Frontend-`restartRequiredFields` enthält zusätzlich `selfRegistrationLinkHours`;
   Backend-Feldmetadaten setzen dafür `RequiresRestart=false`. Die Seite garantiert
   nur für die beiden Tokenlaufzeiten den ausdrücklich dokumentierten Neustart und
   verlangt ansonsten, Hinweise nach dem Speichern zu beachten. Den Unterschied
   sollte die zuständige Softwareprüfung auflösen.
3. **Verschlüsseltes PEM nicht pauschal zugesagt.** Feldhilfe erwähnt Passwort auch
   für verschlüsselte private Schlüssel. `CertificateService.LoadPem` verwendet
   `CreateFromPem`, nicht `CreateFromEncryptedPem`. Eine Unterstützung
   passwortgeschützter PEM-Schlüssel ist hier nicht belegt; die Anleitung nennt
   das Dateipasswort daher konkret für PFX/P12. Praktischer Zertifikatscheck offen.
4. **Fehlerbericht-Freigabe in offenen Clients.** Der Bootstrap lädt bei Änderung
   von Sitzung/Projekt/Server neu, aber nicht auf eine Einstellungsmutation. Daher
   enthält die Anleitung den Reload bereits geöffneter Dashboard-Sitzungen.
   Widerruf/Providerempfang wurden nicht praktisch geprüft. Der API-Test ist
   vorhanden, wird aber im Dashboardformular nicht angeboten; kein UI-Testablauf
   daraus abgeleitet.

## Verweise, Zusatzseiten und Veröffentlichung

- Publikationsvorschlag: Nach Consumer-Rendering und fachlicher Durchsicht als
  Anleitung für die beschriebenen vorhandenen Formulare unter Administration
  sichtbar machen. Derzeit weiterhin versteckt; `meta.json`, Slugfilter, Suche und
  LLM-Index wurden auftragsgemäß nicht geändert.
- Konkreter zusätzlicher Seitenbedarf: eine **Betriebsanleitung für Sicherung,
  Wiederherstellung und Updates einer benannten unterstützten Betriebsform**.
  Benötigt geprüftes Inventar von Datenbank, Dateien, Konfiguration, privaten
  Schlüsseln und ASP.NET-Datenschutzschlüsseln, konsistente Sicherung und echten
  Wiederherstellungstest. Kein Link auf eine noch nicht vorhandene Seite gesetzt.
- Eigene Detailanleitung **Zertifikate verwenden und erneuern** wird sinnvoll,
  sobald Verbraucherzuordnung und reale TLS-/Rotationsprüfung je LDAP/OIDC/MQTT
  vorliegen. Die neue Kurzbedienung hier kann dabei als Einstieg erhalten bleiben.
- Nachbarseiten Integrationen und Sicherheit/Betrieb enthalten weiterhin eigene
  Entwurfsabschnitte. Die Links hier sind Orientierung, keine Abnahme dieser
  Seiten. Auth-Notfall-/Aussperrungsabläufe sollen in Sicherheit/Betrieb bleiben.
- Keine neue allgemeine Feldreferenzseite nötig: belegte Kernfelder stehen hier,
  Anbindungen haben eigene aufgabenbezogene Anleitungen.

## Ausgeführte Checks und Grenzen

- MDX mit vorhandenem `web/node_modules/@mdx-js/mdx` kompiliert: erfolgreich.
- Lokale Prüfung: Frontmatter vorhanden; kein zusätzliches H1; keine TODOs oder
  Checkbox-Schreibaufträge; alle sieben bisherigen H2-Überschriften erhalten;
  alle 15 relativen Seitenlinks und ihre vorhandenen Zielanker aufgelöst.
- Prettier für genau beide eigenen Dateien mit `--ignore-path /dev/null`
  ausgeführt (Docs-Submodule wird vom Consumer normalerweise ignoriert).
- `git diff --check` auf genau den eigenen Dateien und abschließender
  Prettier-Check durchgeführt; Ergebnis siehe abschließende Ausführung.
- Keine Tests, Softwareänderungen, neuen Abhängigkeiten oder geänderten API-/DTO-
  Verträge. Bestehende OpenAPI-/XML-Verträge als Beleg verwendet; keine
  API-Dokumentationsänderung nötig.
- **Keine Browser-, Mobile-, Tastatur-, Website-Consumer-, Hardware-, Provider-
  oder echte Konfigurationsprüfung.** Koordinator übernimmt Rendering/Navigation;
  Wirkung strenger Auth-Vorgaben, Tokenneustart, Zertifikatsrotation und externer
  Fehlerberichtempfang brauchen geeignete Praxiszugänge. Kein globaler Build.

Geänderte Dateien: `web/content/docs/docs/administration/server-einstellungen.mdx`
und dieser Bericht
`web/content/docs/planning/reviews/2026-11-01/administration--server-einstellungen.md`.
