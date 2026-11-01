# Seitenrevision P38: API und Integrationen

## Änderungsbrief

Die bisher versteckte TODO-Seite soll Personen mit Erfahrung in HTTP oder
Nachrichtenclients helfen, für eine konkrete Integration den passenden Zugang zu
wählen. Ergebnis ist ein nutzbarer Einstieg im Bereich Entwickeln: Schnittstelle,
Identität, Berechtigungsumfang und erste Prüfung sind erkennbar. Die vorhandene
URL und die Anker `referenz-und-integrationsweg` und `test-und-betrieb` bleiben.
HTTP-, MQTT-, MCP- und Automation-Details werden in ihren bestehenden Anleitungen
beziehungsweise der generierten Referenz gepflegt. Geprüft werden vorhandener
Backend-Code, OpenAPI-Consumer und Nachbarseiten; praktische Verbindungs- und
Browserprüfungen übernimmt die koordinierte Abschlussrunde. Es werden keine
Zugangsdaten verwendet und keine Software-, Navigations- oder Vertragsdateien
geändert.

## Kurzbefund

- **Entscheidung: verbessert; belegbare Teildokumentation / offene Prüfung.**
- Leserfrage: Welche vorhandene Schnittstelle passt zu meiner Aufgabe, unter
  welcher Identität arbeite ich und wo finde ich den konkreten Vertrag?
- Die Seite enthielt ausschließlich Entwurfsprosa und TODOs. Sie bietet jetzt
  einen Vergleich von HTTP, MCP, Informations-MQTT und Node-RED sowie einen kurzen
  Hinweis auf die aufgabenspezifischen SignalR-Hubs. Es entstand keine zweite
  Endpunkt-, DTO- oder Topic-Referenz.
- Die Abschnitte zur Referenznutzung, zum Berechtigungsumfang und zur ersten
  Testaufgabe ersetzen die Schreibaufträge. Persönliche Buchungen und
  Verwaltungsbuchungen illustrieren die Trennung von Datenumfängen. Globale
  Aktionsrechte und objektbezogene Hardwareberechtigung werden unterschieden.
- Der breite Zugriff der Node-RED-Laufzeit wird ausdrücklich genannt; die
  Ressourcenauswahl einer Flow-Freigabe wird nicht als Laufzeitbeschränkung
  beschrieben. Keine erfundenen Scopes oder anonymen Geschäftsendpunkte.
- Erhalten: Titel, URL, beide bestehenden Überschriften und damit die Anker
  `referenz-und-integrationsweg` und `test-und-betrieb`; die generierte
  OpenAPI-Referenz bleibt Vertragsquelle.

## Geprüfte Quellen

Pfade beziehen sich auf die Wurzel des Software-Repositories, sofern nicht anders
angegeben.

