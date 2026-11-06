# Gesamtrevision: Entwickeln und Automationen

## Änderungsbrief

Sieben bestehende Seiten gegen aktuelle UI, Node-Hilfe und Backend-Verträge prüfen; Anschlussverwaltung als achte Seite aus dem Automationseinstieg ausgliedern. Leser sind Entwickler mit HTTP-/MQTT-/Node-RED-Grundkenntnissen und Administratoren, die Ressourcenanschlüsse einrichten. Das Ergebnis soll die Wahl eines passenden Zugangs und einen begrenzten Test mit erkennbarem Ergebnis ermöglichen. Seitenadressen, Abschnittsanker, Rechte und Folgen bleiben erhalten. Keine Software-, Referenz-, DTO-, Übersetzungs- oder Navigationsänderungen. Die generierte HTTP-Referenz bleibt im Software-Consumer. Keine Hardwarebefehle, externen Systeme, Builds oder Serverstarts. Parallele Protokoll-/S7-Arbeiten sind kein Beleg für veröffentlichten Umfang.

## Seitenprüfung

### `entwickeln/api-integration.mdx` — bewusst erhalten

- Leserfrage / Ergebnis: Welche Schnittstelle passt zur Anwendung, und wessen Rechte gelten? Die Aufgaben-/Zugangstabelle, Referenzcheckliste und der begrenzte Testablauf sind aktuell.
- Quellen: `web/lib/source.ts`, `web/lib/docs-roles.tsx`; `api/Service/Mcp/MarduMcpExtensions.cs`, `Authorization/McpPermissionAuthorizationHandler.cs`; `api/framework/Infrastructure/Network/Broker/MqttInfoPolicy.cs`, `MqttServerHostedService.cs`; `api/Service/Automations/Application/Services/AutomationResourceService.cs`; `api/Service/ManagedResources/Boundary/HttpControllers/ResourceSwitchController.cs`.
- Entscheidung: Unverändert erhalten. Identität, Rechteumfang und Annahme gegenüber Ausführung sind bereits klar getrennt.
- Checks / Grenzen: MDX, Format, relative Ziele und Baseline-Anker bestanden. Keine schreibende Integration ausgeführt.

### `entwickeln/automationsfluesse.mdx` — Ablauf gegliedert

- Leserfrage / Ergebnis: Wie lese ich mit einer vorhandenen Verbindung eine Testressource und erkenne gültige Zustände und Fehler? Vorwissen: Nodes verbinden und `msg.payload` verstehen.
- Quellen: `integrations/node-red/nodes/mardu.html`, `src/index.ts`, `src/runtime/connection.ts`, `src/runtime/resources.ts` und `editor/deployment-lifecycle.js`; `api/Service/Automations/Boundary/Dto/AutomationResourceStateDtos.cs`, `Application/Services/AutomationResourceService.cs`, `Application/Executors/MachineEndSessionAutomationExecutor.cs`; `web/app/[project]/dashboard/automations/page.tsx`.
- Änderung: Lesendes Beispiel, Nachrichtenvergleich, REST-Abgleich, Catch-Pfad und Folgen erhalten. Native `Steps`/`Step` trennen Aufbau, Deploy-/Ergebnisprüfung und Beobachtung. Keine neue Hardware-/Protokollfunktion ergänzt.
- Checks / Grenzen: MDX, Format, Ziele/Anker und JSON-Beispiel bestanden. Kein Node-RED-Fixture verfügbar: kein eigener Flowdeploy, keine Auswahlpagination, Catch-Ausgabe oder Versionsunterdrückung praktisch geprüft. Diese Aussagen sind codebasiert.

### `entwickeln/http-api.mdx` — Ressourcenbeispiel in drei Phasen

- Leserfrage / Ergebnis: Wie melde ich eine Anwendung an und ändere einen Testentwurf ohne fremde Änderungen zu überschreiben? Vorwissen: Shell, HTTP und JSON.
- Quellen: `api/framework/Infrastructure/Identity/Tokens/Boundary/TokensController.cs`, `Services/TokenService.cs`, `Challenges/DatabaseAuthenticationChallengeStore.cs`; `api/framework/Infrastructure/RateLimiting/RateLimitingExtensions.cs`; `api/Service/ManagedResources/Boundary/HttpControllers/ManagedResourcesController.cs`, `Boundary/Dto/ManagedResourceDtos.cs`, `Application/Services/ManagedResourceService.cs`, `Boundary/HttpControllers/ResourceSwitchController.cs`.
- Änderung: Native Schritte für Anlegen, Zurücklesen und Ändern/Prüfen. Bestehende Beispiele, Feldfolgen und Konflikthilfe erhalten; internen Verweis auf die vorherige nummerierte Liste angepasst. Keine Referenzoperationen oder DTOs nachgebaut.
- Checks: MDX, Format, Links/Anker, Bash-/JSON-Syntax bestanden. In der isolierten API `http://localhost:35116`: Anmeldung liefert 200 und Tokenantwort; capabilities, eigenes Profil, eigene Autorisierung und begrenzte Ressourcenliste liefern 200. Paginationhülle mit allen dokumentierten Feldern bestätigt; die Entwurfsseite ist leer.
- Grenzen: Kein Entwurf angelegt/geändert; keine Refreshrotation, MFA-, Passkey- oder OIDC-Anmeldung praktisch geprüft. Zugangsdaten und Token wurden nur im Prozessspeicher verwendet und nicht ausgegeben.

