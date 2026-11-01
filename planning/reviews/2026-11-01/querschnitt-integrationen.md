# Querschnittsprüfung: Integrationen und Betrieb

Stand: 2026-11-01. Unabhängige statische Abschlussprüfung; Produktdateien nur
gelesen. Auftrag: verbleibende wesentliche Fehler in HTTP-, MQTT-, MCP-,
Node-RED-, IP500-, TLS-, Installations- und CLI-Anleitungen erkennen. Es wurden
keine Produktdateien, Verträge oder Konfigurationen geändert.

## Ergebnis

Ein belegter inhaltlicher Restfehler im Integrationsüberblick. In den geprüften
konkreten HTTP-, MQTT-, MCP-, Node-RED-, IP500-, TLS-, Installations- und
CLI-Abläufen keine weiteren wesentlichen Doku-Restfehler festgestellt.

### IP500-Überblick verspricht weiterhin periodische Subscription-Erneuerung

- **Seite:** `docs/administration/integrationen.mdx:86–90`, besonders Zeilen
  88–89: „TLS und der Zeitplan zum Erneuern der Subscriptions“.
- **Problem:** Die Formulierung schreibt dem konfigurierbaren Zeitplan eine
  Laufzeitwirkung zu, die aktuell nicht vorhanden ist. Die inzwischen ausgearbeitete
  kanonische Anleitung `docs/administration/ip500-netzwerk.mdx:55–60` schränkt
  denselben Punkt korrekt ein: Die Abonnements werden beim Verbindungsaufbau
  hergestellt; periodische Wiederanmeldung wird übersprungen. Der Überblick
  widerspricht dieser Erklärung und kann bei ausbleibenden Meldungen zu einer
  falschen Erwartung an den Zeitplan führen.
- **Codebeleg:**
  `api/Framework/Infrastructure/Network/Client/MqttSubscriptionRefreshService.cs:94–102`
  führt in `RefreshConfiguredTopicsAsync` ausdrücklich keine Subscription aus.
  Kommentar und Log nennen die Wiederherstellung beim Reconnect; die Methode
  endet mit `Task.CompletedTask`. Die tatsächlichen Subscription-Aufrufe stehen
  in derselben Datei in `SubscribeConfiguredTopicsAsync:39–90`.
- **Minimaler Korrekturvorschlag:** In der Übersicht „und der Zeitplan zum
  Erneuern der Subscriptions“ entfernen und für Einrichtung sowie die Grenze des
  Feldes **Refresh-Cron** auf `./ip500-netzwerk.mdx` verlinken. Keine neue
  Produktkorrektur ableiten. Der Befund betrifft nur die verbliebene
  uneingeschränkte Überblicksaussage; die bekannte Abweichung ist in der
  Detailanleitung bereits zutreffend beschrieben.

## Geprüfter Zusammenhang und Quellen

Die Doku-Regeln in `AGENTS.md` und `ARBEITSWEISE.md` des Doku-Submoduls sowie
die passenden Seitenberichte vom 2026-11-01 wurden gelesen. Die folgenden
Aussagegruppen wurden mit aktuellen Implementierungen abgeglichen:

