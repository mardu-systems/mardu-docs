# N03: Lernwegteilnahmen begleiten

## Änderungsbrief und Entscheidung

- Leserfrage: Wie ordne ich eine Person einem vorhandenen Lernweg zu, lese ihren
  Fortschritt und bestätige den Abschluss oder beende die Teilnahme?
- Vorwissen: Die koordinierende Person kennt die Person und die Erwerbskriterien
  der einzelnen Badges. Sie braucht keine Kenntnisse der API-Felder.
- Ergebnis: Eine gespeicherte Teilnahme mit unveränderten Anforderungen und
  nachvollziehbar eingeordnetem aktuellem Fortschritt; eine ausdrücklich
  abgeschlossene oder abgebrochene Teilnahme.
- Entscheidung: **Belegbare Teildokumentation / offene Prüfung**. Eine eigene
  Nutzeraufgabe ist vorhanden. Die neue Seite behandelt ausschließlich den Alltag
  mit vorhandenen Lernwegen; lokale Vergabe, Erneuerung und Widerruf bleiben unter
  `docs/administration/badges-verwalten.mdx#vergaben-und-lernwege` kanonisch.
- Heimatbereich: Koordination. Titel wird gegenüber dem Plan auf
  „Lernwegteilnahmen begleiten“ eingegrenzt, der zugewiesene Dateipfad bleibt.
- Vorgehen: Vorhandene Anleitungen und UI/Backend-Verträge abgleichen, kurze
  Aufgabenanleitung mit bestehenden Markdown-Mitteln schreiben, Format und
  relative Verweise prüfen. Navigation und Consumer-Darstellung prüft der
  Koordinator. Keine Softwareänderung und keine echten Vergaben.

## Belegte Aussagen und Quellen

Alle folgenden Pfade sind relativ zur Software-Repository-Wurzel.

| Aussage                                                                                                                                                                                | Quelle                                                                                                                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Badge-Vergaben sind bereits ausreichend beschrieben; keine Wiederholung der Vergabe-/Erneuerungs-/Widerrufsschritte                                                                    | `web/content/docs/docs/administration/badges-verwalten.mdx`, Abschnitte „Voraussetzungen und Rechte“ und „Vergaben und Lernwege“; `docs/koordination/bewertungen.mdx` verweist bereits darauf                                                            |
| Menü „Kompetenzen → Lernwege“ und Leserecht für Kompetenzen                                                                                                                            | `web/components/layout/sidebar/dashboard-navigation.ts:105–120`; Route `web/app/[project]/dashboard/competencies/learning-paths/page.tsx`; `web/components/competencies/shared.tsx:25–49`                                                                |
| Detailansicht enthält Beschreibung, erforderliche Anzahl, enthaltene Badges, optionales Abschluss-Badge und „Teilnahmen“                                                               | `web/components/competencies/learning-paths.tsx:186–287`                                                                                                                                                                                                 |
| Zuordnung, Personenauswahl, Speichern; Liste und Detail mit Zahl, Status und Lernwegversion; Abschluss/Abbruch mit unterschiedlichen Rechten                                           | `web/components/competencies/path-enrollments.tsx:34–268`; `web/components/competencies/shared.tsx:156–219`; `web/components/access/access-entity-picker.tsx:112–137`                                                                                    |
| Exakte deutsche UI-Bezeichnungen                                                                                                                                                       | `web/locales/de/badges.json:499–522`, `web/locales/de/common.json:31`; Status-/Menütitel unter `web/locales/de/competencies.json`                                                                                                                        |
| Lesen = View, Zuordnen = Create, Abschluss = Approve, Abbruch = Update für Competencies                                                                                                | `api/Service/Competencies/Boundary/HttpControllers/LearningPathsController.cs:29–68`; Frontend-Gegenstück `web/components/competencies/shared.tsx:25–34`                                                                                                 |
| Vorhandene Person, aktiver Lernweg, keine zweite offene Teilnahme; Anforderungen und Abschluss-Badge-Version werden bei Zuordnung gespeichert                                          | `api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs:58–80`; `api/Service/Competencies/Entity/LearningPathEnrollment.cs:8–23`                                                                                                    |
| Fortschritt zählt unterschiedliche aktuell wirksame lokale Badges der Person aus der gespeicherten Auswahl, unabhängig vom Vergabezeitpunkt und der aktuellen Badge-Inhaltsversion     | `api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs:142–153`; `api/Service/Competencies/Application/Services/BadgeLearningService.cs:85–86`; Repository lädt lokale Vergaben über `Gateway/BadgeLearningSpecifications.cs:8–18` |
| Abschluss nur für offene Teilnahme mit erreichter Mindestanzahl; gespeicherte Abschluss-Badge-Version, keine doppelte wirksame Vergabe; Abschluss-Badge muss noch aktiv und lokal sein | `api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs:91–118`; `api/Service/Competencies/Application/Services/BadgeLearningService.cs:77–83`                                                                                      |
| Abschluss bleibt historisch, auch wenn aktueller Fortschritt später sinkt; keine automatische Rücknahme                                                                                | `api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs:142–153`; `LearningPathsController.cs`, XML-Beschreibung der Teilnahmeabfrage                                                                                               |
| Abbruch nur für offene Teilnahme, Historie und vorhandene Badges bleiben; erneute Zuordnung nach Abschluss/Abbruch möglich                                                             | `api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs:65–67,120–131`; Abbruchänderung setzt nur `CancelledAtUtc` und `Version`                                                                                                    |

