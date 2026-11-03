# Ressourcenanleitungen umsetzen

**Auftrag:** Den im Chat abgestimmten Einstieg „Ressourcen einrichten“ und die
ausgelagerten Aufgaben ausarbeiten. Leser verwalten Räume und Maschinen; der
Einstieg führt am Beispiel Holzwerkstatt vom Anlegen zum aktiven Raum.

**Umfang:** Nur die Ressourcenanleitung, fünf Anschlussanleitungen, die zugehörige
Navigation und deren Consumer-Zuordnung. Andere Produktseiten bleiben unverändert,
auch bereits vorhandene lokale Änderungen. Keine API-, DTO- oder Produktänderung.

**Mittel:** Vorhandene MDX-Inhalte, Fumadocs-Ordner mit `pagesIndex`, bestehende
Bereichsfilter, lokale UI-Texte, Komponenten und Backend-Verträge. Keine neue
Dependency. Bisherige Seitenadresse und alle neun Abschnittsanker bleiben erhalten.

## Umsetzung

- [x] Ausgangsinhalt und eingehende Links erfassen; UI-Bezeichnungen, Rechte und
      Folgen mit Implementierung und vorhandenen Verträgen abgleichen.
- [x] Den Einstieg unter `docs/koordination/ressourcen.mdx` verdichten. Alte Anker
      führen zu den erhaltenen Einstiegsschritten oder zu sichtbaren Anschlusslinks.
- [x] Unter `docs/administration/` die Anleitungen `ressourcen-buchbarkeit`,
      `ressourcen-zutritt`, `ressourcen-aendern-entfernen`, `ressourcen-wartung` und
      `ressourcen-zustand` ausarbeiten. Vorhandene Freigaben-, Geräte- und
      Automationsanleitungen verlinken, statt sie zu duplizieren.
- [x] Die fünf Seiten als native Unterseiten des bestehenden Ressourceneinstiegs
      veröffentlichen und den vorhandenen Bereichsfilter ergänzen. Koordinationslinks
      behalten ihre bisherigen Adressen und Ziele.
- [x] Navigationstests, Format und Build prüfen. Die sechs Seiten rendern; Links,
      alte Anker, Markdown-Ausgabe und mobile Sidebar prüfen. Umfang und Ergebnisse
      hier ergänzen. Nicht geprüfte Consumer benennen.

## Prüfschwerpunkte

- Aktivierung richtet weder Buchbarkeit noch elektronischen Zutritt ein.
- Globale Rechte und Verwaltungszuständigkeiten nicht vermischen.
- Bei Sperren, Zuordnungslösung, Stilllegung und Löschung bleiben notwendige
  Voraussetzungen und Folgen vor der betroffenen Aktion sichtbar.
- Keine neuen leeren Seiten, keine erfundenen Links und keine veralteten Screenshots.
- Bestehende eingehende Abschnittslinks bleiben ohne Änderungen anderer Seiten nutzbar.

## Ergebnis

Umgesetzt und im Software-Consumer geprüft. Nur die bestehende Ressourcenanleitung
und `docs/administration/meta.json` wurden innerhalb der vorher vorhandenen
Produktquelle verändert. Hinzu kommen die fünf Anleitungen und der Metadatenordner.
Ein SHA-256-Vergleich mit dem Arbeitsstand vor dieser Aufgabe bestätigt, dass alle
anderen Inhalte einschließlich bereits vorhandener lokaler Änderungen unverändert sind.

Der Einstieg behält seine URL unter Koordination und seine Zuordnung zur
Administration. Die neun früheren Abschnittsanker bleiben erhalten: Anlegen führt
zum Einstiegsschritt, ausgelagerte Themen zu sichtbaren Aufgabenlinks. Für diese
Anker wird der vorhandene Fumadocs-Scrollabstand `scroll-m-28` wiederverwendet,
damit die mobile Kopfzeile das Ziel nicht verdeckt. Kein zusätzlicher
Kompatibilitäts-Clientcode, keine neue CSS-Regel und keine Akkordeons.