### `entwickeln/index.mdx` — passenden Verwaltungsweg verlinkt

- Leserfrage / Ergebnis: Wo beginne ich mit meiner Integration? Schnittstellenwahl, Rechteklärung und Bereichswechsel zur Administration bleiben direkt auffindbar.
- Quellen: `web/lib/docs-roles.tsx`, `web/lib/source.ts`, alle fünf einzeln abgeglichenen Integrationsanleitungen; `api/Service/Mcp/MarduMcpExtensions.cs`, `api/framework/Infrastructure/Network/Broker/MqttServerHostedService.cs`, `api/Service/Automations/Application/Services/AutomationResourceService.cs`.
- Entscheidung: Den knappen Bereichseinstieg erhalten. Für die Anschlussaufgabe nach der Einrichtung einen eigenen Verweis auf **Automationsanschlüsse bereitstellen → Administration** ergänzt; keine dekorative Komponente nötig.
- Checks / Grenzen: MDX, Format, relative Verweise und historische Anker bestanden. Keine Aussage über eine schreibende Integration aus dem Bereichseinstieg abgeleitet.

### `entwickeln/mcp-anbindung.mdx` — Verbindungstest gegliedert und Randthemen verdichtet

- Leserfrage / Ergebnis: Wie verbinde ich einen MCP-Client und prüfe einen begrenzten Lesezugriff? Persönliche Tokenverwaltung bleibt im Profil kanonisch dokumentiert.
- Quellen: `api/Service/Mcp/MarduMcpExtensions.cs`, `Tools/NotificationMcpTools.cs`, `McpToolPolicyFilter.cs`, `Authorization/McpEnabledRequirement.cs`, `Authorization/McpAgentCredentialRequirement.cs`, `Authorization/McpPermissionAuthorizationHandler.cs`, `Application/McpAgentConnectionService.cs`; `web/locales/de/settings.json`.
- Änderung: Native Schritte für persönlichen Zugang, Clientkonfiguration und Leseprüfung. Wiederholte Node-RED-/SignalR-Erklärungen auf einen Verweis zur Integrationsübersicht verdichtet. Beide historischen Abschnittsanker als `span` erhalten.
- Checks / Grenzen: MDX, Format, Verweise/Anker und JSON-Aufrufparameter bestanden. Nach zentral freigegebener Aktivierung durch `revision_anbindungen` eigene persönliche Verbindung ausschließlich mit `Permissions.Profile.View` für einen Tag angelegt (201). Über Streamable HTTP `initialize` (200), `notifications/initialized` (202), `tools/list` (200, `notifications_list` vorhanden) und `notifications_list(limit=1)` (200 ohne Toolfehler) geprüft. Anschließend eigene Verbindung widerrufen (204); derselbe Agent-Token liefert danach 401. Kein Token oder Benachrichtigungsinhalt ausgegeben. Keine globale Richtlinie durch diesen Agenten geändert; kein externer MCP-Desktopclient, Tokenwechsel oder schreibendes Tool geprüft.

### `entwickeln/mqtt-events.mdx` — bewusst erhalten

- Leserfrage / Ergebnis: Wie empfange ich freigegebene Informationen und unterscheide Momentaufnahmen von Ereignissen? Vorwissen: MQTT-Client und Topicfilter.
- Quellen: `api/framework/Infrastructure/Network/Broker/MqttInfoPolicy.cs`, `DbMqttAclService.cs`, `MqttAuthorization.cs`, `MqttServerHostedService.cs`, `Boundary/MqttTopicsController.cs`, `Boundary/MqttUsersController.cs`, `Boundary/MqttAclsController.cs`; `api/Service/Devices/Application/Publishing/SystemInfoTelemetryHostedService.cs`, `SystemInfoPublisher.cs`, `DeviceInfoPublisher.cs`, `DeviceInfoContracts.cs`.
- Entscheidung: Abonnementtest, Topicübersicht, Retained-/QoS-Semantik und Fehlerhilfe stimmen weiterhin mit dem Code überein. Unverändert erhalten. Ein Dashboardbild würde die externe MQTT-Clientaufgabe nicht besser erklären.
- Checks / Grenzen: MDX, Format, Ziele/Anker und JSON-Beispiel bestanden. Kein eigener MQTT-Client verbunden, keine ACL geändert und kein Geräteereignis ausgelöst.

