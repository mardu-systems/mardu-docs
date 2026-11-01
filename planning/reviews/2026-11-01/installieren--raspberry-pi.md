# P34: Server auf dem Raspberry Pi installieren

## Änderungsbrief

Leser betreiben einen neuen Raspberry Pi mit 64-Bit-Linux und kennen Docker sowie
ihre Domain- und GitHub-Zugänge. Die Seite beantwortet, wie das fertige
Installationspaket konfiguriert, gestartet, erstmals eingerichtet und später
aktualisiert wird. Heimat ist `installieren/raspberry-pi`.

Plan nach Quellenlektüre: die brauchbare Paket-/Compose-Anleitung behalten,
fehlende Setup-/Administrator-Schritte und Portgrenzen ergänzen, den gefundenen
Konflikt beim Erstsetup offenlegen und anschließend nur die zugewiesenen Dateien
auf Format, MDX und Verweise prüfen. Kein Build, Containerstart oder Hardwaretest.

## Ergebnis

**Belegbare Teildokumentation / offene Prüfung.** Die Seite ist verbessert, aber
die Erstinstallation des aktuellen Quellstands kann wegen des unten belegten
Produktkonflikts nicht als funktionsfähig abgenommen werden.

- Paketdownload, Entpacken, GHCR-Login mit klassischem Token, getrennte
  Zufallswerte, `.env`-Dateirechte, Volumeschutz und Updatebefehle bleiben erhalten.
- Die Voraussetzung des externen IP500-Brokers war zu optional formuliert: Der
  Assistent verlangt diese Verbindung auch ohne ausgewählte Zusatzintegration.
- Nach dem Start erst gesunde Container abwarten, dann den Token lesen. Bedeutung
  und Löschung des Tokens sind beschrieben. Der bisher fehlende Ablauf führt
  durch Datenbanktest, Projekt/Origin, erstes Administratorkonto, Brokerprüfung,
  Integrationen, Fehlerberichterstattung, Validierung und Anwenden.
- Administratorkonto mit eigener E-Mail-Adresse als Benutzername und eigenem
  Passwort statt eines veröffentlichten Standardzugangs erklärt; Mindestlänge
  16 Zeichen und zusätzliche serverseitige Richtlinien genannt.
- Internen API-Port von Dashboard und Datenbank unterschieden; keine ihrer
  internen Ports werden durch das Paket am Host veröffentlicht. HTTPS endet am
  Proxy; MQTT-Ports werden gesondert veröffentlicht. Liveness und Readiness
  bleiben getrennt, einschließlich HTTP 503 während des Setups.
- Nur den Hinweis ergänzt, vor Updates die Datenbankkompatibilität im Zielrelease
  zu prüfen. Kein Sicherungs-/Wiederherstellungsverfahren erfunden.

## Produktbefund für den Koordinator: Erstsetup-Portkonflikt

`deploy/production/docker-compose.prod.yml:60` setzt
`KestrelOptions__HttpPort: 8080`; Caddy-Upstream, interne Dashboard-URL und
API-Healthcheck sind ebenfalls auf 8080 abgestimmt (Zeilen 13, 31, 87).
`web/components/setup/setup-wizard.tsx:311` baut hingegen unabhängig davon den
Request mit `web.httpPort: 5001`. Der Assistent bietet kein Portfeld an und lädt
in `authorize` (Zeilen 613–638) keinen Konfigurationsentwurf.

`api/Framework/Infrastructure/Configuration/Setup/SetupOrchestrator.cs:401`
vergleicht diesen Wert mit der Umgebung; `EnsureLockedValueMatches` (Zeilen
521–534) meldet bei Abweichung einen Fehler. `ValidateAsync` (Zeilen 133–140)
wirft dann `SetupConflictException` mit `ConfigurationLocked`.
`api/Framework/Infrastructure/Settings/SettingsEnvironmentLock.cs:35` bestätigt,
dass gesetzte Prozessumgebungsvariablen als Sperre gelten.

Damit scheitert die unveränderte aktuelle Kombination vor dem Anwenden. Das ist
eine statische Ableitung aus den beteiligten Quellen, kein durchgeführter
Laufzeittest. Ein kurzer sichtbarer Hinweis auf der Produktseite benennt die
Grenze; die Setup-Schritte sind für eine Version ohne diesen Konflikt eingeordnet.
Keine Softwareänderung oder Umgehungsanleitung vorgenommen. Vor einer Abnahme
müssen kompatible API-/Web-Release-Images und das konkrete Installationspaket
praktisch geprüft werden.

## Weitere Quellen

