# P01: Erste Schritte

Seite: `docs/benutzer/erste-schritte.mdx`.
Entscheidung: **verbessert**, zur Prüfung; keine praktische Abnahme.

## Änderungsbrief und Ergebnis

Die Seite beantwortet für erstmals angemeldete Personen: Wie melde ich mich am
richtigen Standort an, prüfe mein Profil und bereite eine erste Buchung vor?
Vorausgesetzt sind Webadresse und freigeschaltetes Konto. Heimat bleibt der
Benutzerbereich. Die bestehende kurze Schrittfolge passt; erforderlich sind nur
präzise Menübezeichnungen und der belegte Abschluss der Anmeldung mit neuen
Wiederherstellungscodes. Keine Software- oder Navigationsänderung.

## Befunde und Änderungen

- **Mein Profil → Kontoeinstellungen** ersetzt den nicht vorhandenen Menüpunkt
  **Profil**. Auf dem Handy folgt weiterhin **Profildaten**.
- Beim Buchungseinstieg steht zusätzlich der mobile Tab **Buchungen**.
- Nach Wiederherstellungscode-Anmeldung oder Zwei-Faktor-Einrichtung führt die
  Oberfläche zunächst zur Erzeugung neuer Wiederherstellungscodes. Speichern und
  Bestätigen sind jetzt als notwendiger Schritt sichtbar. Eine automatische
  Profilvervollständigung vor der Benutzeransicht wird nicht behauptet.
- Beibehalten: serverbezogene Konten, Zugangsvoraussetzungen, angebotene
  Anmeldeverfahren, Weiterleitung zur Benutzeransicht, eigenes Speichern pro
  Profilbereich, noch unverbindliche Buchungsvorbereitung, Freigabe-/Fehlerhilfe,
  Orientierung und Abmelden. Die Seite braucht keine zusätzlichen Komponenten,
  Bilder oder Akkordeons.

## Geprüfte Quellen

Pfade beziehen sich auf das Software-Repository, sofern nicht anders angegeben.

- `web/components/layout/common/account-menu-items.tsx:23–27,78–85` und
  `web/locales/de/navigation.json:25–31,113–140`: Kontoeinstellungen, Abmelden,
  deutsche Desktop-/Mobilbezeichnungen.
- `web/components/profile/profile-settings-layout.tsx:59–77,128–162`:
  mobile Profilübersicht und Profildaten-Link;
  `web/app/[project]/portal/profile/page.tsx:1` sowie `details/page.tsx:1`:
  Wiederverwendung der bestehenden Profilseite.
- `web/app/[project]/dashboard/user-management/profile/profile/page.tsx:16–47`
  und `web/app/[project]/dashboard/user-management/profile/profile-form.tsx:96–115`:
  Profilbereiche und Speichern;
  `api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs:39–40,88–90`:
  getrennte Profil-Lese-/Änderungsrechte.
- `web/app/[project]/auth/auth-page-client.tsx:212–217,275–287,420–427`:
  Einstieg ins Portal, gegebenenfalls Zwei-Faktor-Einrichtung, verfügbare externe
  Anbieter; `web/proxy.ts:348–353`: vorgeschriebene Zwei-Faktor-Einrichtung.
- `web/app/[project]/auth/two-factor/two-factor-page-client.tsx:97–104` und
  `web/app/[project]/auth/setup-two-factor/page.tsx:138–141`:
  Weiterleitung zu Wiederherstellungscodes.
- `web/app/[project]/dashboard/user-management/profile/recovery-codes/page.tsx:5–7`
  und `web/components/profile/RecoveryCodesDialog.tsx:79–87,132–145,226–245`:
  automatische Erneuerung, Speicherbestätigung und anschließende Rückkehr;
  `api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs:190–193`:
  vorhandener Erneuerungsendpunkt.
- `web/components/portal/portal-navigation.ts:5–33` und
  `portal-shell.tsx:147–179,185–231`: Navigation, Profilmenü und Glocke.
- `web/app/[project]/dashboard/bookings/_components/bookings-workspace.tsx:111–150`
  und `web/components/bookings/booking-editor-dialog.tsx:471–502,818–820`:
  Buchungsrechte und eigentliche Buchungsaktion;
  `api/Service/Bookings/Boundary/HttpControllers/BookingsController.cs:49–61`:
  Erstellung erst durch POST.
- Dokumentationskontext: `docs/benutzer/index.mdx`, `buchungen.mdx`, `zutritt.mdx`,
  `docs/ueberblick/benutzerkonten.mdx`, `profil.mdx`, `fehlersuche.mdx`.
  `planning/offene-dokumentationsaufgaben.md` enthält keinen eigenen offenen
  Auftrag zu dieser Einstiegsseite.

## Checks und offene Praxisprüfung

- `bun fmt --check` mit Seite und Bericht als expliziten Dateizielen: erfolgreich.
- `git diff --check -- docs/benutzer/erste-schritte.mdx planning/reviews/2026-11-01/benutzer--erste-schritte.md`:
  erfolgreich.
- Lokaler Python-Lesecheck: Frontmatter, fehlendes zusätzliches H1, vier relative
  Seitenziele und Zielanker `#anmeldung` erfolgreich geprüft. Bestehende
  Überschriften/Anker bleiben unverändert.
- Nur statische Implementierungsprüfung. Keine Browser-, Hardware- oder
  Anbieterprüfung, kein Build. Der Koordinator prüft die Darstellung in den
  Consumern und den angemeldeten Ablauf auf Desktop und Handy; insbesondere
  Profilmenü und Rückkehr nach der Codebestätigung. Hardware ist für diese
  Webportal-Einstiegsseite nicht erforderlich; externe Anmeldung bleibt vom
  eingerichteten Anbieter abhängig.

## Hinweise für den Koordinator

`docs/ueberblick/profil.mdx` verwendet ebenfalls noch **Mein Profil → Profil**.
Dem Koordinator als Folgekorrektur gemeldet; außerhalb dieses Seitenbesitzes nicht
geändert. URL, vorhandene Anker und Zielseiten dieser Seite bleiben bestehen.
Kein zusätzlicher Seitenbedarf. API-/DTO-Dokumentation unverändert, weil keine
API geändert wurde.

Geänderte Dateien: `docs/benutzer/erste-schritte.mdx` und dieser Bericht.
