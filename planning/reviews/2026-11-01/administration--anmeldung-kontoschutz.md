# N12 – Anmeldung und Kontoschutz einstellen

## Änderungsbrief und Entscheidung

Leserfrage: Wie ändere ich die Anmeldevorgaben der Installation und prüfe die
Folgen für vorhandene Konten? Vorausgesetzt sind eine angemeldete Sitzung und
Kenntnis der betroffenen Konten; interne DTOs gehören nicht zum Vorwissen.
Gewünschtes Ergebnis ist eine gespeicherte Vorgabe mit überprüfter neuer
Anmeldung und bekanntem Wiederherstellungsweg. Heimatbereich: Administration.

Plan: Zuerst die verbesserten Bestandsanleitungen und Berichte P11/P18/P27/P28
abgleichen, danach UI und Backend für die vermutete Lücke prüfen. Nur einen
zusätzlichen belegten Nutzerablauf als neue Seite ausarbeiten. Andernfalls die
kanonischen Abschnitte festhalten und ausschließlich diesen Bericht anlegen.

**Begründete Nichtanlage.** Die neue Datei
`docs/administration/anmeldung-kontoschutz.mdx` wird nicht erstellt. Es fehlt kein
eigener, zusätzlich belegter Ablauf für diese Leserfrage. Eine neue Anleitung
würde die vorhandene Auth-Policy-Bedienung, Wirkungsprüfung und Kontohilfe
wiederholen. Die Bestandsseiten bleiben unverändert; ihre noch ausstehende
Praxisprüfung wird durch diese Entscheidung nicht zur Abnahme.

## Kanonische Aufgaben und Zielabschnitte

Die Ziele beziehen sich auf `web/content/docs/` und wurden im vorhandenen Inhalt
geprüft.

| Leseraufgabe                                                | Kanonischer Abschnitt                                                                                                                                    | Bereits vorhandene Abdeckung                                                                                                  |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Installationsweite Anmeldevorgaben ändern                   | `docs/administration/server-einstellungen.mdx#registrierung-und-anmelderichtlinie`                                                                       | Einstieg **Server → Auth Policy**, Registrierung, Kontobestätigung, Standardrolle und Anmeldeschutz.                          |
| Vorgaben speichern und Fehler/Grenzen erkennen              | `docs/administration/server-einstellungen.mdx#einstellungen-lesen-und-speichern` und `#gesperrte-werte-und-neustartbedarf`                               | `Settings.View`/`Settings.Update`, Laden, Validierung, Speichern, Verwerfen, Deployment-Sperren und Wirksamkeit.              |
| Einzelne Anmeldeschutz- und Laufzeitfelder nachschlagen     | `docs/administration/server-einstellungen.mdx#anmeldeschutz-und-laufzeiten-ändern`                                                                       | Erlaubte Verfahren, Admin-Vorgaben, Wiederherstellungscodes, Kontosperre, Passwortanforderungen und Tokenlaufzeiten.          |
| Folgen vor Änderung prüfen und neue Anmeldung kontrollieren | `docs/administration/sicherheit-betrieb.mdx#anmeldeverfahren-und-kontowiederherstellung`                                                                 | Kontoeinrichtung vor Vorgaben, getrennte Neuanmeldung, tatsächliche Passkey-Wirkung, OIDC-MFA und Grenze passwortloser Links. |
| Einer ausgesperrten Person helfen                           | `docs/administration/benutzer-rollen.mdx#bei-anmeldeproblemen-helfen`                                                                                    | Kontostatus/E-Mail, Passwort-Reset, kontobezogene 2FA-Vorgabe, 2FA-Deaktivierung und einzelner Passkey.                       |
| Eigenes Anmeldeverfahren einrichten                         | `docs/ueberblick/profil-sicherheit.mdx#zwei-faktor-anmeldung-einrichten`, `#wiederherstellungscodes-sichern` und `#passkey-hinzufügen-oder-deaktivieren` | Persönliche Einrichtung, Codesicherung, Ersetzen und Deaktivieren mit Folgen und Voraussetzungen.                             |

Querverweisvorschlag für die Koordination: Falls der Zusatzseitenplan oder ein
Bereichseinstieg einen Link „Anmeldung und Kontoschutz einstellen“ vorsieht, als
Ziel **Servereinstellungen → Registrierung und Anmelderichtlinie** verwenden.
Für Wirkungen und Wiederherstellung im selben Kontext auf **Sicherheit und
Betrieb → Anmeldeverfahren und Kontowiederherstellung** verweisen. Keine neue
Navigation und keinen zweiten Inhaltsträger anlegen. Die Bestandsseiten
verlinken die einschlägigen Konto- und Profilabläufe bereits.

## Geprüfte UI- und Backendquellen

Pfade sind relativ zum Software-Repository; Zeilen beziehen sich auf den
statisch geprüften Checkout.

