# Seitenrevision P14: Persönliche Nachweisquellen

## Änderungsbrief

Die Seite beantwortet für angemeldete Personen mit eigenem Anbieterkonto die Frage,
wie sie eine Nachweisquelle verbinden, aktualisieren und trennen und Nachweise nach
Mardu übernehmen. Vorwissen: Anmeldung und eigenes Profil; OAuth- oder API-Wissen
wird nicht vorausgesetzt. Erwartetes Ergebnis sind ein überprüfter Verbindungsstatus
und ein verständliches Importergebnis. Die bestehende URL und die drei
Abschnittsüberschriften bleiben erhalten. Die Seite bleibt die kanonische Anleitung
für persönliche Verbindungen; Nachweise lesen gehört zur Nachbarseite „Meine
Qualifikationen“ im Benutzerbereich. Grundlage sind aktuelle UI/Übersetzungen aus
Web-Commit `21d783b7`, die Profil-Controller und die zugehörigen Services.

Plan: vorhandene knappe Gliederung erhalten, exakte UI-Aktionen und Rechte ergänzen,
Anbieteranmeldung von persönlichem API-Zugang unterscheiden, Ersetzen/erneutes Prüfen
und Trennfolgen erklären, Fehlerhilfe verdichten. Den veralteten Screenshot nicht
weiter als aktuelle Bedienhilfe einbinden. Lokale Format-, MDX- und Linkprüfung;
Browser-/Consumer-Abnahme übernimmt der Koordinator. Kein externer Providerzugriff.

## Befund und Entscheidung

**Verbessert; zur Prüfung.** Die knappe ursprüngliche Gliederung, der Verweis auf
„Meine Qualifikationen“, der Erhalt importierter Nachweise beim Trennen und die
Abgrenzung von Ressourcenfreigaben waren brauchbar und bleiben erhalten.

- Einstieg auf **Kontoeinstellungen** präzisiert; Lese- und Änderungsrechte getrennt.
- Die zwei vorhandenen Tabs und ihre unterschiedlichen Abläufe beschrieben:
  Anbieterweiterleitung mit Rückkehr und anschließendem Abruf sowie persönlicher
  Token mit Eigentumsprüfung. Die Tokenverknüpfung aktiviert keinen Import.
- Erneutes Anmelden, Kontowechsel erst nach Trennen und Beibehalten/Ersetzen eines
  persönlichen Tokens ergänzt. Die Importzahl bezeichnet verarbeitete Einträge,
  nicht zwingend neue Nachweise. Einzelne Fehler löschen erfolgreiche Importe nicht.
- Trennaktion und ihre Folgen mit aktuellen UI-Namen erläutert; deaktivierte
  Anbieter, fehlende Anbieter, geänderte Verbindungen und fehlerhafte persönliche
  Angaben als kurze Fehlerhilfe beschrieben.
- `bilder/profil-nachweisquellen.png` selbst angesehen: Es zeigt den früheren
  Aufklapper, die Schrittleiste und Auswahlkarten. Die aktuelle UI verwendet Tabs.
  Daher die Einbindung entfernt; die Bilddatei bleibt unverändert. Ein aktuelles
  Bild wäre für den Unterschied der Verbindungsmethoden nützlich.

## Konkrete Quellen

Pfade relativ zum Software-Repository, Stellen aus dem aktuellen Arbeitsstand:

