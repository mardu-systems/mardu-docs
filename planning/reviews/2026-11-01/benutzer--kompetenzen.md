# Seitenrevision P07: Meine Qualifikationen

## Änderungsbrief

Leserfrage: Welche eigenen Einweisungen und Nachweise sind gespeichert, wie lese
ich Status und Gültigkeit, und was bedeutet das für eine Ressourcennutzung?
Die Leser kennen das angemeldete Portal, aber nicht die Trennung zwischen
Kompetenzanerkennung, lokaler Badge-Vergabe und importiertem Credential.
Heimatbereich und kanonische Quelle bleiben `docs/benutzer/kompetenzen.mdx`.

Plan: Gute Dreiteilung, Status-/Datumsangaben, Fehlerhilfe und vorhandene Bilder
erhalten. Nur belegte Lücken schließen: exakte Statusbezeichnung, Download in
der Detailansicht, Prüfung gegenüber Anerkennung und Anforderungen einer
Ressource. Anschließend die beiden eigenen Dateien formatieren und lokale
Verweise/Anker/Bilder prüfen. Gemeinsame Render-/Browserprüfung beim Koordinator;
keine Software-, API-, Navigations- oder Provideränderung.

## Entscheidung und Befunde

**Verbessert; zur gemeinsamen Darstellungsprüfung.** Die Seite war bereits eine
brauchbare Anleitung. Die drei Bereiche, Status-/Gültigkeitsunterscheidung,
erhaltene Vergabehistorie, Quellenverweis und Fehlerhilfe bleiben bestehen.

- Einstieg auf die eigene Portalansicht und die drei Datenarten präzisiert.
- Fallback in der Statustabelle von „Unbekannter Zustand“ auf den vorhandenen
  UI-Text „Status nicht geliefert“ korrigiert. Die Bedeutung einer erneuten
  Prüfung bleibt getrennt von der aktuellen Gültigkeit.
- Lokale Vergaben als in Mardu vergebene Badges bezeichnet; vorhandene
  Seitennavigation mit den tatsächlichen Aktionsnamen beschrieben.
- Bei importierten Nachweisen die gleichzeitige Anzeige „Prüfung bestanden“ und
  „Abgelaufen“ erklärt. „Noch nicht geprüft“/unbekannter Prüfstatus bestätigen
  keine Gültigkeit. Prüfung, Anerkennung und Ressourcenfreigabe unterschieden.
- Downloadablauf berichtigt: „Original herunterladen“ steht erst in der mit
  „Nachweis ansehen“ geöffneten Detailansicht. Wiederholung nach Fehler erläutert.
- Anforderungen einer Ressource beim vorhandenen Ressourcenkatalog verortet.
  Die Portal-Qualifikationsansicht selbst zeigt keinen Anforderungsstatus für
  eine bestimmte Ressource. Ein allgemeiner Eligibility-Endpunkt im Backend
  belegt keine solche Portalaktion.
- Vorhandene Bilder visuell geöffnet und erhalten. Der mobile Ausschnitt zeigt
  die Einweisung und den Beginn der lokalen Nachweise, nicht alle drei Bereiche;
  die gemeinsame Bildbeschreibung entsprechend korrigiert. Keine neue Aufnahme.

## Quellen und relevante Stellen

Alle Pfade beziehen sich auf das Software-Repository, sofern nicht anders angegeben.

