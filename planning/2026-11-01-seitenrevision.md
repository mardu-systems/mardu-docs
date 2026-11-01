# Koordination der vollständigen Seitenrevision

Stand: 1. November 2026. Auftrag: jede Seite einzeln mit der Arbeitsweise abgleichen;
gute Seiten unverändert lassen, belegte Fehler und Lücken beheben. Danach Navigation,
Überblick und Querverweise zusammenführen. Ausgangspunkt: Docs `611fe8d`,
Web `ec456bd4`, Hauptrepository `6f2dda9f`.

Abgeschlossen: Einzelprüfung und Consumer-Integration.
[Ergebnis, Gesamtprüfungen und offene praktische Grenzen](2026-11-01-seitenrevision-ergebnis.md).

## Durchführung

- Ein eigener Seiten-Agent pro Seite, mit frischem Kontext und eindeutiger Dateizuständigkeit.
- Gemeinsamer [Agentenbrief](2026-11-01-seitenrevision-agentenbrief.md).
- Agenten schreiben nur ihre Seite und ihren Bericht unter `reviews/2026-11-01/`.
- Der Koordinator besitzt den [Fortschritt](2026-11-01-seitenrevision.json), diese
  Tabelle sowie gemeinsame Navigation, Bereichsstarts und Consumer-Integration.
- Die Wellen 1–6 prüfen Fachseiten; Welle 7 prüft Einstiege nach den Ergebnissen.
  Frei werdende Slots werden mit der nächsten einzelnen Seite belegt.
- Berichte trennen gute unveränderte Inhalte, Änderungen, Quellen, tatsächliche
  Prüfungen und noch fehlende Hardware-/Anbieterbelege. Keine Änderungsquote.
- Generierte API-Seiten werden anhand aller Operationen, Exporte und Quellverträge
  zentral geprüft. Keine manuelle Kopie der generierten Referenz.
- Neue Anleitungen bekommen nach belegtem Bedarf eigene Dateizuständigkeiten.
- Bestehender sauberer Checkout wird weiterverwendet. Keine externen Meldungen,
  Pushes oder Releases. Gemeinsame Tests/Browserprüfungen werden gebündelt.

## Seitenaufträge

