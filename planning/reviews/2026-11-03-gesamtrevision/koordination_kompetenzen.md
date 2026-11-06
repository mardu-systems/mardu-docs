# Prüfbericht Koordination und Kompetenzen · 2026-11-03

## Änderungsbrief

Die sechs zugewiesenen Anleitungen und die zusätzlich beauftragte Trennung der Badge-Vergaben sollen Personen mit vorhandenen Kompetenz- oder
Integrationsrechten zu Definition, Prüfung, lokaler Vergabe, Lernwegabschluss und
Antragsentscheidung führen. Gute bestehende Inhalte bleiben erhalten. Der Abgleich
nutzt aktuelle UI-Komponenten, deutsche Übersetzungen, Controller, DTOs und Services.
Doppelte Abläufe werden an ihre kanonische Anleitung verwiesen; native Fumadocs-
Steps, Callouts und ImageZoom dienen Orientierung und sichtbaren Folgen. URLs und
vorhandene Abschnittsanker bleiben erhalten. Keine API- oder Softwareänderung.

Prüfumfang dieses Pakets: Codelektüre und gezielte Dokumentprüfungen. Zentral
bereitgestellte Browser- und Screenshot-Belege werden getrennt protokolliert;
externe Anbieter, Hardware und reale Berechtigungswirkung sind nicht abgenommen.

## Einzelprüfung

### `koordination/bewertungen.mdx`

- Entscheidung: Gute detaillierte Anleitung erhalten. Datenarten als Vergleichstabelle
  lesbar gemacht, Abschlussfolge vor der Prüfentscheidung sichtbar hervorgehoben.
- Quellen: `web/components/competencies/{workspace,review-queue,assessments,grants,library-detail,policies}.tsx`,
  `web/locales/de/competencies.json`,
  `api/Service/Competencies/Boundary/HttpControllers/{AssessmentRunsController,CompetencyGrantsController}.cs`,
  `api/Service/Competencies/Application/Services/{AssessmentAdministrationService,CompetencyGrantAdministrationService}.cs`.
- Bestätigt: offene und historische Vorgänge, manuelle Verfahren, keine Selbstentscheidung,
  Punktzahlgrenzen, optionale Anmerkung und Ablaufzeit, getrennte Entscheidung/Gültigkeit.
  Import ist keine Anerkennung; externe Laufzeit wird bei manueller Genehmigung nicht übernommen.
- Browser: Eigenen manuellen Kompetenzvorschlag für **Ines Besuch / Holz-Grunderweisung**
  angelegt, als ausstehend gelesen, genehmigt (danach **Derzeit gültig**) und widerrufen.
  Wieder geöffnet: **Entscheidung Genehmigt**, **Nachweisstatus Widerrufen**, **Derzeit nicht gültig**.
  Aktuelle Aufnahme `docs/koordination/bilder/kompetenznachweis-entscheidung-gueltigkeit-aktuell.png`
  eingebunden und visuell geöffnet. Der ursprüngliche Seed-Vorschlag von Marco Stein blieb unverändert.
- Grenze: Reale Einweisung, unterstützte Prüfverfahren mit echten Nachweisen und externe
  Credential-Prüfung nicht ausgeführt; der Browserlauf betrifft manuelle Kompetenznachweise.

### `koordination/vergaben-lernwegteilnahmen.mdx`

- Entscheidung: Kanonische Teilnahme-Anleitung beibehalten. Warnung vor der Verwechslung
  heutiger Lernwegdetails mit gespeicherten Anforderungen sichtbar gemacht; Zählbeispiel ergänzt.
- Quellen: `web/components/competencies/{learning-paths,path-enrollments,badge-people}.tsx`,
  `web/locales/de/badges.json`,
  `api/Service/Competencies/Boundary/HttpControllers/LearningPathsController.cs`,
  `api/Service/Competencies/Application/Services/BadgeLearningService.Paths.cs`,
  `api/Service/Competencies/Boundary/Dto/BadgeLearningDtos.cs`.
- Bestätigt: getrennte Rechte für Zuordnung, Abschluss und Abbruch; aktive Lernwege für neue
  Teilnahme; Snapshot, Gültigkeitszählung, ausdrücklicher Abschluss und erhaltene Vergaben.
