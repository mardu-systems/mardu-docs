# Prüfpaket Anbindungen – 2026-11-03

## Änderungsbrief

Leser sind Personen, die Mardu-Anbindungen mit bereitgestellten Verbindungsdaten einrichten und deren Ergebnis prüfen. Verzeichnis- und Anbieteradministration werden vorausgesetzt; Mardu-Kontozuordnung, Rechte und die Grenzen einzelner Tests werden erklärt. Betroffen sind ausschließlich die sieben zugewiesenen Produktseiten. Die Integrationsübersicht wird als Einstieg verdichtet, gültige Einzelanleitungen bleiben erhalten. Native Fumadocs-Steps ordnen zusammengehörige Einrichtungsphasen; Callouts heben konkrete Folgen hervor. URLs und Überschriftenanker bleiben erhalten. Keine Software-, Vertrags- oder Metadatenänderung.

Quellen sind die aktuellen Seiten, UI-Seiten und Controller, deutsche/englische Übersetzungen sowie die nachfolgend genannten Services. Format und Diff werden lokal geprüft; Rendering, Links/Anker und Screenshots werden mit dem Koordinator abgestimmt. Keine externe LDAP-/OIDC-/MQTT-/IP500-Anbieterprüfung und kein externer Nachrichtenempfang wurden durchgeführt. Die Website ist ein separater, hier nicht gestarteter Consumer.

## Seitenprüfung

Inhalt und eigene Produktprüfung abgeschlossen; zentrale Consumerprüfung ausstehend.

### Integrationen

- Entscheidung: Einstieg verdichtet; alle vorhandenen Abschnittstitel erhalten. Details zu Brokerneustart, Laufkontrolle und Ausstellerpfaden stehen in den kanonischen Einzelanleitungen statt doppelt im Einstieg. Die getrennten Wege für Informationsbroker/IP500 sowie Anmeldung/Nachweisquellen bleiben sichtbar.
- Quellen: `web/lib/settings/config.ts`, `web/lib/settings/search.ts`, `web/app/[project]/dashboard/admin/integrations/{ldap,oidc}/page.tsx` (Weiterleitungen), `web/app/[project]/dashboard/admin/integrations/{openbadges,automations}/page.tsx`; die unten geprüften Einzelanbindungen; `web/locales/{de,en}/settings.json`.
- Prüfung/Grenze: Routen, Begriffe, Rechte und Suchverhalten per Code abgeglichen. Keine Anbieteranbindung oder Flowwirkung aus dem Einstieg praktisch getestet. Rendering/Navigation erfolgt zentral.

### LDAP-Verzeichnis anbinden

- Entscheidung: Gültige Anleitung erhalten, Rechte ohne doppelte technische Permission-Bezeichner formuliert; exakte Feldgruppe **Server & Port** korrigiert. Vier Einrichtungsphasen in native `Steps` gegliedert. Kontolöschfolgen als sichtbarer Callout. Die zuvor fehlende Abschaltung samt Folgen für Konten und Anmeldung ergänzt.
- Quellen UI: `web/app/[project]/dashboard/admin/server/ldap/{page.tsx,use-ldap-settings-controller.ts,ldap-settings.utils.ts,ldap-role-rules.utils.ts}`; `web/locales/{de,en}/settings.json`.
- Quellen Backend: `api/Framework/Infrastructure/Auth/Boundary/LdapIntegrationController.cs`, `api/Framework/Infrastructure/Auth/Application/LdapIntegrationService.cs`, `api/Framework/Infrastructure/Identity/External/{LdapAuthenticationService.cs,LdapSyncService.cs,LdapSyncJob.cs}`, `api/Framework/Infrastructure/Identity/Users/Services/UserService.CreateUpdate.cs`.
- Belegt im Code: Entwurf gegenüber gespeichertem Abgleich, Vorschaupflicht im Formular, Rollenentzug und Entfernen letzter Regel, direkte Admin-Ausnahme, Tokens bei Deprovisionierung, Sync-Abschaltung, lokale Passwortalternative. Keine LDAP-Verbindung, Vorschau mit Anbieter, Synchronisierung oder persönliche LDAP-Anmeldung ausgeführt. Browserprüfung: Felder des deaktivierten Verzeichnisses mit fiktiven Werten bedient, Screenshot `docs/administration/bilder/ldap-verbindung-entwurf-aktuell.png` aufgenommen und visuell geprüft. Kein Speichern/Test; Entwurf beim Verlassen verworfen.