| ID  | Welle | Seite                                                                                                      | Status                                     | Agent          |
| --- | ----- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------ | -------------- |
| P01 | 1     | [benutzer/erste-schritte.mdx](../docs/benutzer/erste-schritte.mdx)                                         | verbessert; Dokuprüfung abgeschlossen      | /root/page_p01 |
| P02 | 1     | [benutzer/dashboard.mdx](../docs/benutzer/dashboard.mdx)                                                   | verbessert; Dokuprüfung abgeschlossen      | /root/page_p02 |
| P03 | 1     | [benutzer/zutritt.mdx](../docs/benutzer/zutritt.mdx)                                                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p03 |
| P04 | 1     | [benutzer/buchungen.mdx](../docs/benutzer/buchungen.mdx)                                                   | verbessert; Dokuprüfung abgeschlossen      | /root/page_p04 |
| P05 | 1     | [benutzer/berechtigungsanfragen.mdx](../docs/benutzer/berechtigungsanfragen.mdx)                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p05 |
| P06 | 1     | [benutzer/kalender.mdx](../docs/benutzer/kalender.mdx)                                                     | verbessert; Dokuprüfung abgeschlossen      | /root/page_p06 |
| P07 | 1     | [benutzer/kompetenzen.mdx](../docs/benutzer/kompetenzen.mdx)                                               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p07 |
| P08 | 1     | [benutzer/benachrichtigungen.mdx](../docs/benutzer/benachrichtigungen.mdx)                                 | verbessert; Dokuprüfung abgeschlossen      | /root/page_p08 |
| P09 | 1     | [benutzer/geraete-status.mdx](../docs/benutzer/geraete-status.mdx)                                         | verbessert; Dokuprüfung abgeschlossen      | /root/page_p09 |
| P10 | 2     | [ueberblick/profil.mdx](../docs/ueberblick/profil.mdx)                                                     | verbessert; Dokuprüfung abgeschlossen      | /root/page_p10 |
| P11 | 2     | [ueberblick/profil-sicherheit.mdx](../docs/ueberblick/profil-sicherheit.mdx)                               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p11 |
| P12 | 2     | [ueberblick/profil-sitzungen.mdx](../docs/ueberblick/profil-sitzungen.mdx)                                 | verbessert; Dokuprüfung abgeschlossen      | /root/page_p12 |
| P13 | 2     | [ueberblick/profil-zutrittsmedien.mdx](../docs/ueberblick/profil-zutrittsmedien.mdx)                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p13 |
| P14 | 2     | [ueberblick/profil-nachweisquellen.mdx](../docs/ueberblick/profil-nachweisquellen.mdx)                     | verbessert; Dokuprüfung abgeschlossen      | /root/page_p14 |
| P15 | 2     | [ueberblick/profil-benachrichtigungen.mdx](../docs/ueberblick/profil-benachrichtigungen.mdx)               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p15 |
| P16 | 2     | [ueberblick/profil-erscheinungsbild.mdx](../docs/ueberblick/profil-erscheinungsbild.mdx)                   | verbessert; Dokuprüfung abgeschlossen      | /root/page_p16 |
| P17 | 2     | [ueberblick/profil-mcp.mdx](../docs/ueberblick/profil-mcp.mdx)                                             | verbessert; Dokuprüfung abgeschlossen      | /root/page_p17 |
| P18 | 3     | [administration/benutzer-rollen.mdx](../docs/administration/benutzer-rollen.mdx)                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p18 |
| P19 | 3     | [administration/tags-verwalten.mdx](../docs/administration/tags-verwalten.mdx)                             | unverändert gut; Dokuprüfung abgeschlossen | /root/page_p19 |
| P20 | 3     | [administration/geraete-verwalten.mdx](../docs/administration/geraete-verwalten.mdx)                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p20 |
| P21 | 3     | [administration/badges-verwalten.mdx](../docs/administration/badges-verwalten.mdx)                         | verbessert; Dokuprüfung abgeschlossen      | /root/page_p21 |
| P22 | 3     | [administration/automationen.mdx](../docs/administration/automationen.mdx)                                 | verbessert; Dokuprüfung abgeschlossen      | /root/page_p22 |
| P23 | 3     | [administration/mcp-verwalten.mdx](../docs/administration/mcp-verwalten.mdx)                               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p23 |
| P24 | 3     | [administration/benachrichtigungen-verwalten.mdx](../docs/administration/benachrichtigungen-verwalten.mdx) | verbessert; Dokuprüfung abgeschlossen      | /root/page_p24 |
| P25 | 3     | [koordination/ressourcen.mdx](../docs/koordination/ressourcen.mdx)                                         | verbessert; Dokuprüfung abgeschlossen      | /root/page_p25 |
| P26 | 4     | [administration/integrationen.mdx](../docs/administration/integrationen.mdx)                               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p26 |
| P27 | 4     | [administration/server-einstellungen.mdx](../docs/administration/server-einstellungen.mdx)                 | verbessert; Dokuprüfung abgeschlossen      | /root/page_p27 |
| P28 | 4     | [administration/sicherheit-betrieb.mdx](../docs/administration/sicherheit-betrieb.mdx)                     | verbessert; Dokuprüfung abgeschlossen      | /root/page_p28 |
| P29 | 4     | [administration/nachweise-datenschutz.mdx](../docs/administration/nachweise-datenschutz.mdx)               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p29 |
| P30 | 4     | [administration/zutritt-verwalten.mdx](../docs/administration/zutritt-verwalten.mdx)                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p30 |
| P31 | 4     | [administration/wartungs-cli.mdx](../docs/administration/wartungs-cli.mdx)                                 | verbessert; Dokuprüfung abgeschlossen      | /root/page_p31 |
| P32 | 4     | [administration/wartungs-cli-referenz.mdx](../docs/administration/wartungs-cli-referenz.mdx)               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p32 |
| P33 | 4     | [benutzer/uebersicht-monitoring.mdx](../docs/benutzer/uebersicht-monitoring.mdx)                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p33 |
| P34 | 5     | [installieren/raspberry-pi.mdx](../docs/installieren/raspberry-pi.mdx)                                     | verbessert; Dokuprüfung abgeschlossen      | /root/page_p34 |
| P35 | 5     | [installieren/inbetriebnahme.mdx](../docs/installieren/inbetriebnahme.mdx)                                 | verbessert; Dokuprüfung abgeschlossen      | /root/page_p35 |
| P36 | 5     | [installieren/abnahme-uebergabe.mdx](../docs/installieren/abnahme-uebergabe.mdx)                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p36 |
| P37 | 5     | [installieren/stoerung-vor-ort.mdx](../docs/installieren/stoerung-vor-ort.mdx)                             | verbessert; Dokuprüfung abgeschlossen      | /root/page_p37 |
| P38 | 5     | [entwickeln/api-integration.mdx](../docs/entwickeln/api-integration.mdx)                                   | verbessert; Dokuprüfung abgeschlossen      | /root/page_p38 |
| P39 | 5     | [entwickeln/http-api.mdx](../docs/entwickeln/http-api.mdx)                                                 | verbessert; Dokuprüfung abgeschlossen      | /root/page_p39 |
| P40 | 5     | [entwickeln/mqtt-events.mdx](../docs/entwickeln/mqtt-events.mdx)                                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p40 |
| P41 | 5     | [entwickeln/mcp-anbindung.mdx](../docs/entwickeln/mcp-anbindung.mdx)                                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p41 |
| P42 | 6     | [koordination/buchungen-verwalten.mdx](../docs/koordination/buchungen-verwalten.mdx)                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p42 |
| P43 | 6     | [koordination/bewertungen.mdx](../docs/koordination/bewertungen.mdx)                                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p43 |
| P44 | 6     | [ueberblick/benutzerkonten.mdx](../docs/ueberblick/benutzerkonten.mdx)                                     | verbessert; Dokuprüfung abgeschlossen      | /root/page_p44 |
| P45 | 6     | [ueberblick/grundlagen-begriffe.mdx](../docs/ueberblick/grundlagen-begriffe.mdx)                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p45 |
| P46 | 6     | [ueberblick/fehlersuche.mdx](../docs/ueberblick/fehlersuche.mdx)                                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p46 |
| P47 | 6     | [ueberblick/neuerungen.mdx](../docs/ueberblick/neuerungen.mdx)                                             | verbessert; Dokuprüfung abgeschlossen      | /root/page_p47 |
| P48 | 6     | [v1/index.mdx](../docs/v1/index.mdx)                                                                       | unverändert gut; Dokuprüfung abgeschlossen | /root/page_p48 |
| P49 | 6     | [v2/index.mdx](../docs/v2/index.mdx)                                                                       | unverändert gut; Dokuprüfung abgeschlossen | /root/page_p49 |
| P50 | 7     | [index.mdx](../docs/index.mdx)                                                                             | unverändert gut; Dokuprüfung abgeschlossen | /root/page_p50 |
| P51 | 7     | [ueberblick/index.mdx](../docs/ueberblick/index.mdx)                                                       | unverändert gut; Dokuprüfung abgeschlossen | /root/page_p51 |
| P52 | 7     | [benutzer/index.mdx](../docs/benutzer/index.mdx)                                                           | verbessert; Dokuprüfung abgeschlossen      | /root/page_p52 |
| P53 | 7     | [koordination/index.mdx](../docs/koordination/index.mdx)                                                   | verbessert; Dokuprüfung abgeschlossen      | /root/page_p53 |
| P54 | 7     | [administration/index.mdx](../docs/administration/index.mdx)                                               | verbessert; Dokuprüfung abgeschlossen      | /root/page_p54 |
| P55 | 7     | [installieren/index.mdx](../docs/installieren/index.mdx)                                                   | verbessert; Dokuprüfung abgeschlossen      | /root/page_p55 |
| P56 | 7     | [entwickeln/index.mdx](../docs/entwickeln/index.mdx)                                                       | verbessert; Dokuprüfung abgeschlossen      | /root/page_p56 |

