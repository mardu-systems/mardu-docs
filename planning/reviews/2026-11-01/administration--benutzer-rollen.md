# P18 – Benutzer und Rollen

- Seite: `docs/administration/benutzer-rollen.mdx`; Heimat Administration.
- Leserfrage: Wie lege ich ein Konto an, verwalte seine Zuordnungen und helfe bei kontobezogenen Sicherheitsproblemen? Voraussetzung: angemeldete Verwaltungsperson mit aufgabenbezogenen Rechten.
- Entscheidung: **verbessert**; statisch geprüft, gemeinsame Darstellung-/Ablaufprüfung offen.
- Änderungsbrief und Plan: Vorhandene Anleitung und Bilder erhalten; Rechte und Folgen gegen UI/Backend abgleichen; kleine Ergänzung mit bestehenden MDX-Mitteln; Format, MDX, Links und Anker lokal prüfen. Keine Software-, Navigations- oder API-Änderung.

## Befund und Umsetzung

- Einladung, Passwortanlage, Freigabe, Status, Rollen-/Gruppenzuweisung und die zweistufige Speicherung waren bereits gut beschrieben und bleiben erhalten.
- Gruppendaten verlangen inzwischen **Anlegen und Bearbeiten**; zusätzlich die beim Öffnen benötigten Rollen-Leserechte genannt.
- Sicherheitsaktionen ergänzt: Reset-Link an bestätigte gespeicherte E-Mail, Folgen des tatsächlichen Passwortresets, 2FA-Vorgabe gegenüber eingerichteter 2FA, sofortige 2FA-/Passkey-Deaktivierung und Administratorpflichten. Persönliche 2FA-Einrichtung über vorhandene Anleitung verlinkt.
- Fehlende eigene Statusänderung sowie Löschhindernisse und erhaltene Historie ergänzt. Fehlerhilfe und tatsächlichen statischen Prüfstand präzisiert.
- Bestehende Steps, Tabs, Bilder, URL und alle bisherigen Anker erhalten. Keine neuen Komponenten, Assets oder API-/DTO-Verträge.

## Quellen

Pfade beziehen sich auf das Software-Repository; Zeilen nennen die geprüften Stellen.

| Aussage                                                      | Code-/UI-Quelle                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Anlagefelder, Einladung voreingestellt                       | `web/app/[project]/dashboard/user-management/users/dialog/add-user-dialog.tsx:41–143`; `api/framework/Core/Identity/Request/CreateUserRequest.cs:125–185`                                                                                                                                                                                    |
| Aktivstatus, Basic, Einladung und Freigabe                   | `api/framework/Infrastructure/Identity/Users/Services/UserService.CreateUpdate.cs:244–318`; `UserService.Invite.cs:14–48` im selben Ordner; `api/framework/Infrastructure/Identity/SelfRegistration/Services/SelfRegistrationService.cs:432–531`; `web/app/[project]/dashboard/user-management/users/pending-registrations-card.tsx:150–179` |
| Eigenschaften, gemeinsame Speicherung und sofortige Aktionen | `web/app/[project]/dashboard/user-management/users/dialog/edit-user-sheet.tsx:463–545,578–625`; `edit-user-security.tsx:84–140,150–298` im selben Ordner                                                                                                                                                                                     |
| Rollen, Gruppen und effektive Rechte                         | `web/app/[project]/dashboard/user-management/users/dialog/user-authorization-tab.tsx:121–198`; `api/framework/Infrastructure/Identity/Users/Boundary/UserController.cs:66–120`; `api/framework/Infrastructure/Identity/Users/Services/UserService.Roles.cs:38–88`                                                                            |
| Gruppenrechte und Speichern                                  | `api/framework/Infrastructure/Identity/Groups/Boundary/UserGroupsController.cs:47–63,78–120`; `web/app/[project]/dashboard/user-management/settings/user-group-details-sheet.tsx:209–233,374–395`                                                                                                                                            |
| Reset-Mail und Sitzungsfolgen                                | `api/framework/Infrastructure/Identity/Users/Services/UserService.Password.cs:20–76,147–166`                                                                                                                                                                                                                                                 |
| 2FA-Einrichtung und Administratorpflicht                     | `api/framework/Infrastructure/Identity/Users/Services/UserService.TwoFactor.cs:90–105`; `api/framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:154–160`                                                                                                                                                                      |
| Passkey-Sperre und letzter Administrator-Passkey             | `api/framework/Infrastructure/Identity/Passkeys/PasskeyService.cs:93–98,259–267,334–346`                                                                                                                                                                                                                                                     |
| UI-Bezeichnungen und Zählerhinweis                           | `web/locales/de/users.json:248–268`; `web/locales/de/settings.json:1277`; `web/locales/de/common.json:9,17,573–574`                                                                                                                                                                                                                          |
| Status- und Löschschutz                                      | `api/framework/Infrastructure/Identity/Users/Hypermedia/UserHypermediaEnricher.cs:28–54`; `api/framework/Infrastructure/Identity/Users/Services/UserService.cs:324–348`; `UserService.Delete.cs:16–29` im selben Ordner                                                                                                                      |
| Offene Vorgänge und erhaltene Historie                       | `api/framework/Infrastructure/Identity/Users/UserDeletionImpactProvider.cs:34–84`; `api/Service/Bookings/Application/Services/BookingDeletionImpactContributor.cs:19–33`; `api/Service/Accesses/Infrastructure/DeletionImpact/AccessDeletionImpactContributor.cs:45–87`                                                                      |

