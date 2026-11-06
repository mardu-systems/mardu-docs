# Gesamtrevision: Benutzer

Stand: 2026-11-03. Paket: die elf Produktseiten aus dem Gesamtplan.

## Auftrag und Maßstab

Leser sind angemeldete Personen, die ihre eigenen Termine, Freigaben und Nachweise
prüfen oder ändern wollen. Vorwissen über interne Module wird nicht vorausgesetzt.
Ziel sind auffindbare Abläufe mit Voraussetzungen, sichtbarem Ergebnis und den
Folgen einer Aktion. Gute Texte bleiben erhalten. Änderungen beschränken sich auf
diese Produktseiten, eigene Bilddateien und diesen Bericht. URLs und vorhandene
Abschnittsüberschriften bleiben erhalten.

Verwendet werden die installierten nativen Fumadocs-Komponenten `ImageZoom`,
`Steps`/`Step`, `Tabs`/`Tab` und `Callout`; keine neue Komponente oder Abhängigkeit.
API- und DTO-Verträge werden nicht verändert. Grundlage sind `AGENTS.md`,
`ARBEITSWEISE.md`, Gesamtplan, Agentenbrief und die überarbeiteten Ressourcen- und
Freigabenanleitungen.

## Seitenprüfung

### benachrichtigungen.mdx

- Entscheidung: Gute Anleitung erhalten, Bilddarstellung und Folgen hervorheben.
- Quellen: `web/components/notifications/notification-bell.tsx`,
  `notification-inbox-sheet.tsx`; `api/Service/Notifications/Boundary/HttpControllers/NotificationsController.cs`;
  `api/Service/Notifications/Application/Services/UserNotificationService.cs`.
- Änderungen: Bestehende aktuelle Aufnahme `posteingang.png` als `ImageZoom`.
  Ein Callout erklärt die Reichweite von Sammelaktionen unabhängig von Suche,
  Filtern und bereits geladenen Einträgen. Keine neuen Zustellversprechen.
- Prüfung: Rechte, Tastenkürzel, Lesestatus, Archivierung, Wiederherstellung und
  Sammelaktionen mit aktuellem Code abgeglichen; Bild visuell geprüft.
- Grenze: E-Mail-, SMS- und Web-Push-Empfang sowie Ruhezeiten bei externen Kanälen
  hier nicht praktisch geprüft.

### berechtigungsanfragen.mdx

- Entscheidung: Inhalt erhalten, veraltete Aufnahme ersetzen.
- Quellen: `web/components/portal/profile-access-requests.tsx`,
  `web/components/access/resource-catalog-workspace.tsx`;
  `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessCatalogController.cs`;
  `api/Service/Accesses/Boundary/Dto/ResourceAccessCatalogDtos.cs`;
  `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs`.
- Änderungen: `berechtigungsanfragen-aktuell.png` als `ImageZoom`; die alte Aufnahme
  zeigte die entfallenen Zusätze `enter` und `operate` am Ressourcennamen.
- Prüfung: Im isolierten Portal als fiktive Miriam Brandt eine Anfrage für
  Holzwerkstatt mit Begründung gesendet. Status **Offen**, eigener Nachrichtentext
  und gesperrte erneute Anfrage im Katalog sichtbar. Danach Rücknahme bestätigt:
  **Zurückgezogen** im Verlauf und **Zugriff anfragen** im Katalog wieder verfügbar.
  Die Aufnahme zeigt den tatsächlich offenen Zustand vor der Rücknahme.
- Grenze: Genehmigen/Ablehnen nicht als Endnutzer ausgeführt; dafür Controller,
  Statusmodell und atomare Vergabeerstellung im Service abgeglichen.

### buchungen.mdx

