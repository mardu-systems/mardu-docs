# P43: Bewertungen

## Änderungsbrief

Leserfrage: Wie finde und entscheide ich eine bestehende Kompetenzprüfung oder einen
Kompetenzvorschlag, und wie unterscheide ich dies von einem importierten Credential?
Leser kennen die zu prüfende Person und die am Standort verlangte Fähigkeit, aber
nicht die getrennten Nachweisarten. Ziel ist ein nachvollziehbar geprüfter Vorgang
mit Ergebnis und aktueller Gültigkeit. Heimatbereich bleibt Koordination;
kanonische Seite bleibt `docs/koordination/bewertungen.mdx`.

Die bisherige Seite enthält ausschließlich Schreibaufträge. Ihre URL und vier
Abschnittsanker bleiben erhalten. Die Überarbeitung beschreibt nur vorhandene
Prüfungen, Kompetenzvorschläge und ihre Grenzen; Badge-Vergaben bleiben in der
vorhandenen Administrationsanleitung. Quellen sind Komponenten, Übersetzungen,
Controller, DTOs, Dienste und Spezifikationen. Geplant sind Format-, Link- und
MDX-Prüfungen für diese Dateien; angemeldete Browser-/Providerprüfung und die
Veröffentlichungsentscheidung verbleiben beim Koordinator. Es werden keine
Kompetenzentscheidungen ausgeführt.

## Entscheidung und Änderungen

**Belegbare Teildokumentation / offene Prüfung**, Arbeitsstand **zur Prüfung**.
Die leere TODO-Seite ist durch eine nutzbare Anleitung ersetzt. Erhalten sind URL
und die vier ursprünglichen Abschnittsüberschriften/Anker; gute ausgearbeitete
Inhalte oder Bilder gab es zuvor nicht.

- Einstiegsweg über Kompetenzeinstellungen und tatsächliche Arbeitsliste mit
  offenen/allen Vorgängen, Suchfeld und fähigkeitsbezogener Auswahl beschrieben.
- Fähigkeit, Katalog, Einweisung, Kompetenznachweis, Badge-Definition/-Vergabe und
  Credential unterschieden. Kein automatischer Zutritt und keine automatische
  Anerkennung aus einem Credential-Prüfstatus abgeleitet.
- Aktive Richtlinien, Start, zwei manuelle Verfahren, Punktzahl/Mindestpunktzahl,
  optionale Anmerkung, Selbstentscheidungsverbot, Abschluss und Folgewirkung erklärt.
  Kein Frageneditor, Dokument-Upload, Rückfrage-, Frist- oder Vertretungswerkzeug
  behauptet. Die angezeigte Prüferperson ist keine exklusive Bearbeitungszuweisung.
- Genehmigung und aktuelle Gültigkeit getrennt; Nachfrist, Ablauf, Quelle,
  gespeicherte Verlaufsangaben, Widerruf und überschreibbare Anmerkung erklärt.
- Externe Anerkennung als Entscheidung über vorhandenen Kompetenzvorschlag
  beschrieben. Serverweite Synchronisation von persönlichen Credential-Importen
  getrennt; externe Laufzeit wird beim manuellen Genehmigen nicht automatisch
  übernommen. Kein vollständiger Credential-/Signaturdialog in der Arbeitsliste
  behauptet.
- Lokale Badge-Vergabe und Erneuerung bleiben in der vorhandenen Anleitung;
  Anerkennungsregeln und persönliche Quellen werden passend verlinkt. Keine API,
  DTOs, Navigation, Software oder Übersetzungen geändert.

## Quellen (statische Prüfung)

Pfade beziehen sich auf den Software-Repository-Root.

| Aussage                                                      | Quelle und relevante Stellen                                                                                                                                                                                                  |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Einstieg, Einstellungen, Arbeitsbereich                      | `web/components/competencies/workspace.tsx:145–247`; Einstellungen verlinken `view=review`; Übersetzungen `web/locales/de/badges.json:523–524`, `web/locales/de/competencies.json:271–346`                                    |
| Offene/alle Vorgänge, Suche, Filter                          | `web/components/competencies/review-queue.tsx:25–90, 95–190`; nur Pending-Vergaben und nicht abgeschlossene Runs sind offen                                                                                                   |
| Fähigkeiten, Richtlinien und Definitionen                    | `web/components/competencies/library-detail.tsx:85–178`; `web/locales/de/competencies.json:191–253`; benachbarte Anleitung `docs/administration/badges-verwalten.mdx`                                                         |
| Start und Entscheidungsformular                              | `web/components/competencies/assessments.tsx:207–276, 309–497`; `web/lib/competencies/rules.ts:86–96`; aktive Daten, optionaler Score/Anmerkung, explizite untere Bestätigung                                                 |
| Rechte                                                       | `web/components/competencies/shared.tsx:28–40`; `api/Service/Competencies/Boundary/HttpControllers/AssessmentRunsController.cs:26, 36, 47, 66`; `CompetencyGrantsController.cs:26, 37, 47, 63, 76, 89`                        |
| Start, Selbstentscheidung, Verfahren, Version, Ergebnisfolge | `api/Service/Competencies/Application/Services/AssessmentAdministrationService.cs:134–304`; keine Beschränkung auf vorherigen Evaluator; Score, Fristen und optionale Notiz im DTO `Boundary/Dto/AssessmentRunDtos.cs:89–113` |
| Kompetenzvorschlag und Widerrufsformular                     | `web/components/competencies/grants.tsx:254–360, 394–553`; Verlauf ist Metadatenansicht, keine Änderungsereignisliste                                                                                                         |
| Entscheidung, Beginn, Ablauf, Duplikat, Widerruf, Notiz      | `api/Service/Competencies/Application/Services/CompetencyGrantAdministrationService.cs:37–162, 199–245`; `Boundary/Dto/CompetencyGrantDtos.cs:54–120`; lokale Genehmigung liest keine externe Laufzeit                        |
| Aktuelle Gültigkeit und Nachfrist                            | `api/Service/Competencies/Gateway/CompetencyGrantSpecifications.cs:30–47`; `Application/Services/AssessmentEvaluationService.cs:36–69, 123–148`                                                                               |
| Serverweite Synchronisation erzeugt Vorschläge               | `api/Service/OpenBadges/Application/OpenBadgesSyncService.cs:56–96`; `OpenBadgesCompetencyProjectionService.cs:17–93`; `CompetencyTrustService.cs:131–149` prüft aktiven Aussteller und aktive Klassen-/Ausstellerzuordnung   |
| Credential-Prüfung ist eigene Information                    | `web/components/integrations/openbadges/profile-imported-credentials.tsx:26–34, 112–171`; `web/locales/de/badges.json:399–414`; `api/Service/OpenBadges/Application/OpenBadgesCredentialVerificationService.cs:39–88`         |
| Automatische Verfahren und Voraussetzungen                   | `api/Service/Competencies/Application/Services/AssessmentEvaluationService.cs:72–110, 185–240, 275–346`; `SourceCredentialId` muss für das externe Verfahren schon gesetzt sein                                               |

