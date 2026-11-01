# P28 — Sicherheit und Betrieb

## Änderungsbrief

Die bisher verborgene TODO-Seite soll Personen mit Verwaltungs- beziehungsweise
Hostzugriff beim Prüfen von Anmelderegeln und Betriebsstörungen helfen. Vorausgesetzt
sind Kenntnisse der eigenen Installation; die Seite erklärt keine Installation.
Ergebnis ist eine belegte Teilanleitung mit erhaltenen bisherigen Abschnittsankern.
Kontobezogene Verwaltungsabläufe bleiben kanonisch in `benutzer-rollen.mdx`,
persönliche Sicherheit im Profil, Hostwiederherstellung in `wartungs-cli.mdx`.
Vorhandene MDX-Links und normale Überschriften genügen. Es werden nur die zugewiesene
Seite und dieser Bericht geändert. Statische Quellen-, Link-, Anker- und
Formatprüfung sind möglich; angemeldeter Browser, OIDC-Anbieter, reale Zustellung,
Zertifikatswechsel und Wiederherstellung bleiben gesondert zu prüfen.

## Entscheidung und Befunde

**Belegbare Teildokumentation / offene Prüfung.** Die Seite enthält nun einen
nutzbaren Sicherheits- und Störungscheck statt TODOs. Gute Hinweise zu lokaler
Kontowiederherstellung, Mitteilungsdiagnose und MCP-Zugriff bleiben erhalten.
Alle fünf vorhandenen Abschnittsüberschriften und damit ihre Anker bleiben bestehen.

- Globale Auth Policy von kontobezogenen Sicherheitsaktionen getrennt; tatsächliche
  Wirkung von 2FA-, Passkey- und Recovery-Schaltern beschrieben. OIDC-MFA-Nachweis
  beim Anbieter von lokaler 2FA unterschieden.
- Vor Änderungen Einrichtung und getrennte Neuanmeldung prüfen; vorhandene
  Sitzung nicht als Beleg behandeln. Token-Laufzeiten benötigen laut Vertrag Neustart.
- Sitzungswiderruf, Kontodeaktivierung, Tag-Sperre und laufende Zutritts-/Editorvorgänge
  unterschieden. Keine Dashboard-Verwaltung fremder Anmeldesitzungen erfunden.
- Rechteprüfung als organisatorisches Beispiel, Audit-Leserecht/Exportrecht und
  Störungsangaben ergänzt. Vorhandene Aufgabenanleitungen werden verlinkt.
- API-Liveness, Readiness, Gesamtprüfungen und Dashboard-Erreichbarkeit abgegrenzt;
  Zertifikatsstatus als gespeicherte Metadaten beschrieben, ohne TLS-Zuweisung zu behaupten.
- Dashboard-Backup als nicht freigegeben gekennzeichnet. Kein hypothetischer
  Sicherungs-, Restore-, Update- oder TLS-Dialog beschrieben.

## Quellen

Pfade sind relativ zum Software-Repository; Zeilen beziehen sich auf den geprüften Stand.