| Aussage                                                                                         | Geprüfte Quelle im Software-Repository                                                                                    |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| API-Release-Tag, `stable` nur für reguläre Releases, ARM64/AMD64                                | `.github/workflows/release-container.yml:43–67`                                                                           |
| Archivname und enthaltene Dateien                                                               | `.github/workflows/release-container.yml:121–146`                                                                         |
| Services, Pflichtvariablen, Ports, Abhängigkeiten, Volumes, Healthchecks, `pull_policy: always` | `deploy/production/docker-compose.prod.yml:1–146`                                                                         |
| .env-Vorlage und getrennte Secrets                                                              | `deploy/production/.env.deploy.example`                                                                                   |
| Routing für Setup und Health, öffentlicher Domainhost                                           | `deploy/production/Caddyfile`                                                                                             |
| Abgrenzung lokaler Entwicklungsstack mit API-Port 5001/Bind-Mounts                              | `docker-compose.yml`                                                                                                      |
| API-Runtime, UID 10001 und Mount-Verzeichnisse                                                  | `api/Server/Dockerfile`, `api/Server/entrypoint.sh`                                                                       |
| Dashboard-Runtime auf Port 3000                                                                 | `web/Dockerfile`                                                                                                          |
| Wizard-Reihenfolge, Pflichtprüfungen und Anmeldeweiterleitung                                   | `web/components/setup/setup-wizard.tsx:175–184`, `:597–605`, `:930–986`, `:1175–1840`; `web/app/[project]/setup/page.tsx` |
| Deutsche UI-Bezeichnungen                                                                       | `web/locales/de/auth.json`, Abschnitt `setup`                                                                             |
| Pflichtdaten für Admin, externe/optionale MQTT-Anbindung                                        | `api/Framework/Infrastructure/Configuration/Setup/SetupModels.cs:371–426`                                                 |
| Passwortprüfung und kein Beispieldaten-Seeding im Setup                                         | `api/Framework/Infrastructure/Configuration/Setup/SetupOrchestrator.cs:236–242`, `:348–369`                               |
| Admin erhält angegebenen Benutzernamen und Admin-Rolle; Setup-Token wird gelöscht               | `api/Framework/Infrastructure/Configuration/Setup/SetupBootstrapper.cs:118–168`                                           |
| Setup-Token ist zufällig und wird als private Datei gespeichert                                 | `api/Framework/Infrastructure/Configuration/Setup/SetupTokenService.cs:16–46`                                             |
| Setup per lokalem Token statt bestehendem Benutzerkonto autorisieren                            | `api/Framework/Infrastructure/Configuration/Setup/Boundary/SetupController.cs:57–99`                                      |
| Setup-Healthzustände und Datenbankinitialisierung                                               | `api/Framework/Infrastructure/SetupModeExtensions.cs:139–146`, `:161–181`                                                 |
| Migrationen beim API-Start; unbekannte Schema-Generation nicht automatisch kompatibel           | `api/Framework/Infrastructure/Persistence/Initialization/ApplicationDbInitializer.cs:23–94`                               |

Die bestehende externe
[GitHub-GHCR-Dokumentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)
wurde am 1. November 2026 gelesen: klassischer PAT, `read:packages`, SSO und
getrennte Paketberechtigungen bestätigt. Keine privaten Paketmetadaten oder
produktiven Zugangsdaten abgefragt.

## Ausgeführte Prüfungen und Grenzen

- Prettier mit vorhandenem `web/node_modules/.bin/prettier`,
  `--ignore-path /dev/null --check` für genau beide zugewiesenen Dateien: bestanden.
  Der explizite Ignore-Pfad ist nötig, da `web/.prettierignore` das Docs-Submodule
  sonst ausschließt.
- Zugewiesene MDX-Datei mit vorhandenem `@mdx-js/mdx` kompiliert: bestanden.
- Frontmatter (`title`, `description`), kein H1, relative Linkziele und alle sieben
  bestehenden Überschriften gegen `HEAD` geprüft: bestanden. Keine Überschrift
  oder URL geändert; bestehende Anker bleiben bestehen.
- `git -C web/content/docs diff --check -- docs/installieren/raspberry-pi.mdx`:
  bestanden.
- Nicht ausgeführt: globaler Build, gemeinsame Navigationstests, Browserrendering,
  Compose-Konfigurationsprüfung/-Start, Download privater Images, Zertifikatsbezug,
  Raspberry-Pi-/Speicher-/Netzwerkprüfung sowie Sicherung/Wiederherstellung.
  Registry-Verfügbarkeit, Web-Image-Releaseworkflow und konkrete veröffentlichte
  Releasekombination sind nicht durch dieses Repository allein nachgewiesen.
  Das PostgreSQL-Verhalten bei einem bereits initialisierten Datenvolume bleibt
  aus der vorhandenen Anleitung erhalten; hier kein Startversuch durchgeführt.

## Verweise und Folgeprüfung

- Der bestehende eingehende Link aus `administration/wartungs-cli.mdx` auf
  `#5-neue-versionen-übernehmen` bleibt gültig.
- Nachbarseite `installieren/index.mdx` bleibt der Einstieg; keine Navigation
  geändert. Kein zusätzlicher Seitenbedarf aus diesem Patch.
- Der Koordinator muss den Produktbefund gesondert aufnehmen und die gemeinsame
  Consumer-/Browserprüfung durchführen. Die Installationsabnahme benötigt ein
  kompatibles Releasepaar, reales Paket, Domain/TLS, externen Broker und Pi.

## Geänderte Dateien

- `web/content/docs/docs/installieren/raspberry-pi.mdx`
- `web/content/docs/planning/reviews/2026-11-01/installieren--raspberry-pi.md`

Bestehende Markdown-/MDX-Mittel wiederverwendet. Keine API-/DTO- oder
Softwareänderung, daher keine Vertragsdokumentation angepasst.
