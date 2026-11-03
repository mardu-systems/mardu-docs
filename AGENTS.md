# Mardu-Dokumentation: Regeln für Agenten

Diese Regeln gelten für `mardu-systems/mardu-docs` und begleitende
Produktdokumentation. Consumer verlinken hierher. Die Entwicklungs- und
Sicherheitsregeln des jeweiligen Projekts gelten zusätzlich. Wende nur Regeln an,
die für die betroffene Dokumentation relevant sind.

Für die Überarbeitung bestehender Funktionen und neue Anleitungen verwende die
[Arbeitsweise mit Änderungsbrief und Prüfschritten](ARBEITSWEISE.md).

## Erst verstehen, dann ändern

- Lies vorhandene Seiten, Navigation, Consumer-Konfiguration und die betroffene
  Implementierung. Verwende bestehende Begriffe, Komponenten und Werkzeuge.
- Bestimme die Leser, ihr Vorwissen und ihre konkrete Frage. Eine Rollenbezeichnung
  allein beschreibt den Wissensstand nicht. Erkläre die fehlenden Zusammenhänge,
  statt vorausgesetztes Teamwissen oder Implementierungsdetails aufzuzählen.
- Prüfe Aufgabenabdeckung auch gegen vorhandene Produktfunktionen. Ein vollständiges
  Seiteninventar belegt keine vollständige Dokumentation; Routen können Weiterleitungen
  oder Platzhalter sein.
- Bewahre gute Anleitungen. Verbessere nur, was für die Aufgabe nötig ist;
  eine neue Struktur verlangt keine vollständige Neufassung aller Seiten.

## Orientierung und Navigation

- Die sechs Einstiege sind **Überblick, Benutzer, Koordination, Administration,
  Installieren und Entwickeln**. Sie sind Lesereinstiege, keine Systemrollen.
  Die Dokumentation soll nach Fragen und Aufgaben auffindbar sein.
- Der Überblick erklärt das Systemmodell: Personen und Ressourcen sowie deren
  Beziehungen. Buchbarkeit, Zutrittspunkte, Geräte, Automationen und Messwerte
  sind je nach Einrichtung Ergänzungen. Ressource und Gerät sind unterschiedliche
  Begriffe; nicht jede Ressource braucht Hardware.
- Bereichsstarts erklären ihren Zweck und führen zu häufigen Aufgaben. Spiegel
  nicht ungeprüft Dashboard-Menüs, interne Module oder sämtliche Einstellungen.
- Gib jeder Seite eine kanonische Quelle und einen erkennbaren Heimatbereich.
  Verlinke sie auch aus anderen passenden Aufgaben; benenne dabei Bereichswechsel.
  Leite aus dem Dokumentationsbereich keine festen Systemrollen ab.
- Gruppiere längere Sidebars mit kurzen Zwischenüberschriften; kurze Listen
  brauchen keine künstliche Hierarchie.
  Ein sichtbarer Eintrag muss zu nutzbarem Inhalt führen, nicht zu einem Schreibauftrag.
- Erkläre Begriffe und Verfahren an einer Stelle. Verlinke sie im passenden Kontext,
  auch über Bereichsgrenzen hinweg. Vermeide wiederholte pauschale Linklisten.
- Erhalte bestehende URLs und verwendete Anker. Navigation und Dateipfad müssen
  nicht identisch sein. Prüfe neben `meta.json` auch Bereichsfilter und Sluglisten
  der Consumer; eine vorhandene Seite ist nicht automatisch sichtbar erreichbar.

## Die passende Seite schreiben

