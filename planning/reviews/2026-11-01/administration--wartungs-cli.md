# P31: Mardu per CLI warten

## Änderungsbrief

Die Seite `docs/administration/wartungs-cli.mdx` beantwortet: Wie stelle ich bei
laufender API ohne Mardu-Login und ohne Reset-E-Mail den Zugang zu einem lokalen
Konto wieder her und prüfe den Serverzustand? Vorausgesetzt werden Terminal-/SSH-
und Docker-Compose-Kenntnisse sowie Zugriff auf den Installationsordner. Erwartetes
Ergebnis sind eine bestätigte Kontoaktion und die anschließende Anmeldung, bei
Diagnose eine lesbare Zustandsübersicht. Heimat bleibt Administration; die
Befehlsreferenz bleibt der Ort für Optionen, Rückgabewerte und Socketkonfiguration.

Die geprüfte Anleitung ist bereits weitgehend zutreffend. Erhalten bleiben Aufbau,
Voraussetzungen, vollständige Docker-Aufrufe, Reset-Schritte, Schutzmechanismen,
Fehlerhilfe und Funktionsgrenzen. Minimaler Patch: die Ergebniskontrolle nennt die
angezeigte Passwortwechselpflicht; der Profilverweis verwendet den aktuellen
Kontomenüeintrag. Statische Quellenprüfung, Format-, MDX- und Linkprüfung sind
geeignet; tatsächliche Kontowiederherstellung und Darstellung bleiben separat zu
prüfen. Keine Konten werden für diesen Auftrag verändert.

## Entscheidung und Befunde

**Verbessert.** Keine fachliche Neufassung erforderlich. Erst verdichtet geprüft:
Die Aufgabenanleitung und die Befehlsreferenz haben bereits getrennte Zwecke;
Schritte oder Schutzinformationen zu entfernen würde die Anleitung verschlechtern.
Danach nur zwei Klarstellungen vorgenommen:

- Nach `Action completed.` die Tabellenzeile `Password change required` mit dem
  gewählten Modus abgleichen (`Yes` temporär, `No` dauerhaft).
- Passwortänderung im angemeldeten Zustand über den belegten Kontomenüeintrag
  `Sicherheit` verlinken; die bisherige Pfadangabe `Mein Profil → Sicherheit`
  entspricht nicht dem aktuellen Kontomenü.

Unverändert belegt: lokale Passwortwiederherstellung nur bei vorhandenem lokalem
Passwort und ohne externe Verwaltung; Standard temporär; permanente Variante
`--permanent`; kein Passwortargument; Terminalpflicht und Bestätigung mit Standard
Nein; Passwortwiederholung verdeckt; Sitzungswiderruf; keine Aktivierung,
E-Mail-Bestätigung oder MFA-Aufhebung; gesondertes Entsperren; Diagnose repariert
nichts. Keine Backup-/OTA-Funktion oder Offline-Wiederherstellung ergänzt.

## Quellen

- `tools/Mardu.Admin.Cli/AdminCli.cs:19–107`: Terminalpflicht beim Menüstart,
  registrierte Befehle, englische Menüpunkte, Passwortmodi und Fehlerabbildung.
- `tools/Mardu.Admin.Cli/Commands.cs:10–45`: Pflicht-/Validierungsverhalten von
  `--email`, `--permanent`, lesende `--json`-Optionen; kein Passwortparameter.
- `tools/Mardu.Admin.Cli/MaintenanceOperations.cs:20–55,76–114`: Terminal- und
  Protokollprüfung vor Änderungen, Kontovorschau, Bestätigung, verdeckte Eingabe,
  Erfolgsanzeige, Healthchecks und Tabellenzeilen einschließlich
  `Password change required`.
- `tools/Mardu.Admin.Cli/MaintenanceClient.cs:15–58`: Unix-Socket, Versionsvergleich
  und Verwendung der zuvor ermittelten Konto-ID bei Änderungen.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.Maintenance.cs:24–59`:
  lokale Kontoprüfung, Passwortregeln, Fortsetzung des Sitzungswiderrufs nach
  Verbindungsabbruch, Entsperren und Sitzungswiderruf.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.Password.cs:137–160`:
  Speichern der Passwortwechselpflicht, Passwortreset und anschließender
  Sitzungswiderruf; Passwortänderungsereignis bleibt bestehen.