| Aussage                                                         | Quelle                                                                                                                                                                                                                                                                                                                                                         |
| --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Kontomenü und Profilnavigation                                  | `web/components/layout/common/account-menu-items.tsx:23`, `web/locales/de/navigation.json:32`, `web/components/layout/settings/profile-nav.config.ts:172`                                                                                                                                                                                                      |
| Profil-Leseschutz und Änderungsrechte                           | `web/components/integrations/openbadges/openbadges-navigation.tsx:36`, `web/components/integrations/openbadges/profile-provider-connections.tsx:70`; Backend: `api/Service/Interoperability/Boundary/ProfileBadgeProvidersController.cs:22`, `:26`, `:43`, `:49`, `:59`; `api/Service/OpenBadges/Boundary/ProfileOpenBadgesLinkController.cs:24`, `:37`, `:55` |
| Weiterleitung und Abschluss bei Rückkehr                        | `web/components/integrations/openbadges/profile-provider-connections.tsx:87`, `:117`; `api/Service/Interoperability/Application/BadgeOAuthConnectionService.cs:35`, `:55`, `:75`                                                                                                                                                                               |
| Tabs, Anbieterstatus, Abruf, Trennbestätigung und Fehlerdetails | `web/components/integrations/openbadges/profile-provider-connections.tsx:167`, `:221`, `:279`, `:294`, `:319`; aktuelle deutsche Texte in `web/locales/de/badges.json:351–435`                                                                                                                                                                                 |
| Erneute Anmeldung und Kontowechsel                              | `api/Service/Interoperability/Application/BadgeOAuthConnectionService.cs:79–86`, `:139`; `api/Service/Interoperability/Application/BadgeProviderSynchronization.cs:22–31`                                                                                                                                                                                      |
| Importzahl, einzelne Fehler, Zeitpunkt, identische Nachweise    | `api/Service/Interoperability/Application/BadgeProviderSynchronization.cs:32–64`; `api/Service/Interoperability/Application/BadgeEvidenceExchange.cs:32–48`                                                                                                                                                                                                    |
| Persönliches Formular, Tokens nicht anzeigen, Trennen           | `web/app/[project]/dashboard/user-management/profile/openbadges/page.tsx:62–151`, `web/locales/de/badges.json:43–60`                                                                                                                                                                                                                                           |
| Token behalten/ersetzen, Eingaben bei Fehler erhalten           | `web/app/[project]/dashboard/user-management/profile/openbadges/use-openbadges-link.ts:52–120`; `api/Service/OpenBadges/Application/OpenBadgesUserLinkService.cs:39–115`                                                                                                                                                                                       |
| Separate Importfreigabe und Identitätsprüfung                   | `api/Service/OpenBadges/Boundary/ProfileOpenBadgesLinkController.cs:38`; `api/Service/OpenBadges/Application/OpenBadgesSyncService.cs:34–99`; `api/Service/OpenBadges/Boundary/OpenBadgesSyncController.cs:21`                                                                                                                                                 |
| Bestehende technische Dokumentation zum neuen UI-Stand          | `web/docs/member-portal-layout.md:221–269`; Web-Commit `21d783b7789f2e21ec02b75d7d39f4a20ad75fcf`                                                                                                                                                                                                                                                              |

Es wurden keine API, DTOs, Übersetzungen oder Software verändert; bestehende
Controller-Dokumentation und UI-Muster wurden als Beleg verwendet.

## Prüfungen und Grenzen

- Formatprüfung mit installiertem Prettier und explizitem Umgehen des
  Submodule-Ausschlusses: beide zugewiesenen Dateien bestanden.
- MDX-Kompilierung mit installiertem `@mdx-js/mdx` bestanden. Frontmatter mit
  `title` und `description` vorhanden; drei bisherige Abschnittsüberschriften
  unverändert; einziges relatives Seitenlinkziel vorhanden.
- `git -C web/content/docs diff --check -- docs/ueberblick/profil-nachweisquellen.mdx planning/reviews/2026-11-01/ueberblick--profil-nachweisquellen.md`
  ohne Befund.
- Keine eigene Browser-, mobile Darstellungs-, Hardware- oder Anbieterprüfung.
  Die Provideranmeldung, Rückkehr, Tokenprüfung und tatsächlichen Antworten eines
  externen Anbieters bleiben praktisch zu prüfen. Die früheren Prüfungen aus dem
  Web-Commit sind keine eigene Abnahme dieser Revision.
- Kein globaler Build und keine Softwaretests für die reine Inhaltsänderung.
  Gemeinsame Consumer-/Browserprüfung liegt beim Koordinator; Website-Consumer
  wurde nicht ausgeführt.

## Koordination und Dateien

Alle bisherigen Abschnittsüberschriften und die URL bleiben erhalten. Der einzige
Seitenverweis führt weiterhin zur vorhandenen Qualifikationsanleitung. Navigation
und Nachbarseiten wurden nicht verändert. Kein zusätzlicher Seitenbedarf.
Screenshotbedarf: heutige Tabs mit fiktivem Anbieterstatus und persönlichem
Formular; kein echter Token und keine externe Provideraktion nötig für das Bild.

Geändert:

- `web/content/docs/docs/ueberblick/profil-nachweisquellen.mdx`
- `web/content/docs/planning/reviews/2026-11-01/ueberblick--profil-nachweisquellen.md`