Vorhandene Geräte-, Automations-, Freigaben- und Zuständigkeitsanleitungen werden
verlinkt. Die bisherigen Screenshots bleiben als Dateien erhalten, werden aber
wegen ihres früheren Layouts nicht mehr eingebunden.

Die unabhängige Inhaltsprüfung führte zu zwei Korrekturen: Bearbeitungs- und
Löschrecht sind unabhängig; die Aus-Bestätigung beim direkten Schalter darf nicht
auf den Austausch eines Zutrittspunkt-Aktors übertragen werden. Der Hinweis auf
den fehlenden Abschaltbefehl beim Lösen einer Zuordnung steht bei beiden Abläufen.

| Prüfung                    | Ergebnis                                                                                                                                                                                                                                                                          |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Navigation Dashboard       | Neuer Gruppentest zunächst 1 Fehler / 53 bestanden, nach Anpassung 54 bestanden. Eltern-URL, fünf Kinder, Eigentümer und eindeutige Platzierung geprüft.                                                                                                                          |
| Doku-Tests Dashboard       | 70 Tests in fünf vorhandenen Testdateien bestanden: Navigation, Markdown, relative Links, Feedback und Quellreferenz.                                                                                                                                                             |
| Format und Code            | Expliziter Formatcheck der geänderten MDX-/JSON-Dateien und scoped TypeScript-Formatcheck bestanden; ESLint der beiden geänderten Dashboard-Dateien bestanden.                                                                                                                    |
| Produktionsbuild Dashboard | Build einschließlich TypeScript erfolgreich.                                                                                                                                                                                                                                      |
| Gerenderte Inhalte         | Sechs Seiten HTTP 200; 76 interne Artikelverweise mit zwölf unterschiedlichen Zielseiten geprüft, keine defekten Links oder Abschnittsziele.                                                                                                                                      |
| Markdown und Suche         | Sechs Markdown-Ausgaben mit aufgelösten Links; Warnungstext erhalten, keine JSX-Ausdrücke. Alle sechs Seiten im LLM-Index; drei Suchanfragen finden die erwarteten neuen Anleitungen.                                                                                             |
| Browser                    | Alle sechs Seiten bei 1440 und 390 px geprüft: keine Seitenfehler oder horizontale Dokumentüberläufe. Alle neun alten Anker abschließend bei 390 px sichtbar; fünf Unterseiten im geöffneten mobilen Ordner, Tastaturaktivierung und Weiterklick vom alten Zugriffsanker geprüft. |
| Website-Consumer           | Nur fünf Slugs in `apps/mardu-de/lib/docs-roles.tsx` ergänzt. Vorher 44/45 Tests mit neuem Inhalt, danach 45/45; ebenfalls 45/45 mit dem dort weiterhin eingebundenen bisherigen Inhalt. Scoped Formatcheck bestanden.                                                            |

Der Website-Content-Verweis wurde nicht geändert. Dort fand kein neuer Build oder
Browsertest statt; die Prüfung verwendet den neuen kanonischen Inhalt über die
bereits vorhandene Testvariable `MARDU_DOCS_TEST_ROOT`. Es wurden keine Änderungen
am Softwareverhalten oder an APIs/DTOs vorgenommen. Die Aussagen wurden gegen
UI, Übersetzungen und Backend-Verträge abgeglichen; ein neuer Hardwaretest gehört
nicht zu dieser Inhaltsüberarbeitung. Nicht committet, gepusht oder veröffentlicht.

## Zweiter Auftrag: native Komponenten und visuelle Hilfen

Umfang: dieselben sechs Ressourcen-Seiten mit nativen Steps, gezielten Callouts
und aktuellen Screenshots beziehungsweise kleinen Diagrammen verständlicher machen.
Die selbst gebaute Sidebar-Gruppenkomponente entfällt zugunsten des Fumadocs-
Standards. Nur die dafür nötige gemeinsame Darstellung und DESIGN.md werden
angepasst; andere Produkttexte bleiben unverändert.

Gemessene Referenzen: Mollie Artikeltext 14 px / 22,4 px Zeilenhöhe; SumUp
17 px / 22 px. Mardu behält 16 px Fließtext. Für die sechs Anleitungen werden
Lesebreite und übermäßige Kopfabstände über native Fumadocs-Props begrenzt.
Keine zweite Typografie-Engine, kein eigener Sidebar-Renderer.

