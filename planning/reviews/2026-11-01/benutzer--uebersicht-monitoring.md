# P33: Übersicht und Systemstatus

## Änderungsbrief

Leserfrage: Wie lese ich Betriebsmetriken und speichere eigene Betriebsdashboards?
Leser kennen die Verwaltungsansicht, benötigen aber keine API-Kenntnisse.
Kanonischer Bereich ist **Administration**, die bestehende URL unter `benutzer/`
bleibt erhalten. Das persönliche Portal-Dashboard hat eine eigene Anleitung.
Geplant ist eine belegte Ergänzung von Rechten, Auswahl/Erstellung/Bearbeitung,
Speichern und Konflikten sowie Zeitbereichen und Aufbewahrung. Gültige Erklärungen
zu Transaktionen, Nullwerten und Benachrichtigungen bleiben erhalten. Prüfung durch
UI-/Backend-Codelektüre, Bildsichtung und lokale Dokumentprüfungen; angemeldete
Browserprüfung und gemeinsame Consumer-Prüfung übernimmt die Koordination.

## Entscheidung und Änderungen

**Verbessert; zur Prüfung, keine praktische Abnahme.** Rechte, Systemstatus-Ablauf,
Dashboard-Auswahl, Startauswahl ohne Vorlagendialog, Erstellung, Umbenennen,
Widgets/Geräteauswahl, Schwellen, Größen, Speichern, Vorschau, Konflikt und Löschen
sind ergänzt. Anzeigezeitraum, Abfrageintervall und Erfassung sind getrennt erklärt.
Auflösungen, 2.000-Punkte-Limit und Aufbewahrungsdefaults sind belegt ergänzt.
Der irreführende Abschnitt „Persönliches Dashboard“ heißt „Eigenes
Betriebsdashboard“; der bisherige Anker `persönliches-dashboard` bleibt explizit
erhalten. Auch `offene-dokumentationsaufgaben` und alle anderen bisherigen
Abschnittsanker bleiben erhalten.

Erhalten sind die Erklärung der Datenbanktransaktionen samt passendem Detailbild,
die Null-/Lücken-Semantik, Bedeutung aktueller Zustände, Standardgrößen und
Benachrichtigungsmetriken mit der Grenze „Versand belegt kein Lesen“ sowie alle
bisherigen Seitenverweise. Die alte pauschale Zuordnung der Geräte zu den
Zugangsmetriken wurde korrigiert: Gerätediagnose nutzt den Dashboard-Metrikpfad
mit wählbarer Historie; Benutzer-/Zutrittspunkt-Zugangsmetriken bleiben separat.

## Quellen und relevante Stellen

Pfade beziehen sich auf das Software-Repository, nicht den Submodule-Root.

- `web/components/layout/sidebar/dashboard-navigation.ts`: Übersicht und
  Betrieb/Systemstatus; dazu `web/locales/de/navigation.json:56–63` und `:304–323`
  (Menünamen, Historienhinweise, Bearbeiten/Vorschau).
- `api/Service/Observability/Boundary/HttpControllers/PersonalDashboardsController.cs:160–310`:
  ownerbezogene Liste und CRUD/Standard mit `Dashboard.View/Create/Update/Delete`,
  Widget-Katalog und Abfrage mit `Dashboard.View`.
- `api/Service/Observability/Application/DashboardWidgetCatalog.cs:8–19` und
  Methode `Widget`: Limits 20 Dashboards/40 Widgets/10 Geräte, Bereiche und
  Datenquellenrechte (`Devices.View` für gerätebezogene Widgets, sonst
  `Dashboard.View`).
- `api/Service/Observability/Application/DashboardDataQueryService.cs:83–107` und
  `EnsureDevicePermissionAsync`: UTC-Abfragefenster, automatische Auflösung bis
  48 Stunden fein, danach Stunde, Minute maximal sieben Tage; zusätzliche
  Geräteleserechte werden serverseitig geprüft.
- `web/app/[project]/dashboard/_components/monitoring-client.tsx:41–72`, `:123–150`,
  `:243–325`: feste Systemkategorien/Anordnung, nach Katalogrecht gefilterte Quellen,
  Aktualisieren/Einstellungen und Erfassungsstatus/Sample-Alter.