## Praxisgrenzen und Produktbefunde

- Nur Codelektüre und Dokumentprüfungen; keine Browser-, Hardware- oder
  Anbieterprüfung und keine laufenden Tests. Vorhandene Tests wurden als ergänzende
  Quelle gelesen, nicht ausgeführt: `service.Test/Competencies/BadgeLearningRulesTests.cs:31–52`
  und `BadgeLearningPostgresTests.cs:45–98` belegen unter anderem getrennte Personen,
  eingefrorene Anforderungen, Abschlussversion und fehlende Credential-/Zugriffsvergabe.
- Die Teilnahmeansicht nennt die gespeicherte Lernwegversion, zeigt aber keine
  vollständige historische Anforderungsliste und kein gespeichertes Abschluss-Badge.
  Deshalb beschreibt die Seite keine solche Ansicht. Bei zwischenzeitlich geänderten
  Lernwegen ist die historische Zuordnung derzeit nicht vollständig im Dialog prüfbar.
- UI bietet „Notiz zur Entscheidung“ für beide Aktionen; `CancelAsync` verwirft
  diese Notiz. `CompleteAsync` verwendet sie nur bei neu erzeugtem Abschluss-Badge,
  nicht bei bereits wirksamem oder fehlendem Abschluss-Badge. Teilnahmeentität und
  Teilnahme-DTO haben kein Notizfeld. Keine Zusage eines Entscheidungsverlaufs in der
  Produktseite; Softwarebefund separat prüfen.
- `badgeLearning.peopleOverviewHint` verspricht Verwaltung von Vergaben,
  Fortschritt und Erneuerungen im Benutzer-Sheet. Tatsächlich rendert
  `web/app/[project]/dashboard/user-management/users/dialog/edit-user-sheet.tsx:704–715`
  dort `CompetencyGrants`; `PathEnrollments` wird ausschließlich aus dem Lernweg-
  Sheet eingebunden. Deshalb keine entsprechende Bedienanleitung über „Personen“.
- Neue Zuordnung wird auf einem inaktiven Lernweg im Frontend weiterhin angeboten,
  der Server lehnt sie ab. Die Anleitung nennt den aktiven Lernweg als Voraussetzung.
- Es gibt in dieser UI keine Selbstregistrierung, Einladungs-, Dokumentupload- oder
  automatische Credential-Anerkennung für Teilnahmen. Die dokumentierte Registrierung
  ist die Zuordnung eines vorhandenen Benutzerkontos durch eine berechtigte Person.
- Offen für den Koordinator: im Consumer Desktop/Mobil das Finden des Lernwegs,
  Personenauswahl, Speichern, Aktualisieren, Abschluss/Abbruch und Rückfrage mit
  fiktiven Testdaten prüfen; keine echten Vergaben auslösen. Kein Hardware-/Provider-
  Test für diesen lokalen Ablauf erforderlich.

## Querverweise und geänderte Dateien

- Neue Produktseite: `docs/koordination/vergaben-lernwegteilnahmen.mdx`.
- Dieser Bericht: `planning/reviews/2026-11-01/koordination--vergaben-lernwegteilnahmen.md`.
- Bestehende APIs, Rechte, Statusübersetzung und Markdown-Tabellen wiederverwendet;
  keine API-/DTO- oder Softwareänderung und daher keine geänderte API-Dokumentation.
- Navigation durch Koordinator ergänzen. Sinnvolle eingehende Verweise:
  Koordination-Start und `administration/badges-verwalten.mdx#zugehoerige-lernwege-ansehen`.
  Die geplante Einrichtungsseite N06 kann auf die Teilnahme-Anleitung verweisen;
  kein Link auf eine noch nicht angelegte Nachbarseite gesetzt.

## Eigene Checks

- Prettier mit vorhandener Web-Konfiguration, expliziten beiden Dateipfaden und
  `--ignore-path /dev/null`: zunächst Formatabweichungen erkannt, anschließend
  beide Dateien formatiert und `--check` erfolgreich (0 Fehler).
- Neue MDX-Datei mit vorhandenem `@mdx-js/mdx` kompiliert: Syntaxprüfung erfolgreich.
  Dies ist kein Consumer-Rendering.
- Relative Links und Abschnittsziele per lokaler Dateiprüfung geprüft: beide Links
  auf die vorhandene kanonische Badge-Seite und ihren Anker funktionieren.
- Frontmatter mit Titel/Beschreibung, fehlendes zusätzliches H1 und fehlende
  TODO-Schreibaufträge geprüft.
- Inhalt beider zugewiesenen Dateien nach Formatierung gelesen; Whitespaceprüfung
  mit `git diff --no-index --check` gegen `/dev/null` für die neuen Dateien.
- Kein Build, Serverstart, Testlauf, Cacheeingriff, Commit oder externe Mutation.