| Bereich            | Geprüfte wesentliche Aussagen und Quellen                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTTP               | Anmeldefelder, 200/202 und MFA, Tokenrotation/-widerruf, Profilrechte und endpunktspezifische Limits: `TokensController.cs`, `CompleteAuthenticationChallengeRequest.cs`, `AuthenticationChallengeMethod.cs`, `TokenResponse.cs`, `ProfileController.cs`, `RateLimitingExtensions.cs`. Ressourcenbeispiele, Enumwerte, Seitengrößen und Versionskonflikt: `ManagedResourceDtos.cs`, `ManagedResourcesController.cs`, `ManagedResourceService.cs`, `ManagedResource.cs`, `PaginationFilter.cs`. |
| Informations-MQTT  | Trennung vom Geräte- und Automation-Vertrag, externe Nur-Lese-Regel, Rollen/ACLs, Deny-Vorrang, QoS, Retained-Unterdrückung, TLS und Client-ID: `MqttServerHostedService.cs`, `MqttInfoPolicy.cs`, `DbMqttAclService.cs`, `MqttBrokerSettings.cs`. Topics, JSON, 60-Sekunden-Veröffentlichung und leere Retained-Payloads bei Löschung: `MqttInfoTopics.cs`, `SystemInfoPublisher.cs`, `SystemInfoTelemetryHostedService.cs`, `DeviceInfoPublisher.cs`, `DeviceInfoContracts.cs`.              |
| MCP                | Zustandsloser Streamable-HTTP-Transport, Bearer je Anfrage, Rechte und Serverfreigaben, persönlicher Tokenlebenszyklus und `notifications_list` mit `limit: 1`: `MarduMcpExtensions.cs`, `McpAgentAuthenticationHandler.cs`, `McpEnabledRequirement.cs`, `McpAgentCredentialRequirement.cs`, `McpAgentConnectionService.cs`, `McpToolPolicyFilter.cs`, `NotificationMcpTools.cs`.                                                                                                              |
| Node-RED           | Breiter Laufzeitzugriff gegenüber Editoridentität, Ressourcen-/Schemaantworten, Versionsvergleich und 30-Sekunden-Abgleich, CloudEvent-Nachrichten und Checkpoint-Bindung: `AutomationResourceService.cs`, `integrations/node-red/src/index.ts`, `src/runtime/connection.ts`, `src/runtime/checkpoints.ts`. Keine Annahme als physische Ausführung bestätigt.                                                                                                                                  |
| IP500              | Passwortbeibehaltung, TLS-Portwechsel und bestehende Validierungen: `Ip500NetworkSettings.cs`, `MqttSettings.cs`, Dashboard `admin/server/ip500-network/page.tsx`. Subscription-Grenze wie oben.                                                                                                                                                                                                                                                                                               |
| TLS / Installation | Kestrel-Dateipfad, Content Root, HTTPS-Standardport 7443, persistenter Ersatz und Neustart: `api/Server/Program.cs`, `PersistentHttpsCertificateProvider.cs`, `docker-compose.https.yml`. Caddy auf 443, API intern 8080, Volumes, Healthcheck, `pull_policy: always`, Installationsarchiv und Stable-Releases: `deploy/production/docker-compose.prod.yml`, `Caddyfile`, `.env.deploy.example`, `.github/workflows/release-container.yml`.                                                    |
| Wartungs-CLI       | Verdeckte interaktive Passwortabfrage, Konto-/Sitzungsaktionen, JSON-Felder, Rückgabewerte und 30-Sekunden-Anfragetimeout: `AdminCli.cs`, `MaintenanceOperations.cs`, `MaintenanceClient.cs`, `UserService.Maintenance.cs`.                                                                                                                                                                                                                                                                    |

## Grenzen und Checks

- Reine Quellen- und Quervergleichsprüfung; keine Browser-, Hardware-, Provider-,
  Broker-, CLI- oder Installationsausführung und keine externen Aktionen.
- Keine globalen Builds oder Tests. Der bekannte Production-8080-/Setup-5001-Konflikt
  ist in der Installationsseite erkennbar eingegrenzt und wird hier nicht erneut
  als Doku-Restfehler gemeldet. Ebenso werden korrekt eingeschränkte
  Produktabweichungen nicht zu neuen Dokumentationsfehlern erklärt.
- Keine erfolgreiche Zustellung, physische Gerätewirkung oder Praxisabnahme aus
  dieser statischen Prüfung abgeleitet.
- Berichtsformat mit vorhandenem Prettier geprüft: erfolgreich.
  `git diff --no-index --check /dev/null` für den neuen Bericht lieferte keine
  Whitespace-Meldungen (Exit 1 wegen des Dateiunterschieds zu `/dev/null`).
- Nur dieser Bericht wurde angelegt; API-/DTO-Dokumentation unverändert.