- Entscheidung: Hauptablauf gliedern, bestehende Regeln und Grenzen erhalten.
- Quellen: `web/app/[project]/portal/bookings/page.tsx`;
  `web/app/[project]/dashboard/bookings/_components/bookings-workspace.tsx`;
  `web/components/bookings/booking-editor-dialog.tsx`, `booking-detail-sheet.tsx`;
  `api/Service/Bookings/Boundary/HttpControllers/BookingsController.cs`;
  `api/Service/Bookings/Application/Services/BookingService.cs`,
  `BookingManagementService.cs`, `BookingAttendanceService.cs`.
- Änderungen: Drei native Phasen für Auswahl/Zeitraum, optionale Wiederholung und
  Prüfen/Buchen. Zeitangaben stehen bei der Eingabe; die Folgen von **Auschecken**
  sind als sichtbarer Callout hervorgehoben. Drei aktuelle, vergrößerbare Aufnahmen
  ersetzen die bisherigen: Das Formular zeigt Ressourcen, Zeitraum und Regeln
  jetzt vor dem Titel; die Liste verwendet einen Ressourcen-Filterschalter.
- Prüfung: Eigene Portalendpunkte auch bei Verwaltungsrechten, Formularfelder,
  Vorabprüfung nur des ersten Serientermins, Status, Serienänderung und -storno,
  kombinierte Buchung sowie Check-in/Check-out gegen UI/Backend abgeglichen.
  Im isolierten Portal **Bauteile für das Holzprojekt** auf **Abrichthobel und
  Dickenhobel** am 03.11.2026, 19–20 Uhr erstellt: Verfügbarkeit positiv, Status
  **Bestätigt**. Beschreibung mit Änderungsgrund gespeichert; neuer Text und
  Änderungsverlauf sichtbar. ICS-Datei über die Detailaktion heruntergeladen.
  Anschließend mit Grund und ausdrücklicher Bestätigung storniert; **Storniert**
  auch in der mobilen Buchungsliste sichtbar. Keine gemeinsamen Seed-Buchungen
  geändert oder gelöscht.
- Grenze: Serien über Zeitumstellung, kombinierte Buchung, automatische
  Nichterscheinensbearbeitung und elektronische Zutrittswirkung nicht praktisch
  abgenommen.

### dashboard.mdx

- Entscheidung: Gute Anleitung erhalten; alte Freigabenaufnahme ersetzen.
- Quellen: `web/components/portal/member-dashboard.tsx`, `use-member-metrics.ts`,
  `member-metric-view.ts`; `api/Service/Observability/Application/MemberPortalDashboard.cs`,
  `PersonalDashboardService.UserMetrics.cs`;
  `api/Service/Observability/Boundary/HttpControllers/ProfileDashboardController.cs`.
- Prüfung: Rechte, eigene Datenquellen, Fünfereinträge, 30-Tage-Ablauffrist,
  getrennte responsive Anordnungen und Konfliktschutz gegen den Code abgeglichen.
  Portal mit fünf fiktiven Gruppenfreigaben geöffnet. Das optionale Widget **Bald
  ablaufende Qualifikationen** über das Menü hinzugefügt, gespeichert und nach
  Neuladen wieder vorgefunden.
- Änderungen: Aktuelle Aufnahme mit eigener Testbuchung, Gruppenfreigaben und
  ausdrücklich leerem Qualifikationsbereich als `ImageZoom` eingebunden. Sie zeigt
  den tatsächlich geprüften Stand vor der späteren Stornierung der Testbuchung.
- Bildbefund: Alte Aufnahme zeigte eine nicht mehr ausgegebene Aktionszeile
  `enter` unter der Freigabe.
- Grenze: Andere Sitzung als Konfliktauslöser und Tastaturgrößenänderung nicht
  praktisch geprüft.

### erste-schritte.mdx

- Entscheidung: Unverändert erhalten; kurze, nutzbare Anleitung.
- Quellen: `web/components/portal/portal-shell.tsx`, `portal-navigation.ts`;
  `web/components/layout/common/account-menu-items.tsx`;
  `web/app/[project]/auth/two-factor/two-factor-page-client.tsx`,
  `web/app/[project]/auth/setup-two-factor/page.tsx`;
  `web/app/[project]/dashboard/user-management/profile/recovery-codes/page.tsx`.