| Aussage                                                                  | Geprüfte Quelle                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Menü und tatsächliche Schalter                                           | `web/components/layout/settings/server-nav.config.ts:61–103`; `web/app/[project]/dashboard/admin/server/auth-policy/page.tsx:138–180,488–539`; `web/locales/de/settings.json:1048–1070`                                                                                                                                                                                                                        |
| Settings.View/Update, Environment-Sperren, Neustart bei Tokenzeiten      | `api/Service/Admin/Settings/Boundary/HttpControllers/AuthPolicySettingsController.cs:29–89,260–305`; `web/components/layout/settings/config-settings-page.tsx:185–192,216–258,327–347`                                                                                                                                                                                                                         |
| Passwortanmeldung, lokale 2FA, Recovery, erneute Kontoprüfung            | `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:108–193,360–397,684–767`                                                                                                                                                                                                                                                                                                                |
| Erlaubte Passkeys und Schutz des letzten aktiven Admin-Passkeys          | `api/Framework/Infrastructure/Identity/Passkeys/PasskeyService.cs:50–79,259–276,329–347`                                                                                                                                                                                                                                                                                                                       |
| OIDC-MFA für aktuelle und kommende Administratoren, AMR/ACR-Nachweis     | `api/Framework/Infrastructure/Auth/Application/OidcBrokerService.cs:202–204,493–545`; MFA-Neuprüfung bei Refresh: `TokenService.cs:725–752`                                                                                                                                                                                                                                                                    |
| 2FA-Deaktivierung und Recovery-Ausgabe                                   | `api/Framework/Infrastructure/Identity/Users/Services/UserService.TwoFactor.cs:90–148`                                                                                                                                                                                                                                                                                                                         |
| Passwortloser Link umgeht eingerichtete/vorgeschriebene 2FA nicht        | `api/Framework/Infrastructure/Identity/Passwordless/PasswordlessLoginService.cs:103–141`; zusätzliche Admin-MFA-Prüfung in `TokenService.cs:493–501,725–767`                                                                                                                                                                                                                                                   |
| Anmeldehistorie existiert als API, keine entsprechende neue UI behauptet | `api/Framework/Infrastructure/Identity/Users/Boundary/UserController.cs:280–299`; `web/app/[project]/dashboard/user-management/users/dialog/edit-user-security.tsx`                                                                                                                                                                                                                                            |
| Sitzungswiderruf und Prüfung an weiteren API-Aufrufen                    | `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:68–105,443–466`; `api/Framework/Infrastructure/Auth/CurrentUserMiddleware.cs:20–40`; `api/Framework/Infrastructure/Identity/Users/Boundary/ProfileSessionsController.cs:77–160`                                                                                                                                                         |
| Audit-Lese-/Exportrechte                                                 | `web/app/[project]/dashboard/admin/server/audit-events/audit-events-client.tsx:73–86`; `api/Framework/Infrastructure/Identity/Audit/Boundary/AuditTrailController.cs`                                                                                                                                                                                                                                          |
| Health-Umfang und HTTP-Status                                            | `api/Framework/Infrastructure/InfrastructureExtensions.cs:373–382,464–486`; ausführliche Zustandsprüfung mit Settings.View: `api/Service/Admin/Settings/Boundary/HttpControllers/InfoController.cs:58–76`; `web/app/api/healthz/route.ts:1–13`                                                                                                                                                                 |
| Zertifikatsstatus und Metadaten                                          | `web/components/server/certificates-card.tsx:84–114,146–194`; `web/app/[project]/dashboard/admin/server/certificates/certificate-settings.presentation.ts:3–64`; `api/Framework/Infrastructure/Certificates/Boundary/CertificatesController.cs:22–114`                                                                                                                                                         |
| Speicherung/Rotation ist von Verwendung getrennt                         | `api/Framework/Infrastructure/Certificates/Application/CertificateService.cs:37–120`; MQTT-Verwendung: `api/Framework/Infrastructure/Network/Broker/MqttServerHostedService.cs:705–712`; externes Vertrauen: `api/Framework/Infrastructure/Certificates/Application/ExternalServerCertificateTrustService.cs:45–84`; eigenes HTTPS-Zertifikat: `api/Server/Hosting/PersistentHttpsCertificateProvider.cs:8–53` |
| Backup nur Platzhalter                                                   | `web/app/[project]/dashboard/admin/server/database-backup/page.tsx:24–36`                                                                                                                                                                                                                                                                                                                                      |
| Kanonische vorhandene Anleitungen                                        | `docs/administration/benutzer-rollen.mdx`, `wartungs-cli.mdx`, `tags-verwalten.mdx`, `benachrichtigungen-verwalten.mdx`, `mcp-verwalten.mdx`; `docs/ueberblick/profil-sicherheit.mdx`, `profil-sitzungen.mdx`; `docs/benutzer/uebersicht-monitoring.mdx`                                                                                                                                                       |

## Produktbefunde und weiterer Seitenbedarf

1. **Belegte Diskrepanz:** Die UI-Hilfe für „Passkeys für Admins erzwingen“
   (`web/locales/de/settings.json:1062–1065`) behauptet ausschließlich Passkey-Anmeldung.
   `RequirePasskeysForAdmins` wird laut repositoryweiter Referenzsuche dagegen nur
   beim Deaktivieren von Passkeys geprüft (`PasskeyService.cs:334–347`).
   `TokenService.AuthenticateAsync` prüft diese Option nicht. Die Anleitung verspricht
   deshalb keine Passkey-exklusive Anmeldung. Produktkorrektur getrennt entscheiden.
