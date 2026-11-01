# P40 – MQTT-Ereignisse beziehen

## Änderungsbrief

- Leserfrage: Wie liest ein externer MQTT-Client freigegebene Mardu-Informationen, ohne Geräteprotokoll und Informationsbroker zu verwechseln?
- Leser: Entwicklung mit Grundkenntnissen in MQTT; Brokeradresse, Zertifikatsvertrauen und freigegebenes MQTT-Lesekonto werden durch den Betrieb bereitgestellt.
- Ergebnis: Exaktes Systemtopic abonnieren, JSON-Zustand einordnen, bei Bedarf freigegebenes Geräteereignistopic ergänzen und Verbindungs-/ACL-Fehler unterscheiden.
- Heimat: Entwickeln; URL und vorhandene Anker `verbindung-und-zugriffsregeln` sowie `topics-und-payloads` bleiben bestehen.
- Bestand: Bisher nur Entwurf/TODOs. Belegbare Trennung von Information, Gerätebefehlen und interner Automation bleibt erhalten.
- Plan: Aus Quellen belegte Voraussetzungen und Leseabfolge, kompakte Topic-/Payloadreferenz und Fehlerhilfe ergänzen; reine statische Dokumentprüfungen, keine Broker-/Geräteaktionen.
- Grenzen: Keine Consumer-/Browser- oder reale MQTT-Abnahme. Administrative MQTT-Einrichtung benötigt weiterhin eine eigene vollständige Anleitung; vorhandene Integrationsübersicht wird verlinkt.

## Entscheidung und Umsetzung

**Belegbare Teildokumentation / offene Prüfung.** Der bisher versteckte TODO-Entwurf wurde zu einem nutzbaren externen Leseablauf ausgearbeitet. Der Text definiert ausdrücklich keinen MQTT-Schreibvertrag für Gerätemanagement oder private Automation-Topics.

- Verbindungsdaten, tatsächlicher Port statt automatischer TLS-Portwahl, TLS 1.2/1.3, Client-ID und eigene MQTT-Anmeldedaten erklärt.
- Rollen `ReaderRestricted`, `ReaderAll`, `Admin`, explizite Subscribe-ACLs, Vorrang überlappender Deny-Regeln und bedingten anonymen Zugriff belegt.
- Begrenzter Test mit dem tatsächlich vom Systempublisher veröffentlichten `v1/info/public/system/state`, fiktivem JSON und Einordnung des Zeitstempels.
- Vorhandene System- und Geräte-Zustandstopics sowie Geräteereignisse mit Publisher-QoS und Retain dokumentiert. Das optionale Entwicklungs-Demo-Topic `/telemetry` für Geräte wurde bewusst nicht als allgemeiner Hardware-Telemetrievertrag dargestellt.
- Topic-Templates, Wildcard-Syntax, JSON-/Null-/Leer-Payload-Verarbeitung, Snapshot gegenüber Ereignisstrom, Wiederverbindung und Fehlerhilfe ergänzt.
- Die vorhandenen Abschnittsüberschriften und damit die Anker `verbindung-und-zugriffsregeln` und `topics-und-payloads` bleiben unverändert. Trennung von Information, Befehlen und interner Automation erhalten.
- Keine Software-/API-/DTO-Verträge geändert; vorhandene XML-/OpenAPI- und Katalogdokumentation als Quelle verwendet. Keine Dependencies oder neuen MDX-Komponenten nötig.

## Quellen

Pfadangaben beziehen sich auf das Software-Repository `/Users/lucaschoeneberg/Documents/GitHub/mardu-rpi-api` und den statisch gelesenen Stand:

