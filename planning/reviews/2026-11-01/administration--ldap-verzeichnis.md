# N08 — LDAP-Verzeichnis anbinden

## Änderungsbrief und Entscheidung

- Leserfrage: Wie richtet eine Person mit Kenntnis ihres Verzeichnisses die aktuelle LDAP-Anbindung ein, prüft Benutzer-/Rollenzuordnung und versteht die Folgen für Abgleich und Anmeldung?
- Eigenständiger Bedarf: `administration/integrationen.mdx#ldap` ist eine gute Übersicht, enthält aber weder die konkreten Zuordnungsregeln noch den vollständigen Einrichtungsablauf. Neue kanonische Aufgabenanleitung im Bereich Administration.
- Gewünschtes Ergebnis: Konfiguration bewusst speichern, manuell abgleichen und Ergebnis kontrollieren; externe Identität und lokales Konto unterscheiden.
- Vorgehen: vorhandene Formulare/Übersetzungen und Backend lesen, Ablauf verdichten, MDX mit vorhandenen Markdown-Mitteln schreiben, Format und Links dateibezogen prüfen. Keine Software-, Navigations- oder API-Änderung.
- Entscheidung: **belegbare Teildokumentation / offene Prüfung**, Status **zur Prüfung**. Keine praktische Abnahme aus Codelektüre.

## Quellen

Pfade relativ zum Software-Repository:

- `web/components/layout/settings/server-nav.config.ts`: LDAP-Menü mit `Integrations.View`, Route `/dashboard/admin/server/ldap`.
- `web/app/[project]/dashboard/admin/integrations/ldap/page.tsx`: alte Integrationsadresse leitet auf Systemeinstellungen weiter.
- `web/app/[project]/dashboard/admin/server/ldap/page.tsx`: Verbindung, Auswahl Verzeichnistyp/Transport/Zertifikatsprüfung, Secretaktion, Suchbereiche/Filter, „Zuordnung anpassen“, Synchronisierung, Bestätigungen und Verlauf.
- `web/locales/de/settings.json`, `settings.ldap`: genaue Feld-/Aktionsbezeichnungen und Meldungen.
- `web/app/[project]/dashboard/admin/server/ldap/ldap-settings.utils.ts`: Vorlagen, Mappingfelder und Payload; `ldap-settings.presentation.ts`: Fingerprints und Risikobestätigungen.
- `web/app/[project]/dashboard/admin/server/ldap/ldap-role-rules.tsx` und `.utils.ts`: Gruppensuche, vorhandene lokale Rolle, Behalten/Entziehen; Entzugsverwaltung gilt pro Rolle und Entfernen der letzten Regel entfernt deren Verwaltung.
- `web/app/[project]/dashboard/admin/server/ldap/use-ldap-settings-controller.ts`: Validierung vor Test/Vorschau/Speichern; gespeicherter Stand und aktuelle Vorschau als Bedingung für manuellen UI-Sync; Verlauf letzte fünf Läufe.
- `api/framework/Infrastructure/Auth/Boundary/LdapIntegrationController.cs`: Settings-API-Rechte, SecretWriteOnly und ENV-Sperren. Lesen, Verlauf und Gruppensuche: `Settings.View`; Speichern, Validieren, Verbindungstest, Vorschau und Sync: `Settings.Update`.
- `api/framework/Infrastructure/Identity/Roles/Boundary/RolesController.cs:26–27` und `api/framework/Infrastructure/Certificates/Boundary/CertificatesController.cs:22–24`: Rollenliste benötigt `Roles.View`, CA-Liste `Settings.View`.
- `api/framework/Core/Auth/LdapSettings.cs`: Suchbereich-Fallbacks, TLS-Pflicht bei Bind-DN, tatsächliche Validierungen und Auswahlwerte. `api/framework/Infrastructure/Auth/Boundary/Dto/LdapIntegrationDtos.cs`: Secretänderungsflag und Bestätigung dauerhafter Löschung.
- `api/framework/Infrastructure/Auth/Application/LdapIntegrationService.cs`: `UpdateAsync` registriert/entfernt regelmäßigen Job und aktualisiert Laufzeitsnapshot; `BuildUpdatedSettings` erhält Secret ohne Änderungsflag, setzt bei Flag auch leeren Wert; `PreviewSyncAsync` ist Schätzung; `RunSyncAsync` stellt Hintergrundauftrag ein.
- `api/framework/Infrastructure/Identity/External/LdapStartupConnectivityCheckHostedService.cs`: optionaler initialer Sync nach Startprüfung.
- `api/framework/Infrastructure/Identity/External/LdapSyncService.cs`: Vollabgleich mit Benutzerfilter (`{0}` → `*`), Benutzeranlage/-änderung, Rollen und Deprovisioning nur für LDAP-Konten; Admin-Ausnahme; Deaktivierung/Löschung mit Tokenwiderruf.
- `api/framework/Infrastructure/Identity/External/LdapSyncJob.cs`: Verlauf, Status und separate Zahl fehlgeschlagener Benutzer.
- `api/framework/Infrastructure/Identity/External/LdapAuthenticationService.cs`: Verzeichnissuche und Bind mit Benutzerpasswort vor externer Principal-Erstellung.
- `api/framework/Infrastructure/Identity/Users/Services/UserService.CreateUpdate.cs`: `CreateOrUpdateUserFromExternalPrincipal`, `AttemptLinkingAsync`, `ReconcileExternalRolesAsync`, `CreateExternalUserAsync`, `UpdateExternalUserAsync`: lokales Konto ohne Passwortanlage, bestehende externe Loginzuordnung zuerst; E-Mail-Linking prüft bestätigte E-Mail des lokalen Zielkontos; „Kein Linking“, „Nur manuell“ und „Nur Subject“ bieten keinen weiteren automatischen Match.
- `api/framework/Infrastructure/Identity/Tokens/Services/TokenService.cs`, `AuthenticateAsync`/`TryAuthenticateWithLdapAsync`: zuerst lokales Passwort, dann LDAP; anschließend Kontorichtlinie und lokaler zweiter Faktor. Keine Behauptung, dass LDAP lokale Anmeldung generell ausschließt oder MFA ersetzt.

