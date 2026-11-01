# N06: Kompetenzen, Kataloge und Lernwege

## Änderungsbrief

- Leserfrage: Wie definiere ich Fähigkeiten und Bereiche, ordne sie in Katalogen und richte daraus beziehungsweise aus vorhandenen Badges einen Lernweg ein?
- Vorwissen: Unterschiede zwischen Definition und persönlichem Nachweis werden erklärt; keine Kenntnis interner DTOs erforderlich.
- Ergebnis: Gespeicherte, wiederauffindbare Definitionen und ein Lernweg mit verständlicher Mindestanzahl, Reihenfolge und Abschlussregel.
- Entscheidung: Eigene Anleitung erforderlich. `administration/badges-verwalten.mdx` ist bereits kanonisch für Badgeassistent, Badge-Voraussetzungen, lokale Badgekopien und Vergaben. `koordination/bewertungen.mdx` behandelt persönliche Nachweisentscheidungen und Anerkennung. Beide erklären die Einrichtung von Fähigkeiten/Katalogen und Lernwegen nicht ausreichend.
- Heimat: Administration; keine zusätzliche Seite für jedes technische Modell.
- Plan: UI, Übersetzungen, Rechte und aktuelle Controller-/Servicepfade abgleichen; nur fehlende Aufgaben ausarbeiten; gemeinsame Badge-/Bewertungsschritte verlinken; beide eigenen Dateien formatieren und Links prüfen.
- Prüfzugang: ausschließlich statische Quellenprüfung. Gemeinsame Consumer-/Browser-/Navigationsprüfung beim Koordinator.

## Befund und Umsetzung

Zur Prüfung: belegbare Teildokumentation, keine praktische Abnahme. Die neue Seite erklärt lokale Fähigkeit/Bereich und Katalog, CASE-Import mit einmaliger Einordnung, lokale Kopien sowie Lernwegerstellung, Bearbeitung, Teilnahme und ausdrücklich bestätigten Abschluss. Mindestanforderungen einzelner Badges bleiben per Ankerlink in der bestehenden Badgeanleitung; Anerkennung bleibt unter Bewertungen.

Wesentliche Grenzen sind sichtbar: Beziehungen übertragen keine Nachweise/Rechte; lokale Kopien sind neue Identitäten; Lernwegreihenfolge ist nur Orientierung; Teilnahmen behalten ihren Anforderungsstand; aktuelle gültige lokale Badgevergaben bestimmen den Fortschritt; Abschluss wird bestätigt und ist historisch. Kein Automatismus für Voraussetzungserfüllung, Credential-Anerkennung oder Ressourcenzugriff wird behauptet.

## Quellen

Alle Pfade relativ zum Software-Repository. Quellen statisch gelesen, keine Daten geändert:

- `web/components/competencies/workspace.tsx`: `WorkspaceSettings` (Einstiege zu Fähigkeitsverwaltung, Katalogerstellung/-import), `LibraryContent` und Lernwegansicht.
- `web/components/competencies/library.tsx`: `CompetencyLibrary` mit Anlegen, Katalogfilter, Inaktivfilter, Katalog öffnen.
- `web/components/competencies/library-detail.tsx`: `CompetencyReadPage`, Bearbeiten, Herkunft, Struktur/Verlauf und lokale Kopie unter Weitere Angaben.
- `web/components/competencies/definitions.tsx`: `DefinitionEditor`, Art/Katalog nur bei Anlage, erforderliche Felder, Aktivstatus, Speichern und schreibgeschützte importierte Inhalte.
- `web/components/competencies/catalogue-editor.tsx`: lokale Metadaten, Pflichtfelder und Aktivstatus.
- `web/components/competencies/frameworks.tsx`: `CatalogueImport` (Dateigrenze, Vorschau, Ergebnis), `CatalogueDetail` (Einträge, Bearbeiten, Export).
- `web/components/competencies/definition-structure.tsx`: `DefinitionSource` (Kopie und Einordnung), `StructureEditor` (Beziehungen).
- `web/components/competencies/learning-paths.tsx`: Liste, Detail, `PathEditor`, Auswahl aktiver Badges, separate lokale Abschlussdefinition, Pfeilreihenfolge und Mindestanzahl.
- `web/components/competencies/path-enrollments.tsx`: Zuordnen, Fortschritt/Status, ausdrücklicher Abschluss, Abbruchbestätigung.
- `web/components/competencies/shared.tsx`: `useCompetencyPermissions`; `web/locales/de/competencies.json`, `web/locales/de/badges.json`: verwendete UI-Namen und Bedeutungshinweise.
- `api/Service/Competencies/Boundary/HttpControllers/CompetenciesController.cs`, `CompetencyCatalogController.cs`, `CompetencyFrameworksController.cs`, `LearningPathsController.cs`: Rechte und Operationsverträge. Der UI-CASE-Import verwendet `case-import` / `ICaseExchangeService`, nicht den älteren Subset-Import unter `import`.
- `api/Service/Competencies/Application/Services/CompetencyService.cs`: eindeutiger Kompetenzcode, aktive lokale Zielkataloge, feste Art/Katalogzuordnung, neue Revision bei Änderung.
- `api/Service/Competencies/Application/Services/CompetencyCatalogService.cs`: fester Katalogcode, Kopie ohne Nachweise, Klassifizierung nur aus Unclassified, Strukturvalidierung.
- `api/Service/Competencies/Application/Services/CaseExchangeService.cs`: vollständige Quellaufbewahrung, noch nicht eingeordnete Definitionen, nicht abgebildete Beziehungen, doppelte Quell-URI wird abgewiesen.
- `api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs`: aktive Referenzen, erreichbare Mindestanzahl, Teilnahme-Snapshot, aktuelle effektive Vergaben, manuell bestätigter Abschluss mit optionaler Vergabe, bestehende gültige Abschlussvergabe wird nicht dupliziert, Abbruch ohne Löschung.
- `api/Service/Competencies/Boundary/Dto/BadgeLearningDtos.cs`, `CatalogDtos.cs`: Grenzen und beschreibende Semantik.
- Bestehende Produktseiten: `administration/badges-verwalten.mdx`, `koordination/bewertungen.mdx`, `benutzer/kompetenzen.mdx`; Bedarf aus `planning/offene-dokumentationsaufgaben.md`, Abschnitt badges-verwalten.

## Prüfungen und offene Grenzen

- `web/node_modules/.bin/prettier --ignore-path /dev/null --write` auf beiden eigenen Dateien; anschließender `--check` erfolgreich. Der ausdrückliche Ignore-Pfad berücksichtigt das sonst im Software-Consumer ausgeschlossene Submodule.
- Lokale Python-Leseprüfung: alle sechs relativen Links und vorhandenen Zielanker aufgelöst; Frontmatter mit Titel/Beschreibung, kein H1 und keine nachgestellten Leerzeichen geprüft.
- `git -C web/content/docs diff --check -- docs/administration/kompetenzen-lernwege.mdx planning/reviews/2026-11-01/administration--kompetenzen-lernwege.md` ohne Meldung; bei den neuen Dateien sind Format-/Leerzeichenprüfung zusätzlich durch die genannten direkten Dateiprüfungen abgedeckt.
- Keine Builds, Serveraktionen, Browserprüfung, externen Anbieteraufrufe oder Datenmutationen ausgeführt.
- Koordinator: neue Seite in Navigation/Consumer-Liste eintragen; Darstellung im Dashboard-Consumer und Website prüfen, einschließlich mobiler Ansicht und Markdown-Ausgabe.
- Praxisprüfung mit fiktiven Daten offen: Katalog und Fähigkeit erstellen/kopieren, CASE-Datei importieren/einordnen, Lernweg speichern/bearbeiten, Person zuordnen, Mindestanzahl und Abschluss/Abbruch prüfen. Dazu keine Hardware nötig; ein fremder Katalog braucht eine geeignete gültige Beispieldatei.

## Querverweise für den Koordinator

- Von Administration-Start sowie badges-verwalten, Abschnitt „Zugehörige Lernwege ansehen“, auf diese neue Seite verlinken.
- Von Bewertungen beim Hinweis zur Fähigkeitsdefinition auf diese Seite verlinken; Entscheidungen bleiben dort kanonisch.
- Keine Links zu noch nicht existierenden Neuseiten aufgenommen. Verweise auf bestehende Badge- und Bewertungsanleitungen geprüft.

## Geänderte Dateien

- `web/content/docs/docs/administration/kompetenzen-lernwege.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--kompetenzen-lernwege.md`

Keine API-/DTO-Dokumentation geändert; keine Software-/Navigationsänderung.
