# P12: Eigene Sitzungen verwalten

## Änderungsbrief

Leserfrage: Wo bin ich mit meinem Konto angemeldet, und wie beende ich einzelne,
andere oder alle Anmeldesitzungen? Die Anleitung richtet sich an angemeldete
Personen ohne Wissen über Token oder interne Authentifizierungsabläufe. Heimat
bleibt die vorhandene Profilseite unter `ueberblick/profil-sitzungen`; der
Benutzereinstieg bleibt Aufgabe der bestehenden Consumer-Navigation.

Ergebnis: UI-Einstieg, Sitzungsmerkmale, Bestätigung und Folgen des Widerrufs
stimmen mit dem vorhandenen Frontend und Auth-Backend überein. Gute Inhalte,
URL, Überschriftenanker und Beispielbild bleiben erhalten. Geplant ist ein
kleiner Textpatch für Kontoeinstellungen, aktuelle Sitzung, Ansichten und
Widerrufswirkung. Prüfungen erfolgen statisch und dateibezogen; Browserprüfung
und eine Prüfung mit ausschließlich dafür angelegten Testanmeldungen bleiben
beim Koordinator. Es werden keine echten Sitzungen widerrufen.

## Entscheidung und Befunde

**Verbessert; zur Prüfung, keine praktische Abnahme.** Die bisherige Anleitung
war kurz und bereits weitgehend brauchbar. Nach Verdichtung der Aktionsbeschreibung
wurden die belegten Lücken ergänzt:

- Einstieg auf **Kontoeinstellungen** korrigiert; direkter Einstieg **Aktive
  Sitzungen** bleibt erhalten. Umfang sind eigene Anmeldesitzungen des aktuellen
  Servers, keine Zutritts- oder Maschinensitzungen.
- Aktuelle Sitzung mit **Aktuell** und deaktiviertem **Dieses Gerät** erklärt.
  Das ist ein Schutz der Oberfläche; der Einzelwiderruf-Endpunkt verbietet die
  eigene aktuelle Sitzung nicht. Die Anleitung behauptet keinen API-Schutz.
- Desktop-Tabelle mit Sortierung, mobile Liste und Hilfe bei leeren Filtertreffern
  ergänzt. Fehlende Standortangaben werden eingeordnet.
- Bestätigung für Einzel-, andere und alle Sitzungen ergänzt. Folgen stehen
  sichtbar vor der Auswahl; **Alle abmelden** enthält den nötigen Hinweis auf den
  anschließenden Anmeldeweg. Der Kontomenü-Weg zum Abmelden des aktuellen Browsers
  ergänzt die deaktivierte Einzelaktion.
- Falsche pauschale Aussage entfernt, dass Zugriffstoken nach Widerruf bis zum
  Ablauf weitergelten. Die Middleware prüft die Sitzungskennung auch bei
  API-Anfragen und lehnt widerrufene Sitzungen ab. Der Text verspricht kein
  sofortiges Verschwinden einer schon geöffneten Ansicht.
- Profilrechte, IP-/Standortgrenzen, Sicherheitsverweis, Fehlerhilfe und Hinweis
  auf unveränderte Zutrittsmedien bleiben erhalten. Die bestehenden Aktionen
  ändern Refresh-Token-Sitzungen, keine Zutrittsmedien.
- Vorhandenes Bild visuell gelesen: fiktive Adressen `192.0.2.10`/`.20`, aktuelle
  Sitzung, Filter und Aktionen passen zur Erklärung. Es ist ein Bestandsbild,
  kein Nachweis einer aktuellen Browserprüfung. Kein neues Asset erforderlich.

## Quellen

Pfade beziehen sich auf das übergeordnete Software-Repository:

- `web/components/layout/common/account-menu-items.tsx:20–48,88–99`:
  Kontoeinstellungen, direkte Sitzungsnavigation und Abmeldung.
- `web/locales/de/navigation.json:24–32,75,95` und
  `web/locales/de/account.json:58–120`: genaue deutsche UI-Bezeichnungen,
  Dialogtexte, Leerzustand und Filter.
- `web/lib/profile-navigation.ts:3–16` sowie
  `web/app/[project]/portal/profile/sessions/page.tsx:1`: derselbe Sitzungsinhalt
  in Benutzer- und Verwaltungsansicht, kontextabhängige Profilnavigation.
- `web/app/[project]/dashboard/user-management/profile/sessions/page.tsx:96–121`:
  Suche und Sortierung; `:124–151`: Nachladen bzw. lokale Abmeldung nach Erfolg;
  `:174–240`: bestätigte Sammelaktionen, deaktiviert ohne andere Sitzungen;
  `:299–349,351–479`: mobile Liste und Desktop-Tabelle;
  `:491–523`: deaktiviertes **Dieses Gerät** und bestätigter Einzelwiderruf.
