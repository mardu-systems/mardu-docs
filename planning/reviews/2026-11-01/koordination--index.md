# P53: Koordination – Bereichseinstieg

**Entscheidung: verbessert.**

Leserfrage: Welche Anleitung hilft mir bei laufenden Entscheidungen über
Ressourcennutzung, Nachweise und Lernwegteilnahmen? Die Leser kennen ihre
organisatorische Aufgabe, müssen aber weder die Dokumentationsbereiche noch
die Trennung von Einrichtung und laufender Entscheidung kennen.

Änderungsbrief: Den kurzen Einstieg um die ausgearbeiteten Buchungs-, Zugangs-,
Bewertungs- und Lernweganleitungen ergänzen und den überholten Schreibhinweis
entfernen. Die Ressourcenanleitung bleibt die kanonische Quelle für Wartung und
gehört zur Administration; globale Schließzeiten gehören zur Buchungsverwaltung.
Bestehende URLs und Anker, die Abgrenzung zu eigenen Benutzeraufgaben und die
Unterscheidung persönlicher Nachweise und Ressourcenfreigaben bleiben erhalten.
Nur diese Seite und dieser Bericht werden geändert. Die eigene Prüfung umfasst
Format, Verweise und Anker; die gemeinsame Consumer-Prüfung übernimmt der
Koordinator.

## Befunde und Änderungen

- Der bisherige Abschluss behauptete, Buchungs- und Zugangsanträge sowie
  Bewertungen seien noch nicht beschrieben. Diese Aussage entfällt. Die Seite
  verlinkt die vier ausgearbeiteten Aufgaben unter „Anfragen entscheiden“ und
  „Qualifikationen einordnen“.
- Ressourcenstatus, Sperren, Wartung und Buchbarkeit bleiben bei der bestehenden
  Ressourcenanleitung. Der Bereichswechsel zur Administration steht vor den
  Links. Globale Schließzeiten führen zum eigenen Abschnitt der
  Buchungsverwaltung. Keine zusätzliche Wartungsseite angelegt (N01).
- Die organisatorische Aufgabenverteilung ist ausdrücklich von Systemrechten
  getrennt. Die Voraussetzungen bleiben in den Aufgabenanleitungen, statt
  hier deren Rechte- und Zuständigkeitstabellen zu duplizieren.
- Eigene Buchungen und der eigene Qualifikationsstand bleiben verlinkt, ebenso
  Ressourceneinrichtung und Badge-Definition. Lokale Badge-Vergaben führen mit
  benanntem Bereichswechsel zur Administration. Die Unterscheidung von
  Definition, persönlicher Vergabe und Ressourcenfreigabe bleibt erhalten.
- URL und die fünf bisherigen Anker bleiben erhalten: `in-diesem-bereich`,
  `ressourcen-im-alltag`, `qualifikationen-einordnen`,
  `offene-dokumentationsaufgaben`, `umfang-der-anleitungen`. Der letzte
  Überschriftenanker ist nun ausdrücklich gesetzt; der Abschnitt heißt
  „Eigene Nutzung und Einrichtung“. Keine Bilder oder neuen Komponenten.

## Quellen

- `web/content/docs/docs/koordination/buchungen-verwalten.mdx:11–38,66–94,129–163`:
  Rechte, Schließzeiten und fremde Buchungen. Die Umsetzung dazu steht in
  `api/Service/Bookings/Boundary/HttpControllers/AdminBookingsController.cs:25–163`
  (getrennte View-/Create-/Update-Rechte) und
  `api/Service/Bookings/Boundary/HttpControllers/BookingPoliciesController.cs:55–94`
  (Schließzeiten mit Verwaltungsrechten). Die UI prüft Rechte und bietet
  Entscheidungen in
  `web/app/[project]/dashboard/bookings/requests/booking-admin-center.tsx:106–124,414–425`.
- `web/content/docs/docs/koordination/zugangsantraege-entscheiden.mdx:13–86`:
  eigene Rechte-/Zuständigkeitsprüfung und Zugangsentscheidung.
  `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessRequestsController.cs:24–64`
  schützt Lesen und Entscheidungen getrennt;
  `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:242–249,301–302,359–365`
  prüft zusätzlich die Zuständigkeit zur Ressource.
- `web/content/docs/docs/koordination/bewertungen.mdx:18–43,79–108,161–185`:
  Anforderungen, Prüfungen und vorgeschlagene Kompetenznachweise.
  `api/Service/Competencies/Boundary/HttpControllers/AssessmentRunsController.cs:24–92`
  trennt View, Create und Approve. Die UI begrenzt manuelle Entscheidungen in
  `web/components/competencies/assessments.tsx:320–339`.
- `web/content/docs/docs/koordination/vergaben-lernwegteilnahmen.mdx:15–31,77–110`:
  Zuordnung, Abschluss, Abbruch und getrennte Badge-Verwaltung.
  `api/Service/Competencies/Boundary/HttpControllers/LearningPathsController.cs:55–86`
  schützt die Teilnahmeaktionen je Aufgabe und trennt sie von Zugriffsrechten.
- `web/content/docs/docs/koordination/ressourcen.mdx:57–71,132–167`:
  Status, Buchbarkeit, Ausfälle und Wartung. Bestehende kanonische Zielabschnitte
  wiederverwendet; keine Beschreibungen dieser Abläufe kopiert.

## Eigene Checks und Grenzen

- Dateibezogene Prüfung und Formatierung mit dem installierten Prettier,
  `--ignore-path /dev/null`; abschließendes `--check` erfolgreich.
- Read-only-Prüfung mit Bun und den vorhandenen Paketen `@mdx-js/mdx` und
  `github-slugger`: MDX kompiliert; 13 lokale MDX-Verweise einschließlich
  vorhandener Zielfragmente aufgelöst. Alle fünf Anker aus dem bisherigen
  Git-Stand bleiben vorhanden. Frontmatter, fehlendes zusätzliches H1 und
  Entfernung der alten Planhinweise geprüft.
- Dateibezogenes `git diff --check` erfolgreich. Keine Softwareänderung,
  API-/DTO-Änderung oder Anpassung ihrer Vertragsdokumentation.
- Ausschließlich statische Dokument-/Codeprüfung und MDX-Kompilation.
  Keine Browser-, Hardware- oder Anbieterprüfung, kein globaler Build und
  keine praktische Abnahme. Der Website-Consumer wurde nicht ausgeführt.

Der Koordinator integriert die Aufgaben in `meta.json` und den Consumer-Listen
und übernimmt Navigation sowie Darstellung in den Consumern. Keine zusätzliche
Nachbarseite erforderlich. Kein belegter Produktfehler; offene Grenze ist die
gemeinsame Consumer-Prüfung.

Geänderte Dateien:

- `web/content/docs/docs/koordination/index.mdx`
- `web/content/docs/planning/reviews/2026-11-01/koordination--index.md`