| Quelle                                                                                                                     | Beleg                                                                                                                                                       |
| -------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `api/Framework/Infrastructure/Network/Broker/Configuration/MqttBrokerSettings.cs:19–119`                                   | Standardport, TLS, selbstsignierte Zertifikate, anonyme Filter, Wildcards, Authentifizierungssperre und reservierte Client-IDs                              |
| `api/Framework/Infrastructure/Network/Broker/MqttServerHostedService.cs:220–263, 270–342, 350–443`                         | Aktivierung, Listenerwahl/TLS 1.2 und 1.3; Client-ID-/Anmeldeprüfung; Subscribe-Entscheidung, Retained-Unterdrückung und Ablehnung aller externen Publishes |
| `api/Framework/Infrastructure/Network/Broker/DbMqttAclService.cs:28–142`                                                   | Anonymer Pfad, Datenbankbenutzer, Passwortprüfung je Verbindung, Aktivstatus, Client-ID-Bindung, Rollenzugriff und aktive Subscribe-ACLs                    |
| `api/Framework/Infrastructure/Network/Broker/MqttInfoPolicy.cs:53–165, 171–216`                                            | Filter vollständig innerhalb von Allow, überlappendes Deny, QoS-Limit, Retain-Begrenzung, Syntax, unresolved Templates, private Adaptergrenze               |
| `api/Common/Contracts/MqttInfoTopics.cs:10–60`                                                                             | Kanonische Informations-Topics und Geräte-ID als eine Topic-Ebene                                                                                           |
| `api/Service/Devices/Application/Publishing/SystemInfoPublisher.cs:7–43`                                                   | Tatsächlich veröffentlichte Systemtopics, QoS 1/0 und Retain true/false                                                                                     |
| `api/Service/Devices/Application/Publishing/SystemInfoTelemetryHostedService.cs:19–75`                                     | Veröffentlichung bei aktivem/verfügbarem Broker, 60 Sekunden zwischen Veröffentlichungsversuchen, Gesundheits-/Laufzeitdaten und Fehlerbehandlung           |
| `api/Service/Devices/Application/Publishing/DeviceInfoPublisher.cs:8–79, 94–189`                                           | Geräte-Topic-Katalog, tatsächliche Veröffentlichungsparameter und leere Retained-Payloads zum Entfernen gelöschter Gerätesnapshots                          |
| `api/Service/Devices/Application/Publishing/DeviceInfoContracts.cs:8–363, 366–455`                                         | Topicbezogene Zustandsmodelle, Laufzeitsemantik, Ereignisfelder und nullable Metadaten, JSON-Feldnamen und UTC-/Sekundeneinheiten                           |
| `api/Service/Devices/Application/Logging/DeviceLogService.cs:20–65`                                                        | Reguläre Spiegelung neuer Geräteprotokolleinträge als MQTT-Ereignisse                                                                                       |
| `api/Framework/Infrastructure/Network/Broker/BrokerPublishService.cs:16–46`                                                | UTF-8-/JSON-Serialisierung und interne Broker-Injektion; hier kein eigener numerischer Payload-Bytehöchstwert definiert                                     |
| `api/Framework/Infrastructure/Network/Broker/Boundary/MqttTopicsController.cs:16–48`                                       | Katalogroute, HTTP-Authentifizierung, Recht `Integrations.View`, Templates und Payloadbeschreibungen                                                        |
| `api/Framework/Infrastructure/Network/Broker/Boundary/MqttUsersController.cs:111–180` sowie `MqttAclsController.cs:71–187` | Trennung bestehender Verbindungen und Entfernung gespeicherter Abonnements nach Benutzer-/Passwort-/ACL-Änderungen                                          |
| `web/content/docs/docs/administration/integrationen.mdx#mqtt`                                                              | Vorhandener administrativer Einstieg, Bezeichnungen und Abgrenzung zur ausgehenden IP500-Verbindung                                                         |

## Checks und Prüfgrenzen

- Lokale vorhandene Prettier-Installation gezielt für beide eigenen Dateien verwendet; erster Check meldete Tabellenformatierung, anschließend korrigiert.
- Produktseite mit der vorhandenen `@mdx-js/mdx`-Installation kompiliert; Frontmatter, beide ursprünglichen Überschriften, beide relativen Seitenziele einschließlich `#mqtt` und parsebares JSON-Beispiel per einmaligem lokalem Prüfskript geprüft.
- Abschließender Prettier- und Diff-Whitespace-Check siehe nachgetragenes Ergebnis unten.
- Kein globaler Build, keine globalen Tests, kein neuer Formatter/Check im Repository angelegt.
- Keine Browser-/Consumerdarstellung, kein MQTT-Client-/TLS-/ACL-Verhalten und keine Hardware praktisch geprüft. Das Beispiel ist aus Publisher und DTO abgeleitet, keine behauptete Empfangsausgabe.
- Kein numerischer Payload-Maximalwert behauptet: In den geprüften Anwendungs-Publishpfaden ist kein solcher Vertrag angegeben. Transport-/Bibliotheksgrenzen wurden nicht vermutet.
- Für praktische Prüfung: freigegebenes Testlesekonto und Broker mit bekanntem Zertifikat; exaktes Systemtopic, abgelehntes fremdes Topic, erlaubte/verbotene Wildcards, falsches Passwort, Retained-Begrenzung und Wiederverbindung nach Rechteänderung prüfen. Anschließend Consumerdarstellung und mobile Tabellenlesbarkeit prüfen lassen.

## Übergabe und Seitenbedarf

- Eine vollständige **administrative MQTT-Einrichtungsanleitung** fehlt weiterhin als eigener Ablauf: Listener/TLS-Zertifikat aktivieren, Brokerstatus prüfen, Benutzer erstellen, konkrete Subscribe-ACL vergeben, Wirkung und Widerruf prüfen. Die bestehende Integrationsübersicht genügt als Einstieg, ersetzt diese praktische Anleitung aber nicht. Keine nicht existierende Seite verlinkt.
- Navigation/Veröffentlichungsliste unverändert; Koordinator entscheidet nach Consumerprüfung über Sichtbarkeit der bisher verborgenen Seite. Den Verweisnamen „MQTT für Entwickler“ in der Integrationsübersicht bei Bedarf an den tatsächlichen Seitentitel angleichen.
- Keine weiteren Seiten, Software, Navigation, Übersetzungen oder Backlogs verändert; kein Commit.

## Geänderte Dateien

- `web/content/docs/docs/entwickeln/mqtt-events.mdx`
- `web/content/docs/planning/reviews/2026-11-01/entwickeln--mqtt-events.md`

Abschließendes Ergebnis: Prettier für beide eigenen Dateien erfolgreich; `git diff --check -- docs/entwickeln/mqtt-events.mdx` im Dokumentations-Submodule ohne Befund. MDX-Kompilierung und lokale Verweis-/JSON-/Frontmatter-/Ankerprüfungen erfolgreich. Die praktische und visuelle Abnahme bleibt offen.
