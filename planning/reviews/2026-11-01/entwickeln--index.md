# Seitenrevision P56: Entwickeln

## Änderungsbrief

Personen mit Erfahrung in Softwareintegration sollen von diesem Bereichsstart
aus den passenden Zugang und die zugehörige Anleitung finden. Die inzwischen
ausgearbeiteten HTTP-, MQTT- und Node-RED-Seiten ersetzen den bisherigen Hinweis
auf fehlende Anleitungen. Der Einstieg unterscheidet Identität, technische Rechte
und die mit den Verantwortlichen abzusprechende Freigabe. Gute Orientierung,
Bereichswechsel und bestehende Anker bleiben erhalten. Nur diese Seite und dieser
Bericht werden geändert; Navigation und gemeinsame Consumer-Prüfung übernimmt die
Koordination. Der Umfang umfasst Quellenabgleich, MDX-Kompilierung, Format- und
Linkprüfung, keine praktische Integration oder Browserabnahme.

## Kurzbefund

- **Entscheidung: verbessert; offene Consumer-Prüfung.** Leserfrage: Welche
  Anleitung passt zu meiner Integration, welchen Zugang verwendet sie und was
  muss mit den Verantwortlichen geklärt werden?
- Der veraltete Hinweis auf fehlende HTTP-, MQTT- und Flow-Anleitungen wurde
  durch Links auf die vorhandenen ausgearbeiteten Seiten ersetzt. Die neue
  `automationsfluesse.mdx` lag beim Lesen und bei der Linkprüfung vor.
- Informations-MQTT wird als externer Lesezugang, Produkt-MCP als Zugang zu
  Mardu-Daten und Aktionen beschrieben. Es entstehen keine zusätzlichen
  SignalR- oder Protokollpaket-Anleitungen.
- Der Einstieg trennt organisatorische Absprache, Identität und technische
  Berechtigung. Node-RED-Editor und Laufzeitzugang sind getrennt; die breite
  Laufzeitberechtigung bleibt sichtbar. Keine Rolle wird aus dem Doku-Bereich
  abgeleitet.
- Erhalten: Überblickslink, Referenzhinweis, Quellcode-Abgrenzung, alle drei
  Abschnittsüberschriften sowie die alten Anker `in-diesem-bereich` und
  `offene-dokumentationsaufgaben`. Die native virtuelle API-Referenz bleibt unter
  `entwickeln/API`; keine Referenzdateien wurden angelegt oder geändert.

## Quellenabgleich

Pfade beziehen sich auf die Wurzel des Software-Repositories.

- `web/lib/source.ts:29–39`: OpenAPI wird als native Quelle unter
  `entwickeln/API` mit Backend-Verträgen eingebunden;
  `web/lib/docs-roles.tsx:161–182` ordnet den Bereich und das API-Präfix zu.
- `web/content/docs/docs/entwickeln/api-integration.mdx`, `http-api.mdx`,
  `mqtt-events.mdx`, `mcp-anbindung.mdx` und `automationsfluesse.mdx`:
  Aufgaben, Zugangstypen, Grenzen und erste lesende Beispiele abgeglichen.
- `api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs:25–47`:
  persönlicher HTTP-Aufruf, authentifiziertes Konto und Profilrecht;
  `api/Framework/Infrastructure/Identity/Tokens/Boundary/TokensController.cs:27–59`:
  Anmeldung und Tokenantwort.
- `api/Service/Mcp/MarduMcpExtensions.cs:88–114,120–140`: HTTP-Transport,
  Produktwerkzeuge und autorisierte MCP-Route.
  `api/Service/Mcp/Authorization/McpPermissionAuthorizationHandler.cs:30–58`
  prüft delegierte Rechte und aktuelle Kontorechte;
  `api/Service/Mcp/McpToolPolicyFilter.cs:19–55` begrenzt Tools durch die Richtlinie.
- `api/Framework/Infrastructure/Network/Broker/MqttServerHostedService.cs:415–432`:
  alle externen Veröffentlichungen werden zurückgewiesen;
  `Boundary/MqttUsersController.cs:19–60` desselben Broker-Verzeichnisses:
  getrennte MQTT-Benutzerverwaltung mit Integrationsrechten.
- `api/Service/Automations/NodeRed/Boundary/HttpControllers/NodeRedEditorSessionsController.cs:17–39`:
  persönliche Editor-Sitzung und View-Recht.
  `api/Service/Automations/Boundary/HttpControllers/AutomationResourcesController.cs:11–39`
  verwendet dagegen den Automation-Zugang.
  `api/Service/Automations/Application/Services/AutomationResourceService.cs:23–45,299–307`
  liest Ressourcen nach Laufzeitauthentifizierung ohne Flow-Ressourcenauswahl;
  `AutomationExecutionService.cs:23–60,116–123` im selben Verzeichnis behandelt
  registrierte Aktionsaufrufe der Laufzeit.
- `integrations/node-red/nodes/mardu.html:1553,1658,1688` und folgende Abschnitte:
  bestehende Node-Hilfe als Vertragsnachschlageweg. Die Administrationsseiten
  `mcp-verwalten.mdx`, `integrationen.mdx#mqtt` und `automationen.mdx` bleiben
  kanonische Einrichtungseinstiege.

## Ausgeführte Checks und Grenzen

- Prettier mit bestehender `web/.prettierrc` nur auf beide eigenen Dateien
  angewendet und abschließend geprüft; der standardmäßig ignorierte Doku-Pfad
  wurde für diese beiden Dateien ausdrücklich einbezogen.
- Produktseite mit vorhandenem `@mdx-js/mdx` kompiliert. Alle neun relativen
  Linkziele existieren; der MQTT-Zielanker wurde geprüft. Zwei explizite alte
  IDs und alle drei bisherigen Überschriften sind erhalten.
- `git diff --check` für die eigenen Dateien und statischer Diffabgleich.
- Keine API-/DTO-/Softwareänderung; keine zusätzliche Vertragsdokumentation nötig.
- Nicht durchgeführt: Consumer-/Browser-/Mobile-/Theme-Prüfung,
  Markdown-/LLM-Ausgabe, reale HTTP-/MCP-/MQTT-Verbindung, Node-RED-Deploy oder
  Hardware-/Providerprüfung. Keine Abnahmebehauptung aufgrund statischer Checks.

## An die Koordination

Die Startseite verlinkt nun die nutzbaren Integrationsseiten. Zum Prüfzeitpunkt
enthält `entwickeln/meta.json` weiterhin nur MCP und API; HTTP-, MQTT-,
Integrationsübersicht und Flow-Anleitung müssen in der gemeinsamen Navigation
berücksichtigt werden. `web/lib/docs-roles.tsx` enthält noch keinen ausdrücklichen
Slug für `entwickeln/automationsfluesse`. Diese Dateien wurden nicht verändert.
Native API-Navigation sowie beide Consumer gemeinsam rendern. In den
Nachbarseiten bestehen noch frühere Hinweise auf eine fehlende Flow-Anleitung;
deren Abgleich liegt bei der Koordination.

## Geänderte Dateien

- `web/content/docs/docs/entwickeln/index.mdx`
- `web/content/docs/planning/reviews/2026-11-01/entwickeln--index.md`