- Browser: Seed-Lernweg **Vom Entwurf zum Prototyp** mit Teilnahmen **2 / 2, Abschluss möglich**
  und **3 / 2, Abgeschlossen** gelesen, unverändert aufgenommen und die Anzeige im Text erklärt.
  Bild `docs/koordination/bilder/lernweg-teilnahmen-fortschritt-aktuell.png` visuell geöffnet.
  Separaten Lernweg **Werkstattstart: Dokumentationsprüfung** mit einem zuvor lokal vergebenen
  Testbadge angelegt; Miriam zugeordnet (**1 / 1, Abschluss möglich**), Abschluss ausdrücklich
  bestätigt und neu geladen (**Abgeschlossen**). Keine Seed-Teilnahme geändert.
- Grenze: Keine tatsächliche Lernleistung und kein optionales Abschluss-Badge praktisch geprüft;
  Abbruch/Snapshot-Folge sind über Code belegt.

### `koordination/zugangsantraege-entscheiden.mdx`

- Entscheidung: Ablauf und Rechte sind aktuell und bleiben erhalten. Folge einer Genehmigung
  vor der Entscheidung als Callout hervorgehoben.
- Quellen: `web/app/[project]/dashboard/access-management/requests/requests-page-client.tsx`,
  `web/locales/de/access.json`,
  `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessRequestsController.cs`,
  `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs`.
- Bestätigt: objektbezogene Zuständigkeit zusätzlich zu globalen Rechten; offene Anträge;
  Vorbelegung von 30 Tagen, optionale Genehmigungsnotiz und erforderlicher Ablehnungsgrund;
  gemeinsame Speicherung von Antrag und direkter Freigabe; Versionskonflikte.
- Browser: Administrationsroute geöffnet; **Keine offenen Anträge** und Rückladesteuerung gelesen.
  Im Testbestand gab es keinen offenen Antrag; Entscheidung daher nicht praktisch ausgeführt.
- Grenze: Kein Hardwarezutritt und keine konkrete Rechtekombination
  mit einem eingeschränkten Koordinationskonto durchgespielt.

### `administration/badges-verwalten.mdx`

- Entscheidung: Fachliche Details erhalten. Vier echte Assistentenphasen mit nativen
  Steps; Bilder bei der zugehörigen Handlung mit ImageZoom. Veraltete Einbindungen für
  Eigenschaften, Voraussetzungen und historische Eigenschaften entfernt; aktuelle Aufnahmen
  für Assistent, Eigenschaften und Versionsvergleich ergänzt. Vollständige Personen-/Vergabeaufgabe
  mit Genehmigungsrechten in die neu beauftragte Koordinationsanleitung ausgelagert; alle sechs
  alten Abschnittsanker als Spans erhalten und auf die neue Anleitung verwiesen.
- Quellen: `web/components/competencies/{badge-creation-sheet,qualifications,badge-criteria-section,badge-skills-section,badge-validity-fields,badge-version-history,badge-activation-section,badge-library,badge-people,publications}.tsx`,
  `web/locales/de/{competencies,badges}.json`,
  `api/Service/Competencies/Boundary/HttpControllers/{BadgeAwardsController,QualificationsController,CompetencyPublicationsController}.cs`,
  `api/Service/Competencies/Application/Services/{BadgeLearningService,QualificationService,QualificationService.Exchange,PublicationService}.cs`.
- Bestätigt im Browser am isolierten System `http://localhost:3415/docs-revision`:
  neue lokale Definition mit zwei vorhandenen lokalen Fähigkeiten und 90 Tagen erstellt;
  Assistentenschritte, aktuelle Kriterienbezeichnung, Übernahme beider Fähigkeiten als erforderlich,
  Prüfübersicht und gespeicherte Eigenschaften geöffnet.
- Eigene Aufnahmen (fiktive Seed- und Testdaten, heller Modus):
  `docs/administration/bilder/badge-erstellen-voraussetzungen-aktuell.png`,
  `badge-erstellen-pruefen-aktuell.png`, `badge-eigenschaften-aktuell.png`, `badge-versionen-aktuell.png`.
  Alle einzeln visuell geöffnet und auf Lesbarkeit geprüft. Gültigkeit auf 180 Tage als neue
  Inhaltsversion gespeichert; Versionsvergleich 90 → 180 Tage praktisch bestätigt.