## Integration nach den Seitenprüfungen

- [x] Alle 56 Berichte und Patches gegen Quellen und Auftrag prüfen.
- [x] Fehlende Aufgaben kanonischen Seiten zuordnen und belegbaren Inhalt ergänzen.
- [x] Überblick und sechs Bereichsstarts mit dem geprüften Umfang abgleichen.
- [x] Navigation/Suche nur mit nutzbaren Seiten erweitern, alte URLs und Anker erhalten.
- [x] Relative Links, Abschnittsanker, Bilder und Markdown-Ausgaben prüfen.
- [x] API-Referenz und alle generierten Exporte strukturell prüfen.
- [x] Browserprüfungen bündeln; Desktop, Mobil, Themes und praktische Abläufe berücksichtigen.
- [x] Passende Tests, Typecheck, Lint und Build ausführen; offene Grenzen berichten.

## Entscheidungen und Wiederaufnahme

- Der JSON-Fortschritt ist die Zuordnungsquelle. Vor neuer Vergabe vorhandenen
  Seitenbericht und Agentenstatus prüfen; abgeschlossene Seiten nicht neu starten.
- Kein Seiten-Agent darf Navigation, gemeinsamen Backlog oder Softwarecode ändern.
  Bestätigte Produktfehler gehen mit Beleg an den Koordinator.
- Eine statische Prüfung ist keine Hardware-/Versandabnahme. Offene Belege werden
  außerhalb des Produkttexts festgehalten.

## Bereichsübergreifende Befunde während Welle 1

- P01 → Profilseite P10: Profilzugang heißt im aktuellen Kontomenü
  „Kontoeinstellungen“. Alte Folge „Mein Profil → Profil“ abgleichen.