- `web/app/[project]/dashboard/_components/dashboard-client.tsx:177–220`,
  `:304–407`, `:490–736`, `:760–885`, `:945–1185`: Auswahl mit URL vor Standard,
  Name und Entwurf, Erstellung, Wechsel-Verwerfensabfrage, Speichern und HTTP-412-
  Behandlung, Mutationen, Widgetauswahl und Konfiguration. `:430–441`: **Neu laden**
  bei Konfigurations-/Konfliktfehler. **Vorschau** toggelt nur den Bearbeitungsmodus,
  ein eigener Verwerfen-Knopf ist hier nicht implementiert.
- `web/app/[project]/dashboard/_lib/dashboard-layout.ts:202`: gespeicherte
  Startauswahl mit Standardbereich 24h und Refresh 30 Sekunden; getrennte
  Breakpoint-Layouts. `web/app/[project]/dashboard/_components/dashboard-widget-card.tsx:94–142`:
  Schwellenmarkierung, veraltete Daten, Tastaturverschieben/-größenänderung.
  `web/locales/de/common.json:610–645`: Konfigurationsnamen, Beispieldaten,
  Schwellen ohne Alarmwirkung.
- `api/Service/Observability/Application/PersonalDashboardService.cs`:
  `NormalizeName`, `NormalizeNameForComparison`, `EnsureNameAvailableAsync`,
  `EnsureMatchingETag`, `DeleteCoreAsync` belegen Namen, Eigentum, Konflikte und
  Ersatz des gelöschten Standarddashboards.
- `web/components/metrics/metric-history-controls.tsx` und
  `web/app/[project]/dashboard/_lib/widget-registry.ts:20–41`: fünf rollierende
  Fenster, Jahr = 365 Tage, Auflösungswechsel; `:1270–1317`:
  Transaktionssumme/-rate, gestapelte Commits/Rollbacks, Deadlocks separat.
  `web/docs/dashboard-metrics-api.md`: ergänzender bestehender Vertragsabgleich.
- `api/Service/Observability/Application/MetricsQueryService.cs:22`, `:30`,
  `:131–181`: neueste 2.000 Punkte, Teilhistorie, ältester Wert, fehlende Stundenfelder.
  `web/app/[project]/dashboard/_components/dashboard-grid.tsx:26–76`: sichtbare
  Historienhinweise mit ältestem/erstem angezeigten Punkt.
- `api/Framework/Infrastructure/Telemetry/MetricsSettings.cs:11–24`:
  Erfassung, konfigurierbare Intervalle, 30/365 Tage Defaults;
  `api/Service/Observability/Application/TimescaleRetentionPolicySynchronizer.cs`:
  Aufbewahrung für Rohdaten und Stundenaggregate.
  `api/Service/Observability/Application/OperationalMetricsCollector.cs:36–42`:
  deaktivierte Erfassung erzeugt keine neuen Messpunkte.
  `api/Service/Observability/Boundary/HttpControllers/MetricsSettingsController.cs:24–43`:
  gesonderte `Settings.View/Update`-Rechte.
- `web/app/[project]/dashboard/device-management/device-settings/device-settings-sheet.tsx:215–223`:
  aktuelle Registerbezeichnung **Diagnose** (`web/locales/de/devices.json:522`).
  `device-monitoring-tab.tsx:34–57`, `:93–111`: wählbare Dashboard-Historie und
  separate Geräteansicht. `api/Service/Observability/Boundary/HttpControllers/PersonalDashboardsController.cs:69–109`:
  gemeinsame Gerätevorlage je Konto, unabhängig vom geöffneten Gerät.
- `web/lib/docs-roles.tsx:142` und `web/content/docs/docs/administration/meta.json`:
  vorhandene kanonische Zuordnung zur Administration; keine Navigationsänderung nötig.

## Bilder und Prüfgrenzen

Alle drei ursprünglich eingebundenen PNGs wurden lokal visuell geöffnet.
`datenbank-metriken.png` ist ausgebunden, die Datei bleibt bestehen: Es zeigt eine
Deadlocks-Diagrammreihe und den älteren Transaktionsuntertitel ohne Intervallangabe.
Das widerspricht dem aktuellen Renderer `widget-registry.ts:1270–1317`, der nur
Commits/Rollbacks als Balken führt. `datenbank-transaktionen.png` zeigt die passende
Trennung samt 30-Minuten-Beschriftung und Tooltip und bleibt erhalten.
`systemstatus-metriken.png` bleibt als Beispiel der Systemwidgets mit fehlender
Temperaturmessung erhalten; der Alttext behauptet keine sichtbaren Zeitreihenlücken
mehr. Es zeigt ältere Bedienung ohne die inzwischen sichtbaren Feldlabels für
Zeitraum/Auflösung. Kein Bild ist eine neue praktische Abnahme.

