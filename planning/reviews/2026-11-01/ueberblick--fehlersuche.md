# P46 – Fehlerhilfe für das Mitgliederportal

- Seite: `docs/ueberblick/fehlersuche.mdx`
- Leserfrage: Welche Ursache passt zu meiner sichtbaren Fehlermeldung, was kann ich selbst prüfen und wann brauche ich den Standort?
- Entscheidung: **verbessert**, zur Prüfung; ausschließlich statisch geprüft, keine praktische Abnahme.

## Änderungsbrief und Umsetzung

Mitglieder kennen die betreffende Portalansicht, aber nicht die Trennung von Anmeldestatus, Funktionsrechten, Ressourcenfreigabe und Nachweisprüfung. Die vorhandene symptomorientierte Übersicht bleibt der kanonische Einstieg. Plan und Umsetzung: bestehende Tabellen und Nachbarverweise mit UI/Verträgen abgleichen, belegte Lücken ergänzen, irreführende Verallgemeinerungen ersetzen und nur diese Seite prüfen.

- Den Profilzugang als **Kontoeinstellungen** benannt. Freiwilliges **Profil vervollständigen** von vorgeschriebener Passwortänderung/Zwei-Faktor-Einrichtung getrennt.
- Anmeldung um Serverfehler, abgelaufenen Anmeldevorgang und Sitzungsablauf ergänzt. Passwortwiederherstellung auf vergessenes lokales Passwort begrenzt; keine pauschale Neuanmeldung, Kontotrennung oder externe Kontomanipulation empfohlen.
- Rechteabfragefehler von fehlenden Rechten sowie Portalzugriff von Ressourcennutzung getrennt. Katalogstatus **Verfügbar** bestätigt weder persönlichen Zugang noch Hardwarezustand.
- Kalenderhilfe um ersetzte/widerrufene Links und erneute Rechte-/Kontoprüfung beim Abruf ergänzt.
- Einweisungen, lokale Badgevergaben und importierte/signierte Nachweise mit passenden nächsten Schritten unterschieden. Verifikation und Ablaufdatum getrennt; Anbieteranmeldung importiert nicht automatisch. Persönlichen API-Zugang nicht mit Anbieterimport gleichgesetzt.
- Benachrichtigungen um bestätigte Kontaktziele, Web-Push-Abo und Grenzen einer In-App-Mitteilung ergänzt. Ladefehler nicht als Leerzustand behandelt; Hinweise zu Entwürfen und Konflikten präzisiert.
- Erhalten: Titel, Beschreibung, URL, alle sieben Abschnittsüberschriften/Anker, Kartenverlustmeldung, Quellenlinks, Hinweise zu ungespeicherten Änderungen und sensible Angaben bei Rückfragen. Die Seite hatte keine Bilder; kein Bild entfernt oder neu erzeugt.

## Geprüfte Quellen

Pfade ab Software-Repository; Zeilen beziehen sich auf den statisch gelesenen Stand:

- `web/components/layout/common/account-menu-items.tsx:19–35`: Kontoeinstellungen und Sicherheitszugang; `web/components/portal/portal-shell.tsx:55–58,84–87,130–145`: Verwaltungszugang und abgelaufene Sitzung.
- `web/locales/de/auth.json:8–39,145–182`: konkrete Login-, Server-, Link- und Faktorfehler sowie Wiederherstellungsaktionen; `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:108–177,684–716`: Kennungsprüfung, Zwei-Faktor-Pflicht, Sperre, Inaktivität, E-Mail und Passwortwechsel.
- `web/components/profile/profile-completion-banner.tsx:20–35` und `web/app/[project]/dashboard/user-management/profile/complete/complete-page-client.tsx`: Ausfüllstand und überspringbare Profilerweiterung; Nachbaranleitung `docs/ueberblick/profil.mdx`.
- `web/components/portal/portal-resources.tsx`, `web/components/portal/portal-qualifications.tsx:53–66`: Wiederholung einer fehlgeschlagenen Rechteabfrage getrennt von fehlender Berechtigung.
- `api/Service/Accesses/Boundary/Dto/ResourceAccessCatalogDtos.cs:29–63` und `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:60–110`: Betriebsstatus, Freigabe, Buchung, offener Antrag und Kompetenzanforderungen getrennt; `web/components/portal/profile-access-grants.tsx:108–165` und `docs/benutzer/zutritt.mdx`: Freigabezeiten und Medienstatus.
- `web/components/bookings/booking-editor-dialog.tsx:500–519,769–783`: Entwurf bleibt bei Speicherfehler bestehen, Konfliktmeldung; `api/Service/Bookings/Application/Services/BookingService.cs:95,171–180,449–451`: Verfügbarkeitsprüfung und spätere Konflikte.
- `api/Service/Bookings/Boundary/HttpControllers/BookingCalendarSubscriptionsController.cs:56–73`: Leserecht bei jedem Feedabruf; `api/Service/Bookings/Application/Services/BookingCalendarSubscriptionService.cs:46–75`: Widerruf und Kontozustand; `docs/benutzer/kalender.mdx`: Linkwechsel, Dateikopie versus Abo.
- `web/components/portal/portal-qualifications.tsx:42–49`: drei getrennte Quellen; `web/components/competencies/profile-competencies.tsx:31–79`, `web/components/competencies/profile-badge-awards.tsx:30–57`, `web/components/integrations/openbadges/profile-imported-credentials.tsx:23–42,103–120,192–196`: Fehler, Gültigkeit und Verifikation getrennt.
- `api/Service/Competencies/Boundary/HttpControllers/ProfileCompetenciesController.cs:22–38` sowie `api/Service/Interoperability/Boundary/ProfileCredentialsController.cs:47–49`: Kompetenzanerkennung und Credential-Verifikation sind keine Ressourcenentscheidung.
- `web/components/integrations/openbadges/profile-provider-connections.tsx:101–108,269–290,319–340`: Verbindung und ausdrücklicher Import mit Fehlerdetails getrennt; `docs/ueberblick/profil-nachweisquellen.mdx`: persönlicher API-Zugang versus Anbieterimport.
- `api/Service/Notifications/Application/Services/NotificationChannelAvailabilityService.cs:26–55`: Serververfügbarkeit und bestätigte Kontaktziele/Push-Abos; `docs/benutzer/benachrichtigungen.mdx` und `docs/ueberblick/profil-benachrichtigungen.mdx`: Rechte, Filter, Ruhezeiten, Kanäle und keine Empfangsbestätigung.
- `web/components/profile/profile-draft-provider.tsx:31,94,187–193,215–227`: Entwurfswarnung und Verwerfen. Geprüfte Nachbarseiten: Benutzer-Buchungen, Kalender, Qualifikationen, Zutritt und Posteingang sowie Profil, Sicherheit, Nachweisquellen und Zutrittsmedien.

## Checks und Praxisgrenzen

- MDX mit dem vorhandenen `@mdx-js/mdx` kompiliert: erfolgreich.
- Vorhandenen Prettier ausschließlich für beide eigenen Dateien mit `--ignore-path /dev/null` ausgeführt; anschließendes `--check`: erfolgreich. `bun fmt` hatte die Dateien im Submodul nicht berücksichtigt (0 Dateien), deshalb die ausdrückliche Prettier-Prüfung.
- Zwölf relative Seitenlinks einschließlich Zielanker geprüft: Ziele vorhanden, `profil-vervollständigen` vorhanden. Alle sieben Abschnittsüberschriften gegen `HEAD` verglichen: unverändert.
- `git -C web/content/docs diff --check -- docs/ueberblick/fehlersuche.mdx planning/reviews/2026-11-01/ueberblick--fehlersuche.md`: erfolgreich.
- Keine globalen Builds, Softwaretests oder externen Schreibaktionen ausgeführt. Keine Software-, API-, DTO-, Navigations- oder Assetänderungen. Bestehende Markdown-Tabellen, Listen und relative MDX-Verweise wiederverwendet; API-Dokumentation unverändert, da kein API-Vertrag geändert wird.

Koordinator: die geänderte Seite in beiden Dokumentations-Consumern rendern; schmale Ansicht, lange Tabellen und Ankersprung zu `profil-vervollständigen` prüfen. Keine Browser-, Mobil-, Hardware-, Mail/SMS/Push-, SSO-, Passkey- oder echte Anbieterimportprüfung durchgeführt. Externen Empfang und physische Freischaltung daher nicht als bestätigt behandeln. Keine weitere Seite, Navigation oder neue Themen nötig; kein belegter Produktfehler aus dieser statischen Seitenprüfung.

## Geänderte Dateien

- `web/content/docs/docs/ueberblick/fehlersuche.mdx`
- `web/content/docs/planning/reviews/2026-11-01/ueberblick--fehlersuche.md`