- Prüfung: Navigation, Kontoeinstellungen, Dokumentationslink und Abmelden gegen
  UI/Code abgeglichen. Anmeldung am isolierten Server praktisch erfolgreich.
  Wiederherstellungscode- und Einrichtungspfad führen laut Code zur verpflichtenden
  Bestätigung neuer Wiederherstellungscodes.
- Grenze: Zwei-Faktor-Neueinrichtung, externe Anmeldung und Wiederherstellungsfall
  nicht mit realem Anbieter ausgeführt.

### geraete-status.mdx

- Entscheidung: Unverändert erhalten. Die Trennung von Ressourcenzustand,
  Buchungsstatus und physischer Rückmeldung bleibt erforderlich.
- Quellen: `web/components/access/access-catalog-presentation.tsx`,
  `resource-catalog-workspace.tsx`;
  `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs`;
  `api/Service/Accesses/Boundary/Dto/ResourceAccessCatalogDtos.cs`.
- Prüfung: Katalogstatus, Bedingungen und Detailzugang gegen Code und die
  tatsächlich sichtbare Holzwerkstatt im isolierten Katalog abgeglichen.
- Grenze: Keine angeschlossene Tür, Maschine oder reale Störung vorhanden;
  Störungskontakt bleibt standortabhängig.

### index.mdx

- Entscheidung: Unverändert erhalten; Aufgabentabelle ist passend und kompakt.
- Quellen: `web/components/portal/portal-navigation.ts`, `portal-shell.tsx`,
  `portal-resources.tsx`, `portal-qualifications.tsx`;
  `web/components/layout/common/account-menu-items.tsx`.
- Prüfung: Vier Desktop-Tabs, Profilmenü, Bereichswechsel und ausschließlich eigene
  Portalansichten gegen Code und Browsernavigation abgeglichen. Verlinkte
  Produktseiten vorhanden. Bei 390 × 844 Pixeln die untere Navigation **Start**,
  **Ressourcen**, **Buchungen**, **Nachweise** im Browser bestätigt.
- Grenze: Sichtbarkeit der Verwaltung hängt von den konkreten Kontorechten ab;
  nicht jede Rechtekombination praktisch durchgespielt.

### kalender.mdx

- Entscheidung: Gültigen Ablauf erhalten, vertraulichen Link sichtbar einordnen.
- Quellen: `web/components/bookings/booking-calendar-subscription-dialog.tsx`;
  `web/app/[project]/dashboard/bookings/_components/bookings-workspace.tsx`;
  `web/lib/bookings/booking-presentation.ts`;
  `api/Service/Bookings/Boundary/HttpControllers/BookingCalendarSubscriptionsController.cs`;
  `api/Service/Bookings/Application/Services/BookingCalendarSubscriptionService.cs`,
  `BookingService.cs`.
- Änderungen: Callout zum Zugriff mit dem persönlichen Link und zum Ersetzen bei
  Verlust oder Weitergabe. Bestehende passende Aufnahme als `ImageZoom`.
- Prüfung: 366-Tage-Dateiexport, 30/335-Tage-Abozeitraum, nur einmal angezeigter
  Link, Ersetzen/Widerrufen und Prüfung des aktiven Kontos/Rechts im Code bestätigt.
  Bestehendes Bild enthält keinen persönlichen Link und passt zum aktuellen Dialog.
- Praktischer Nachweis: Kalenderzugang über die UI erstellt. Der lokale Abruf
  lieferte HTTP 200 mit `BEGIN:VCALENDAR`. Über **Neuen Link erstellen** und die
  Bestätigung ersetzt: alter Link HTTP 401, neuer Link HTTP 200. Danach über
  **Zugang widerrufen** bestätigt: neuer Link HTTP 401 und **Kein Kalenderzugang
  aktiv.** in der UI. Links nur im Arbeitsspeicher des Browserablaufs verwendet,
  nicht in Ausgaben, Screenshots oder Dokumentation übernommen. Separaten
  ICS-Dateidownload aus Buchungsdetails ebenfalls praktisch ausgeführt.
