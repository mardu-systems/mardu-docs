# Buchungen verwalten überarbeiten

Auftrag: Die vorhandene Koordinationsanleitung verdichten und mit nativen
Fumadocs-Komponenten sowie aktuellen Screenshots verständlicher machen.
Leser entscheiden Anfragen und verwalten Buchungen anderer Personen; eigene
Buchungen und die Ressourceneinrichtung bleiben in ihren vorhandenen Anleitungen.

Umfang: `docs/koordination/buchungen-verwalten.mdx`, zugehörige neue Bilder und
dieser Änderungsbrief. Keine anderen Produktseiten, Navigation, APIs oder DTOs
ändern. Bestehende URL und Abschnittsanker erhalten. Keine neuen Dependencies.

Quellen: aktuelle Buchungsoberfläche, Übersetzungen, Controller, Services und
DTO-Validierungen; vorhandene native Steps, Callout und ImageZoom samt Lightbox.

- [x] Buchungsentscheidungen, Bearbeitung, Stornierung, Regeln und Rechte abgleichen.
- [x] Anleitung nach Aufgaben verdichten und notwendige Folgen sichtbar lassen.
- [x] Screenshots aus aktueller Oberfläche mit fiktiven Daten aufnehmen.
- [x] Format, Build, Links/Anker, Suche, Markdown, Bilder und mobile Darstellung prüfen.
- [x] Ergebnisse und Grenzen dokumentieren; andere Inhalte per Hashvergleich schützen.

Prüfschwerpunkte: offene Anfragen belegen Kapazität; Ablehnung braucht einen
Grund; kombinierte Buchungen und Serien haben unterschiedliche Änderungsumfänge;
Schließzeiten stornieren keine bestehenden Buchungen. Screenshots belegen die
Softwareoberfläche, keine physische Zutrittsprüfung oder externe Zustellung.

## Inhaltliche Entscheidungen

Die Seite bleibt die vorhandene Koordinationsanleitung. Buchungen finden steht
vor der Entscheidung; Umplanen, Stornieren, Vertretungsbuchung und gemeinsame
Regeln sind direkt erreichbare Aufgaben. Die neun bisherigen Abschnittsanker
bleiben durch vorhandene Überschriften oder native Scrollabstand-Aliasse erhalten.
Keine neue Seite oder Navigationsänderung.

Doppelte Regelerklärungen, allgemeine Kalenderbedienung und die Tabelle aller
numerischen Gruppenlimit-Grenzen entfallen. Die große Rechtetabelle wird durch
gemeinsame Voraussetzungen und zusätzliche Rechte direkt bei der Aufgabe ersetzt. Die Oberfläche validiert diese Werte;
Einrichtung und Nutzerabläufe werden über die vorhandenen Anleitungen verlinkt.
Rechte, Genehmigungspflicht, Geltungsbereich von Serien/kombinierten Buchungen,
Stornierungsfolgen und Konflikte bleiben erhalten.

Drei native Steps führen von der Prüfung über die Entscheidung zur Ergebniskontrolle.
Andere Aufgaben bleiben nummerierte Listen. Ein Warn-Callout zeigt vor dem Anlegen
einer Schließzeit den Konflikt mit vorhandenen Buchungen. Drei native ImageZoom-
Abbildungen verwenden die vorhandene Lightbox; keine Akkordeons, zusätzliche CSS-
Regeln oder eigenen Komponenten.

## Praktische Belege und offene Grenzen

Screenshots am 03.11.2026: aktuelle Dashboard-Oberfläche, Deutsch, helles Theme,
isolierte Testdatenbank und ausschließlich fiktive Daten. Per vorhandenen APIs
wurden Lina Berger, die aktive Holzwerkstatt und zwei offene Buchungen angelegt.
Aufnahmen zeigen Anfragenliste, Genehmigungsdialog und globale Schließzeiten.

Die Genehmigung erfolgte über die UI; der anschließend per API gelesene Datensatz
hatte Status Bestätigt und den eingetragenen Entscheidungsgrund. Eine normale
administrative Änderung setzte die Buchung wegen der Ressourcenregel wieder auf
Genehmigung offen; damit wurde auch diese Aussage der Anleitung praktisch bestätigt.
Eine globale Schließzeit wurde über die UI gespeichert (HTTP 201, ein Eintrag).
Die geöffneten Buchungsdetails bestätigten, dass Entscheidungen anschließend in
der Anfragenliste getroffen werden müssen; dieser fehlende Schritt wurde ergänzt.

Bestehende UI-Abweichung: Der Ablehnungsdialog nennt den Entscheidungsgrund
optional, die aktuelle DTO-Validierung verlangt ihn. Die Anleitung nennt die
Pflicht ausdrücklich; keine Softwareänderung im Dokumentationsauftrag.

Serien und kombinierte Buchungen, Gruppenlimits sowie Sperrkonflikte wurden gegen
aktuelle Komponenten, Controller, Services und Validierungen geprüft. Sie wurden
in dieser Aufgabe nicht sämtlich erneut End-to-End durchgespielt. Keine externe
Benachrichtigungszustellung oder Hardwarewirkung geprüft. Kein Website-Build;
vorhandene native Komponenten werden dort bereits für die Ressourcen-Seiten genutzt.

## Abschließende Prüfung

| Prüfung               | Ergebnis                                                                                                                                                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Produktionsbuild      | Erfolgreich, einschließlich TypeScript.                                                                                                                                                                                  |
| Vorhandene Doku-Tests | 66 Tests für Navigation, Markdown und relative Links bestanden.                                                                                                                                                          |
| Desktop und Mobil     | Bei 1440, 390 und 320 px HTTP 200, keine Browser-Seitenfehler und kein horizontaler Dokumentüberlauf. Drei native Steps, drei geladene Bilder mit Alternativtext, 16 px Fließtext.                                       |
| Tastatur und Bestand  | Alle drei Lightbox-Bilder per Enter geöffnet und per Escape geschlossen. Alle neun bisherigen Abschnittsanker bei 390 px sichtbar unter der mobilen Kopfzeile.                                                           |
| Links und Export      | 21 interne Artikelverweise auf sieben Seitenziele einschließlich Abschnitten geprüft. Markdown enthält alle drei aufrufbaren Bilder und den Warnungstext; keine Steps-/ImageZoom-/Callout-Ausdrücke oder Imports.        |
| Suche                 | LLM-Index enthält die Seite. Suchbegriff Buchungsanfragen findet sie nach Präzisierung der Überschrift direkt.                                                                                                           |
| Umfang                | SHA-256-Vergleich bestätigt: nur die vorhandene Seite wurde gegenüber dem Start dieser Aufgabe verändert; drei neue Screenshots und dieser Plan ergänzt. Andere Produktseiten, Navigation und Consumer-Code unverändert. |

Der Formatcheck berücksichtigt den Submodule-Inhalt ausdrücklich mit
`prettier --ignore-path /dev/null`, da das Dashboard das Content-Submodule sonst
ignoriert. Die Screenshot-Testinstanz wird nach den Aufnahmen entfernt; die
Doku-Vorschau bleibt auf Port 3400 verfügbar. Keine neuen Dependencies,
API-/DTO-Änderungen, Commits, Pushes oder Veröffentlichungen.