| Beleg                                               | Quelle und relevante Stelle                                                                                                                                                                                                                                                                                                                               |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tatsächlicher Einstieg und Leserecht                | `web/components/layout/settings/server-nav.config.ts:61–73`: Route `/dashboard/admin/server/auth-policy`, `Settings.View`.                                                                                                                                                                                                                                |
| Registrierungsmodi und voneinander abhängige Felder | `web/app/[project]/dashboard/admin/server/auth-policy/page.tsx:23–88`: deaktiviert, direkt, mit Freigabe; bestätigtes Konto bei Freigabe.                                                                                                                                                                                                                 |
| Vorhandene Schalter und Einstellungen               | Dieselbe Datei `:137–179`: Passkeys erlauben, Recovery-Codes, Anzahl, Administrator-Vorgaben. `:486–530`: abhängige Änderungen, gemeinsames Formular und Neustartfelder.                                                                                                                                                                                  |
| Lesen, Schreiben, Hot Reload und Feldsperren        | `api/Service/Admin/Settings/Boundary/HttpControllers/AuthPolicySettingsController.cs:30–74`: `Settings.View`, Runtime-Metadaten, Deployment-Sperren und Neustart für Tokenfelder; `:77–135`: `Settings.Update`, Update-Vertrag und Konfigurationsspeicherung.                                                                                             |
| Passwortanmeldung und verpflichtende 2FA            | `api/framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:151–187`: fehlende vorgeschriebene Einrichtung wird abgewiesen; TOTP-/Recovery-Challenge abhängig von Policy. `:719–752`: MFA-Nachweis je Anmeldeverfahren.                                                                                                                        |
| Schutz des letzten aktiven Administrator-Passkeys   | `api/framework/Infrastructure/Identity/Passkeys/PasskeyService.cs:259–276,334–345`: Prüfung beim Deaktivieren eines oder aller Passkeys.                                                                                                                                                                                                                  |
| Wechselwirkung von 2FA und Passkeys                 | `api/framework/Infrastructure/Identity/Users/Services/UserService.TwoFactor.cs:66–85`: 2FA wird zuerst aktiviert, anschließend werden alle Passkeys deaktiviert.                                                                                                                                                                                          |
| Grenzen der Recovery-Ausgabe                        | Dieselbe Datei `:107–122`: Policy kann Ausgabe untersagen; Ausgabe ruft derzeit eine feste Anzahl von zehn Codes ab.                                                                                                                                                                                                                                      |
| UI verlangt Codesicherung nach 2FA-Einrichtung      | `web/app/[project]/dashboard/user-management/profile/authentication/two-factor-setup.tsx:224–233`: `RecoveryCodesDialog` mit `regenerateOnOpen` und `requireCompletion`; `web/app/[project]/auth/setup-two-factor/page.tsx:133–141` und `web/app/[project]/dashboard/user-management/profile/recovery-codes/page.tsx:7`: entsprechender separater Ablauf. |
| Verhalten bei erforderlicher Codesicherung          | `web/components/profile/RecoveryCodesDialog.tsx:62–87,140–143`: Erzeugungsaufruf, Fehlermeldung, automatischer Start und Abschlussbedingung.                                                                                                                                                                                                              |

## Produktwidersprüche und Prüfgrenzen

Die folgenden Befunde begründen keine neue Anleitung für eine vermeintlich
funktionierende Kombination. Keine Policy wurde verändert.

- **Passkey-Pflicht ist keine belegte ausschließliche Passkey-Anmeldung.** Die
  UI-Hilfe in `web/locales/de/settings.json:1062–1065` behauptet das, während die
  geprüften Login-/Deaktivierungspfade den Schutz des letzten aktiven
  Administrator-Passkeys belegen. `sicherheit-betrieb.mdx` grenzt dies bereits
  ausdrücklich ab. Die pauschale Sammelbezeichnung „Zusätzliche Anmeldevorgaben“
  in der Tabelle der Servereinstellungen darf nicht als Nachweis exklusiver
  Anmeldung gelesen werden. Die präzise Wirkung bleibt im kanonischen
  Sicherheitsabschnitt; eine mögliche Präzisierung der Sammelbezeichnung ist
  eine Aufgabe am Bestand, kein Grund für eine neue Seite.
- **2FA und vorgeschriebene Administrator-Passkeys können kollidieren.** Die
  Aktivierung ruft nach dem Setzen von 2FA `DisableAllCredentials` auf; dessen
  Schutzprüfung kann die Deaktivierung ablehnen. P11/P28 melden diese Reihenfolge
  bereits. Kein erfolgreicher Kombinationsablauf und keine Standardempfehlung
  daraus abgeleitet.
- **Recovery-Policy und Einrichtungs-UI passen nicht in jedem Zustand zusammen.**
  Bei `AllowRecoveryCodes=false` lehnt das Backend die Ausgabe ab, die geprüften
  2FA-Oberflächen verlangen danach trotzdem die Codesicherung. Statisch bestätigt,
  praktisch nicht reproduziert. Zusätzlich entspricht die feste Zehn in
  `GenerateRecoveryCodes` nicht dem veränderbaren Feld `recoveryCodeCount`
  (Frontend: 1–20). Die gespeicherte Anzahl ist deshalb kein belegter Nachweis
  für die tatsächlich ausgegebene Anzahl. Produktprüfung getrennt erforderlich.

Ausgeführte Checks: vier Bestandsseiten vollständig gelesen, passende
Bestandsberichte und offene Aufgaben abgeglichen; Quelltext und deutsche
Feldbezeichnungen der oben genannten Stellen geprüft; Zielüberschriften im
Bestand kontrolliert. Prettier für diesen Bericht ausgeführt und anschließend
mit `--check` bestätigt. `git diff --no-index --check /dev/null` für den neuen
Bericht lieferte keine Whitespace-Meldung (Exit 1 wegen der neuen Datei).
Keine neue MDX-Datei, keine Link-/Navigationsänderung, keine
Software- oder API-/DTO-Änderung; bestehende OpenAPI-Verträge dienen nur als
Quelle. Tests oder Build sind für die reine Nichtanlageentscheidung nicht
ausgeführt worden.

Offen bleiben eine autorisierte Neuanmeldung unter geänderten Vorgaben,
Authenticator-/Passkey-Geräte, E-Mail-Zustellung und OIDC-Anbieterprüfung sowie
die praktische Reproduktion der genannten Konflikte. Keine Browser-, Hardware-,
Provider- oder Consumer-Abnahme durch diesen Auftrag.

Geänderte Datei ausschließlich:
`web/content/docs/planning/reviews/2026-11-01/administration--anmeldung-kontoschutz.md`.