Die Quellen `web/content/docs/AGENTS.md`, `ARBEITSWEISE.md`, der Seitenbrief,
`planning/offene-dokumentationsaufgaben.md` und benachbarte Anleitungen wurden gelesen.

## Prüfergebnis und Grenzen

- Prettier mit vorhandener Installation und ausdrücklich leerem Ignore-Pfad für
  genau die zwei eigenen Dateien: erfolgreich. Die Consumer-Konfiguration ignoriert
  ansonsten das komplette Dokumentationssubmodule.
- MDX mit vorhandenem `@mdx-js/mdx` kompiliert (Frontmatter vor der isolierten
  Kompilierung entfernt): erfolgreich.
- Sechs relative Links auf vorhandene Dateien und ihre angefragten Zielanker geprüft;
  alle vier alten Abschnittsüberschriften weiterhin vorhanden; kein TODO im Produkttext.
- Keine Browser-, Mobil-, Tastatur-, Hardware- oder Providerprüfung durchgeführt.
  Kein globaler Build, keine echten Bewertungen, Vergaben oder Widerrufe ausgeführt.

**Konkrete Prüfgrenze:** In den geprüften Produktionsdiensten existiert kein
Schreibpfad für `CompetencyGrant.SourceCredentialId`; eine repositoryweite Suche
unter `api/Service` und `api/framework` fand Modell/Mapping, Lesepfade und
Widerrufskaskade, keine Zuweisung. Das externe automatische Verfahren verlässt die
Auswertung ohne verknüpfte Credential-ID (`AssessmentEvaluationService.cs:277–279`).
Eine funktionierende persönliche OB3-Import→lokale Anerkennungs-Verknüpfung darf
deshalb nicht aus dem vorhandenen Formularangebot abgeleitet werden. Kein
Softwarefehler im Rahmen dieser Dokumentationsaufgabe behoben; Integrationspfad
gesondert praktisch/technisch klären.

## Publikationsvorschlag und Übergabe

Nach gemeinsamer Render-/Navigationsprüfung als abgegrenzte Anleitung zu Prüfungen
und Kompetenzvorschlägen in Koordination anbieten. Die Seite behauptet keine
vollständige Katalogpflege oder universelle Credential-Anerkennung. Für praktische
Abnahme sind eine geeignete Testperson, genehmigungsberechtigter zweiter Benutzer,
aktive Richtlinien für Bestätigung/Online-Prüfung und ein externer Pending-Vorschlag
nötig. Prüfen: Einstieg, beide Entscheidungsarten, Selbstentscheidung, optionale
Notizen, Gültigkeit/Verlauf und Darstellung ohne vorhandene Nachweise. Produktive
Kompetenzentscheidungen sind dafür nicht erforderlich; Fixtures/Testinstallation
verwenden.

Koordinator: Veröffentlichungsliste/Navigation und bisherige Aussage auf
`docs/koordination/index.mdx:39` gemeinsam bewerten. Von bestehenden
Administrationsseiten führen bereits Links auf diese URL. Keine Navigation im
Seitenauftrag verändert.

**Gesonderte Anleitungen:** Die lokale Badge-Vergabe, Erneuerung und Widerruf sind
bereits unter `administration/badges-verwalten.mdx#vergaben-und-lernwege` beschrieben;
diesen Ablauf nicht erneut auf der Bewertungsseite pflegen. Für Teilnahme an
Lernwegen, Fortschritt und Abschluss-Badge besteht ein eigener Anleitungsbedarf
(`web/components/competencies/path-enrollments.tsx`, `learning-paths.tsx`,
`api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs`).
Dieser wurde nicht als scheinbar unterstützte Bewertungsfunktion ergänzt.
Katalogpflege/Import/Versionen benötigen ebenfalls eine separate vollständige
Anleitung, falls dies nicht durch einen anderen Seitenauftrag gedeckt wird.

Geänderte Dateien:

- `web/content/docs/docs/koordination/bewertungen.mdx`
- `web/content/docs/planning/reviews/2026-11-01/koordination--bewertungen.md`
