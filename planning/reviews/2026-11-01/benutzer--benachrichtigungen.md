# P08: Benachrichtigungen lesen

## Änderungsbrief

Leserfrage: Wie finde und lese ich eigene Mitteilungen, ändere ihren Lesestatus
und räume den Posteingang auf? Angemeldete Personen kennen das Dashboard, aber
nicht zwingend die Bedeutung von Archiv, Sammelaktionen oder Versandkanälen.
Kanonische Anleitung bleibt `docs/benutzer/benachrichtigungen.mdx`; Profil- und
Administrationseinstellungen werden dort nicht dupliziert. Ziel ist eine
präzisere Aufgabenanleitung auf Grundlage vorhandener UI, Übersetzungen,
Inbox-Verträge und Zustellungslogik. Gute Abschnitte, URL, Anker und Bild bleiben
erhalten. Geplant sind kleine Textkorrekturen zu Lesen, Sammelaktionen,
Ladebutton und Zustellungsbegriffen. Eigene Prüfungen: Quellenabgleich,
Formatierung, Links/Bilddatei, Ankererhalt und fokussierte vorhandene UI-Tests.
Browserdarstellung in beiden Consumern sowie tatsächliche Zustellung werden mit
dieser statischen Revision nicht abgenommen; kein Versandauftrag.

## Ergebnis: verbessert, praktische Prüfung offen

Die vorhandene Aufgabenfolge ist gut und bleibt erhalten. Keine neue Seite oder
Umstrukturierung nötig. Verdichtet wurden die bisherigen allgemeinen Aussagen
über Aktionen zu konkreten Schaltern und ihren Folgen; danach wurden belegte
Abgrenzungen ergänzt:

- Glockenzähler zählt nur ungelesene, nicht archivierte Mitteilungen.
- Exakter Ladebutton heißt **Weitere Mitteilungen laden**.
- Öffnen von Details markiert nicht als gelesen; **Bereich öffnen** führt zum
  zugehörigen Bereich, nicht zwingend zu einem einzelnen Vorgang.
- Lesen/Ungelesen, Archivieren und Wiederherstellen sind mit UI-Namen beschrieben.
  Wiederherstellen erhält den Lesestatus. **Rückgängig** gehört zur Erfolgsmeldung
  einer einzelnen Archivierung.
- Sammelaktionen können auch durch Suche/Filter ausgeblendete und noch nicht
  geladene Einträge betreffen; im Archiv sind sie deaktiviert. Fachliche Grenze:
  **Alle als gelesen markieren** verwendet den Erstellungszeitpunkt der neuesten
  geladenen Mitteilung als Stichtag, **Gelesene archivieren** die aktuelle Zeit.
  Keine Aussage ergänzt, dass parallel neu eingehende Mitteilungen zwingend
  mitbearbeitet würden.
- Posteingang und Lesestatus beziehen sich auf In-App, nicht auf bestätigten
  E-Mail-/SMS-/Web-Push-Empfang. In-App-Auswahl beeinflusst die Sichtbarkeit neu
  verarbeiteter Meldungen; Ruhezeiten verzögern den In-App-Inhalt nicht.

Unverändert gut: Profilrechte, Tastenkürzel, Such-/Kategorie-/Prioritätsfilter,
Mondsymbol, technische Details in der Verwaltung, Empfängerrechte einschließlich
möglichem Wegfall früherer Meldungen sowie Fehlerhilfe. Fiktives Bestandsbild und
alle vier Abschnittsüberschriften bleiben unverändert. Keine fachlichen Folgen
für die zugehörige Buchung/Freigabe behauptet. API-/DTO-Dokumentation nicht
angepasst, da keine Verträge oder Software geändert wurden.

## Code- und UI-Belege

Pfade relativ zum Software-Repository; Zeilen beziehen sich auf den geprüften Stand.

