# P11: E-Mail und Anmeldesicherheit

Seite: `docs/ueberblick/profil-sicherheit.mdx`.
Entscheidung: **verbessert; zur Prüfung**, keine praktische Abnahme.

## Änderungsbrief

Leserfrage: Wie ändere ich meine Anmeldedaten und Faktoren, ohne den Zugang zu
verlieren? Angemeldete Personen kennen ihr Konto, benötigen aber keine Kenntnisse
der Authentifizierungsimplementierung. Ergebnis sind nachvollziehbare Abläufe
einschließlich Voraussetzungen und Folgen. Kanonische Anleitung bleibt diese
Profilseite unter der bisherigen URL im Heimatbereich persönlicher Benutzeraufgaben.
Umfang: nur diese Seite und dieser Bericht; bestehende Anker, Bilder und Verweis
auf Sitzungen bleiben erhalten. Statische UI-, Übersetzungs- und Backendprüfung
vor dem Patch; anschließend Format-, MDX-, Verweis- und Ankerprüfung. Browser,
Mailanbieter, Authenticator und Passkey-Geräte bleiben getrennt praktisch zu prüfen.

## Befunde und Änderungen

- Veralteten Einstieg „Mein Profil“ durch **Kontomenü → Sicherheit** beziehungsweise
  **Kontoeinstellungen → Authentifizierung** ersetzt; Lesen und Ändern der eigenen
  Sicherheitsdaten benötigen unterschiedliche Profilrechte.
- E-Mail-Ablauf war richtig: aktuelles lokales Passwort, Anforderung an die neue
  Adresse, Änderung erst nach Bestätigung. Prüfung der Erfolgsmeldung und der
  Profiladresse ergänzt. Keine tatsächliche Zustellung behauptet oder ausgelöst.
- Passwortformular und standortabhängige Anforderungen erhalten. Fehlende Folge
  ergänzt: Passwortwechsel widerruft sämtliche Refresh-Tokens; bestehende
  Sitzungen können sich nicht mehr erneuern. Kein sofortiger Logout versprochen.
- Beim Aktivieren der Zwei-Faktor-Anmeldung werden alle vorhandenen Passkeys
  deaktiviert. Diese vorhandene Produktfolge steht jetzt vor den Schritten.
  Bisher fehlende Deaktivierung einschließlich ungültigem Authenticator-Schlüssel
  und notwendiger Neueinrichtung ergänzt. Pflicht zur Einrichtung und Sperre der
  Profilaktion bei vorgeschriebener 2FA erhalten.
- Codeverwaltung präzisiert: serverseitig erlaubte Wiederherstellungscodes setzen
  aktive 2FA voraus; sie ersetzen den zweiten Faktor, nicht das Passwort. Exakte
  UI-Aktionen, Sicherungsbestätigung und Einmalverwendung genannt. Nach Anmeldung
  mit einem Code wird im Folgedialog automatisch ein neuer Satz erzeugt; damit
  verlieren auch die übrigen alten Codes ihre Gültigkeit.
- Passkey-Grundablauf und Browservoraussetzungen erhalten. **Ersetzen** ergänzt:
  neuer Passkey zuerst, Deaktivierung des Vorgängers nach erfolgreicher Registrierung.
  Standortfreigabe, mögliche Mengenbegrenzung und Verbot der Deaktivierung des
  letzten vorgeschriebenen Administrator-Passkeys ergänzt.
- Verdichtung: doppelte Aussage zur vorgeschriebenen 2FA-Deaktivierung entfernt;
  Abläufe bleiben sichtbar, ohne zusätzliche Komponenten oder Akkordeons.

## Quellen

Pfade beziehen sich auf das übergeordnete Software-Repository.