- Grenze: Abruf und Aktualisierung in einem externen Kalenderprogramm nicht
  durchgeführt; kein fremder Empfang behauptet.

### kompetenzen.mdx

- Entscheidung: Fachinhalt erhalten, die beiden Geräteansichten alternativ zeigen.
- Quellen: `web/components/portal/portal-qualifications.tsx`;
  `web/components/competencies/profile-competencies.tsx`, `profile-badge-awards.tsx`;
  `web/components/integrations/openbadges/profile-imported-credentials.tsx`;
  `api/Service/Competencies/Boundary/HttpControllers/ProfileCompetenciesController.cs`,
  `ProfileBadgeAwardsController.cs`;
  `api/Service/Competencies/Application/Services/CompetencyGrantAdministrationService.cs`.
- Änderungen: Bestehende visuell passende Screenshots in nativen Desktop-/Handy-Tabs
  und mit `ImageZoom`. Notwendige Angaben und Warnungen bleiben außerhalb der Tabs.
- Prüfung: Drei Datenquellen, Status/Gültigkeit, Widerruf, Pagination und Originaldownload
  gegen aktuelle Komponenten und Controller abgeglichen. Beide Aufnahmen visuell
  mit diesem Aufbau verglichen; keine pauschale Ersetzung.
- Grenze: Reale externe Signaturprüfung, Import und Dateiabruf nicht ausgeführt.

### uebersicht-monitoring.mdx

- Entscheidung: Präzise Messwertgrenzen erhalten, eine Doppelverlinkung entfernen,
  nutzbaren Bildausschnitt vergrößerbar machen.
- Quellen: `web/app/[project]/dashboard/_components/monitoring-client.tsx`,
  `dashboard-client.tsx`; `web/app/[project]/dashboard/_lib/widget-registry.ts`;
  `web/components/metrics/metric-history-controls.tsx`;
  `api/Service/Observability/Application/DashboardDataQueryService.cs`,
  `MetricsQueryService.cs`, `PersonalDashboardService.cs`, `SystemMetricsReader.cs`;
  `api/Framework/Infrastructure/Telemetry/MetricsSettings.cs`.
- Änderungen: Passenden Transaktionsausschnitt als `ImageZoom` erhalten. Veraltete
  Gesamtaufnahme entfernt: dort fehlen die aktuellen Labels **Zeitraum** und
  **Auflösung**, außerdem steht noch `24h` statt **Letzte 24 Stunden**.
  Widget-Schwellen als Callout von Alarmregeln abgegrenzt. Wiederholten Link auf das
  persönliche Dashboard am Seitenende entfernt; der Einstieg enthält ihn bereits.
- Prüfung: Rechte, 48-Stunden-/Sieben-Tage-Auflösungsgrenze, 2.000-Punkte-Limit,
  Aufbewahrung, eigene Dashboardgrenzen und Aggregation gegen Code abgeglichen.
  Bestehende historische Anker `persönliches-dashboard` und
  `offene-dokumentationsaufgaben` bleiben erhalten.
- Grenze: Kein realer Linux-/RPi-Host und kein vollständiges Messjahr praktisch
  geprüft. Das Transaktionsbild bleibt ein vorhandenes fiktives Beispiel.

### zutritt.mdx

- Entscheidung: Gute Begriffstrennung erhalten; aktuelles Katalogmotiv ergänzen.
- Quellen: `web/components/portal/portal-resources.tsx`, `profile-access-grants.tsx`;
  `web/components/access/resource-catalog-workspace.tsx`,
  `access-catalog-presentation.tsx`;
  `api/Service/Accesses/Application/Services/ProfileAccessGrantService.cs`,
  `ResourceAccessCatalogService.cs`;
  `api/Service/Accesses/Boundary/HttpControllers/ProfileAccessGrantsController.cs`.
