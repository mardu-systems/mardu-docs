# Gesamte Dokumentation am aktuellen Produkt überarbeiten

> Ausführung: unabhängige Seitenpakete parallel nach dem Agentenbrief bearbeiten;
> gemeinsame Darstellung, Verlinkungen und Abnahme durch den Koordinator.

**Auftrag:** Das für Ressourcen, Buchungen und Freigaben bewährte Vorgehen auf
alle Doku-Punkte anwenden. Bestehende gute Anleitungen erhalten; andere gegen
aktuelle Funktionen prüfen, verdichten und mit passenden nativen Fumadocs-Mitteln
und aktuellen visuellen Belegen verständlich ausarbeiten.

**Bestand:** 74 handgeschriebene MDX-Dateien einschließlich Bereichseinstiegen
und historischen Adressen. Die generierte HTTP-Referenz bleibt aus ihren Verträgen
generiert. Jede Bestandsdatei hat einen Besitzer in
[der Auftragsliste](2026-11-03-gesamtrevision.json).

**Quellen:** aktuelle UI, Übersetzungen, Controller, DTOs und Services;
[Doku-Regeln](../AGENTS.md), [Arbeitsweise](../ARBEITSWEISE.md) und die zuletzt
überarbeiteten Ressourcen-, Buchungs- und Freigabenanleitungen als Muster.

## Grenzen und Prüfschwerpunkte

- Keine neue Designsprache, Dependencies, allgemeine CSS-Anpassung oder
  pauschale Umschreibung guter Texte. Komponenten dienen einer Leseraufgabe.
- URLs und bisherige Abschnittsanker erhalten; fehlende Navigation oder Links
  nach dem Seitenabgleich zusammenhängend korrigieren.
- Rechte, Voraussetzungen, Auswirkungen und relevante Fehlerhilfe erhalten.
  Hauptabläufe sichtbar; keine notwendigen Schritte in Akkordeons verstecken.
- Screenshots aus der aktuellen Oberfläche mit fiktiven Daten. Historische
  Aufnahmen prüfen und nur bei belegtem Bedarf ersetzen. Keine nachgezeichnete UI.
- Codeabgleich, API-/Browserprüfung und Hardware-/Anbieterprüfung unterscheiden.
  Externe Anmeldung, Nachrichtenzustellung und physische Zutrittswirkung benötigen
  jeweils eigene Belege. Fehlende Zugänge sind keine erfolgreiche Abnahme.
- Produktfehler getrennt festhalten; dieser Auftrag ändert die Dokumentation.
  Die zuvor beauftragte Freigaben-Korrektur bleibt unverändert erhalten.
- Bereits offene Änderungen bewahren. Keine Commits, Pushes oder Veröffentlichung.

## Ausführung

- [x] Alle 74 Seiten und gerenderten Anker vor Änderungen erfassen.
- [x] Zuständigkeiten ohne überlappende Dateipakete verteilen.
- [x] Jede Seite: Leserfrage und aktuellen Ablauf abgleichen; nur nötige Änderungen.
- [x] Jede Seite: distill, danach polish; eigene Quellen und Prüfgrenzen protokollieren.
- [x] Benötigte Screenshots mit isoliertem Testzugang aufnehmen und prüfen.
- [x] Übersicht, Bereichseinstiege, Querverweise und Navigation zusammenführen.
- [x] MDX-Format, Doku-Tests, Build, Links, Bilder, historische Anker, Suche und
      Markdown-Ausgabe prüfen. Alle Seiten auf Desktop und Mobil rendern.
- [x] Befunde, tatsächlich geänderte und bewusst erhaltene Seiten sowie verbleibende
      Prüfgrenzen im Abschlussbericht und Seiteninventar festhalten.

Die vorhandenen Doku-Tests sind unter `web/tests/lib/docs-*.test.*` abgelegt.
Gemeinsame Prüfungen und Serverstarts erfolgen ausschließlich durch den Koordinator,
damit parallele Arbeiten keine Build-Ausgaben oder Browserzustände überschreiben.

## Nach unabhängiger Durchsicht: Aufgaben entflechten

Die erste Seitenprüfung hat keine neue sicherheitsrelevante Falschaussage belegt,
aber vier überladene Aufgabenfolgen gezeigt. Deshalb folgt vor der Gesamtabnahme
noch diese Strukturkorrektur:

- Badge-Vergaben als eigene Koordinationsanleitung von Definitionspflege trennen.
- Runtime-/Zugangskonfiguration und Automationsanschlüsse in zwei Anleitungen führen;
  allgemeine Schalterbedienung zur kanonischen Ressourcenanleitung verlinken.
- Benutzergruppenpflege vollständig unter Rollen und Gruppen führen, statt für
  Anlegen/Löschen zwischen zwei Anleitungen hin und her zu wechseln.
- Anmeldevorgaben, Integrationszertifikate und Monitoring-Einrichtung aus der
  allgemeinen Servereinstellungsseite als drei eigene Aufgaben ausarbeiten.

Die fünf neuen Seiten verwenden vorhandene, aktuell geprüfte Inhalte. Alte
Adressen und Abschnittsanker bleiben als Einstiege erhalten. Native Unterseiten
und die bestehende Consumer-Bereichszuordnung werden gemeinsam angepasst.

Umsetzung und gemeinsame Prüfungen: [Ergebnisbericht](2026-11-03-gesamtrevision-ergebnis.md).
Hardware-/Anbietergrenzen sind dort und in den Paketberichten ausdrücklich getrennt.
