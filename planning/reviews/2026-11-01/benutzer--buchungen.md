# P04 – Meine Buchungen

Seite: `docs/benutzer/buchungen.mdx`. Heimatbereich: Benutzer.

Änderungsbrief: Die Anleitung richtet sich an angemeldete Personen, die ihre eigenen
Reservierungen finden, erstellen, ändern, stornieren und ihre Anwesenheit erfassen
möchten. Vorwissen: Ressource und Zeitraum der gewünschten Nutzung sind bekannt.
Die bestehenden Überschriften, URLs, Bilder und Querverweise bleiben erhalten.
Nach Abgleich von Portalroute, Buchungsformular, Details, Übersetzungen, Rechten,
DTOs und Services werden nur falsche Bedienhinweise und fehlende Auswirkungen
korrigiert. Danach folgen Format-, MDX- und Verweisprüfung; Consumer- und reale
Ablaufprüfung bleiben dem Koordinator vorbehalten.

## Entscheidung und Änderungen

**Verbessert; zur Prüfung, keine praktische Abnahme.** Der vorhandene Zuschnitt
als Benutzeranleitung war passend. Alle sechs Überschriften und damit vorhandene
Anker, drei Bilder sowie Links zu Zutritt und Kalender bleiben erhalten.

- Rechte und Portalgrenze konkretisiert: eigene Buchungen auch mit Verwaltungsrechten;
  Lesen, Erstellen und Ändern getrennt, Anwesenheit und Stornierung benötigen Update.
- Kalender-/Fremdbelegungshinweis aus dem Portalablauf entfernt: Die Portalroute
  verwendet ausschließlich Listenmodus. Verfügbarkeit wird im Formular geprüft.
- Nicht vorhandenes Zeitzonen-Eingabefeld entfernt; Browserzeit von der Zeitzone
  der angezeigten Ressourcen-Wochenzeiten unterschieden. Titelgenerierung,
  Serienauswahl und Begrenzung auf 200 Termine ergänzt.
- Vorabprüfung des ersten Serientermins von Prüfung aller Termine beim Speichern
  unterschieden. Kombinierte Ressourcen werden gemeinsam gebucht und storniert.
- Einzeländerung, Änderung folgender bestätigter Serientermine und erneute
  Genehmigung nach Änderungen ergänzt; Stornierungsumfänge präzisiert.
- Check-in-Pflicht, zulässiges Zeitfenster, bedingte NoShow-Freigabe und Folgen des
  Auscheckens sichtbar beschrieben. Kein Versprechen physischer Gerätebetätigung.
- Nicht belegte Aufforderung „lies die Rückmeldung“ bei Ablehnung entfernt:
  Detailkomponente zeigt den Stornierungsgrund, aber keinen gesonderten
  Entscheidungsgrund. Statusübersicht, Entwurfsschutz und Fehlerhilfe erhalten.

## Quellen

Pfade sind relativ zum Software-Repository; Zeilen beziehen sich auf den geprüften Stand.

| Aussage                                                  | Quellen                                                                                                                                                                                                                                                       |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Portal zeigt eigene Buchungen als Liste                  | `web/app/[project]/portal/bookings/page.tsx:4`; `web/app/[project]/dashboard/bookings/_components/bookings-workspace.tsx:117–150`, `:221–248`, `:803–818`                                                                                                     |
| Rechte für Lesen/Erstellen/Ändern/Stornieren/Anwesenheit | `api/Service/Bookings/Boundary/HttpControllers/BookingsController.cs:27–65`, `:160–203`, `:234–266`; Ressourcen-Voraussetzung zusätzlich Workspace `:145–150` und Formular `:292–307`                                                                         |
| Exakte UI-Texte, Regeln, Status und Rückmeldungen        | `web/locales/de/bookings.json` (`booking.actions`, `editor`, `fields`, `recurrence`, `status`, `feedback`); `web/components/bookings/booking-status-badge.tsx`                                                                                                |
| Zeitraum, lokales Datum/Uhrzeit statt Zeitzonenfeld      | `web/components/bookings/booking-date-time-range-picker.tsx:70–92`, `:145–163`; `web/components/bookings/booking-editor-dialog.tsx:599–648`; Ressourcenzeitzone außerdem `api/Service/Bookings/Application/Services/BookingService.cs:165–179`, `:482`        |
| Serien, Höchstzahl und Vorabprüfung                      | `web/components/bookings/booking-recurrence-editor.tsx:55–170`; `web/lib/bookings/booking-recurrence.ts:33–42`; `api/Service/Bookings/Application/Services/BookingCalendarService.cs:21–67`; Formular `:292–322`; `BookingService.cs:165–209`                 |
| Kombinierte Buchung                                      | `web/components/bookings/booking-editor-dialog.tsx:470–480`; `api/Service/Bookings/Application/Services/BookingManagementService.cs:310–411` (Verfügbarkeit vor gemeinsamem Speichern), `:527–554`; `BookingService.cs:257–270` (Einzelstornierung abgelehnt) |
| Änderungen und Stornierung von Serien                    | Formular `:435–458`, `:751–766`; `BookingManagementService.cs:253–305`, `:763–785`; `BookingService.cs:295–333`                                                                                                                                               |
| Details, Stornierungsgrund, Umfang und Bestätigung       | `web/components/bookings/booking-detail-sheet.tsx:263–306`, `:418–478`; aktive Statuswerte in `web/lib/bookings/booking-presentation.ts:95–98`                                                                                                                |
| Check-in, Frist, Auschecken und NoShow                   | `api/Service/Bookings/Application/Services/BookingAttendanceService.cs:24–109`; `api/Service/Bookings/Gateway/BookingSpecifications.cs:72–84`; Detailaktionen `:484–505`; statusabhängiger Zutrittsnachweis in `BookingSpecifications.cs:45–56`               |
| Validierung                                              | `api/Service/Bookings/Boundary/Dto/BookingDtos.cs:270–281`, `:296–315`, `:342–415` (Ende nach Beginn, positive Menge, Ressourcenlimit, Pflichtgrund für Stornierung)                                                                                          |

