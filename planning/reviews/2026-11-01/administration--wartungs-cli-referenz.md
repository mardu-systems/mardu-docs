# P32 – Wartungs-CLI: Befehle und Optionen

## Änderungsbrief

Leser sind Betreiber mit Terminal-/Docker-Grundwissen, die Syntax, verfügbare
Optionen, JSON-Felder und Rückgabewerte von `mardu-admin` nachschlagen. Die
kanonische Handlungsanleitung bleibt `administration/wartungs-cli.mdx`; diese
Seite bleibt Referenz im Bereich Administration. Alle Befehle, Wirkungen,
Konfigurationswerte und Sicherheitsgrenzen werden gegen Parser, CLI-Operationen
und Server geprüft. Der bestehende Aufbau und alle Überschriftenanker bleiben
erhalten. Geplant sind nur eine kompakte Optionsübersicht, die vollständige
Konto-JSON-Feldzuordnung und genauere Fehler-/Rückgabewertbeschreibungen.
Statische Inhalts-/Link-/Formatprüfungen sind möglich; keine Kontoänderung,
Containeraktion oder globale Builds. Consumer-Rendering übernimmt der Koordinator.

## Ergebnis: verbessert

Die sechs implementierten Befehle und alle anwendungseigenen Optionen waren
bereits enthalten. Die Seite bleibt eine Referenz und wiederholt keinen
Passwort-Reset-Ablauf der Nachbarseite. Ergänzt wurden:

- Eine Optionsübersicht mit Geltungsbereich und Standardverhalten, einschließlich
  `--email`-Validierung und Entfernen äußerer Leerzeichen.
- Alle neun Felder der Konto-JSON-Ausgabe mit Typ, Null-Semantik und Bedeutung;
  Wartungsprotokollversion `1` ergänzt.
- Der Unterschied zwischen nicht strukturierten Fehlerpanels und regulärem
  Diagnose-JSON bei Rückgabewert `1`.
- Beispiele für Fehler mit Rückgabewert `1` sowie das Anfragezeitlimit von
  30 Sekunden und dessen Abbruchcode `130`.

Erhalten sind sämtliche bisherigen Überschriften/Anker, Docker-Aufrufe,
Kontoaktionen, interaktive Bestätigung, Socket-Konfiguration/-rechte,
Auditbeschreibung und der Link auf die kanonische Handlungsanleitung.
API-/DTO-Implementierung und deren XML-Dokumentation wurden nicht verändert;
die Produktreferenz bildet die vorhandenen Verträge ab.

## Geprüfte Quellen

Pfade relativ zum Software-Repository; Zeilen beziehen sich auf den gelesenen Stand:

- `tools/Mardu.Admin.Cli/AdminCli.cs:21–84`: Menüstart, Befehlsregistrierung,
  Socket-Override, Parser-/Abbruch-/Verbindungs-/Antwortfehler und Rückgabewerte;
  `:88–111`: Menü, Standard-Passwortmodus und Fehlerpanel.
- `tools/Mardu.Admin.Cli/Commands.cs:9–61`: alle Befehlsoptionen, validierte
  E-Mail-Adresse, optionale boolesche Flags und Dispatch.
- `tools/Mardu.Admin.Cli/MaintenanceOperations.cs:10–55`: JSON-Namenskonvention,
  Kontoausgabe, Terminalpflicht, Protokollprüfung, Standardbestätigung Nein,
  verdeckte Passwortwiederholung, temporär/permanent;
  `:59–105`: Versions-/Diagnose-JSON, Diagnosecodes und Kontotabelle.
- `tools/Mardu.Admin.Cli/MaintenanceClient.cs:13–47`: Unix-Socket, Anfragezeitlimit,
  E-Mail-Trim und Kompatibilitätsprüfung; `:75–82`: Antwortfehler und leere Antwort.
- `api/Framework/Core/Identity/ILocalUserMaintenance.cs:19–46`: DTO-Felder,
  Nullwerte, Passwortwechselstandard und Diagnose-/Versionsvertrag.
- `api/Framework/Core/Identity/MaintenanceProtocol.cs:7–13` und
  `LocalMaintenanceOptions.cs:6–12`: Protokollversion, Socket-Standard,
  Betreiberidentität und Listener-Defaults.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.Maintenance.cs:15–86`:
  Kontosuche, Einschränkung lokaler Resets, Entsperren, Sitzungswiderruf,
  Zustandsprojektion und Auditwerte.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.Password.cs:137–158`:
  Passwortwechselpflicht, Security-Stamp-/Passwortänderung und Sitzungswiderruf.
- `api/Server/Hosting/LocalMaintenanceServer.cs:19–31,46–72`: Plattformbedingung,
  absolute Socket-Pfade, Dateirechte und isolierter Listener;
  `LocalMaintenanceEndpoints.cs:37–57`: Konto-, Versions- und Health-Endpunkte.
- `api/Server/Dockerfile:63,70,91`: CLI-Publish-Verzeichnis, `/app` und Imagepfad.
- `service.Test/Framework/Identity/MaintenanceOperationsTests.cs:13–30,49–143`:
  vorhandene Testbelege für Health-JSON/-Codes, Passwortmodus,
  Zielkonto-ID, Bestätigungsabbruch, Protokollabweichung und Passwortwiederholung;
  nur gelesen, nicht ausgeführt.

## Eigene Checks und Grenzen

- Vorhandenes Prettier auf beide eigenen Dateien mit `--ignore-path /dev/null`
  angewendet und anschließend geprüft; nötig, weil der Consumer das gesamte
  Doku-Submodul sonst ignoriert.
- MDX mit installiertem `@mdx-js/mdx` und `remark-gfm` kompiliert: erfolgreich.
- Frontmatter und den relativen Seitenlink per lokalem Python-Check geprüft:
  gültig. Alle fünf vorhandenen Abschnittsüberschriften mit `git show HEAD`
  verglichen: unverändert. Die eingehenden Anker der Nachbaranleitung bleiben gültig.
- `git diff --check` für die eigenen Dateien: erfolgreich.
- Keine CLI-/Docker-Aktion, Kontomutation, Tests oder Builds ausgeführt.
  Kein Browser-/Container-/Hardwaretest behauptet. Consumer-Rendering und
  Darstellung der Tabellen bleiben beim Koordinator; ein praktischer Test von
  CLI-Fehlerausgabe/Timeout ist nicht erfolgt.

## Hinweise an den Koordinator

Keine weiteren Seiten, Anker oder Navigationsänderungen erforderlich. Die
Nachbaranleitung wird separat bearbeitet. Das Software-Entwicklerdokument
`docs/mardu-admin.md` enthält zusätzlich private Protokoll- und Betriebsdetails;
seine Aussagen wurden gegen den Code geprüft und nicht ungeprüft übernommen.
Keine bestätigten Produktfehler aus dieser statischen Prüfung.

Geänderte Dateien:

- `web/content/docs/docs/administration/wartungs-cli-referenz.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--wartungs-cli-referenz.md`
