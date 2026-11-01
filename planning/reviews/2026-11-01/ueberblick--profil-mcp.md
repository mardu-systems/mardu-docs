# P17 – Eigene MCP-Verbindungen

- Seite: `docs/ueberblick/profil-mcp.mdx`.
- Leserfrage: Wie richte ich einen persönlichen Agentenzugang ein, ersetze seinen Token und entziehe den Zugriff? Vorausgesetzt sind ein eigenes Konto und ein kompatibler Client; Heimatbereich bleibt Überblick / eigenes Profil.
- Entscheidung: **verbessert**, mit zwei kleinen Textkorrekturen. Die bereits verdichtete Anleitung, Bilder, URLs und Überschriften bleiben erhalten.
- Änderungsbrief / Plan: Kontomenü, Profilnavigation, Rechte, persönliche Tokens und MCP-Authentifizierung statisch abgleichen; nur belegte Abweichungen korrigieren; Format und lokale Verweise prüfen. Keine Softwareänderung oder echte Freigabe.

## Befunde und Quellen

- Einstieg auf **Kontoeinstellungen → MCP-Verbindungen** berichtigt: `web/components/layout/common/account-menu-items.tsx:24`, `web/locales/de/navigation.json:32`, `web/components/layout/settings/profile-nav.config.ts:180`. Mobile Benutzeransicht verwendet dieselbe Navigationskonfiguration (`web/components/profile/profile-settings-layout.tsx:43`, `:116`); die Portalroute verwendet dieselbe MCP-Seite (`web/app/[project]/portal/profile/mcp/page.tsx:1`).
- Profil-Leserechte für Liste/Fähigkeiten und Profil-Änderungsrechte für Erstellen, Rotation und Widerruf bestätigt: `api/Service/Mcp/Boundary/HttpControllers/McpAgentConnectionsController.cs:24`, `:33`, `:42`, `:59`, `:70`.
- Pflichtname bis 128 Zeichen, mindestens eine delegierbare Berechtigung, Serverstandard und kürzere Laufzeit, aktive Verbindungsgrenze, einmalige Tokenrückgabe und Eigentümerprüfung bestätigt: `api/Service/Mcp/Boundary/Dto/McpAgentConnectionDtos.cs:33`, `api/Service/Mcp/Application/McpAgentConnectionService.cs:77`, `:107`, `:274`.
- Rotation ersetzt den gespeicherten Tokenhash ohne neues Ablaufdatum; Widerruf bleibt in der Liste sichtbar und macht die Verbindung inaktiv: `api/Service/Mcp/Application/McpAgentConnectionService.cs:126`, `:149`, `:301`; Darstellung in `web/app/[project]/dashboard/user-management/profile/mcp/page.tsx:276`.
- Rechte bleiben durch ausgewählte Tokenrechte, aktuelle Benutzerrechte und Serverrichtlinie begrenzt: `api/Service/Mcp/Authorization/McpPermissionAuthorizationHandler.cs:35`, `:55`, `api/Service/Mcp/McpToolPolicyFilter.cs:34`, `api/Service/Mcp/Application/McpAgentConnectionService.cs:168`.
- **OAuth-Abgrenzung:** Dieser persönliche MCP-Zugang bietet im geprüften UI und MCP-Backend einen manuell erstellten opaken Bearer-Token. Kein OAuth-Freigabedialog, Provider-Redirect oder OAuth-Widerrufsablauf ist hier implementiert; deshalb keine solchen Schritte ergänzt. Quellen: `api/Service/Mcp/MarduMcpExtensions.cs:58`, `:88`, `api/Service/Mcp/Authorization/McpAgentAuthenticationHandler.cs:29`, `web/app/[project]/dashboard/user-management/profile/mcp/page.tsx:245`, `:397`, `:543`.
- Hinweis auf eine Fehlermeldung beim Erstellen entfernt: Der Erstellungsdialog erhält das vorhandene `error`-Prop nicht; `mutationError` wird erst nach dem Schließen angezeigt (`web/app/[project]/dashboard/user-management/profile/mcp/page.tsx:239`, `:245`, `:336`, `:399`). Zusätzlich setzt der Controller jeden 409-Konflikt beim Erstellen auf „deaktiviert“, auch wenn die aktive Verbindungsgrenze erreicht wurde (`use-profile-mcp-controller.ts:151`; Backend `McpAgentConnectionService.cs:101`). Produktbefund an Koordination; keine Software geändert.

## Prüfung und verbleibender Umfang

- Statische UI-, Übersetzungs-, Vertrags- und Backendprüfung durchgeführt. `prettier --ignore-path /dev/null --check` für beide eigenen Dateien und `git diff --check` bestanden. Lokale Python-Prüfung bestätigt beide Bilddateien, den relativen Seitenlink, den Abschnittsanker, Frontmatter und fehlendes zusätzliches H1.
- Keine eigene Browser-, Client- oder Providerprüfung. Aktuellen Kontomenüzugang in Desktop und mobiler Benutzeransicht, Darstellung der vorhandenen Bilder, einmalige Tokenanzeige, reale Streamable-HTTP-Verbindung sowie Ablehnung nach Rotation/Widerruf mit einem Testkonto prüfen. Vorhandene ältere Prüfberichte/Bilder wurden nicht als heutige Abnahme gewertet.
- Keine Überschriften/Anker, Navigationsdateien oder Nachbarseiten geändert. Verweise auf Administration und bestehende Abschnittsanker bleiben erhalten. Kein zusätzlicher Seitenbedarf.
- Geänderte Dateien: diese Berichtsdatei und `docs/ueberblick/profil-mcp.mdx`. API-/DTO-Dokumentation unverändert, da keine API geändert wurde.