### `administration/automationen.mdx` — Runtime-Einstieg und optionale Zugangsregel

- Leserfrage / Ergebnis: Wie aktiviere und prüfe ich die gemeinsame Node-RED-Verbindung, und wann braucht ein Zugang eine zusätzliche Flow-Freigabe? Voraussetzungen für Runtime/Editor und für die optionale Zugangsregel werden getrennt genannt.
- Quellen: `web/app/[project]/dashboard/admin/integrations/automations/page.tsx`, `use-automation-settings-controller.ts`; `web/app/[project]/dashboard/automations/page.tsx`, `flow-settings-sheet.tsx`; `web/locales/de/settings.json`, `resources.json`; `api/Service/Automations/Boundary/HttpControllers/AutomationSettingsController.cs`, `NodeRed/Boundary/HttpControllers/NodeRedFlowsController.cs`, `NodeRed/Application/Services/NodeRedFlowService.cs`, `Application/AutomationOptions.cs`; `api/Service/ManagedResources/Boundary/HttpControllers/ResourceSwitchController.cs`, `ResourceEndpointBindingsController.cs`; `integrations/node-red/nodes/mardu.html`, `editor/deployment-lifecycle.js`.
- Änderung: Runtime-Einrichtung, Status/Reparatur und die optionale Zugangsprüfung getrennt. Anschlussverwaltung in die neue Anleitung ausgelagert. Alle bisherigen Abschnittsanker bleiben mit `span`-Muster und kurzen Zielverweisen erreichbar. Folgen des Deaktivierens als nativer Warnhinweis und aktuelles Einrichtungsbild erhalten. Keine S7-Erweiterung übernommen.
- Browserbeleg: In eigener Sitzung `docs-revision-entwickeln` auf `/docs-revision/dashboard/admin/integrations/automations` den deaktivierten, nicht verbundenen Ausgangszustand gelesen. Aktuellen Screenshot des Hauptbereichs ohne Konto-/Seitennavigation als `bilder/automationen-einrichtung-aktuell.png` aufgenommen, visuell geprüft und mit `ImageZoom` samt Alttext eingebunden.
- Checks / Grenzen: MDX, Format, Ziele und sämtliche historischen Anker bestanden. Kein Aktivieren/Reparieren, keine gespeicherte Zugangsregel, kein Schaltauftrag und kein Node-RED-Deploy. Die Einrichtungsansicht belegt keine verbundene Laufzeit oder physische Wirkung.

### `administration/automationen-anschluesse.mdx` — eigenständige Anschlussaufgabe

- Leserfrage / Ergebnis: Wie stelle ich mit einer bereits eingerichteten Mardu-Verbindung Gerätefunktionen bereit und ändere oder entferne sie mit bekanntem Deploy-Ergebnis? Vorwissen: Node-RED, Ressourcenverwaltung und der konkrete Geräteprotokollvertrag.
- Quellen: Dieselben abgeglichenen Node-/Deploy-Verträge wie oben, insbesondere `integrations/node-red/nodes/mardu.html`, `editor/deployment-lifecycle.js`, `api/Service/Automations/NodeRed/Application/Services/NodeRedDeploymentService.cs`, `NodeRedDeploymentProjection.cs`, `api/Service/Automations/Application/AutomationOptions.cs`; zusätzlich die kanonischen Zielseiten `docs/administration/ressourcen-zustand.mdx` und `ressourcen-zutritt.mdx` sowie `api/Service/ManagedResources/Boundary/HttpControllers/ResourceEndpointBindingsController.cs` und `Application/Services/ResourceEndpointBindingService.cs` zur Abgrenzung von Beobachtungs- und Schalterzuordnungen.
- Änderung: Veröffentlichung, Simulationen, nativer Reader mit Node-RED-Maschinenaktor, Gerätefrist, Anschlussbearbeitung, bestätigtes Entfernen und Node-Ausfälle aus der bisherigen Sammelseite übernommen. Allgemeine Schalterbedienung und das Lösen von Zuordnungen durch Verweise auf die Ressourcenzustands-/Zutrittsanleitung ersetzt. Funktionsvergleich statt wiederholter Bedienanleitung. Node-RED-spezifische Hardwarebestätigung, Sperren, Verlust einer Deploy-Antwort, ID-Wiederverwendung und Geräteabschaltung erhalten. Ressourcenheimat als **Administration** benannt, historischer `koordination/ressourcen`-Pfad bleibt unverändert.
- Native Mittel / Bildbelege: `Steps`/`Step` für Veröffentlichen, passenden Ressourcenvorgang und Beispielprüfung. Das echte Einrichtungsbild bleibt bei der Runtime-Anleitung. Mangels eigener Node-RED-Laufzeit kein Anschlussbild als vermeintlicher Produktbeleg ergänzt.
- Checks / Grenzen: MDX, Format, relative Ziele und Zielanker geprüft. Kein echter Node-RED-Deploy, keine Gerätefrist und keine physische Wirkung praktisch geprüft. Navigation/Inventar und übrige eingehende Links übernimmt die Koordination.

