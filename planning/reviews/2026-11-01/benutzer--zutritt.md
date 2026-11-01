# Seitenrevision P03: Zugänge & Ressourcen

## Änderungsbrief

- Seite: `docs/benutzer/zutritt.mdx`; Heimatbereich Benutzer.
- Leserfrage: Welche Ressourcen und eigenen Freigaben kann ich sehen, welche Bedingungen gelten und wie finde ich eine anforderbare Ressource?
- Vorwissen: angemeldetes Konto, keine Kenntnisse über Zugangsbereiche oder interne Verträge.
- Ergebnis: eigene zeitliche Zuordnung und Katalogangebot unterscheiden, Mediumbindung erkennen und die passende Folgeanleitung finden.
- Plan nach Codelektüre: bestehende drei Abschnitte und Anker erhalten; getrennte Leserechte, Mediumbindung und Katalogstatus präzisieren; Fehlerhilfe um belegte Ausblendungsgründe ergänzen. Keine Verwaltungsabläufe duplizieren.
- Prüfungen: statischer Abgleich von UI, Übersetzungen, Services und Spezifikationen; vorhandene Bilder ansehen; seitenbezogene Format-, MDX- und Linkprüfung. Browser-/Hardwareprüfung übernimmt der Koordinator.

## Entscheidung

**Verbessert; zur Prüfung.** Die Seite bleibt eine Anleitung zum Lesen eigener
Freigaben und zum Finden von Ressourcen. Keine praktische Abnahme behauptet.

## Befunde und Änderungen

- Profil-Leserechte, Katalog-Leserechte und zusätzliche Anfragerechte getrennt genannt.
- Aussage über direkte, Gruppen- und Medienfreigaben erhalten; aktuelle Gruppenzugehörigkeit und Bindung an das angegebene Medium präzisiert. Medienstatus und Mediengültigkeit zusätzlich zur Freigabe prüfen.
- Gültigkeitszeitraum und Wochenzeitfenster bleiben erhalten. Ergänzt: „Keine wöchentliche Einschränkung“ hebt den Zeitraum nicht auf; „Stand“ nennt den Prüfzeitpunkt, „Neu laden“ wertet erneut aus.
- Katalogschritte auf vorhandene Suche nach Ressourcennamen, Seitennavigation und UI-Felder „Benötigter Zugang“ / „Erforderliche Einweisungen“ abgestimmt. „Details“ zeigt keine vollständige Zugriffsentscheidung und keine zusätzliche Konfiguration, sondern die einzelne Katalogkarte mit Hinweis.
- „Verfügbar“ als Betriebsstatus von persönlicher Freigabe, Buchung und offenem Antrag unterschieden. Keine Zusage über Tür-, Maschinen- oder persönliche Berechtigungszustände.
- Fehlende Katalogeinträge und fehlende Anfrageaktion anhand der tatsächlichen Filter erläutert; eigene Freigaben können auch für verborgene oder deaktivierte Zugänge sichtbar bleiben. Frühere Gruppen-/Medienzuordnungen und gelöschte Freigaben werden nicht als dauerhafter Verlauf versprochen.
- Gute Abgrenzung zeitlicher Freigabe gegenüber Einweisung, Buchung, Aufsicht und Medium erhalten. Bestehende Folgeanleitungen zu Anträgen, Medien und Fehlerhilfe weiterverwendet; Qualifikationsseite im Nutzungskontext verlinkt.
- Nach Sichtprüfung der alten Bilder und Rücksprache mit dem Koordinator drei veraltete Bildverweise samt Bildunterschriften entfernt. Assets bleiben unverändert; Ersatzbilder benötigen einen aktuellen UI-Zugang.

## Quellen

Pfade relativ zum Software-Repository; Zeilen beziehen sich auf den gelesenen Stand.

