# P06: Kalender exportieren und abonnieren

## Änderungsbrief

Die Seite `docs/benutzer/kalender.mdx` beantwortet für angemeldete Benutzer mit
eigenen Buchungen die Frage, wie sie Termine einmalig übernehmen oder fortlaufend
abonnieren und den Kalenderzugang später beenden. Vorwissen: Buchung und
Kalenderprogramm; kein API- oder Tokenwissen. Heimat bleibt Benutzer.
Bestehende Gliederung, URL, Überschriftenanker und Bild bleiben erhalten.
Geplant sind eng begrenzte Präzisierungen zu Exportumfang, Leserechten, einmaliger
Linkanzeige und Folgen von Ersatz/Widerruf. Quellen sind die vorhandene
Buchungsoberfläche, deutsche Übersetzungen, Controller, Kalenderdienst und
Zugangsprüfung. Lokale Format-/MDX-/Verweisprüfungen erfolgen nach dem Patch;
Browser-, Website-Consumer- und Anbieterprüfungen übernimmt die gemeinsame
Abnahme. Keine Kalenderabos oder externen Einträge werden angelegt.

## Entscheidung und Befunde

**Verbessert; zur Prüfung, keine praktische Abnahme.** Die bisherige Seite ist
eine gute kurze Anleitung und bleibt in ihrem Zuschnitt erhalten. Im gemeinsamen
Backlog gibt es keinen eigenen Kalenderauftrag. Die angrenzenden Seiten
`docs/benutzer/buchungen.mdx` und `docs/benutzer/index.mdx` verlinken die Seite
bereits passend.

- Gute Inhalte erhalten: Unterschied zwischen Dateiimport und Abo, keine
  Rücksynchronisation von Kalenderänderungen, HTTPS/Erreichbarkeit/`localhost`,
  einmalige Linkanzeige, Ersatz und Widerruf mit Bestätigung, verbleibende lokale
  Termine sowie das als fiktives Beispiel gekennzeichnete Bild.
- Verdichtet/präzisiert: Den unbestimmten Rechtevorbehalt durch die benötigten
  Buchungs-Leserechte ersetzen; Voraussetzungen für Abo-Verwaltung und Abrufe
  nennen. Den Fehlerweg über **Erneut versuchen** angeben.
- Export ergänzt: genaue Aktion **Eigene Buchungen exportieren**, nur auf größeren
  Bildschirmen sichtbar; 366-Tage-Zeitraum, unabhängig von Such-/Listenfiltern.
  Detail-Export enthält die komplette gespeicherte Serie beziehungsweise die
  gemeinsam gebuchten Ressourcen. Vorhandene Serieninformation bleibt erhalten.
- Abo ergänzt: vor Schließen kopieren, bestehenden aktiven Zugang ersetzen,
  ein Link pro Konto und Folgen für alle eingerichteten Abos. UTC-Bezug des
  mitwandernden Zeitraums und Ausschluss abgelehnter Buchungen nennen.
- Keine Software-, API-, DTO- oder Navigationsänderung. Die bestehende technische
  API-Dokumentation bleibt unverändert; keine neuen Verträge werden eingeführt.

## Quellen

Alle Pfade beziehen sich auf das Software-Repository, sofern nicht anders angegeben.
Die Prüfung erfolgte statisch am vorhandenen Arbeitsstand.

