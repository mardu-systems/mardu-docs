# P52 — Benutzeransicht

## Änderungsbrief

Leserfrage: Wo beginne ich mit meinen eigenen Aufgaben, und wie erreiche ich
Kontoeinstellungen oder Verwaltungsaufgaben? Vorwissen: angemeldetes Konto, noch
keine Kenntnis der Portalnavigation oder Rechteaufteilung. Die kurze Aufgabentabelle
und vorhandenen Anleitungen bleiben erhalten. Ergänzt werden nur der konkrete
Kontoeinstieg, die Grundleserechte und der fehlende Störungsweg. Der Benutzerbereich
ist ein Lesereinstieg, keine vorausgesetzte Systemrolle. Kanonische Quelle bleibt
`docs/benutzer/index.mdx`; Profilseiten behalten ihre bestehenden `ueberblick`-URLs.
Prüfung: Quellenabgleich, lokale Links/Anker und gezielte Formatprüfung. Gemeinsame
Consumer-/Mobilprüfung übernimmt der Koordinator.

## Entscheidung und Änderungen

**Verbessert; statisch geprüft, Darstellung zur gemeinsamen Prüfung.**

- Persönlichen Datenumfang auch bei zusätzlichen Verwaltungsrechten und
  Profil-Leserechte für Dashboard, eigene Freigaben, Qualifikationen und Kontodaten
  ergänzt. Buchungen und Katalog haben gesonderte Leserechte; die Einzelanleitungen
  bleiben die Quelle für weitere Voraussetzungen und Änderungsrechte.
- Konkreten Einstieg **Mein Profil → Kontoeinstellungen** ergänzt. Die acht
  vorhandenen Profilanleitungen bleiben über die Profilseite erreichbar; keine
  zusätzliche Linkliste für sämtliche Einstellungen angelegt.
- Den bereits ausgearbeiteten Weg für Ressourcenzustände und Störungsmeldungen
  aus der Aufgabentabelle verlinkt. Alle neun Benutzeranleitungen sind damit aus
  diesem Einstieg erreichbar; Betriebsmetriken bleiben über die Aufgabenanleitungen
  erreichbar und werden nicht als persönliche Standardaufgabe dargestellt.
- Beschreibung der ersten Schritte auf deren tatsächlichen Umfang begrenzt:
  Anmeldung, Profil und Buchungsvorbereitung. Die eigentliche Buchungsanleitung
  bleibt gesondert verlinkt.
- Dokumentationsbereiche als Lesereinstiege von Systemrollen abgegrenzt.
- Gute knappe Zweispaltentabelle, Desktop-/Handybezeichnungen, Kontomenü,
  Verwaltungswechsel, alle fünf Abschnittsüberschriften und historische Profil-URLs
  erhalten. Tabellenzellen bestehen weiterhin nur aus kurzen Aufgaben und Links.

## Quellen und Belege

Pfade relativ zum Software-Repository:

- `web/content/docs/docs/benutzer/`: Abgleich mit `erste-schritte.mdx`,
  `dashboard.mdx`, `zutritt.mdx`, `berechtigungsanfragen.mdx`, `buchungen.mdx`,
  `kalender.mdx`, `kompetenzen.mdx`, `benachrichtigungen.mdx` und
  `geraete-status.mdx`; `uebersicht-monitoring.mdx` zum Abgrenzen der Betriebsaufgaben.
- `web/content/docs/docs/ueberblick/profil.mdx` und die sieben
  `profil-*.mdx`-Anleitungen: eigener Kontoeinstieg, Rechte und Aufgabenverteilung;
  Details und Einstellungen werden dort erklärt und hier nicht dupliziert.
- `web/components/portal/portal-navigation.ts:5`,
  `web/components/portal/portal-shell.tsx:146` und `:214`:
  vier Desktop-Tabs, mobile Navigation, bedingter Verwaltungswechsel und Kontomenü.
- `web/locales/de/navigation.json:26` und `:112`:
  **Kontoeinstellungen**, **Mein Profil**, Desktop-/Mobilbezeichnungen und Wechsel.