- `api/framework/Infrastructure/Identity/Users/Boundary/ProfileSessionsController.cs:75–108,127–137`:
  eigene Sitzungen, Profil-Leserecht, aktuelle Kennung, optionale Geo-IP-Angabe;
  `:144–207`: Profil-Änderungsrecht, Widerruf der eigenen Sitzungen und
  Ausnahme der aktuellen Sitzung anhand ihres Claims.
- `api/framework/Infrastructure/Identity/Tokens/Specifications/ActiveTokensByUserSpec.cs:8–12`:
  nur nicht widerrufene, nicht abgelaufene Sitzungen der angemeldeten Person.
- `api/framework/Infrastructure/Auth/CurrentUserMiddleware.cs:17–38` und
  `api/framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:61–105,447–466`:
  Gültigkeitsprüfung, Ablehnung und Cache-Invalidierung nach Widerruf.
- `web/services/auth/clientSession.ts:224–268`: kontobezogene lokale Abmeldung,
  versuchter Backend-Widerruf und Weiterleitung zur Anmeldung.
- `service.Test/Framework/Identity/TokenServiceRevocationTests.cs:17–45`:
  vorhandener Regressionstest für Cache-Invalidierung nach gespeichertem
  Widerruf. Nur gelesen, nicht ausgeführt.

## Prüfungen und offene Grenzen

Ausgeführt und erfolgreich:

- Lokales `web/node_modules/.bin/prettier --check` für beide eigenen Dateien,
  mit `web/.prettierrc` und `--ignore-path /dev/null`, da der Consumer das
  Dokumentations-Submodule sonst ausschließt.
- MDX-Kompilierung der Produktseite mit dem vorhandenen `@mdx-js/mdx` über Bun;
  dies prüft die Syntax, ersetzt keine Consumer-Darstellung.
- Dateibezogene Prüfung von Frontmatter, relativem Seitenlink und Bilddatei;
  alle bisherigen H2-Überschriften stimmen mit `HEAD` überein.
- `git -C web/content/docs diff --check` für die eigenen Pfade und Durchsicht
  des Seitendiffs.

Kein Build, kein Serverstart und keine echten Sitzungsaktionen. Keine automatisierten
Verhaltenstests ausgeführt, da ausschließlich Dokumentation geändert wurde.

Der Koordinator soll die Seite im Software-Consumer und im Website-Consumer
rendern. Desktop und Mobilansicht, Bilddarstellung, Tabelle, Links und
Tastaturbedienung prüfen. Mit zwei eigens dafür angelegten Testanmeldungen kann
anschließend geprüft werden: aktuelle Sitzung bleibt bei **Andere abmelden**
erhalten; **Dieses Gerät** ist deaktiviert; Bestätigungen lassen sich abbrechen;
widerrufene Anmeldung scheitert beim folgenden API-Zugriff; **Alle abmelden**
führt zur Anmeldung. Für reine Darstellung keine vorhandenen echten Sitzungen
widerrufen. Unterschiedliche Anzeige bei Ladefehler und leerem Filterergebnis
ebenfalls prüfen. Keine Hardware- oder Anbieterprüfung erforderlich.

Möglicher Software-Folgepunkt: Die Sitzungsseite prüft Profil-Änderungsrechte
nicht vor dem Anzeigen der Widerrufsaktionen; das Backend erzwingt diese Rechte.
Eine nur leseberechtigte Testperson sollte den vorgesehenen Fehlerzustand prüfen.
Die Dokumentation benennt die benötigten Rechte, ohne unsichtbare Aktionen zu
versprechen. Keine Softwareänderung in diesem Auftrag.

## Verweise und Dateien

URL und alle bestehenden Überschriftenanker bleiben erhalten. Der relative Link
zu `./profil-sicherheit.mdx` und das bestehende Bild bleiben erhalten. Kein neuer
Seitenbedarf, keine Navigationsänderung. Nachbarseiten werden parallel geprüft;
ihre älteren Profilbezeichnungen wurden hier nicht geändert. API/DTO-Vertrag und
seine vorhandene OpenAPI-/XML-Dokumentation wurden nur gelesen.

Geändert werden ausschließlich:

- `web/content/docs/docs/ueberblick/profil-sitzungen.mdx`
- `web/content/docs/planning/reviews/2026-11-01/ueberblick--profil-sitzungen.md`