- Wähle einen Hauptzweck nach [Diátaxis](https://diataxis.fr/compass/): Lernen,
  eine Aufgabe erledigen, Fakten nachschlagen oder Zusammenhänge verstehen.
  Daraus folgt kein zusätzlicher Pflichtordner und keine starre Seitenvorlage.
- Eine Anleitung nennt, soweit nötig: Ziel, Rechte und Voraussetzungen, Schritte,
  erwartetes Ergebnis und Abhilfe bei relevanten Problemen. Bedingungen und Folgen
  stehen vor der betroffenen Aktion, besonders bei Verlust, Widerruf und Löschung.
- Verwende exakte UI-Bezeichnungen. Schreibe aktiv, sachlich und direkt; keine
  Werbung, unbelegten Versprechen, Floskeln oder bedeutungsarmen Verstärkungen.
  Erläutere unbekannte Abkürzungen und verwende Domänenbegriffe durchgehend gleich.
- **Erst verdichten, dann ausarbeiten:** Entferne Wiederholungen, irrelevante
  Sonderfälle und technische Details ohne Nutzen für die Aufgabe. Glätte danach
  Reihenfolge, Überschriften, Übergänge und Darstellung. Kürze nicht nach Quote;
  Rechte, Voraussetzungen, Grenzen und notwendige Warnungen bleiben erhalten.
  Wiederhole die Kurzbeschreibung nicht im ersten Absatz. Beginne mit der nötigen
  Einordnung, Voraussetzung oder Handlung. Prüfprosa und fehlende Funktionen
  gehören nur in die Anleitung, wenn sie die nächste Entscheidung beeinflussen.
- Nutze Absätze zum Erklären, nummerierte Schritte für Abläufe und Tabellen für
  Vergleiche. Halte Hauptaufgaben sichtbar. Akkordeons brauchen einen konkreten
  Nutzen und dürfen keine notwendigen Schritte, Voraussetzungen oder Folgen
  verstecken. Tabs eignen sich für echte alternative Abläufe.
- Verwende soweit möglich durchgehend native Fumadocs-Komponenten und APIs für
  Navigation, Inhaltsdarstellung und Seitenaktionen. Nutze vorhandene
  Markdown-/MDX-Standards und prüfe die installierten Fumadocs-Mittel, bevor du
  eigenes JSX, Styling oder zusätzliche Logik einführst. Eigene Lösungen brauchen
  einen konkreten Bedarf, den die vorhandenen Mittel nicht abdecken; Komponenten
  werden nach ihrem Nutzen für die Leser gewählt.
- Vorhandene Übersetzungen müssen in Bedeutung, Beispielen und Verhalten
  übereinstimmen. Neue Sprachen benötigen einen Auftrag.

## Verhalten und Prüfungen belegen

- Prüfe UI, Backend-Verhalten, Berechtigungen und vorhandene Verträge, bevor du
  Funktionen beschreibst. Erfinde keine Felder, Automatismen, Statuscodes,
  Zeitangaben oder Kompatibilität. Verfügbare und geplante Funktionen trennen.
- Unterscheide Codelektüre, automatisierte Tests, Browserprüfung und reale
  Hardware-/Anbieterprüfung. Keiner dieser Belege ersetzt pauschal die anderen.
  Beschreibe den tatsächlichen Prüfumfang und offene Grenzen; ein Versandauftrag
  belegt beispielsweise noch keinen externen Empfang.
- Nutze vorhandene OpenAPI-/Swagger- und XML-Dokumentationswege für API-Verträge;
  generierte Dateien nicht von Hand ändern. Dokumentiere bei API-Änderungen
  Authentifizierung/Rechte, Request/Response, Pflicht-/optionale Felder,
  Null-/Leer-Semantik, Defaults, Validierung, Statuscodes und relevante Fehler.
  Ergänze Bedeutung und gültige Beispiele; Einheiten, Versionierung, Pagination
  und Parallelität nur, soweit vorhanden. Produktanleitungen verlinken die Referenz.
- Verwende fiktive, reproduzierbare Beispiele ohne echte Zugangsdaten, persönliche
  Daten oder interne Produktionsinformationen.

## Grafiken und Lesbarkeit

- Verwende Diagramme für Beziehungen, Systemgrenzen und Abläufe; Screenshots für
  schwer auffindbare Bedienung oder wichtige UI-Zustände. Nicht jeder Schritt
  braucht ein Bild. Halte Diagramme klein und erkläre ihre Aussage zusätzlich als Text.
- Mermaid ist eine mögliche Quelle, kein Beleg für vorhandene Darstellung im
  Consumer. Prüfe gerenderte Diagramme, Schrift und Lesbarkeit auch mobil.
- Screenshots stammen aus der vorhandenen Oberfläche. Keine generierten oder
  nachgezeichneten UI-Bilder als Produktbeleg. Halte Sprache, Theme und Testdaten
  innerhalb einer Anleitung passend; zeige genügend Orientierung.
- Informative Bilder brauchen Alternativtext. Wesentliche Informationen stehen
  auch als Text bereit; Code und Ausgaben bleiben kopierbar. Echte Daten müssen
  vollständig entfernt werden, Weichzeichnen genügt nicht.

## Ablage, Pflege und Abschluss

- Veröffentlichte MDX-Seiten liegen unter `docs/`, Bilder im passenden
  `bilder/`-Ordner. Pläne, Entwürfe, Schreibaufträge und Agentenanweisungen bleiben
  außerhalb von `docs/` und damit außerhalb der Produktnavigation und Suche.
- Jede veröffentlichte MDX-Seite erhält `title` und `description` im Frontmatter,
  kein zusätzliches H1. Neue Seiten in `meta.json` und den nötigen Consumer-Listen
  eintragen. Relative MDX-Seitenlinks beginnen mit `./` oder `../`.
- Pflege Dokumentation zusammen mit Verhaltensänderungen. Inhalt, Bilder und
  Submodule-Stände müssen bei einem Release in allen Consumern zusammenpassen.
  Prüfe historische Adressen und Versionsstrukturen, bevor du sie änderst.
- Führe Commits, Pushes, Submodule-Bumps und Veröffentlichungen nur im Umfang
  des Auftrags aus. Eine Inhaltsänderung ist kein Veröffentlichungsauftrag.
- Prüfe Format, Links, Anker, Bilder und Navigation mit vorhandenen Werkzeugen.
  Geänderte Produktseiten im Consumer rendern und je nach Änderung mobile Ansicht,
  Tastaturbedienung oder Abläufe prüfen. Keine erfundenen CI-Gates oder Testbehauptungen.
  Bei reinen Planungs-/Regeldateien genügen passende Dokumentprüfungen.
- Berichte kurz Änderungen, wiederverwendete Mittel, Prüfungen und offene Grenzen.
  Markiere eine Anleitung erst nach den erforderlichen Prüfungen als abgenommen.

Methodische Grundlagen: [Google: Zielgruppe](https://developers.google.com/tech-writing/one/audience),
[Google: Barrierefreiheit](https://developers.google.com/style/accessibility),
[GOV.UK: Akkordeons](https://design-system.service.gov.uk/components/accordion/) und
[Write the Docs: Docs as Code](https://www.writethedocs.org/guide/docs-as-code/).
