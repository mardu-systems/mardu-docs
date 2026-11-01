# Querschnittsprüfung: Ressourcen, Freigaben und Nachweise

## Auftrag und Ergebnis

Unabhängiger abschließender Inhaltsabgleich der aktualisierten Ressourcen-,
Zutritts-, Freigaben-, Buchungs-, Kompetenz-, Badge-, Lernweg-, Antrags- und
Metrikanleitungen mit vorhandener UI und Backend. Dokumentationsregeln und
`ARBEITSWEISE.md` sowie die zugehörigen Seitenberichte vom 01.11.2026 wurden
berücksichtigt. Produktdateien wurden ausschließlich gelesen.

**Keine zusätzlichen belegten wesentlichen Restfehler festgestellt.** Es gibt
aus dieser Prüfung keinen weiteren Korrekturauftrag an einer Produktseite.
Dies ist eine statische Inhaltsprüfung, keine praktische Abnahme.

## Geprüfter Zusammenhang

- Ressourcenregel, Verwaltungszuständigkeit und persönliche Freigabe sind
  getrennt. Ein Recht an einer übergeordneten Ressource wird nicht als automatisch
  vererbtes Recht beschrieben. Hardwarezuordnung und gespeicherte Freigabe
  bestätigen weder Leserreaktion noch physische Freischaltung.
- Die neue Freigabenanleitung unterscheidet Neuanlagen für Benutzer und Gruppen
  von vorhandenen Tag-Vergaben. Gültigkeitsbeginn, exklusives Ende, Wochenzeiten,
  Zeitzone und Entzug einer einzelnen Vergabe passen zu Editor und Service.
  Der Entzug wird zutreffend weder als vollständige Sperre aller Zugangswege noch
  als Sitzungsende oder Abschaltauftrag beschrieben.
- Die Antragsentscheidung erzeugt eine direkte Personenfreigabe ohne zusätzliche
  Wochenfenster, keinen Kompetenznachweis. Ablehnung entzieht keine vorhandene
  Freigabe. Globale Rechte, ressourcenbezogene Zuständigkeit, offener Status und
  Versionsprüfung bleiben unterscheidbar.
- Buchbarkeit und Buchungsnachweis werden getrennt. Buchungszugriffsziele müssen
  ausdrücklich gespeichert werden; bestätigte Buchungen, Stornierung, Check-out
  und Nichterscheinen werden nicht als physische Hardwareaktionen dargestellt.
- Fähigkeitsdefinition, Kompetenzanerkennung, lokale Badge-Vergabe und signiertes
  Credential werden nicht gleichgesetzt. Neue Inhaltsversionen verändern keine
  bestehenden Vergaben. Die lokale Badge-Vergabe wird als ausdrückliche
  Entscheidung mit vorheriger Prüfung der Voraussetzungen beschrieben.
- Lernwegteilnahmen behalten ihre Anforderungen und gegebenenfalls die Version
  des Abschluss-Badges. Fortschritt zählt unterschiedliche aktuell gültige lokale
  Badge-Vergaben. Abschluss erfordert Bestätigung und bleibt historisch erhalten;
  Abbruch widerruft keine Badges. Die fehlende vollständige historische
  Anforderungsliste in der Teilnahmeansicht ist in der Teilnahme-Anleitung
  ausdrücklich begrenzt.
- Zugangsmetriken trennen das UTC-Fenster der Entscheidungen von aktuell offenen
  Sitzungen und deren getrennten Sichtrechten. Betriebsmetriken haben einen
  eigenen Zeitraum, Auflösungen und Aufbewahrungsgrenzen; Nullwerte werden nicht
  pauschal als Nachweis vollständig erfasster Historie beschrieben.

## Unmittelbar gegengeprüfte Codequellen

Pfade relativ zum Software-Repository; zusätzlich wurden die Quellenzuordnungen
und bekannten Grenzen der jeweiligen Seitenberichte gelesen.

- `web/components/access/access-grant-editor.tsx`,
  `api/Service/Accesses/Application/Services/ResourceAccessAdministrationService.cs`
  (`ListGrantsAsync`, `CreateGrantAsync`, `UpdateGrantAsync`, `DeleteGrantAsync`),
  `AccessGrantScheduleEvaluator.cs` und `ResourceAccessAuthorizationService.cs`
  (`FindMatches`).
- `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs`
  (`ListRequestsAsync`, `ApproveRequestAsync`, `RejectRequestAsync`,
  `EnsurePendingAndVersion`, `IsSubjectMatch`).
- `api/Service/Bookings/Application/Services/BookingAttendanceService.cs`,
  `BookingManagementService.cs` und
  `api/Service/Bookings/Gateway/BookingSpecifications.cs`.
- `web/components/competencies/learning-paths.tsx`, `path-enrollments.tsx`,
  `api/Service/Competencies/Boundary/HttpControllers/LearningPathsController.cs`,
  `api/Service/Competencies/Application/Services/BadgeLearningService.cs` und
  `BadgeLearningService.Paths.cs`.
- `api/Service/Accesses/Application/Services/ResourceAccessActivityService.Metrics.cs`
  und die Rechteverträge der Observability-Controller.

## Abgrenzung und Prüfungen

Die bereits an die Koordination gemeldete pauschale Tag-Formulierung in der
Ressourcenanleitung ist kein neuer Befund dieses Berichts. Die Entscheidung,
Scope- und Zutrittspunktaufgaben in der bestehenden Ressourcenanleitung zu
belassen, wird nicht erneut geöffnet. Bereits korrekt eingegrenzte Produktfehler
der Seitenberichte werden nicht als neue Dokumentfehler wiederholt.

Geändert wurde ausschließlich dieser Bericht. Keine Produkt-, API-/DTO-,
Navigations- oder Softwareänderung; daher keine Anpassung der API-Dokumentation.
Quellenlektüre und Inhaltsvergleich sowie Format- und Whitespaceprüfung des
Berichts wurden ausgeführt. Keine Builds, Tests, Browser-, Hardware- oder
Anbieterprüfung und keine echten Freigaben, Anträge, Buchungen oder Vergaben.
Gemeinsames Consumer-Rendering und die in den Seitenberichten benannten
praktischen Prüfungen bleiben bei der Koordination.