- `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:447–470`:
  Sitzungswiderruf und Invalidierung der Cacheeinträge.
- `api/Framework/Core/Identity/ILocalUserMaintenance.cs`: dokumentierte Konto- und
  Resetmodelle; lokale Passwortwiederherstellung, Pflichtfelder und Fehlerszenarien.
- `api/Server/Program.cs:181–218`, `api/Server/Hosting/LocalMaintenanceServer.cs`,
  `LocalMaintenanceEndpoints.cs`, `api/Framework/Core/Identity/LocalMaintenanceOptions.cs`:
  Normalbetrieb, lokaler Listener, Dateirechte, Pfad und registrierte Diagnose.
- `api/Server/Dockerfile:63,70,80–97`, `docker-compose.yml:101–107`: enthaltene CLI,
  `/app` als Arbeitsverzeichnis, Benutzer `mardu`, privater Socketbereich.
- `web/components/layout/common/account-menu-items.tsx:29–35`,
  `web/locales/de/navigation.json:31`: Kontomenüeintrag `Sicherheit` führt zur
  Authentifizierung im Profil.
- Nachbarseiten: `docs/administration/wartungs-cli-referenz.mdx`,
  `docs/administration/sicherheit-betrieb.mdx`,
  `docs/ueberblick/profil-sicherheit.mdx`, `docs/installieren/raspberry-pi.mdx`.
- Bestehende Tests `service.Test/Framework/Identity/AdminCliTests.cs` und
  `MaintenanceOperationsTests.cs` nur gelesen: Terminalpflicht, ungültige
  Parameter, Bestätigung, Protokollabweichung, verdeckte Eingabe und Passwortmodi.
  Nicht ausgeführt; keine Testabnahme behauptet.

## Checks und Praxisgrenzen

Ausgeführt und erfolgreich:

- `node web/node_modules/prettier/bin/prettier.cjs --check` für beide eigenen
  Dateien: Format korrekt (auch Ausgangsseite vor Änderung bereits korrekt).
- Einzelkompilierung der Seite mit vorhandenem `@mdx-js/mdx`: erfolgreich.
- Lokale lesende Node-Prüfung mit vorhandenem `github-slugger`: alle fünf
  relativen MDX-Verweise einschließlich Zielankern vorhanden; die sechs
  Überschriften stimmen mit `HEAD` überein.
- `git -C web/content/docs diff --check` für die eigenen Dateien: erfolgreich;
  Produktdiff manuell auf die zwei Klarstellungen begrenzt geprüft.

Browser, laufender Container,
Kontowiederherstellung, getrennte CLI-Verbindung und erneute Anmeldung sind in
diesem Auftrag nicht praktisch geprüft. Der Koordinator übernimmt gemeinsames
Rendering und Navigation. Für eine Verhaltensabnahme ist eine isolierte
Testinstallation mit lokalem Testkonto, temporärem und dauerhaftem Modus sowie
Entsperren/Sitzungswiderruf erforderlich. Keine Software- oder API-Vertragsänderung;
keine angepasste API-/DTO-Dokumentation erforderlich.

## Verweise und Drift

- URL und alle sechs bestehenden Überschriften/Anker bleiben erhalten. Keine Bilder
  oder neuen Komponenten. Vorhandene relative Seitenlinks bleiben bestehen.
- Kein neuer Seitenbedarf; kein Widerspruch zur zugewiesenen Befehlsreferenz
  festgestellt.
- Außerhalb des Dateieigentums: `docs/mardu-admin.md` im Software-Repository nennt
  unter „Passwort zurücksetzen“ noch pauschal einen Image-Build/Neustart als ersten
  Schritt. Die aktuelle Produktanleitung beschränkt das auf ältere Images und
  sagt zutreffend, dass ein Reset keinen Build/Neustart erfordert. Dieser Drift
  wurde dem Koordinator gemeldet; die Datei bleibt unverändert.

## Geänderte Dateien

- `web/content/docs/docs/administration/wartungs-cli.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--wartungs-cli.md`