2. **Relevanter Querverweis an Profil-Agenten:** `UserService.TwoFactor.cs:64–85`
   aktiviert 2FA und ruft danach `DisableAllCredentials` auf. Die Einrichtung von
   2FA kann damit vorhandene Passkeys deaktivieren beziehungsweise mit dem Schutz
   des letzten Administrator-Passkeys kollidieren. Nicht durch eine andere Anleitung
   als unabhängige, folgenlose Einrichtung darstellen; praktische Prüfung offen.
3. Globale Kontoschutzregeln haben eine belegte eigene Einstellungsseite. Für den
   aktuellen Umfang reicht der Ablauf hier; eine zusätzliche Produktseite ist nicht
   nötig. Die vollständige Feldreferenz gehört zu Servereinstellungen. Runtime-
   Verhalten von Kennwort-/Lockout-Regeln vor einer umfassenden Hot-Reload-Aussage
   prüfen: `IdentityExtensions.cs:17–28` übernimmt IdentityOptions bei Konfiguration;
   `UserService.cs:89–116` prüft neue Passwörter zusätzlich gegen aktuelle AuthPolicy.
4. **Belegter eigener Anleitungsbedarf Zertifikate:** Import (PFX/PEM, optionaler
   Schlüssel), Rotation unter gleicher ID, Löschung und Verwendung als CA für
   LDAP/OIDC beziehungsweise MQTT sind vorhandene verschiedene Aufgaben. Eine
   separate Anleitung ist sinnvoll, sobald die Auswirkungen beim jeweiligen
   Verbraucher geprüft sind. Quellen: Zertifikatscontroller/-service/-seite oben,
   `ExternalServerCertificateTrustService`, `LdapIntegrationController.cs:170,209`,
   `OidcRuntimeSchemeManager.cs:191,225`, `MqttServerHostedService.cs:705–712`.
   Kein Link auf eine noch nicht vorhandene Seite angelegt.
5. Für vollständige Sicherung/Restore/Update fehlt hier eine abgenommene
   installationsbezogene Anleitung. Technische Teilquellen existieren etwa unter
   `docs/automations/deployment-operations.md:293` und
   `docs/production-runtime-env-contract.md`; sie belegen keinen vollständigen
   Restore der gesamten Mardu-Installation. Nicht allein durch Textfreigabe schließen.

## Checks und Prüfgrenzen

MDX-Parserprüfung mit vorhandenem `@mdx-js/mdx`: erfolgreich. Sämtliche 16 relativen
Seitenlinks einschließlich Zielankern mit vorhandenem `github-slugger` gegen die
Dateien geprüft: erfolgreich. Keine TODOs oder offenen Aufgaben im Produkttext.
Die fünf früheren Abschnittsüberschriften sind per Vergleich mit `git show HEAD`
erhalten. `bun fmt --check` für beide zugewiesenen Dateien und `git diff --check`:
erfolgreich.
Keine Software-,
API- oder DTO-Verträge geändert; bestehende OpenAPI-Verträge als Quelle verwendet.
Kein globaler Build und keine Softwaretests erforderlich oder ausgeführt.

Nicht praktisch geprüft: angemeldeter Settings-/Kontenschutzablauf,
Neuanmeldung und Refresh nach Richtlinienänderung, OIDC-MFA beim realen Anbieter,
Zertifikatsimport/-wechsel bei laufenden Verbrauchern, tatsächlicher Health-Aufruf,
CLI-Hostzugriff, E-Mail-Versand sowie vollständige Sicherung/Restore/Update.
Consumer-Rendering, mobile Ansicht und gemeinsame Navigation übernimmt der Koordinator.

## Publikationsvorschlag

Als begrenzte Anleitung nach Consumerprüfung veröffentlichbar; die Seite enthält
keine Schreibaufträge mehr und behauptet keine vollständige Betriebsanleitung.
Die Passkey-Diskrepanz muss beim Review sichtbar bleiben. Sichtbarkeit in
`administration/meta.json` und Consumerlisten entscheidet der Koordinator;
Navigation wurde hier nicht geändert. Bestehende URL und fünf Abschnittsanker bleiben erhalten.

## Geänderte Dateien

- `web/content/docs/docs/administration/sicherheit-betrieb.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--sicherheit-betrieb.md`