| Quelle                                                                                                                                                | Relevante Stellen                                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `web/components/layout/common/account-menu-items.tsx:21`                                                                                              | Kontoeinstellungen und direkter Sicherheitslink; beide Profilkontexte                                                                                         |
| `web/components/layout/settings/profile-nav.config.ts:89` und `web/locales/de/navigation.json:26`                                                     | Profilbereich Authentifizierung, aktuelle Kontomenübezeichnungen                                                                                              |
| `api/framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs:40`                                                                        | Profil-Leserecht; ab Zeile 105 Änderungen mit `Profile.Update`, Recovery-Policy ab Zeile 194                                                                  |
| `web/components/profile/change-email-dialog.tsx:45`                                                                                                   | neue, andere gültige Adresse und aktuelles Passwort; Anfrage ab Zeile 105                                                                                     |
| `api/framework/Infrastructure/Identity/Users/Services/UserService.EmailChange.cs:18`                                                                  | Verwaltungsvoraussetzungen, Passwortprüfung, belegte Adressbelegung; Mailversandauftrag ab Zeile 102; tatsächliche Adressänderung in `ConfirmUserEmailChange` |
| `web/app/[project]/auth/confirm-email-change/page.tsx:151`                                                                                            | Bestätigungsanfrage, Erfolg/Fehler und erneutes Laden des Profils                                                                                             |
| `api/framework/Infrastructure/Identity/Users/Services/UserService.cs:400`                                                                             | vorhandenes lokales Passwort; E-Mail-Verwaltung zusätzlich vom Provider abhängig, `CanChangeEmail` ab Zeile 451                                               |
| `web/app/[project]/dashboard/user-management/profile/authentication/change-password-card.tsx:83`                                                      | Passwortformular, Fehlerbehandlung und Sperre ohne lokales Passwort                                                                                           |
| `api/framework/Infrastructure/Identity/Users/Services/UserService.Password.cs:158`                                                                    | Passwortwechsel; `ApplyPasswordChangeAsync` ab Zeile 207 aktualisiert Security-Stamp und widerruft Tokens                                                     |
| `api/framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:447`                                                                           | ohne einzelnes Refresh-Token werden alle Tokens der Person widerrufen                                                                                         |
| `web/app/[project]/dashboard/user-management/profile/authentication/two-factor-setup.tsx:68`                                                          | Schlüssel erzeugen, prüfen/aktivieren und anschließende verpflichtende Codesicherung                                                                          |
| `web/app/[project]/dashboard/user-management/profile/authentication/disable-two-factor-button.tsx:23`                                                 | deaktivierte Aktion bei `twoFactorEnforced`, Bestätigungsdialog                                                                                               |
| `api/framework/Infrastructure/Identity/Users/Services/UserService.TwoFactor.cs:66`                                                                    | Passkeys werden beim Aktivieren deaktiviert; Deaktivierung ab Zeile 90, Codesatzersatz ab Zeile 107                                                           |
| `api/framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:154`                                                                           | Pflicht zur 2FA-Einrichtung; Recovery-Code als zweiter Faktor ab Zeile 233, einmalige Einlösung ab Zeile 284                                                  |
| `web/components/profile/RecoveryCodesDialog.tsx:49`                                                                                                   | normale Verwaltung und automatische Neuerzeugung; Generieren, Kopieren, Download und Sicherungsbestätigung                                                    |
| `web/app/[project]/auth/two-factor/two-factor-page-client.tsx:97` und `web/app/[project]/dashboard/user-management/profile/recovery-codes/page.tsx:5` | nach Recovery-Anmeldung Weiterleitung zur automatischen Neuerzeugung mit verpflichtender Sicherungsbestätigung                                                |
| `web/components/profile/passkey-card.tsx:105`                                                                                                         | Browserregistrierung; Ersetzen/Deaktivieren ab Zeile 266                                                                                                      |
| `api/framework/Infrastructure/Identity/Passkeys/PasskeyService.cs:124`                                                                                | Registrierung und Kapazitätsprüfung; Ersatz deaktiviert alten Eintrag ab Zeile 224; Policy für letzten Administrator-Passkey ab Zeile 334                     |
| `web/locales/de/auth.json:155` und `web/locales/de/settings.json:1270`                                                                                | exakte deutsche Formularaktionen und Folgenhinweise                                                                                                           |

## Prüfungen und Grenzen

- `bun fmt --check docs/ueberblick/profil-sicherheit.mdx planning/reviews/2026-11-01/ueberblick--profil-sicherheit.md`
  aus `web/content/docs/`: nach Formatierung des Berichts erfolgreich. Der erste
  Aufruf aus `web/` berücksichtigt das Submodul wegen `.prettierignore` nicht;
  deshalb zusätzlich aus dem Submodul und mit explizitem Prettier-Aufruf geprüft.
- Vorhandene Screenshots mit Bildbetrachter geprüft: Passwortformular enthält
  keine Eingabewerte; 2FA-Bild zeigt Zustand vor Schlüsselerzeugung ohne QR-Code
  oder Secret. Bilder unverändert erhalten; keine neue Browseraufnahme.
- Direkte Kompilierung mit vorhandenem `@mdx-js/mdx` über `bun -e`: erfolgreich.
- Lokale Python-Prüfung gegen `git show HEAD`: alle fünf bisherigen
  Abschnittsüberschriften unverändert, alle drei Link-/Bildziele vorhanden und
  erforderliches Frontmatter erhalten. Damit bleibt insbesondere der eingehende
  Anker `#passwort-ändern` erhalten.
- `git -C web/content/docs diff --check -- docs/ueberblick/profil-sicherheit.mdx`:
  erfolgreich.
- Keine Software-, API- oder DTO-Änderung; bestehende API-Dokumentation nur als
  Vertragsquelle gelesen. Keine globale Testsuite oder Builds gestartet.
- Noch erforderlich: Darstellung der geänderten Seite im Software- und Website-
  Consumer einschließlich mobiler Lesbarkeit; reale Testabläufe ausschließlich
  mit autorisierten Testkonten, Mailzustellung, Authenticator und Passkey-Gerät.

## Hinweise an die Koordination

- Bestehender eingehender Link `administration/wartungs-cli.mdx#passwort-ändern`
  bleibt gültig; sein Linktext nennt noch „Mein Profil → Sicherheit“.
- Kein Bedarf an neuer Produktseite oder neuer Navigation. Die benachbarten
  Profilseiten haben teilweise denselben veralteten Einstieg und werden hier
  auftragsgemäß nicht geändert.
- Offene Produktprüfung: Beide 2FA-Einrichtungsoberflächen fordern anschließend
  Codesicherung, auch wenn `AllowRecoveryCodes=false` die Erzeugung untersagt.
  `two-factor-setup.tsx` öffnet `RecoveryCodesDialog` mit `regenerateOnOpen` und
  `requireCompletion`; die separate Setupseite navigiert ebenfalls zur erzwungenen
  Codeverwaltung. Der Konflikt ist statisch belegt; keine entsprechende Policy
  verändert und keine praktische Reproduktion durchgeführt.
- Bei gleichzeitig erzwungenen Administrator-Passkeys und Aktivierung von 2FA
  kann `DisableAllCredentials` durch die Passkey-Policy scheitern, nachdem 2FA
  bereits gesetzt wurde (`UserService.TwoFactor.cs:80–85`,
  `PasskeyService.cs:269–271,334–346`). Produktprüfung separat erforderlich;
  kein behaupteter erfolgreicher Ablauf für diese Kombination.

## Geänderte Dateien

- `docs/ueberblick/profil-sicherheit.mdx`
- `planning/reviews/2026-11-01/ueberblick--profil-sicherheit.md`