- Grenze: Anbieterimport und echte signierte Ausstellung nicht geprüft. Produktwiderspruch
  zur ersten Versionsnummer separat unten; Text nennt deshalb „erste Inhaltsversion“.

### `koordination/badge-vergaben.mdx` (zusätzlich beauftragte Aufteilung)

- Entscheidung: Bestehende vollständige Abschnitte **Vergaben einer Person finden** und
  **Vergaben und Lernwege** von der Definitionspflege getrennt. Eigene Voraussetzungen
  für View/Approve und Benutzerleserechte, aktive lokale Definition, Versionsstand und
  manuelle Kriterienprüfung; passende Fehlerhilfe übernommen. Eigene Verweise aus
  Bewertungen und Lernwegteilnahmen aktualisiert. Keine Metadatenänderung.
- Quellen: `web/components/competencies/{badge-people,badge-library,qualifications}.tsx`,
  `api/Service/Competencies/Boundary/HttpControllers/BadgeAwardsController.cs`,
  `api/Service/Competencies/Application/Services/BadgeLearningService.cs`,
  `web/locales/de/badges.json` und die erhaltenen Inhalte der bisherigen Verwaltungsseite.
- Browser: Eigenes Badge **Werkstattstart: Arbeitsschutz** mit Version 0 / 90 Tagen an
  Miriam Brandt vergeben. Nach Änderung auf Version 1 / 180 Tage blieb die vorhandene
  Vergabe bei Version 0 / 90 Tagen. **Erneuern** erzeugte eine gültige Version 1 / 180 Tage
  und erhielt Version 0 als **Widerrufen oder ersetzt**. Beide Datensätze neu geöffnet/gelesen.
  Eigene Aufnahme `docs/koordination/bilder/badge-vergaben-erneuerung-aktuell.png` zeigt
  beide Zeilen, visuell geöffnet. Das ist ein fiktiver Testfall, keine echte Einweisung.
- Grenze: Lokaler Badge-Widerruf wurde über Code, nicht praktisch geprüft; der praktisch
  ausgeführte Widerruf eines Kompetenznachweises ist eine andere Datenart. Keine externe
  signierte Credential-Wirkung behauptet. Sidebar und fremde Verweise integriert der Koordinator.

### `administration/kompetenzen-lernwege.mdx`

- Entscheidung: Einrichtung von Fähigkeiten, Katalogen und Lernwegen erhalten. Doppelte
  Teilnahme-/Abschlussanleitung samt erneutem Rechteschema und Fehlerhilfe entfernt und
  am erhaltenen Anker auf die kanonische Koordinationsanleitung verwiesen. Exakte heutige
  Bezeichnung „Herkunft, Zuordnung & weitere Angaben“ für Fähigkeitsdetails übernommen.
- Quellen: `web/components/competencies/{workspace,library-detail,definitions,definition-structure,catalogue-editor,frameworks,learning-paths}.tsx`,
  `web/locales/de/{competencies,badges}.json`,
  `api/Service/Competencies/Boundary/HttpControllers/{CompetencyCatalogController,LearningPathsController}.cs`,
  `api/Service/Competencies/Application/Services/{CompetencyService,CompetencyCatalogService,CaseExchangeService,BadgeLearningService.Paths}.cs`.
- Bestätigt: Definitionen erteilen keine persönlichen Nachweise; Art/Katalog bleiben bei
  Änderung fest; einmalige Klassifizierung importierter Einträge; lokale Kopien; getrenntes
  aktives lokales Abschluss-Badge; spätere Änderungen verändern keine gespeicherten Teilnahmen.
- Browser: Eigener aktiver Lernweg mit Name, Beschreibung und einem aktiven lokalen Badge
  über die Oberfläche erstellt und anschließend erfolgreich für eine Teilnahme verwendet.
- Grenze: CASE-Import, neue Fähigkeit/Katalog und Beziehungen nicht erneut über die Oberfläche angelegt.

### `administration/nachweissysteme-anbinden.mdx`

- Entscheidung: Anbieterwege und belegte Produktgrenzen erhalten. Konto-Anbieter in drei
  echte Phasen gegliedert: Registrieren, Rückleitungsadresse/Freigabe, persönlicher Abruf.
  Aktivierungsblockade der serverweiten Synchronisation als sichtbaren Callout belassen.