| Aussage                                                                           | Quelle und relevante Stellen                                                                                                                                                                                                                     |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Profilrechte, Glocke, Tastenkürzel, Ruhezeitenanzeige                             | `web/components/notifications/notification-bell.tsx:27–48, 98–113, 125–176`; `api/Service/Notifications/Boundary/HttpControllers/NotificationsController.cs:25, 56–57, 67, 88, 104, 121, 139`                                                    |
| Exakte deutsche Namen, Ladebutton                                                 | `web/locales/de/settings.json:2718–2781`, insbesondere `loadMore` bei 2757                                                                                                                                                                       |
| Filtern, Details öffnen ohne Lesestatusänderung, Lese-/Archivaktionen, Rückgängig | `web/components/notifications/notification-inbox-sheet.tsx:153–188, 221–300, 331, 472–503, 553–598, 735–755`                                                                                                                                     |
| Technische Details und Bereichsverknüpfung                                        | `web/components/notifications/notification-inbox-sheet.tsx:630–638, 688–729, 886–918`                                                                                                                                                            |
| Sammelaktionen ohne Such-/Kategoriefilter mit Stichtag                            | `web/lib/stores/notification-store.ts:226–258`; `api/Service/Notifications/Gateway/Persistence/Specifications/UserNotificationsCutoffSpec.cs:7–27`; `api/Service/Notifications/Application/Services/UserNotificationService.cs:136–164, 219–257` |
| Archivieren/Wiederherstellen ändert nicht den Lesestatus                          | `api/Service/Notifications/Entity/UserNotification.cs:49–67`; `api/Service/Notifications/Application/Services/UserNotificationService.cs:166–217`                                                                                                |
| Suchfelder, Sichtbarkeit, Zählung                                                 | `api/Service/Notifications/Gateway/Persistence/Specifications/UserNotificationsFilterSpec.cs:68–107`; `UnreadUserNotificationCountSpec.cs:7–12`; `api/Service/Notifications/Application/Services/NotificationAudienceService.cs:91–169`          |
| In-App-Auswahl, getrennte externe Zustellungen und Ruhezeiten                     | `api/Service/Notifications/Application/Services/NotificationProcessor.cs:140–229, 243–257`; `api/Service/Notifications/Application/Policy/NotificationPolicyEngine.cs:45–108, 131–141`                                                           |

## Eigene Prüfungen

- Bestehende UI-Tests ausgeführt: `bun run test:run
tests/components/notification-inbox-sheet.test.tsx
tests/components/notification-bell.test.tsx
tests/components/notification-bell-quiet-hours.test.tsx --coverage.enabled=false`
  aus `web/`: **3 Dateien, 28 Tests bestanden**. Erwartete `offline`-Logs stammen
  aus den absichtlich simulierten Fehlerfällen. Keine Tests geändert.
- Vorhandenes Prettier gezielt auf der MDX-Seite und diesem Bericht geprüft.
- `git -C web/content/docs diff --check` gezielt für beide eigenen Dateien.
- Lokaler Python-Prüfschritt: Frontmatter vorhanden, kein zusätzliches H1,
  alle vier Überschriften gegenüber `HEAD` erhalten, relativer MDX-Link und
  Bestandsbilddatei vorhanden. Rückverweis
  `ueberblick/profil-benachrichtigungen.mdx#welche-meldungen-du-bekommst` bleibt gültig.

Keine eigenen Browser-, Hardware- oder Providerprüfungen, keine echten Nachrichten
versandt. Bestehendes Bild nicht als neue Abnahme gewertet. Koordinator prüft
Darstellung im Software- und Website-Consumer, mobil sowie Link/Bild-Ausgabe.
Bei praktischer Funktionsprüfung besonders Leserechte ohne Änderungsrechte,
Sammelaktionen bei aktiven Filtern und Wiederherstellen einer ungelesenen
Mitteilung prüfen. Versand-/Providerprüfung ist für einen externen Empfangsbeleg
separat erforderlich; sie ist kein Ergebnis dieser Seitenrevision.

## Verweise und geänderte Dateien

URL, Anker und Bildpfad erhalten. Profilverweis benennt den Bereichswechsel zum
Überblick. Keine Navigationsänderung und kein zusätzlicher Seitenbedarf erkennbar.
Nachbarseite `ueberblick/profil-benachrichtigungen.mdx` bleibt die kanonische
Anleitung für Kanäle und Ruhezeiten. Keine anderen Dateien bewusst bearbeitet.

- `docs/benutzer/benachrichtigungen.mdx`
- `planning/reviews/2026-11-01/benutzer--benachrichtigungen.md`