- Prüfung: Eigene direkte, Gruppen- und Medienzuordnungen, Gültigkeit und
  Wochenzeiten gegen Code abgeglichen. Im Browser Gruppenfreigaben, Katalogsuche,
  Einweisungsanforderung und Anfrageblocker der Holzwerkstatt geprüft.
- Änderungen: Neue `ImageZoom`-Aufnahmen der Gruppenfreigabe für **Seminarraum
  klein** und der Katalogsuche nach **Holzwerkstatt**. Herkunft und Nutzungsbedingungen
  sind getrennt sichtbar; keine alte Aufnahme mit entfallenen Aktionsbezeichnungen
  wieder eingeführt.
- Grenze: Mediennutzung und weitere Bedingungen am Hardwareleser nicht praktisch
  geprüft. Ein zeitlicher Status bleibt ausdrücklich keine Zutrittsentscheidung.

## Gemeinsame Prüfungen und offene Punkte

- Ein eigener Browser `docs-revision-benutzer` verwendet ausschließlich den
  isolierten Server auf Port 3415 mit API 35116 und fiktiven Workshop-Seed-Daten.
  Zugangsdaten und persönliche Kalenderlinks werden nicht dokumentiert.
- Native Komponenten-APIs anhand der installierten Fumadocs-Deklarationen und des
  vorhandenen `web/mdx-components.tsx` geprüft.
- Prettier-Prüfung aller elf zugewiesenen MDX-Dateien und dieses Berichts erfolgreich.
  Scoped `git diff --check` erfolgreich. Statischer Abgleich gegen den gespeicherten
  Ausgangsstand: alle 52 bisherigen Überschriften und expliziten Anker erhalten;
  alle 43 relativen Seitenverweise und zwölf statischen Bildimporte zeigen auf
  vorhandene Dateien. Globale Doku-Prüfungen koordiniert der Hauptagent.
- Alle sieben neuen Produktaufnahmen vor dem Einbinden visuell geprüft. Zwischenstände
  mit Next-Dev-Overlay, Kompilierungsanzeige oder Ladezustand wurden verworfen und
  durch fertige Ansichten ersetzt. Alte nicht mehr eingebundene Bilddateien bleiben
  unangetastet.
- Consumer gezielt im selben Browser geprüft: **Meine Buchungen** mit nativen
  Steps bei 390 × 844 und 1280 × 900 Pixeln gerendert und Aufnahmen visuell geprüft;
  **Meine Qualifikationen** bei 390 × 844 Pixeln mit ausgewähltem **Handy**-Tab
  geprüft. Keine horizontale Seitenüberschreitung bei diesen Ansichten. Native
  Bildvergrößerung geöffnet und mit Escape wieder geschlossen. Das ersetzt keine
  Vollprüfung aller elf Seiten, sämtlicher Themes oder der Tastaturbedienung.
- Die parallele Arbeit verursachte vorübergehend Build-Overlays wegen noch fehlender
  fremder Bildimporte und einer MDX-Zwischenfassung. Nach Wiederherstellung durch
  die zuständigen Agenten wurden die betroffenen Abläufe erneut ausgeführt. Diese
  Zwischenstände sind keine bestätigten Produktfehler.
- Kein Serverstart, Build, Commit, Push, Hardware- oder Anbieterabnahme durch
  dieses Paket.
- Kleiner Produktbefund außerhalb des Patches: Der Anfragedialog rendert hinter
  dem Ressourcennamen ein verwaistes ` ·` in
  `web/components/access/resource-catalog-workspace.tsx` (DialogDescription).
  Im Browser an Holzwerkstatt sichtbar; beeinflusst das Absenden nicht.