| Aussage                                                                                      | Quelle und relevante Stelle                                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Getrennte Leserechte, persönliche Abschnitte                                                 | `web/components/portal/portal-resources.tsx:50–62`; `api/Service/Accesses/Boundary/HttpControllers/ProfileAccessGrantsController.cs:34`; `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessCatalogController.cs:24,35`          |
| Aktuelle Benutzergruppen und aktuell eigene Medien, kein Gültigkeitsfilter der eigenen Liste | `api/Service/Accesses/Application/Services/ProfileAccessGrantService.cs:41–65`; `api/Service/Accesses/Gateway/ProfileAccessGrantsSpecification.cs:21–28`                                                                                   |
| Herkunft, Medienstatus/-gültigkeit, Stand, Suche, Neu laden, Seiten                          | `web/components/portal/profile-access-grants.tsx:39–97,110–171`; UI-Texte `web/locales/de/resources.json:477–520`; `web/locales/de/common.json:43,52`                                                                                      |
| Zeitstatus und Grenze zur Entscheidung                                                       | `web/lib/access/profile-grant-presentation.ts:3–15`; `api/Service/Accesses/Boundary/Dto/ProfileAccessGrantDto.cs:4–17`                                                                                                                     |
| Zeitzone, über Mitternacht, fehlende Wochenbeschränkung                                      | `web/components/access/access-grant-schedule.tsx:19–36`; `api/Service/Accesses/Application/Services/AccessGrantScheduleEvaluator.cs:7–31`                                                                                                  |
| Katalogkarte, Ort, Status, Zugangsvoraussetzung, Einweisung, Details-Hinweis                 | `web/components/access/access-catalog-presentation.tsx:33–105`; `web/components/access/resource-catalog-workspace.tsx:237–258,293–321`; UI-Texte `web/locales/de/resources.json:22–24,94–99`, `web/locales/de/access.json:489–516,607–609` |
| Katalogfilter und Suche                                                                      | `api/Service/Accesses/Gateway/ResourceAccessSpecifications.cs:319–348` (nur AccessEnabled und nicht Hidden; Suche nach Name)                                                                                                               |
| Freigabe-/Buchungsnachweise, Antragsgründe, Anfragbarkeit                                    | `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:62–128,403–412`; `web/components/access/resource-catalog-workspace.tsx:137–142,253–265`                                                                         |
| Verfügbarkeit = Betriebsstatus einschließlich Hierarchie und Sperren                         | `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:98–124`; `api/Service/ManagedResources/Application/Services/ResourceOperationServices.cs:257–298`                                                               |

## Checks und Grenzen

- Regeln und Nachbaranleitungen gelesen; relevante UI-/Backend-Quellen statisch abgeglichen.
- Alle drei bisherigen PNGs mit dem Bildwerkzeug angesehen; keine Browser- oder Hardwareprüfung daraus abgeleitet.
- Seitenbezogene Formatierung mit `bun fmt --ignore-path=/dev/null` (der Consumer ignoriert das Doku-Submodule standardmäßig).
- MDX mit vorhandenem `@mdx-js/mdx` und `remark-gfm` kompiliert; erfolgreich.
- Frontmatter, relative Seitenziele und drei unveränderte Überschriften automatisch gegen den vorherigen Git-Stand geprüft; erfolgreich. Nach Entfernen der Bilder vier Seitenverweise, keine Bildverweise.
- `git -C web/content/docs diff --check`; erfolgreich. Keine Softwareänderung, kein globaler Build, keine Tests verändert.
- Offen beim Koordinator: Consumer-Rendering, Markdown-/Agentenausgabe, Navigation und angemeldete Desktop-/Mobilprüfung mit direkten, Gruppen- und Medienfreigaben sowie unterschiedlichen Anfragestatus. Keine Hardware-/Providerabnahme durchgeführt.

## Folgearbeit für den Koordinator

- Aktuelle Aufnahmen für `docs/benutzer/bilder/freigaben.png`, `ressourcenkatalog.png` und `ressource-mobil.png` erstellen, falls Bilder weiter benötigt werden. `freigaben.png` enthält „Holzwerkstatt · enter“, während `profile-access-grants.tsx:121` nur den Ressourcennamen zeigt. Die Katalogbilder enthalten „Betreten“ / „Bedienen“ und alte Begriffe „Vergabe oder Buchung“; `ResourceCatalogCard` zeigt keine solche Aktion und verwendet die aktuellen Übersetzungen „Zugriffsvergabe …“. Außerdem zeigt das alte Beispiel „Eine Freigabe ist erforderlich“, das die aktuelle `ListCatalogAsync`-Gründeliste dort nicht erzeugt. Bilder erst nach aktueller Aufnahme erneut einbinden.
- Bestehende Anker `eigene-freigaben-prüfen`, `ressource-im-katalog-finden`, `wenn-etwas-fehlt` und URL bleiben erhalten. Bestehende Nachbarlinks gültig; kein zusätzlicher Seitenbedarf für diese Leserfrage.
- Kleine Abweichung in bestehender technischer API-Dokumentation zur späteren Korrektur: `ProfileAccessGrantsController.cs:29–30` verspricht Such-/Sortierfeld „action code“. Die aktuelle Specification sucht und sortiert Ressourcennamen und Grant-ID, keinen Action-Code. Kein Softwareverhalten geändert.
- Keine bestätigten Produktfehler aus diesem statischen Seitenabgleich.

## Geänderte Dateien

- `web/content/docs/docs/benutzer/zutritt.mdx`
- `web/content/docs/planning/reviews/2026-11-01/benutzer--zutritt.md`

Keine API/DTO-Verträge verändert; bestehende Verträge nur als Beleg verwendet.