### Anmeldung über OpenID Connect einrichten

- Entscheidung: Detaillierte gültige Kontozuordnungs- und Rückleitungsregeln erhalten. Rechte verdichtet; drei Einrichtungsphasen in native `Steps` gegliedert. Grenze der isolierten Test-Anmeldung als sichtbarer Callout.
- Quellen UI: `web/app/[project]/dashboard/admin/server/oidc/{page.tsx,oidc-provider-editor.tsx,oidc-settings-sections.tsx,use-oidc-settings-controller.ts}`; `web/locales/{de,en}/settings.json`.
- Quellen Backend: `api/Framework/Infrastructure/Auth/Boundary/OidcIntegrationController.cs`, `api/Framework/Infrastructure/Auth/Application/{OidcBrokerService.cs,OidcPrincipalMappingService.cs,OidcRuntimeSchemeManager.cs,OidcTestLoginService.cs}`.
- Belegt im Code: getrennte Rückleitungen, PKCE, kein UserInfo-Abruf, automatische Kontoanlage und Verknüpfung mit Registrierungsvorgaben, MFA-Allowlisten, verwaltete Rollen, Hot-Reload und Versionskonflikte. Kein externer Provider registriert, aktiviert oder gespeichert; keine Discovery-, Token- oder Anmeldeprüfung ausgeführt. Browserprüfung: Provider nur im lokalen Entwurf hinzugefügt, fiktive Endpunkte und Public-Client-Verfahren eingetragen, Schritt **Prüfen** geöffnet. Screenshot `docs/administration/bilder/oidc-pruefen-entwurf-aktuell.png` visuell geprüft; Entwurf beim Verlassen verworfen. Im isolierten Zugang zeigt die Seite **Versionskennung fehlt** und blockiert Speichern; Ursache nicht untersucht, Koordinator informiert.

### MQTT-Zugänge verwalten

- Entscheidung: Gültige Anleitung erhalten, Demo-Heartbeat-Erklärung verdichtet. Vier Einrichtungsphasen in native `Steps` gegliedert; Unterbrechung beim Speichern vor dem ersten Schritt hervorgehoben.
- Quellen UI: `web/app/[project]/dashboard/admin/integrations/mqtt/{page.tsx,use-mqtt-broker-settings-controller.ts}`, `web/components/integrations/mqtt/{mqtt-acl-editor-dialog.tsx,mqtt-users-card.tsx,mqtt-runtime-overview.tsx}`, `web/locales/{de,en}/settings.json`.
- Quellen Backend: `api/Service/Devices/Boundary/HttpControllers/MqttInfoBrokerSettingsController.cs`, `api/Service/Devices/Application/Publishing/MqttInfoPublishingSettings.cs`, `api/Framework/Infrastructure/Network/Broker/{MqttInfoPolicy.cs,MqttServerHostedService.cs}`, `api/Framework/Infrastructure/Network/Broker/Boundary/{MqttUsersController.cs,MqttAclsController.cs,MqttBrokerStatusController.cs}`.
- Belegt im Code: Lesezugriff externer Clients, eingeschränkter Kontotyp, Wildcards, überlappende deny-Regeln, QoS/Retained, Trennung und Abonnemententfernung bei Verwaltungsänderungen, Pflichtfeld Demo-ID. Browserprüfung: Brokerstatus **Läuft**, eingeschränktes Konto `werkstatt-monitor` angelegt, exakte ACL `v1/info/public/system/state` gespeichert und anschließend `subscribe / allow`, **Aktiv**, QoS 1 in der Liste geprüft. Screenshot `docs/administration/bilder/mqtt-leseregel-aktuell.png` zeigt den Editor vor dem Speichern und wurde visuell geprüft. Kein externer Client, Nachrichtempfang, Neustart oder Widerruf am Client getestet.

### IP500-Netzwerk anbinden