| Aussage                                                                         | Konkrete Quelle                                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Export- und Abo-Aktionen; Detail-Export auch mobil                              | `web/app/[project]/dashboard/bookings/_components/bookings-workspace.tsx:365–380, 572–605`; `web/components/bookings/booking-detail-sheet.tsx:210–222, 507–514`                                                                                                                                   |
| 366 Tage ab Ansichtsdatum; Filter werden nicht übergeben                        | `web/lib/bookings/booking-presentation.ts:44, 151–156`; Workspace `:161, 365–375`                                                                                                                                                                                                                 |
| Einzel-Export umfasst Serie oder Buchungsgruppe                                 | `api/Service/Bookings/Application/Services/BookingService.cs:335–354`; `api/Service/Bookings/Gateway/BookingSpecifications.cs:218–237, 334–348`                                                                                                                                                   |
| Leserechte für Export und Abo-Verwaltung                                        | `api/Service/Bookings/Boundary/HttpControllers/BookingsController.cs:203–232`; `api/Service/Bookings/Boundary/HttpControllers/BookingCalendarSubscriptionsController.cs:23–48`                                                                                                                    |
| Fester Zeitraum, UTC, Rechteprüfung beim Feedabruf                              | `api/Service/Bookings/Boundary/HttpControllers/BookingCalendarSubscriptionsController.cs:56–73`; `api/Service/Bookings/Boundary/BookingCalendarAuthenticationHandler.cs:21–38`                                                                                                                    |
| Eigene Buchungen, abgelehnte ausgeschlossen                                     | `api/Service/Bookings/Application/Services/BookingService.cs:356–372`; `api/Service/Bookings/Gateway/BookingSpecifications.cs:88–105`                                                                                                                                                             |
| Kontostatus, Passwortwechsel, Security-Stamp-Bindung, ein Link, Ersatz/Widerruf | `api/Service/Bookings/Application/Services/BookingCalendarSubscriptionService.cs:22–76`                                                                                                                                                                                                           |
| Gespeicherte Serientermine, Änderungs-/Stornierungsstand                        | `api/Service/Bookings/Application/Services/BookingCalendarService.cs:213–278`                                                                                                                                                                                                                     |
| Einmalige Anzeige, Backend-Adresse, Status erneut laden, Bestätigungen          | `web/components/bookings/booking-calendar-subscription-dialog.tsx:32–109, 130–232`                                                                                                                                                                                                                |
| Deutsche Bezeichnungen und Hinweise                                             | `web/locales/de/bookings.json:8, 106, 548–564`                                                                                                                                                                                                                                                    |
| Bereits vorhandener technischer Vertrag und Testfälle als ergänzende Lektüre    | `docs/booking-calendar-subscription.md`; `web/docs/calendar-subscription-readiness.md`; `web/tests/components/booking-calendar-subscription-dialog.test.tsx`; `service.Test/Bookings/BookingCalendarSubscriptionServiceTests.cs`; `service.Test/Bookings/BookingCalendarSubscriptionHttpTests.cs` |

Die vorhandenen Testquellen wurden punktuell eingesehen, nicht ausgeführt.
Insbesondere bestätigt die bloße Testlektüre keinen funktionierenden Anbieterabruf.

## Ausgeführte Prüfungen

- `bun fmt --check content/docs/docs/benutzer/kalender.mdx content/docs/planning/reviews/2026-11-01/benutzer--kalender.md`
  im Consumer `web/`: erfolgreich. Zusätzlich vorhandenes Prettier mit
  `--check --ignore-path /dev/null` auf genau diese beiden Dateien angewendet,
  damit die Submodule-Ausnahme in `.prettierignore` den Check nicht auslässt.
- MDX-Kompilierung der Seite mit installiertem `@mdx-js/mdx` über Bun:
  erfolgreich, keine Ausgabedateien erzeugt.
- Lokale Python-Prüfung: alle fünf bestehenden Überschriften unverändert,
  `title`/`description` vorhanden, Bilddatei vorhanden und neuer interner
  Abschnittsverweis passend.
- `git -C web/content/docs diff --check -- docs/benutzer/kalender.mdx`:
  erfolgreich. Keine globalen Builds oder Softwaretests gestartet.

## Offene Praxisprüfung und Koordination

- Software-Consumer rendern: Desktop und mobile Aktionsanzeige, interner
  Abschnittslink, bestehendes Bild und Markdown-/Agentenausgabe. Das Bild wurde
  nicht als neue praktische Abnahme verwendet.
- Mit geeignetem Testkonto Abo erstellen, schließen/erneut öffnen, ersetzen,
  widerrufen sowie Fehler/erneutes Laden prüfen; Rechteentzug und blockiertes
  Konto prüfen. Dazu braucht es eine ausdrücklich vorgesehene Testumgebung.
- In einem freigegebenen Kalenderprogramm Import gegenüber Abo, Serienänderung,
  Stornierung, Aktualisierungsintervall und verbleibende Kopien nach Widerruf
  prüfen. Keine Anbieterkompatibilität wird behauptet. Keine externen
  Kalenderaktionen wurden ausgeführt.
- Website-Consumer wurde nicht ausgeführt. Gemeinsame Navigation und
  Darstellung bleiben beim Koordinator. Kein zusätzlicher Seitenbedarf und
  kein belegter Produktfehler aus dieser Prüfung; URL und alle bisherigen
  Überschriftenanker bleiben erhalten.

## Geänderte Dateien

- `web/content/docs/docs/benutzer/kalender.mdx`
- `web/content/docs/planning/reviews/2026-11-01/benutzer--kalender.md`