## Gemeinsame Prüfnachweise

- `bun x --bun prettier --ignore-path /dev/null --check` aus `web/` auf alle acht eigenen Seiten: erfolgreich.
- Scoped `git -C web/content/docs diff --check --` auf eigene Pfade: keine Whitespace-Diagnose.
- Alle acht Seiten mit installiertem `@mdx-js/mdx` im Speicher kompiliert: erfolgreich; keine generierten Dateien.
- 50 relative und lokale Markdown-Verweise mit gültigen Zielen/Ankern. Alle Baseline-IDs aus `/tmp/mardu-docs-revision-20261103/baseline-render.json` im Quelltext erhalten.
- Elf Bash-/JSON-Codeblöcke mit `bash -n` beziehungsweise JSON-Parser syntaktisch geprüft; nichts ausgeführt.
- Keine API-/DTO-Dokumentationsänderung; vorhandene XML-/OpenAPI-Verträge und Node-Hilfe wiederverwendet. Keine Software-, Test-, Übersetzungs-, Metadaten- oder Navigationsänderung.

## Abnahmestand

Im ersten Prüflauf alle sieben Bestandsseiten in der isolierten Browsersitzung bei 1440 × 1000 und 390 × 844 gerendert. Alle Baseline-IDs im DOM erhalten, keine defekten Artikelbilder und kein horizontaler Viewportüberlauf. Ein einzelner Desktopabruf von `api-integration` lieferte während paralleler Dev-Änderungen 500; erneute Prüfung bei beiden Breiten lieferte 200. Die vier geänderten Seiten zusätzlich auf Desktop/Mobil aufgenommen und visuell geprüft: native Steps, verschiebbare Codeblöcke und Einrichtungsbild. Auf Mobil das Einrichtungsbild geöffnet (nativer offener Dialog) und per Escape wieder geschlossen. Zwei zunächst verwendete Prüfselektoren passten nicht zum aktuellen Lightbox-Dialog; nach DOM-/Komponentenabgleich über `dialog[open]` geprüft. Belege unter `/tmp/mardu-docs-revision-20261103/entwickeln-visual/`, DOM-Ergebnisse in `entwickeln-browser-render.txt`. Die öffentliche Website, Markdown-/Agentenausgabe und gemeinsame Navigationstests bleiben Teil der koordinierten Prüfung. Keine vollständige praktische Abnahme von Node-RED, Geräten oder externen Anbietern. Keine bestätigten zusätzlichen Produktfehler. Parallele S7-/Protokolländerungen weder verändert noch als veröffentlicht beschrieben.

## Prüfung nach der Strukturkorrektur

- `automationen`, `automationen-anschluesse`, der Entwicklerindex und `automationsfluesse` erneut bei 1440 × 1000 und 390 × 844 geladen: alle acht Fälle HTTP 200, keine fehlenden Baseline-IDs und kein horizontaler Viewportüberlauf. Die Anschlussseite zeigt drei native Schritte; der Runtime-Einstieg verwendet keine künstliche Schrittgliederung.
- Beide Administrationsseiten auf Desktop/Mobil aufgenommen und die vier Bilder visuell geprüft. Das echte Einrichtungsbild ist erhalten. Die neue Seite war beim Aufnehmen noch ohne zentrale Metadatenzuordnung erreichbar und zeigte daher den allgemeinen Seitenbaum; Navigation/Inventar übernimmt die Koordination.
- Belege: `/tmp/mardu-docs-revision-20261103/entwickeln-struktur-browser.txt` und `entwickeln-visual/struktur-*.png`.
- Alle acht Produktseiten erneut im Speicher kompiliert, Prettier auf Seiten und Bericht erfolgreich; scoped `diff --check` ohne Diagnose. Für die neue ungetrackte Anschlussdatei zusätzlich `diff --check --no-index /dev/null` ohne Whitespace-Diagnose; Exit 1 zeigt ausschließlich den neuen Inhalt an. 50 relative/lokale Verweise sowie alle bisherigen Anker bleiben gültig.
- Die Strukturänderung hat keine erneute Hardware-, MQTT- oder Node-RED-Laufzeitprüfung ausgelöst. Die zuvor belegten HTTP-/MCP-Leseprüfungen gelten unverändert; keine weiteren Token oder Systemeinstellungen verändert.
