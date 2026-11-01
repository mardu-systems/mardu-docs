# P50 – Dokumentationsstart

## Auftrag und Entscheidung

- Seite: `docs/index.mdx`; Heimatbereich: bereichsübergreifender Wegweiser, im Software-Consumer dem Überblick zugeordnet.
- Leserfrage: „Ich kenne Mardu noch nicht oder suche eine Anleitung: Wo beginne ich für meine Aufgabe?“ Vorwissen über Menüs, Systemrollen oder interne Module ist nicht erforderlich.
- Ergebnis: **unverändert gut**. Der kurze Einstieg erklärt den ersten Lernschritt und ordnet Aufgaben allen sechs Lesereinstiegen zu. Keine belegte Orientierungslücke erfordert eine Textänderung.
- Vorgehen: Regeln und Arbeitsweise, offene Aufgaben und Zusatzseitenplan lesen; die sechs verlinkten Bereichsstarts und Consumer-Zuordnung vergleichen; anschließend Format, Verweise, Frontmatter und Anker dateibezogen prüfen. Keine Produkt- oder Navigationsänderung.

## Befunde und erhaltene Inhalte

| Aussage des Wegweisers                                     | Geprüfte Quelle und Befund                                                                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Zuerst das Systemmodell verstehen                          | `docs/ueberblick/index.mdx:6–15,24–47`: Personen, Ressourcen und optionale technische Ergänzungen werden erklärt; Ressource und Gerät werden unterschieden. Der vorhandene erste Link ist passend.                                                                                                                                           |
| Eigene Ressourcen, Buchungen und Kontoeinstellungen nutzen | `docs/benutzer/index.mdx:6–30`: persönliche Freigaben, Buchungen, erste Nutzung, Profil und Hilfe.                                                                                                                                                                                                                                           |
| Verfügbarkeit und Nutzung organisieren                     | `docs/koordination/index.mdx:6–25`: laufende Organisation, Ressourcenstatus, Wartung und Buchbarkeit. Der Einstieg verlangt keine feste Systemrolle.                                                                                                                                                                                         |
| Konten, Ressourcen, Technik und Betrieb einrichten         | `docs/administration/index.mdx:6–57`: Personen, Ressourcen, Geräte, Anbindungen und Betrieb sind die vorhandenen Themen.                                                                                                                                                                                                                     |
| Einen Server aufbauen und Geräte aufnehmen                 | `docs/installieren/index.mdx:6–23`: Serverinstallation und ausdrücklich benannter Wechsel zur Geräteverwaltung. Der Wegweiser verspricht keine vollständige Montage- oder Hardwareabnahme.                                                                                                                                                   |
| Eigene Software anbinden                                   | `docs/entwickeln/index.mdx:6–26`: Integrationsziel, MCP und HTTP-Referenz; der Wegweiser behauptet keine Anleitung zur gesamten Serverentwicklung.                                                                                                                                                                                           |
| Lesereinstiege vergeben keine Rechte                       | `docs/koordination/index.mdx:6–8`, `docs/administration/index.mdx:10–12` und `web/lib/docs-roles.tsx:25,69–178`: sechs Navigationsdefinitionen mit eigenem Bereichsstart; keine Rollenvergabe durch diese Struktur.                                                                                                                          |
| Navigation und Dokumentationsumfang                        | `docs/meta.json:3–10` führt genau die sechs Bereiche neben dem Start. `planning/offene-dokumentationsaufgaben.md:46–68` und `planning/2026-11-01-zusatzseiten.json` belegen verbleibenden bzw. ergänzten Aufgabenbedarf. Der vorsichtige Umfangshinweis bleibt zutreffend; ein vollständiges Seiteninventar wäre kein Vollständigkeitsbeleg. |

Die neuen Fachanleitungen gehören in ihre jeweiligen Bereiche. Sie begründen keine weitere Featureliste auf dem Dokumentationsstart. Alle sechs Einstiege, die bestehenden Formulierungen und die URL bleiben erhalten; keine v1-/v2-Einstiege ergänzt. Vorhandene Mittel bleiben Frontmatter, Absätze, Aufgabentabelle und relative MDX-Verweise. API-/DTO-Dokumentation ist nicht betroffen.

## Links, Anker und Übergabe

- Alle sieben Seitenverweise lösen auf vorhandene Dateien auf: zweimal `./ueberblick/index.mdx` sowie je einmal `./benutzer/index.mdx`, `./koordination/index.mdx`, `./administration/index.mdx`, `./installieren/index.mdx` und `./entwickeln/index.mdx`.
- Die Startseite enthält keine eigenen Überschriften-/ID-Anker und keine Links mit Fragment. `baseline-anchors.json` verzeichnet für `index.mdx` lediglich `nd-page`; dieser Consumer-Anker wird durch die unveränderte Produktquelle nicht angefasst. Seine gerenderte Fortexistenz ist Teil der gemeinsamen Consumerprüfung.
- Root-Metadaten und die `start`-Werte in `web/lib/docs-roles.tsx` stimmen mit allen sechs Zielen überein. Zusatzseiten-Navigation und Aktualisierung der betroffenen Bereichsstarts übernimmt der Koordinator. Insbesondere die dort noch vorhandenen Umfangshinweise müssen nach Abschluss der Zusatzseiten zum finalen Bestand passen; keine Änderung an diesen Nachbarseiten im P50-Auftrag.

## Ausgeführte Checks und Grenzen

- Installiertes Prettier mit `web/.prettierrc`, ausdrücklich `--ignore-path /dev/null`, für `docs/index.mdx` und diesen Bericht: bestanden.
- Lokale Python-Leseprüfung: sieben relative Verweise / sechs vorhandene Ziele, genau die sechs Bereichsstarts in Root-Metadaten, Frontmatter mit Titel/Beschreibung, kein zusätzliches H1, keine Quell-IDs und keine Fragmentlinks: bestanden.
- `git -C web/content/docs diff --check -- docs/index.mdx planning/reviews/2026-11-01/index.md`: ohne Meldung; zusätzlich die neue Berichtsdatei auf nachgestellte Leerzeichen geprüft.
- Ausschließlich statische Prüfung. Kein Browser, kein globaler Build und keine Hardware-/Anbieterprüfung durchgeführt. Die Produktseite bleibt unverändert; gemeinsames Rendering, Consumer-Navigation und finales Zusammenspiel der Zusatzseiten sind nicht durch diesen Bericht abgenommen.

Geänderte Datei: nur `planning/reviews/2026-11-01/index.md`. `docs/index.mdx` ausdrücklich unverändert belassen.