- [x] Nativen Sidebar-Standard wiederherstellen und lokale Lesedarstellung abstimmen.
- [x] Komponenten und Verständlichkeit der sechs Seiten überarbeiten, alte Anker erhalten.
- [x] Aktuelle Screenshots mit fiktiven Daten und passende Diagramme einbinden.
- [x] Desktop, Mobil, Zoom, Suche, Markdown und Verweise prüfen; Ergebnisse ergänzen.


### Ergebnis des zweiten Auftrags

Die Sidebar verwendet wieder den nativen `DocsLayout`-Renderer; der eigene
Separator mit Großschreibung, Trennlinien und zusätzlichen Abständen wurde entfernt.
Die fünf Unterseiten haben kurze native Linknamen. Seitentitel und URLs bleiben
vollständig erhalten. Die gemeinsamen Sidebar-Änderungen gelten für die Doku;
Lesebreite und kompakter Seitenkopf sind auf die sechs Ressourcenanleitungen begrenzt.

Native `Steps`/`Step` strukturieren zusammenhängende Einrichtungsschritte.
Unabhängige Aufgaben bleiben eigenständige Abschnitte. Zwei gezielte Warnungen
stehen bei endgültiger Stilllegung beziehungsweise beim Lösen von Schaltern.
Alle sechs Seiten verwenden `ImageZoom` mit der vorhandenen Lightbox und
beschreibenden Alternativtexten. Tabellen bleiben Tabellen; keine neuen Akkordeons.

Drei aktuelle Screenshots zeigen das Anlegen des Raums, die Buchbarkeit und eine
Sperre. Sie wurden am 03.11.2026 in der vorhandenen Oberfläche mit einer isolierten
Testdatenbank und fiktiven Daten aufgenommen. Raum, Buchungskonfiguration und Sperre
wurden dort über die UI gespeichert. Das sind Softwareprüfungen, kein Hardwaretest.
Drei kleine SVG-Diagramme erklären Zutrittsbeziehungen, den Ressourcenlebenszyklus
und die getrennten Schaltzustände. Ihre Aussagen stehen auch im Text.

| Prüfung | Ergebnis |
| --- | --- |
| Build und Code | Produktionsbuild mit TypeScript erfolgreich; scoped ESLint, Format und Design-Lint bestanden. Layout-/Typografie-Detektoren ohne Befund. |
| Doku-Tests | 66 Tests für Navigation, Markdown und relative Links bestanden. Website-Navigation mit neuem kanonischem Inhalt: 45 Tests bestanden. |
| Desktop und Mobil | 18 Aufrufe: alle sechs Seiten bei 1440, 390 und 320 px ohne Seitenfehler oder horizontalen Dokumentüberlauf. Alle Bilder geladen. Fließtext 16 px / 28 px. |
| Bedienung | Mobile Sidebar zeigt alle fünf Unterseiten, ist scrollbar und per Tastatur bedienbar. Seitenwechsel schließt sie; native Lightbox öffnet per Enter und schließt per Escape. |
| Bestandslinks | Alle neun historischen Anker sowie die beiden bisherigen nummerierten Schrittanker bei 390 px sichtbar unter der Kopfzeile. 76 Artikelverweise ohne defekte Ziele. |
| Export und Suche | Alle sechs Markdown-Ausgaben enthalten aufrufbare Bilder und Alttexte ohne Komponenten-JSX oder Imports. LLM-Index und drei Suchanfragen geprüft. |
| Umfang | SHA-256-Vergleich: nur die sechs Ressourcen-MDX-Dateien und deren Ordner-Metadaten wurden gegenüber dem Beginn dieses Auftrags verändert; sechs Bilddateien ergänzt. Andere Produkttexte unverändert. |

React Doctor meldet 475 bestehende projektweite Befunde. Diese wurden nicht im
Rahmen der Doku-Aufgabe bearbeitet. Kein neuer Website-Build/Browsertest und kein
Hardwaretest; API und DTOs unverändert. Nicht committet oder veröffentlicht.