- P03: Drei veraltete Ressourcenbilder zeigen alte Action-/Modusbegriffe.
  Nachweislich irreführende Bilder entfernen; keine Produktansicht erfinden.
- P04: UI zeigt Wiederholung auch für mehrere Ressourcen; der aktuelle Submitpfad
  priorisiert die kombinierte Buchung. Dokumentation muss den unterstützten
  Einzelressourcen-Serienablauf beschreiben; Produktabweichung separat verfolgen.
- P07: Persönliche Qualifikationen zeigen keinen Eligibility-/Anforderungsstatus.
  Verwaltungs-Endpunkte nicht als Portalaktion beschreiben.
- P08: Öffnen einer Mitteilung markiert sie nicht automatisch gelesen;
  Sammelaktionen nicht als auf sichtbare Suchtreffer begrenzt beschreiben.

## Belegte Zusatzbedarfe

Der [Zusatzseitenplan](2026-11-01-zusatzseiten.json) ordnet fehlende Aufgaben aus
Bestandsplan und Seitenberichten eigenen Agenten zu. Ein Titel ist noch kein
Veröffentlichungsauftrag: der jeweilige Agent prüft zuerst einen tatsächlich
verfügbaren Ablauf. Überschneidet er sich vollständig mit einer verbesserten
Bestandsanleitung, bleibt die bestehende Quelle kanonisch. Nicht angebotene
Funktionen werden als Bedarf dokumentiert, nicht mit erfundenen Schritten ergänzt.
Die sieben Einstiege werden erst nach dieser Lückenprüfung abschließend bearbeitet.

## Prüfgrundlage und offene praktische Zugänge

- Alle 56 Ausgangsrouten antworteten auf dem bisherigen lokalen Consumer mit HTTP 200.
- 383 Artikel-IDs (davon 377 stabile Abschnittsanker) sind unter `reviews/2026-11-01/baseline-anchors.json`
  für die Erhaltungsprüfung gesichert.
- Vorhandene E2E-Speicherzustände sind für eine frühere Testinstanz und lassen
  sich mit der aktuellen lokalen Sitzungskonfiguration nicht verwenden. Es sind
  keine aktuellen E2E-Testkonto-Variablen gesetzt. Keine Nutzercredentials angefordert
  oder offengelegt und keine reale Kontomutation vorgenommen.
- Statische Quellenprüfung, Dokument-Rendering und Backend-/Provider-/Hardware-
  Abnahme bleiben getrennte Nachweise.

## Korrekturen nach unabhängiger Querschnittsprüfung

- LDAP-Deprovisioning: Admin-Ausnahme nur bei direkter Rollenzuweisung;
  Gruppen-Admins ausdrücklich von dieser Ausnahme abgegrenzt.
- IP500-Überblick verspricht keine periodische Subscription-Erneuerung mehr.
- LDAP-/OIDC-Settingsrechte und zusätzliche UI-/Navigationsrechte abgeglichen.
- LDAP-Testaktualität nicht mit erfolgreichem Verbindungstest gleichgesetzt.
- Aktiver Freigabeneditor bietet neue Person-/Gruppenfreigaben, keine neue
  Tag-Freigabe; Ressourcenanleitung auf kanonische Freigabenanleitung abgestimmt.
- Vorhandenen Flow-Leitfaden aus MCP-/MQTT-Entwicklerseiten erschlossen.
- Profilverweis in Posteingang auf aktuellen Kontoeinstellungen-Einstieg korrigiert.
- Deutsche handgeschriebene Artikel erhalten lang=de unabhängig von der
  übergeordneten Dashboard-Sprache.
- Markdown-Dateiverweise werden über den bestehenden Fumadocs-Stringifier und
  native source.resolveHref auf öffentliche Ziele aufgelöst; eigene Tests.

## Abschließender Consumer-Abgleich

- Alle Seiten erneut im gebauten Software-Consumer gerendert. Abschnittsanker,
  Bilder, Links, Suchfilter, Bereichswechsel und Markdown-Ausgabe geprüft.
- Die vorhandene native Fumadocs-Lightbox behebt den fehlenden Tastaturzugang
  der bisherigen Zoom-Darstellung; Enter und Escape praktisch geprüft.
- Website-Filter in zwei Content-Ständen geprüft; gemeinsame HTTP-Verweise
  auf portable Methoden/Pfade umgestellt. Der Website-Content-Gitlink bleibt alt.
- Erledigte Schreibaufträge im Backlog durch offene praktische Prüfungen ersetzt.
- Commit auf anschließenden ausdrücklichen Auftrag; keine externen Meldungen,
  Pushes oder Veröffentlichung.
