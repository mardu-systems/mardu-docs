# P16 – Erscheinungsbild und Anzeigeformate

Änderungsbrief: Angemeldete Personen möchten Theme, Sprache und Anzeigeformate
einstellen und wissen, welche Auswahl sofort im Browser gilt und welche im Konto
gespeichert wird. Die kanonische Anleitung bleibt unter ihrer bestehenden URL im
Profilzweig des Benutzerbereichs. Geplant ist ein kleiner Textpatch anhand der
vorhandenen UI, Hooks, Locale-Dateien und Backend-Zeitzonenauflösung; Bild und
bestehende Anker bleiben erhalten. Lokale Dokumentprüfungen folgen, die gemeinsame
Browser-/Consumer-Prüfung übernimmt der Koordinator.

## Entscheidung: verbessert, zur Prüfung

- Zugang auf **Kontoeinstellungen → Erscheinungsbild** aktualisiert.
- Sofortige Anwendung und Browserspeicherung ohne Speicherknopf erklärt; die
  wiederholte Sofortwirkung im Theme-Abschnitt entfernt.
- Sprachpräferenz unter **Profil** mit Deutsch/Englisch und notwendigem Speichern
  ergänzt. Kein zusätzliches Sprachformular unter Erscheinungsbild behauptet.
- Kontozeitzone von der separaten Ruhezeitenzeitzone abgegrenzt und die vorhandene
  Benachrichtigungsanleitung verlinkt. Theme/Systemmodus, Formatvorschau,
  Buchungszeitzone, Bedienhilfen, URL, alte Überschriftenanker und Bild erhalten.

## Belege

Quellenpfade relativ zum Software-Repository:

- `web/components/layout/common/account-menu-items.tsx:23–27,51–65`,
  `web/locales/de/navigation.json:25–38` und
  `web/components/layout/settings/profile-nav.config.ts:74–86`: Zugang und Labels.
- `web/app/[project]/dashboard/user-management/profile/appearance/page.tsx:40–127,139–141,306–505`:
  Theme, Schalter, Zeitzonensuche und Datums-/Zeit-/Zahlenoptionen, direkte Setter,
  keine Speicheraktion. `web/app/providers.tsx:22–27`: Systemmodus via next-themes.
- `web/hooks/use-format-settings.ts:13–35,79–202`: Browserspeicher und
  Systemvorgaben via `Intl`; `web/hooks/use-accessibility.ts:10–66` und
  `web/app/globals.css:226–288`: Speicherung und Darstellung der Bedienhilfen.
- `web/app/[project]/dashboard/user-management/profile/account/account-form.tsx:221–254,373–475`:
  getrennte Speicheraktionen für Sprache und Kontozeitzone; erfolgreicher
  Sprachwechsel ruft `setLocale` auf. `web/lib/users/languages.ts:6–9`:
  Deutsch/Englisch. `web/lib/i18n.tsx:117–148`: Browserlocale und Cookie.
- `api/framework/Infrastructure/Identity/Users/Services/UserService.CreateUpdate.cs:447–467`:
  Speicherung im Konto;
  `api/framework/Infrastructure/RequestPreferences/RequestTimeZoneService.cs:23–52`:
  Kontozeitzone mit globalem/System-Fallback für serverseitige Zeitangaben.
- `api/Service/Notifications/Application/Policy/NotificationPolicyEngine.cs:164–190,201–213`:
  Ruhezeiten und Digest nutzen `QuietHoursTimeZoneId`, nicht die Kontozeitzone;
  Digest-Fallback ist UTC.
- `api/Service/Bookings/Application/Services/BookingService.cs:482` und
  `BookingManagementService.cs:779,825`: `OriginalTimeZoneId` am Termin.
- `web/locales/de/settings.json:1239–1266,1902–1932`: exakte UI-Texte.

## Checks und Grenzen

- `bun fmt --check` für genau Seite und Bericht erfolgreich.
- Seite mit vorhandenem `@mdx-js/mdx` kompiliert; alle vier lokalen Bild-/Seitenverweise
  und die verwendeten Zielanker auf Existenz geprüft. `git diff --check` für die
  eigenen Dateien erfolgreich. Bestehenden Screenshot selbst angesehen: zeigt
  ausschließlich die belegte Theme-Auswahl, keine personenbezogenen Daten.
- Ausschließlich statische Prüfung, keine Abnahme. Koordinator: gerenderte Seite
  und mobile Darstellung in beiden Consumern sowie angemeldetes Ändern, Neuladen,
  Systemmoduswechsel, Formatvorschau und Sprachspeicherung prüfen. Keine Hardware-
  oder Anbieterprüfung für diese Seite nötig.
- Produktgrenze: `useFormatSettings` wird außerhalb der Einstellungsseite nur in
  `web/components/portal/member-dashboard.tsx:77,160` verwendet. Gemeinsame Tabellen
  (`web/lib/table/date-time.ts:3–10`) formatieren unabhängig via `Intl`.
  Deshalb keine Zusage einer dashboardweit einheitlichen Wirkung ergänzt.
- Produktbefund: Deutsche Zahlenformatoptionen enthalten englische Bezeichnungen
  (`web/locales/de/settings.json:1906–1909`). Kein Softwarepatch im Seitenauftrag.
  Die Kontozeitzonenbeschreibung in derselben Locale behauptet Erinnerungen und
  Zeitpläne; die geprüfte Benachrichtigungspolicy hat eine eigene Zeitzone.
- Keine Navigation, neuen Seiten, API-/DTO-Verträge oder Software geändert.
  Nachbarseite `profil.mdx` enthält ebenfalls die pauschale Zuordnung der
  Kontozeitzone zu Benachrichtigungen; Abgleich durch deren Seitenauftrag nötig.

Geänderte Dateien: `docs/ueberblick/profil-erscheinungsbild.mdx` und dieser Bericht.