## Produktgrenzen und Hinweise an den Koordinator

1. **Wiederholung bei mehreren Ressourcen wird ignoriert:**
   `BookingEditorDialog` zeigt bei jeder neuen Buchung den Wiederholungseditor
   (`:742–749`). Der Submit-Zweig für mehrere Ressourcen (`:470–480`) sendet
   ausschließlich `CreateCombinedBookingRequestDto`; dessen Vertrag
   (`BookingDtos.cs:60–83`) enthält keine Wiederholung. Erst der nachgeordnete
   Einzelressourcen-Zweig (`:497–510`) erstellt eine Serie. Kein Laufzeittest
   durchgeführt. Die Anleitung beschränkt Serien deshalb auf eine Ressource;
   ein Software-Fix ist nicht Teil dieses Seitenauftrags.
2. **API-Zusammenfassungen sind teilweise älter als der Vertrag:**
   `BookingsController.cs:49` nennt „immediately confirmed exclusive booking“,
   während `BookingService.cs:483` abhängig von Regeln auch `PendingApproval`
   erzeugt. Weitere Zusammenfassungen bei Update/CancelGroup nennen nur confirmed,
   während Services auch offene Buchungen behandeln. Keine API-Datei geändert;
   fachliche Beschreibung folgt der Implementierung.
3. **Bildabgleich:** Alle drei vorhandenen PNGs wurden selbst geöffnet. Sie zeigen
   fiktive Daten und passen zu den genannten Aufgaben. Das Formularbild zeigt eine
   ältere Feldreihenfolge und noch keinen Block „Buchbare Zeiten und Regeln“.
   Ersatzbild beim gemeinsamen angemeldeten Browserdurchlauf erwägen; keine neuen
   Screenshots oder praktische Abnahme behauptet.
4. Gemeinsame Browserprüfung: Portal mit View/Create/Update-Varianten, Check-in
   innerhalb/außerhalb Frist, NoShow nur mit aktivierter Freigabe, Check-out mit
   Statuswechsel und Restkapazität, kombinierte Stornierung sowie Serie mit
   Folgeterminänderung und Zeitumstellung prüfen. Kein Hardware-/Providerlauf
   durchgeführt; Tür-/Maschinenwirkung ausdrücklich nicht als geprüft dargestellt.
5. Bestehende Links auf `./zutritt.mdx` und `./kalender.mdx` bleiben erhalten.
   Kein neuer Seitenbedarf und keine Navigation geändert. Die Verwaltungsanleitung
   `docs/koordination/buchungen-verwalten.mdx` ist beim Lesen noch ein Entwurf;
   deshalb kein neuer Verweis dorthin aufgenommen.

## Checks und geänderte Dateien

Ausgeführt und bestanden:

- Vorhandenes Prettier auf genau beiden Dateien mit `--ignore-path /dev/null`
  ausgeführt, da der Consumer das Dokumentationssubmodul sonst ausnimmt.
- Produktseite mit dem vorhandenen `@mdx-js/mdx` kompiliert, Frontmatter vorab
  separat geprüft. Das ist eine Syntaxprüfung, keine Consumer-Darstellungsprüfung.
- Bestehende sechs Überschriften mit `HEAD` verglichen: unverändert. Alle fünf
  relativen Seiten-/Bildziele auf vorhandene Dateien geprüft.
- `git diff --check` für die zugewiesenen Dateien ohne Befund.

Geändert ausschließlich:

- `docs/benutzer/buchungen.mdx`
- `planning/reviews/2026-11-01/benutzer--buchungen.md`

Bestehende Markdown-Struktur und Bilder wiederverwendet; keine API oder DTOs
verändert, daher keine API-Vertragsdokumentation angepasst. Software und zweiter
Doku-Consumer wurden nicht gebaut oder gerendert.