| Quelle                                                                                                                                                                       | Beleg                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `web/app/[project]/portal/qualifications/page.tsx:1–5`                                                                                                                       | Route verwendet `PortalQualifications`.                                                                                        |
| `web/components/portal/portal-qualifications.tsx:18–50`                                                                                                                      | Profil-Leserecht; drei eigene, unabhängig geladene Komponenten; keine Anforderungsprüfung.                                     |
| `web/components/competencies/profile-competencies.tsx:16–24, 48–81`                                                                                                          | Statuszuordnung, aktuelle Wirksamkeit, Gültigkeitsbeginn/-ende, nächste Prüfung.                                               |
| `web/locales/de/competencies.json:49–52, 71–73, 339–351`                                                                                                                     | Exakte UI-Bezeichnungen, unbekannter Status, Bereichsnamen und Trennung der Datenarten.                                        |
| `api/Service/Competencies/Boundary/HttpControllers/ProfileCompetenciesController.cs:22–38`                                                                                   | Nur eigene Anerkennungen inklusive ausstehender und früherer Zustände; `Profile.View`; keine Vergabeaktion.                    |
| `api/Service/Competencies/Boundary/Dto/CompetencyGrantDtos.cs:15–27` und `api/Service/Competencies/Gateway/CompetencyGrantSpecifications.cs:31–46`                           | Wirksamkeit hängt unter anderem von Zustand, Gültigkeitsfenster, Widerruf und Nachfrist ab; Ressourcenregeln bleiben getrennt. |
| `web/components/competencies/profile-badge-awards.tsx:16–96`                                                                                                                 | Lokale Vergaben, Datum/Status/Verlauf und 20 Einträge pro Seite.                                                               |
| `api/Service/Competencies/Boundary/HttpControllers/ProfileBadgeAwardsController.cs:20–42` und `api/Service/Competencies/Application/Services/BadgeLearningService.cs:85–103` | Eigene Vergabehistorie; aktuelle Gültigkeit, kein Ressourcenrecht oder Credential-Export.                                      |
| `web/components/integrations/openbadges/profile-imported-credentials.tsx:23–46, 71–76, 103–187, 192–224`                                                                     | Prüfstatus und Ablauf getrennt; Details, Originaldownload, Fehlererhalt und Seitennavigation.                                  |
| `web/locales/de/badges.json:396–416`                                                                                                                                         | Navigationsaktionen, Prüfstatusnamen, Anerkennungshinweis und Downloadbezeichnung.                                             |
| `api/Service/Interoperability/Boundary/ProfileCredentialsController.cs:25–47` und `api/Service/Interoperability/Gateway/ProfileCredentialPageSpecification.cs:10–17`         | Eigene Credentials, keine implizite Kompetenzvergabe; Originalexport; nach Datum sortierte Seiten.                             |
| `web/components/access/access-catalog-presentation.tsx:85–103` und `web/components/access/resource-catalog-workspace.tsx:293–321`                                            | Erforderliche Kompetenzen und Ressourcen-Detailansicht im Portal.                                                              |
| `api/Service/Competencies/Boundary/HttpControllers/QualificationsController.cs:84–90`                                                                                        | Separate Auswertung von Qualifikationsanforderungen mit `Competencies.View`; keine stille Badge- oder Zugangsvergabe.          |
| `web/tests/components/portal-qualifications.test.tsx`                                                                                                                        | Vorhandene Tests für Status/Gültigkeit, Historie, Teilfehler, Details/Download, unbekannte Prüfzustände und Datenisolation.    |

## Ausgeführte Checks und Grenzen

- Vorhandenes Prettier gezielt mit `--ignore-path /dev/null` für beide eigenen
  Dateien ausgeführt; der normale Consumer-Ignore schließt `content/docs` aus.
- MDX mit vorhandenem `@mdx-js/mdx` kompiliert: erfolgreich. Das ist eine
  Syntaxprüfung, kein Fumadocs-/Browser-Render.
- Lokaler Dateiverweis-Check: beide MDX-Seitenziele und beide Bilddateien
  vorhanden; alle fünf bestehenden H2-Überschriften unverändert; Frontmatter
  vorhanden, kein zusätzliches H1. Keine Anker umbenannt oder neue Links ergänzt.
- `bun run test:run tests/components/portal-qualifications.test.tsx` aus `web/`:
  **15 Tests bestanden**. Vorhandener Vitest-Lauf mit gemockten APIs; kein echter
  Providerabruf und keine Prüfung realer Nachweisdateien. Reguläre ignorierte
  Coverage-/JUnit-Ausgaben wurden durch die bestehende Testkonfiguration erzeugt.
- Vorhandene Desktop- und Mobil-PNGs geöffnet und mit den statischen
  Komponenten/Übersetzungen verglichen. Sie sind vorhandene Beispiele und kein
  Nachweis einer jetzt durchgeführten Browserprüfung.

Der Koordinator übernimmt Consumer-Render, mobile Darstellung und gemeinsame
Navigationsprüfung. Eine angemeldete praktische Prüfung mit echten Daten sowie
Nachweisimport, Anbieterprüfung und Dateidownload wurde nicht ausgeführt. Für
diese reine Seitenrevision ist keine Hardwareprüfung erforderlich. Keine
Produktfehler festgestellt; keine zusätzliche Seite oder Navigationsänderung nötig.

## Geänderte Dateien

- `web/content/docs/docs/benutzer/kompetenzen.mdx`
- `web/content/docs/planning/reviews/2026-11-01/benutzer--kompetenzen.md`

Bestehende Portal-Komponenten, Übersetzungen, API-/DTO-Dokumentation und
MDX-/Bildmuster wurden als Quellen wiederverwendet. APIs und DTOs unverändert;
keine API-Dokumentation angepasst.
