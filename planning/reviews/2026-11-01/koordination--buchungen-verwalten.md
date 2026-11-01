# P42 – Buchungen verwalten

## Änderungsbrief

Die bisher versteckte TODO-Seite wird zur belegbaren Verwaltungsanleitung für
Personen, die Anfragen entscheiden und Buchungsbedingungen pflegen. Vorausgesetzt
sind Kenntnisse der Ressourcen und der organisatorischen Zuständigkeit; daraus
folgen keine Systemrechte. Ziel sind nachvollziehbare Entscheidungen, Umplanungen,
Stornierungen sowie Gruppenlimits und globale Schließzeiten. Kanonische Heimat
bleibt `docs/koordination/buchungen-verwalten.mdx`; persönliche Abläufe bleiben in
`docs/benutzer/buchungen.mdx`, Ressourcenkonfiguration in `docs/koordination/ressourcen.mdx`.

Quellen sind vorhandene Verwaltungs-UI, deutsche Übersetzungen, Buchungsdienste,
Controller und DTO-Validierung. Die vier vorhandenen Abschnittsanker bleiben
erhalten. Geplant sind nur die zugewiesene Seite und dieser Bericht, danach
Format-, MDX-, Link-/Anker- und Diff-Prüfung. Consumerdarstellung und angemeldete
Praxisprüfung übernimmt der Koordinator; keine Buchungen werden verändert.

## Entscheidung und Umsetzung

**Belegbare Teildokumentation / offene Prüfung.** Die Seite beantwortet, wie eine
zuständige Person Anfragen entscheidet, fremde Buchungen umplant oder storniert
und die Buchungsbedingungen ändert. Die bisherigen TODO-Aufträge sind durch
belegte Abläufe ersetzt; alle vier Hauptüberschriften und damit Altanker bleiben
erhalten. Darüber hinaus enthielt die Seite keine fertige Anleitung oder Bilder.

- Organisatorische Zuständigkeit und Systemrechte sind getrennt. Eigene
  Buchungen und Ressourcenkonfiguration werden über vorhandene Anleitungen
  erschlossen, nicht neu erklärt.
- Gruppenlimits folgen dem strengsten Wert aus Ressource und allen Gruppen;
  leere Felder ergänzen keine Grenze. Entfernen einer Gruppenregel hebt andere
  Regeln nicht auf.
- Schließzeiten verhindern neue Buchungen; bestehende offene/bestätigte
  Buchungen einschließlich Puffer verhindern das Anlegen. Keine automatische
  Stornierung versprochen. Die UI bietet jährliche Wiederholung mit zehn Terminen,
  Einzel-/Serienlöschung und dadurch Ausnahmen durch Entfernen einzelner Termine.
- Entscheidungen gelten gemeinsam für die Ressourcen einer kombinierten Buchung,
  nicht für alle Termine einer Serie. Änderungen prüfen die Regeln erneut und
  können eine neue Genehmigung erfordern. Fremde Serien lassen sich in den
  Verwaltungsdetails nicht vollständig stornieren.
- Kalender und Liste sind Planungsansichten, keine Auslastungsstatistik. Sichtbare
  Buchungen und personenbezogene Angaben sind nicht auf die organisatorische
  Zuständigkeit eingeschränkt. Ressourcenfilter benötigen eigene Leserechte.

## Quellen

Alle Pfade beziehen sich auf den Software-Repository-Root.

| Beleg                                                          | Quelle und relevante Stellen                                                                                                                                                                                                           |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Menüs, Weiterleitungen und aktueller Eigentümer                | `web/components/layout/sidebar/dashboard-navigation.ts:160–199`; `web/app/[project]/dashboard/admin/bookings/resources/page.tsx:3–9`; `web/app/[project]/dashboard/admin/bookings/policies/page.tsx:3–9`                               |
| Verwaltungsrechte und unterstützte Aktionen                    | `api/Service/Bookings/Boundary/HttpControllers/AdminBookingsController.cs:28–290`; `BookingPoliciesController.cs:27–121` im selben Verzeichnis; `api/Framework/Infrastructure/Identity/Groups/Boundary/UserGroupsController.cs:24–40`  |
| Eigene/alle Buchungen, Kalender, Filter, zusätzliche UI-Rechte | `web/app/[project]/dashboard/bookings/_components/bookings-workspace.tsx:97–163`, `:223–252`, `:438–460`, `:533–597`, `:789–831`                                                                                                       |
| Anfragenliste und Gruppenentscheidung                          | `web/app/[project]/dashboard/bookings/requests/booking-admin-center.tsx:104–179`, `:232–260`, `:395–440`                                                                                                                               |
| Gruppenlimits in der Gruppe                                    | `web/app/[project]/dashboard/user-management/settings/user-group-details-sheet.tsx:786–801`; `web/components/bookings/admin/booking-group-policy.tsx:19–124`, `:175–222`                                                               |
| Strengste Grenze / keine Neuberechnung bestehender Buchungen   | `api/Service/Bookings/Application/Services/BookingPolicyService.cs:17–45`, `:61–105`; `api/Service/Bookings/Boundary/Dto/BookingPolicyDtos.cs:8–19`, `:70–84`                                                                          |
| Schließzeitformular, jährliche Serie und Zeitzone              | `web/components/bookings/admin/booking-policies-panel.tsx:168–190`, `:292–391`; `web/components/bookings/admin/booking-closures-sheet.tsx:35–110`                                                                                      |
| Schließzeit-Konflikt und Löschumfang                           | `api/Service/Bookings/Application/Services/BookingCalendarClosureService.cs:30–98`; `api/Service/Bookings/Gateway/BookingSpecifications.cs:140–147`; `api/Service/Bookings/Application/Services/BookingAvailabilityService.cs:206–228` |
| Status, Änderung, Gruppen-/Serienumfang und Nebenläufigkeit    | `api/Service/Bookings/Application/Services/BookingManagementService.cs:207–305`, `:435–554`, `:598–657`, `:721–785`; `web/components/bookings/booking-editor-dialog.tsx:292–322`, `:405–458`, `:751–766`                               |
| Stornierung und fehlende Verwaltungs-Serienstornierung         | `web/components/bookings/booking-detail-sheet.tsx:183–196`, `:418–478`; `api/Service/Bookings/Boundary/Dto/BookingDtos.cs:411–436`                                                                                                     |
| Benachrichtigungsabsicht, kein Zustellbeleg                    | `api/Service/Notifications/Boundary/Consumers/BookingNotificationEventConsumer.cs:44–75`                                                                                                                                               |
| Exakte UI-Texte und Feiertagsmarkierungen                      | `web/locales/de/bookings.json`; `web/locales/de/navigation.json:8–14`; `web/components/bookings/booking-calendar-board.tsx:279–301`                                                                                                    |