Bildbedarf: aktuelle angemeldete Desktopaufnahme von Systemstatus mit den
beschrifteten Historienfeldern; aktuelle Datenbankübersicht als Ersatz des
ausgebundenen Bildes; optional Dashboardeditor mit Name/Widget/Speichern und
Konfliktzustand. Für die Anleitungen reichen fiktive Daten, keine generierte UI.
Vorhandene Bilder stammen aus dem Bestand; ihre Erzeugung wurde nicht neu verifiziert.

Offen für Koordination: angemeldete Browserprüfung von Erstellung, Vorschau,
Speichern, Wechsel-Verwerfen, Konflikt/**Neu laden**, Layout auf Desktop/Handy,
Schwellen-/Beispielvorschau sowie Datenquellenrechten. Echte Ausfälle,
Retentionablauf und reale Gerätetelemetrie wurden nicht erzeugt/geprüft.
Beide Consumer einschließlich MDX-Darstellung/Markdown-Ausgabe sind gemeinsam zu
prüfen. Keine Backend-, Hardware- oder Providerabnahme behauptet.

Beobachtete Produktgrenzen für gesonderte Prüfung: Die obere Toolbar in
`dashboard-client.tsx:521–575` bietet Neu/Standard/Bearbeiten/Speichern ohne
durchgängige Prüfung der jeweiligen Schreibrechte an; die API schützt die
Mutationen. Der allgemeine Widgetdialog-Hinweis sagt „Ansicht speichern“, während
die obere Betriebsdashboard-Aktion „Speichern“ heißt. Keine Softwarekorrektur im
Seitenauftrag. Auf der Produktseite werden die tatsächlich benötigten Rechte und
die vorhandene Speicheraktion beschrieben.

Zusätzlicher statischer Befund zur Nullwertgrenze:
`widget-registry.ts`, Fall `authentication.logins` ab Zeile 1986, setzt erfolgreiche
und fehlgeschlagene Anmeldungen nach leerer Historie und fehlender Summary auf
`0` zurück. Damit kann diese Anzeige auch ohne Beobachtung 0 liefern. Keine
Browserreproduktion. Die frühere pauschale Behauptung, jede angezeigte Null sei
gemessen, wurde deshalb durch die Unterscheidung eines vorhandenen Null-Messpunkts
von fehlenden Messungen ersetzt, mit Prüfung von Status/Sample-Alter/Verlauf.
Eine Softwarekorrektur bleibt außerhalb dieses Seitenauftrags.

## Geänderte Dateien und Checks

- `web/content/docs/docs/benutzer/uebersicht-monitoring.mdx`
- `web/content/docs/planning/reviews/2026-11-01/benutzer--uebersicht-monitoring.md`

Ausgeführt und bestanden:

- Prettier für genau beide Dateien, mit `--ignore-path /dev/null`, weil der
  Software-Consumer das externe Docs-Submodule sonst ignoriert; danach `--check`.
- MDX-Inhalt mit vorhandenem `@mdx-js/mdx` und `remark-gfm` kompiliert. Frontmatter
  separat geprüft und für diesen reinen Syntaxcheck abgetrennt. Der erste Versuch
  mit `remark-frontmatter` scheiterte am nicht direkt verfügbaren Paket; keine
  Dependency nachinstalliert.
- Lokale Linkprüfung: alle Seitenziele und Zielanker, beide verbleibenden
  Bildpfade, Frontmatter und fehlendes H1 geprüft. Alle bisherigen Überschriften-
  und expliziten Anker gegen `HEAD` verglichen und erhalten.
- `git -C web/content/docs diff --check` für die beiden eigenen Dateien.
- Visuelle Sichtung der drei ursprünglichen Bilder, wie oben beschrieben.

Keine Software-, API-/DTO-, Navigations- oder Assetdatei geändert; bestehende
UI-Komponenten und Verträge werden nur dokumentiert. Keine globalen Builds,
Commits oder externen Aktionen.