- Entscheidung: Gültige Anleitung erhalten; Einrichten und Ergebnisprüfung als zwei native `Steps`, Wiederverbindungsunterbrechung sichtbar hervorgehoben und wiederholte Ergebnisgrenzen verdichtet.
- Quellen UI: `web/app/[project]/dashboard/admin/server/ip500-network/page.tsx`; `web/locales/{de,en}/settings.json`.
- Quellen Backend: `api/Service/Devices/Boundary/HttpControllers/Ip500NetworkSettingsController.cs`, `api/Service/Devices/Application/Ip500NetworkSettings.cs`, `api/Framework/Infrastructure/Settings/Boundary/Dto/SettingsSectionDataDtos.cs`, `api/Framework/Infrastructure/Network/Client/{MqttClientHostedService.cs,MqttSubscriptionRefreshService.cs,Configuration/MqttSettings.cs}`.
- Belegt im Code: Password-behalten-Verhalten, Host/Client-ID/Port, zusammenpassende Credentials, Cron-Pflicht, Standardportwechsel der UI, Hot-Reload und übersprungene periodische Neuanmeldung. Die UI-Hinweise über leeres Cron/periodische Wiederherstellung weichen weiterhin von der Laufzeit ab; Dokumentation beschreibt das tatsächliche Verhalten. Browserprüfung: IP500-Formular vollständig geladen, Aktivierungsschalter und Cron-Feld sichtbar. Keine Werte geändert oder gespeichert; kein IP500-Broker, Edge-Router oder Gerät praktisch geprüft.

### MCP für Agenten freigeben

- Entscheidung: Text bewusst unverändert. Die Seite ist bereits knapp, auf Einrichten/Begrenzen/Widerruf ausgerichtet und enthält die notwendigen Grenzen. Nur eine aktuelle `ImageZoom`-Aufnahme der gespeicherten Richtlinie ergänzt, damit die Serverfreigabe und getrennten Tool-Schalter auffindbar sind.
- Quellen UI: `web/app/[project]/dashboard/admin/integrations/mcp/{page.tsx,use-mcp-settings-controller.ts}`; `web/lib/settings/config.ts`; `web/locales/{de,en}/settings.json`.
- Quellen Backend: `api/Service/Mcp/{MarduMcpOptions.cs,McpToolPolicyFilter.cs}`, `api/Service/Mcp/Boundary/HttpControllers/McpSettingsController.cs`, `api/Service/Mcp/Application/McpAgentConnectionService.cs`, `api/Service/Mcp/Authorization/{McpEnabledRequirement.cs,McpAgentCredentialRequirement.cs,McpAgentAuthenticationHandler.cs,McpPermissionAuthorizationHandler.cs}`.
- Belegt im Code: drei Grenzen, nur lesbare Route, Live-Richtlinie und Rechteüberschneidung, fehlender automatischer Tokenwiderruf beim Abschalten. Eigene Browserprüfung: Auf ausdrückliche Freigabe des Koordinators im isolierten Runtime nur MCP-Endpunkt, persönliche Verbindungen und Agent-only aktiviert; Schreib-/destruktive Tools ausgeschaltet belassen. Speichern und Neuladen erfolgreich, alle fünf Schalterzustände erneut bestätigt. Screenshot `docs/administration/bilder/mcp-lesezugang-aktuell.png` visuell geprüft. Geteilte API-Evidenz von `revision_entwickeln`: persönliche Verbindung nur mit `Permissions.Profile.View`, Laufzeit ein Tag (201); initialize 200, initialized-Notification 202, tools/list 200, notifications_list(limit=1) 200 ohne Toolfehler; Verbindung widerrufen (204), alter Token anschließend 401. Tokens und persönliche Nachrichten wurden nicht ausgegeben. Keine Schreib-/Löschtools getestet; Richtlinie bleibt für die weitere isolierte Abnahme aktiv.

### Benachrichtigungen einrichten und prüfen