## Produktgrenzen und Praxisprüfung

1. **Ablehnungsgrund fälschlich als optional beschriftet:**
   `web/components/bookings/admin/booking-decision-dialog.tsx:54–60` verwendet den
   gleichen Übersetzungsschlüssel für beide Entscheidungen. Der Ablehnungsvalidator
   in `api/Service/Bookings/Boundary/Dto/BookingDtos.cs:429–436` verlangt einen Grund;
   Genehmigen erlaubt einen fehlenden Grund (`:419–426`). In der Anleitung steht
   die wirksame Pflicht mit Hinweis auf die Beschriftung. Softwarekorrektur bleibt
   außerhalb dieses Auftrags.
2. **P04-Befund übernommen und am Code abgeglichen:** Der Wiederholungseditor wird
   bei neuen Buchungen auch für mehrere Ressourcen angezeigt
   (`booking-editor-dialog.tsx:742–749`). Die Submit-Zweige für kombinierte Buchungen
   (`:459–480`) senden keine Wiederholung; erst der Einzelressourcen-Zweig
   (`:481–510`) erzeugt eine Serie. Die Anleitung beschränkt Serien auf eine
   Ressource und verspricht keine kombinierte Serie.
3. **Veraltete Controller-Zusammenfassungen:** Unter anderem bezeichnet
   `AdminBookingsController.cs:54` das Anlegen für andere Personen als bestätigt,
   während `BookingService.cs:68–108` den gemeinsamen regelgeprüften Pfad verwendet.
   Der Text folgt der Implementierung und verspricht keine Umgehung der
   Genehmigungspflicht. Keine API-Datei geändert.
4. Der Koordinator sollte mit einer geeigneten Testinstallation mindestens
   View/Update/Create-Rechte getrennt, Ablehnung ohne/mit Grund, kombinierte
   Entscheidung, konkurrierende Änderung, Umplanung mit neuer Genehmigung,
   Verwaltungs-Stornierungsumfang und Schließzeitkonflikte prüfen. Zusätzlich
   Gruppenlimits aus mehreren Gruppen, leere Felder und Zeitzonen über einen
   jährlichen Terminwechsel prüfen. Hier wurden keine Browser-, Hardware- oder
   Providerprüfungen und keine Buchungsmutationen durchgeführt.

## Checks, Publikationsvorschlag und Dateien

Ausgeführt und bestanden:

- Vorhandenes Prettier für die beiden zugewiesenen Dateien mit
  `--ignore-path /dev/null`, da die Consumer-Konfiguration das Submodul ausnimmt.
- Produktseite mit vorhandenem `@mdx-js/mdx` kompiliert; `title` und `description`
  im Frontmatter geprüft. Dies ist eine Syntaxprüfung, keine Consumerabnahme.
- Alle vier ursprünglichen Hauptüberschriften mit `HEAD` verglichen. Alle vier
  relativen Seitenziele und drei verwendeten Zielanker geprüft. Keine Bilder,
  zusätzlichen Komponenten oder ungeprüften neuen Seitenlinks eingeführt.
- `git diff --check` nur für die zugewiesenen Dateien.

**Publikationsvorschlag:** Nach gemeinsamer Consumerdarstellung und angemeldeter
Prüfung als Verwaltungsanleitung unter Koordination aufnehmen. Die Seite bleibt
bis dahin im Zustand **zur Prüfung**. `docs/koordination/meta.json` bietet sie
derzeit nicht an; `web/lib/docs-roles.tsx:114` kennt den Slug bereits. Der
Koordinator muss gegebenenfalls Navigation, Bereichseinstieg und die Verbindung
aus der persönlichen Anleitung ergänzen. Keine Navigation selbst geändert.
Kein zusätzlicher Seitenbedarf festgestellt.

Geändert ausschließlich:

- `web/content/docs/docs/koordination/buchungen-verwalten.mdx`
- `web/content/docs/planning/reviews/2026-11-01/koordination--buchungen-verwalten.md`

Vorhandene Markdown-Tabellen, Überschriften, UI und API-Verträge wiederverwendet.
Keine API-/DTO-Änderung und damit keine Anpassung der Vertragsdokumentation.
Keine Softwaretests oder globalen Builds ausgeführt. Beide Consumerdarstellungen
bleiben offen.