- `web/components/layout/common/account-menu-items.tsx:21` und `:84`:
  Kontoeinstellungen und Dokumentation in neuem Tab;
  `web/lib/documentation-navigation.ts:9`: Benutzer-Dokumentation im Portalkontext.
- `web/components/profile/profile-settings-layout.tsx:47` und `:112`:
  mobile Bereichsliste; `web/lib/profile-navigation.ts:7`: Profil bleibt im Kontext.
- `web/components/portal/member-dashboard.tsx:57`,
  `portal-resources.tsx:50` und `portal-qualifications.tsx:26` im selben Verzeichnis:
  getrennte Leseprüfungen für Profil und Katalog.
- `web/app/[project]/portal/bookings/page.tsx:4` und
  `web/app/[project]/dashboard/bookings/_components/bookings-workspace.tsx:140`,
  `:159`, `:239`: Portal verwendet persönliche Buchungen, unabhängig von
  zusätzlichen Verwaltungsrechten.
- `api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs:39`:
  Profil-Leserecht und aktuell angemeldete Person;
  `api/Service/Observability/Boundary/HttpControllers/ProfileDashboardController.cs:22`:
  persönliches Dashboard mit Profil-Leserecht;
  `api/Service/Accesses/Boundary/HttpControllers/ProfileAccessGrantsController.cs:33`
  und `Application/Services/ProfileAccessGrantService.cs:29` in demselben Modul:
  eigene Freigaben, aktuelle Gruppen und eigene Medien;
  `api/Service/Competencies/Boundary/HttpControllers/ProfileCompetenciesController.cs:29`:
  Profil-Leserecht und ausschließlich eigene Einweisungen;
  `api/Service/Bookings/Boundary/HttpControllers/BookingsController.cs:27`:
  eigene Buchungen mit Buchungs-Leserecht.
- `web/lib/docs-roles.tsx:57` und `:82`,
  `web/content/docs/docs/benutzer/profil/meta.json`:
  alle acht Profilseiten gehören trotz historischer `ueberblick`-URLs zum
  Benutzer-Lesereinstieg. Navigation nur gelesen.

## Ausgeführte Checks und Grenzen

- Gezielt mit vorhandenem Prettier formatiert; abschließende Formatprüfung beider
  eigenen Dateien mit `--ignore-path /dev/null` (Docs sind im Consumer sonst
  ausgeschlossen).
- Mit vorhandenem `@mdx-js/mdx` den Inhalt ohne Frontmatter erfolgreich kompiliert.
- Alle 14 relativen Seitenverweise auf existierende Dateien geprüft; alle beginnen
  mit `./` oder `../`. Keine fragmentierten Links oder Bilder auf dieser Seite.
- Vergleich der Überschriften mit `HEAD`: alle fünf bisherigen Abschnittsanker
  unverändert.
- Gezielt `git diff --check` für die beiden eigenen Dateien ausgeführt.
- Keine Builds, globalen Tests, Browser-, Hardware- oder Anbieterprüfung.
  Koordinator: Seite in beiden Consumern sowie Tabelle und Profil-Einstieg in
  schmaler Ansicht prüfen. Die schlichte Zweispaltentabelle ist statisch knapp
  gehalten; mobile Lesbarkeit noch nicht praktisch bestätigt.
- Nachbarbefund für Koordinator: `docs/benutzer/benachrichtigungen.mdx` bezeichnet
  den Profilverweis noch als „Profil → Überblick“, obwohl `docs-roles.tsx` und
  Profil-Metadaten den Benutzerbereich festlegen. Keine Änderung der Nachbarseite
  im vorliegenden Auftrag. Kein neuer Seitenbedarf festgestellt.

## Geänderte Dateien

- `web/content/docs/docs/benutzer/index.mdx`
- `web/content/docs/planning/reviews/2026-11-01/benutzer--index.md`

Bestehende Markdown-Tabelle, relative Verweise und kanonische Anleitungen
wiederverwendet. Keine Software- oder API-/DTO-Vertragsänderung; vorhandene
API-Dokumentation unverändert. Status bleibt **zur Prüfung**, nicht abgenommen.