- Entscheidung: Vorbereitung, SMTP-Test und Ereignistest als drei native `Steps`. Trennung zwischen Mailserverübergabe und Empfang als Callout; erforderliches SMTP-Konto vor der Nutzung klargestellt. Aussage zur Verarbeitung korrigiert: sofort fällige Zustellungen werden direkt angestoßen, Minutenjobs prüfen zusätzlich fällige Aufträge.
- Quellen UI: `web/app/[project]/dashboard/admin/server/mail-settings/{page.tsx,use-mail-settings-controller.ts}`, `web/components/notifications/notification-inbox-sheet.tsx`; `web/locales/{de,en}/settings.json`.
- Quellen Backend: `api/Service/Admin/Settings/Boundary/HttpControllers/MailSettingsController.cs`, `api/Framework/Infrastructure/Mailing/SmtpMailService.cs`, `api/Service/Notifications/Application/Services/{NotificationProcessor.cs,NotificationChannelAvailabilityService.cs,NotificationPreferenceService.cs,NotificationAudienceService.cs}`, `api/Service/Notifications/Application/Catalog/NotificationCatalog.cs`, `api/server/Hosting/NotificationHostingExtensions.cs`.
- Belegt im Code: SMTP-STARTTLS und Authentifizierungspflicht, Passwort-behalten-Verhalten, Test mit gespeicherten Werten, Kanalverfügbarkeit und bestätigte Kontakte, getrennte Worker. Browserprüfung: SMTP-Formular und **Versand testen** geladen, Testknopf ohne Empfänger gesperrt. Keine Konfiguration geändert, weder E-Mail noch SMS/WebPush versendet; kein externes Zielpostfach geprüft.

## Gemeinsame Prüfungen

- Bestehende URLs und sämtliche bisherigen Überschriftentexte unverändert; LDAP erhält einen zusätzlichen Abschnitt.
- Native Komponenten aus `fumadocs-ui/components/steps` und `fumadocs-ui/components/image-zoom`, Callout aus `web/mdx-components.tsx`; keine neue Komponente, Abhängigkeit oder CSS. Vier eigene aktuelle Screenshots mit fiktiven Angaben aus dem isolierten Produktzugang, alle mit Alttext und visuell geprüft.
- Keine API/DTO-Verträge geändert; bestehende Produktbeschreibungen an den aktuellen Verträgen geprüft.
- Abschließende Format- und Diffchecks sind im folgenden Prüfergebnis aufgezeichnet.
- Consumer-Rendering, Markdown-Ausgabe und zentraler Link-/Ankercheck noch offen. Diese Seiten werden hier nicht als vollständig abgenommen markiert.

## Beobachtete Produktgrenzen

- OIDC-Editor im isolierten Zugang: **Versionskennung fehlt**; keine Aussage zur Ursache oder zur Einrichtung bei einem realen Provider. Dem Koordinator gemeldet.
- SMTP-Oberfläche bezeichnet das Konto als optional, `SmtpMailService` verlangt Benutzername und Passwort. Vorhandene Dokumentation dazu erhalten und vor dem Test sichtbar gemacht.
- IP500-Hinweis zu leerem Cron und periodischer Subscription-Erneuerung passt nicht zur aktuellen Validierung/Laufzeit. Kein Softwarepatch im Doku-Paket.
- MCP-Lesezugang wurde nur in der vom Koordinator ausdrücklich freigegebenen isolierten Laufzeit aktiviert. Produktive Einstellungen und Anbieter wurden nicht verändert.

## Abschließendes Prüfergebnis

- `bun x --bun prettier --ignore-path /dev/null --check` für die sieben Seiten und diesen Bericht: erfolgreich.
- `git -C web/content/docs diff --check -- <eigene Seiten und Bericht>`: erfolgreich.
- Statischer Abgleich mit `git show HEAD:<Seite>`: sämtliche bisherigen Überschriften in allen sieben Seiten erhalten; kein bestehender Seitenpfad geändert. Dies ersetzt den zentralen gerenderten Ankercheck nicht.
- Die vier neuen PNGs wurden jeweils mit dem Bildbetrachter geprüft; kein nachgezeichnetes Bild und keine unkenntlich gemachten Echtdaten. Die Ausschnitte stammen direkt aus der laufenden Oberfläche.
- Keine Builds, Serverstarts, Testsuites, Commits oder Metadatenänderungen durch dieses Paket.