| Aussage                                                                  | Quelle / relevante Stelle                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTTP-Referenz aus Backend-Vertrag, keine manuell gepflegte Zweitreferenz | `web/lib/openapi.ts:6–8` lädt `contracts/backend-swagger-docs.json`; `web/lib/source.ts:29–39` bindet OpenAPI in den Consumer ein. `api/Framework/Infrastructure/OpenApi/OpenApiExtensions.cs:61–83` registriert Bearer-Schema und Operationsprozessoren.                                                                                                                                                                                                                                                                  |
| Kontozugang und Aktionsrechte                                            | `api/Framework/Infrastructure/Identity/Tokens/Boundary/TokensController.cs:25–65` dokumentiert Anmeldung und mögliche MFA-Challenge. `api/Framework/Infrastructure/Auth/Policy/RequiredPermissionAuthorizationHandler.cs` prüft Benutzerberechtigungen.                                                                                                                                                                                                                                                                    |
| Eigene Buchungen gegenüber Verwaltung                                    | `api/Service/Bookings/Boundary/HttpControllers/BookingsController.cs:20–34` verwendet persönliche Liste und `Bookings.View`; `AdminBookingsController.cs:19–44` verwendet `BookingAdministration.View` und die administrative Liste/Details.                                                                                                                                                                                                                                                                               |
| Objektbezogene Hardwareberechtigung zusätzlich zur Endpunktberechtigung  | `api/Framework/Core/Identity/IResourceHardwareAuthorization.cs:6–14` fordert `ManageHardware` für die konkrete Ressource und belässt die Endpunktprüfung beim Aufrufer.                                                                                                                                                                                                                                                                                                                                                    |
| MCP-Transport und Richtlinien                                            | `api/Service/Mcp/MarduMcpExtensions.cs:88–90,120–129` konfiguriert HTTP-Transport und autorisierte Route; `McpToolPolicyFilter.cs:19–39,47–55` filtert Tool-Liste und Aufrufe anhand der Serverfreigaben.                                                                                                                                                                                                                                                                                                                  |
| Persönliche MCP-Rechte                                                   | `api/Service/Mcp/Authorization/McpPermissionAuthorizationHandler.cs:30–58` prüft delegierte Verbindungsrechte und aktuelle Kontorechte. Die bestehende Anleitung `web/content/docs/docs/entwickeln/mcp-anbindung.mdx` liefert den lesenden Einstieg und Tokenwechsel.                                                                                                                                                                                                                                                      |
| Informations-MQTT und eigene Brokerkonten                                | `api/Framework/Infrastructure/Network/Broker/MqttInfoPolicy.cs:18–25,51–98` beschreibt den Informationsbaum und Subscription-Regeln; `MqttServerHostedService.cs:415–430` weist externe Publikationen ab. `Boundary/MqttUsersController.cs` und `Boundary/MqttAclsController.cs` verwalten getrennte MQTT-Benutzer und ACLs.                                                                                                                                                                                               |
| MQTT bei Automation liefert Meldungen, Aktionen bleiben HTTP             | `api/Service/Automations/Application/IAutomationMqttServices.cs:20–25,40–44`; `Boundary/HttpControllers/AutomationExecutionsController.cs:13–40` stellt die authentifizierte Aktionsausführung über `AutomationJwt` bereit.                                                                                                                                                                                                                                                                                                |
| Breiter Node-RED-Laufzeitzugriff; getrennte Editoridentität              | `api/Service/Automations/Application/Services/AutomationResourceService.cs:23–43,EnsureAuthenticated` liest den unterstützten Katalog für die authentifizierte Laufzeit. `Application/AutomationAuthentication.cs` definiert `AutomationJwt`; `NodeRed/Application/NodeRedEditorAuthentication.cs` definiert den eigenen Editorzugang. Kanonische UI-Anleitung: `web/content/docs/docs/administration/automationen.mdx`, Abschnitt „Automatisierungen aktivieren“, einschließlich Auswirkungen der Flow-Ressourcenauswahl. |
| Hub- und Gruppenprüfung bei Tags                                         | `api/Service/Tags/Boundary/Hubs/UserTagHub.cs:14–37,53–70` schützt den Hub und die Benutzer-/Taggruppen. Es wird daraus kein allgemeiner SignalR-Ereignisvertrag abgeleitet.                                                                                                                                                                                                                                                                                                                                               |
| Auftrag ist keine Gerätebestätigung; Simulationsbeispiele                | Bestehende `web/content/docs/docs/administration/automationen.mdx`, Abschnitte „Schalten und Rückmeldungen prüfen“ und „Mit Beispielen prüfen“.                                                                                                                                                                                                                                                                                                                                                                            |

## Eigene Checks und Prüfgrenzen

- Prettier auf beide eigenen Dateien angewendet beziehungsweise geprüft. Der
  erste Formatcheck fand Tabellenformatierung in der Produktseite; anschließend
  wurde nur diese Datei formatiert.
- Die Produktseite wurde mit dem vorhandenen `@mdx-js/mdx` aus `web/node_modules`
  kompiliert. Alle fünf relativen MDX-Linkziele existieren. Die beiden bisherigen
  Überschriften sind vorhanden; TODO-/Entwurfsplatzhalter sind entfernt.
- Statischer Quellen- und Diffabgleich; keine API-, DTO- oder Softwareänderungen.
- Nicht durchgeführt: Browser-/Mobile-/Theme-Rendering, Markdown-/LLM-Ausgabe des
  laufenden Consumers, HTTP-/MCP-/MQTT-Verbindungsversuche, Node-RED-Deploy,
  Hardware- oder Providerprüfung. Keine Zugangsdaten oder externen Requests
  verwendet. Keine Aussage über einen praktisch erfolgreichen Integrationslauf.

## Koordination und Publikationsvorschlag

Die Seite ist nach gemeinsamer Consumer-/Navigationsprüfung als
Integrationsübersicht zur Veröffentlichung geeignet. Sie beansprucht keine
vollständige Protokollanleitung. Vor Aufnahme in die Navigation die parallel
bearbeiteten Linkziele `http-api.mdx` und `mqtt-events.mdx` auf nutzbaren Stand
prüfen. Derzeit listet `entwickeln/meta.json` nur MCP und die Referenz; der
Bereichsstart beschreibt HTTP/MQTT noch als nicht ausgearbeitet. Diese Änderungen
gehören der Koordination und wurden hier nicht vorgenommen.

Die frühere TODO-Forderung, lesende und ändernde Integrationen praktisch
auszuführen, ist durch die statische Überarbeitung nicht erfüllt. Ein vollständiger
SignalR-Leitfaden und eine Anleitung zum eigenen Automation-Adapter bleiben
separate Themen; kein weiterer Platzhalter wurde angelegt.

## Geänderte Dateien

- `web/content/docs/docs/entwickeln/api-integration.mdx`
- `web/content/docs/planning/reviews/2026-11-01/entwickeln--api-integration.md`