## Fachliche Grenzen und Befunde für den Koordinator

1. `server-einstellungen.mdx` nennt bei LDAP `Integrations.Update`. Tatsächlich benutzt LDAP die Settings-Rechte für API-Aktionen. Übersicht/Querverweis entsprechend angleichen.
2. `integrationen.mdx#ldap` behauptet einen **erfolgreichen** aktuellen Verbindungstest als technische Speicherbedingung. In `use-ldap-settings-controller.ts:220–228` prüft `connectionTestCurrent` nur die Übereinstimmung des Fingerprints; `handleSave` prüft keinen erfolgreichen Ergebniswert. Ein abgeschlossener fehlgeschlagener Test erfüllt diese UI-Bedingung ebenfalls. Die neue Anleitung fordert Ergebnisprüfung und Fehlerbehebung, behauptet keine technische Erfolgssperre. Kein Softwarefix im Auftrag.
3. Vorschau ist keine Zusage für den späteren Vollabgleich: `SearchPreviewUsersAsync` verwendet eine einzelne Suche und direkte Gruppen; der Vollabgleich nutzt paginierte Suche, rekursive Gruppen und zusätzliche Subjects. E-Mail-Verknüpfung und Admin-Ausnahme werden in den Vorschauzahlen nicht vollständig nachgebildet. Produkttext bezeichnet Zahlen als voraussichtliche Änderungen und verlangt Kontrolle des Laufs.
4. `LdapSyncJob` kann `Succeeded` mit `FailedUsers > 0` speichern. Deshalb Status **und** Fehleranzahl kontrollieren; Erfolg nicht nur aus Statusfarbe ableiten.
5. Secretentfernung ist beim Speichern belegt. Kandidatenprüfung (`BuildRequestCandidateAsync`) ersetzt einen leeren Entwurf jedoch wieder durch das dynamisch gespeicherte Secret. Test mit geleertem Secret ist daher keine zuverlässige Bestätigung des Zustands nach Speichern. Die Anleitung enthält keine Aufforderung, durch Leer-Test eine Secretentfernung zu validieren. Zusätzlich ENV-only-Secret-Wiederverwendung in Tests praktisch prüfen; Kandidat-Fallback liest dynamisch gespeicherte, nicht sämtliche effektiven Werte.
6. Namen „Kein Linking“/„Nur manuell“ bedeuten im vorhandenen Code keine Sperre automatischer Neuanlage. Bereits vorhandener externer Login wird immer zuerst gesucht; sonst kann ein neues lokales Konto entstehen. Es gibt auf dieser Seite keine manuelle Kontenzuordnung. In der Anleitung erklärt, kein erfundener manueller Ablauf.

## Checks und offene Praxisprüfung

- `bun fmt --check` für beide eigenen Dateien erfolgreich; wegen der Consumer-Ignore-Regeln zusätzlich explizite Prüfung mit vorhandenem Prettier 3.9.10 und `--ignore-path /dev/null` durchgeführt. MDX-Tabellen anschließend damit formatiert und beide Dateien erneut geprüft.
- Frontmatter (`title`, `description`), Verzicht auf zusätzliches H1 und Existenz aller relativen Seitenlinks mit lokalem Python-Check geprüft.
- `git -C web/content/docs diff --check -- <beide eigene Pfade>` ohne Meldung; neue Dateien zusätzlich unmittelbar gelesen und formatiert.
- Kein Build, Serverstart, Testlauf gegen ein Verzeichnis oder externe Mutation.

Offen: Consumer-Render in Software und Website, Navigation durch Koordinator; Browserprüfung von Formularzuständen, ENV-Sperren, Secretänderung und Risikodialogen; reale Server-/TLS-/Schema-/Gruppenprüfung, Anmeldung inklusive Kontorichtlinie/MFA und Abgleich mit repräsentativen Testkonten. Keine Norm- oder Anbieterkompatibilitätszusage aus Vorlagennamen.

## Querverweise und Dateien

- Koordinator: neue Seite in Administration veröffentlichen und aus `integrationen.mdx#ldap` sowie `server-einstellungen.mdx` verlinken. Bestehenden LDAP-Anker der Übersicht erhalten.
- Die Seite verlinkt die vorhandene Benutzer-/Rollenanleitung für lokale Rechte. Keine Links auf noch fehlende Zusatzseiten.
- Geändert: `web/content/docs/docs/administration/ldap-verzeichnis.mdx`, dieser Bericht.
- API-/DTO-Dokumentation unverändert, da kein Vertrag geändert wurde.