- Quellen: `web/components/competencies/badge-providers.tsx`,
  `web/components/integrations/openbadges/openbadges-navigation.tsx`,
  `web/app/[project]/dashboard/admin/integrations/openbadges/use-openbadges-settings-controller.ts`,
  `api/Service/Interoperability/Application/BadgeProviderAdministration.cs`,
  `api/Service/OpenBadges/Application/{OpenBadgesIntegrationService,OpenBadgesSyncService,OpenBadgesCompetencyProjectionService}.cs`,
  `api/framework/Infrastructure/Configuration/Setup/SetupIntegrationProbes.cs`,
  `api/server/Program.cs` (Zeitplan mit Begrenzung auf 59 Minuten).
- Bestätigt per Code: HTTPS-Endpunkte, Client-Methoden, Secret-Semantik,
  gespeicherte Konfiguration als Testgrundlage, fehlende Aktivierungsmöglichkeit bei
  deaktiviertem Stand, getrennte persönliche und serverweite Importwege.
- Browser: Konto-Anbieter-Verwaltung geöffnet (keine Anbieter im isolierten Bestand),
  **Anbieter hinzufügen** geöffnet und aktuelle Felder, drei Token-Authentifizierungsmethoden,
  deaktivierte Vorbelegung und Hinweis auf Rückleitungs-URL nach Speicherung gelesen.
  Ohne externen Anbieter keine Konfiguration gespeichert.
- Grenze: Keine externe Registrierung, Anmeldung, Token-Validierung, Nachweiszustellung
  oder Ausstellungsberechtigung beim Anbieter geprüft.

## Produktbefunde außerhalb dieses Doku-Patches

1. Badge-Assistent behauptet erste Inhaltsversion **1**, das tatsächlich neu erstellte
   Badge erscheint mit **Version 0 · aktuell**. In `QualificationService.cs` übernimmt
   die Revision die anfängliche `Version = 0`; aktueller Browserbeleg vorhanden.
   Anleitung nennt keine falsche Nummer mehr.
2. Das Teilnahmenformular sendet eine **Notiz zur Entscheidung**, die der Teilnahme-
   Datensatz nicht speichert: `CompleteAsync` übergibt sie nur an eine gegebenenfalls
   neu angelegte Abschluss-Badge-Vergabe; `CancelAsync` ignoriert sie. Kein
   nachvollziehbarer Notizverlauf an der Teilnahme. Aus Code abgeleitet, keine neue
   Historienbehauptung in die Anleitung aufgenommen.
3. Lernwegdetails zeigen im Aktivstatus das unübersetzte `competencyManagement.active`.
   In `web/components/competencies/shared.tsx` wird dieser Schlüssel verwendet,
   `web/locales/de/competencies.json` enthält ihn nicht. Im Browser bestätigt; kein Softwarepatch.
4. Bestehende Aktivierungsblockade der serverweiten OpenBadges-Synchronisation erneut
   im Code bestätigt: Frontend verlangt aktuelle Validierung vor Aktivierung,
   Backendprobe lehnt deaktiviert gespeicherte Konfiguration ab. Keine Produktänderung.

## Dokumentprüfungen

- Prettier `--ignore-path /dev/null --check` für alle sieben MDX-Dateien und diesen Bericht nach finalen Inhalts- und Bildeinbindungen erfolgreich.
- Scoped `git diff --check` erfolgreich.
- Vorhandene Anker der sechs Bestandsseiten mit `/tmp/mardu-docs-revision-20261103/baseline-render.json`
  verglichen: alle erhalten. Die sechs ausgelagerten Vergabeabschnitte bleiben als explizite Span-IDs
  auf der bisherigen Adresse; auf der neuen Seite besitzen sie weiterhin ihre Überschriften.
  Quellenprüfung mit bestehendem `github-slugger`; kein Ersatz für die gemeinsame Renderprüfung.
- Relative MDX-Zieldateien und lokale Bildimports auf Existenz geprüft: erfolgreich.
- Keine API/DTO-Verträge oder Softwaredateien geändert; keine neue API-Dokumentation nötig.
- Consumer-Rendering, Markdown-Ausgabe und gerenderte Anker erfolgen gemeinsam durch
  den Koordinator. Browser wurde zeitweise von einem fehlenden Bildimport einer
  parallelen Seite blockiert; kein Serverneustart oder Eingriff an fremden Dateien.