## Checks und Grenzen

- Beide eigenen Dateien mit vorhandenem `bun fmt` über stdin formatiert, da `content/docs` im Consumer absichtlich ignoriert wird; anschließend Formatvergleich ausgeführt.
- Produktseite mit vorhandenem `@mdx-js/mdx` kompiliert: Syntax gültig.
- Lokale Verweise einschließlich Bilder und Zielfragmente geprüft: **22** auflösbar; **25** bisherige Anker erhalten.
- `git -C web/content/docs diff --check -- docs/administration/benutzer-rollen.mdx planning/reviews/2026-11-01/administration--benutzer-rollen.md`: ohne Befund.
- Keine Browser-, E-Mail-, Hardware-/Providerprüfung, globalen Builds oder Verwaltungsaktionen ausgeführt. Alte Bilder nicht als neue praktische Abnahme gewertet. Consumer-Rendering und angemeldete Prüfung insbesondere von 2FA-/Passkey-Konflikten und Löschvorschau bleiben für die gemeinsame Abnahme offen; kein neuer Screenshot zwingend nötig.

## Für die Koordination

- Separate Anleitung für **Rollen erstellen und Rechte bearbeiten** sinnvoll: `web/components/roles/role-list.tsx:24–50`, `role-detail.tsx:258–271,325–432` im selben Ordner. Nicht mit der bereits beschriebenen Zuweisung verwechseln.
- Gruppenanlage und -löschung benötigen ergänzende Anleitung; vorhandene Form-/Löschaktionen: `web/app/[project]/dashboard/user-management/settings/user-group-form-dialog.tsx:60–70`, `user-group-row-actions.tsx:65–79` im selben Ordner. Hier keine neue Seite oder Navigation angelegt.
- Passwortloser Zugang und Zusammenführen von Konten bleiben außerhalb des dokumentierten Umfangs. Die kontobezogenen Sicherheitsaktionen können aus `sicherheit-betrieb.mdx` auf `benutzer-rollen.mdx#bei-anmeldeproblemen-helfen` verlinkt werden.
- Geänderte Dateien: ausschließlich `docs/administration/benutzer-rollen.mdx` und dieser Bericht im Doku-Submodul. Keine Commits.
