# Ergebnis der vollständigen Seitenrevision

Stand: 1. November 2026. Ausgangspunkt: Docs `611fe8d`, Dashboard `ec456bd4`,
Hauptrepository `6f2dda9f`. Diese Revision ist lokal; sie wurde nicht veröffentlicht.

## Umfang und Ergebnis

56 vorhandene handgeschriebene Seiten wurden einzeln an Seiten-Agenten vergeben,
gegen Implementierung und Dokumentationsregeln geprüft und anschließend
zusammengeführt. 51 Seiten wurden verbessert, fünf bleiben unverändert. 16
zusätzliche Themen wurden getrennt geprüft: 13 neue Anleitungen schließen belegte
Lücken; drei vorgeschlagene Seiten hätten vorhandene Anleitungen dupliziert.

Damit gibt es 67 aktuelle veröffentlichte Anleitungen, zwei weiterhin erreichbare
historische Einstiege und 554 generierte API-Operationen. Das ist die Abdeckung der
vorhandenen Dokumentation und der festgestellten Lücken, keine Zusage, jede
mögliche Produkteinstellung abschließend dokumentiert zu haben.

Die sechs Bereiche bleiben Überblick, Benutzer, Koordination, Administration,
Installieren und Entwickeln. Bestehende URLs und stabile Abschnittsanker bleiben
erhalten. Neue Inhalte sind in Gruppen eingeordnet; Bereichswechsel verweisen auf
die kanonische Anleitung. Gute Anleitungen wurden nicht nach einer Änderungsquote
umgeschrieben. Die vorhandenen Systemdiagramme bleiben erhalten.

## Einzelne Seiten und Belege

Die [Gesamtprüfdaten](reviews/2026-11-01/gesamtpruefung.json),
die [Auftragstabelle](2026-11-01-seitenrevision.md) und der
[maschinelle Fortschritt](2026-11-01-seitenrevision.json) enthalten jede
Bestandsseite. Für jede Seite gibt es einen Bericht mit Quellen, Änderungen,
Prüfungen und Grenzen. Die folgenden fünf Seiten wurden bewusst nicht geändert:

- [administration/tags-verwalten.mdx](../docs/administration/tags-verwalten.mdx) · [Prüfbericht](reviews/2026-11-01/administration--tags-verwalten.md)
- [v1/index.mdx](../docs/v1/index.mdx) · [Prüfbericht](reviews/2026-11-01/v1--index.md)
- [v2/index.mdx](../docs/v2/index.mdx) · [Prüfbericht](reviews/2026-11-01/v2--index.md)
- [index.mdx](../docs/index.mdx) · [Prüfbericht](reviews/2026-11-01/index.md)
- [ueberblick/index.mdx](../docs/ueberblick/index.mdx) · [Prüfbericht](reviews/2026-11-01/ueberblick--index.md)

Neue Anleitungen:

- [Zugangsanträge entscheiden](../docs/koordination/zugangsantraege-entscheiden.mdx) · [Prüfbericht](reviews/2026-11-01/koordination--zugangsantraege-entscheiden.md)
- [Vergaben und Lernwegteilnahmen begleiten](../docs/koordination/vergaben-lernwegteilnahmen.mdx) · [Prüfbericht](reviews/2026-11-01/koordination--vergaben-lernwegteilnahmen.md)
- [Rollen und Gruppen verwalten](../docs/administration/rollen-gruppen.mdx) · [Prüfbericht](reviews/2026-11-01/administration--rollen-gruppen.md)
- [Verwaltungszuständigkeiten vergeben](../docs/administration/verwaltungszustaendigkeiten.mdx) · [Prüfbericht](reviews/2026-11-01/administration--verwaltungszustaendigkeiten.md)
- [Kompetenzen und Lernwege einrichten](../docs/administration/kompetenzen-lernwege.mdx) · [Prüfbericht](reviews/2026-11-01/administration--kompetenzen-lernwege.md)
- [Nachweissysteme anbinden](../docs/administration/nachweissysteme-anbinden.mdx) · [Prüfbericht](reviews/2026-11-01/administration--nachweissysteme-anbinden.md)
- [LDAP-Verzeichnis anbinden](../docs/administration/ldap-verzeichnis.mdx) · [Prüfbericht](reviews/2026-11-01/administration--ldap-verzeichnis.md)
- [Anmeldung über OpenID Connect](../docs/administration/oidc-anmeldung.mdx) · [Prüfbericht](reviews/2026-11-01/administration--oidc-anmeldung.md)
- [MQTT-Zugänge verwalten](../docs/administration/mqtt-broker.mdx) · [Prüfbericht](reviews/2026-11-01/administration--mqtt-broker.md)
- [IP500-Netzwerk anbinden](../docs/administration/ip500-netzwerk.mdx) · [Prüfbericht](reviews/2026-11-01/administration--ip500-netzwerk.md)
- [Zertifikate und HTTPS verwalten](../docs/administration/zertifikate-https.mdx) · [Prüfbericht](reviews/2026-11-01/administration--zertifikate-https.md)
- [Eigene Automationsflüsse entwickeln](../docs/entwickeln/automationsfluesse.mdx) · [Prüfbericht](reviews/2026-11-01/entwickeln--automationsfluesse.md)
- [Ressourcenfreigaben verwalten](../docs/administration/freigaben-verwalten.mdx) · [Prüfbericht](reviews/2026-11-01/administration--freigaben-verwalten.md)

Die drei Nichtanlagen und ihre Gründe stehen im
[Zusatzseitenplan](2026-11-01-zusatzseiten.json). Verfügbarkeit/Wartung,
Anmeldung/Kontoschutz und Bereiche/Zutrittspunkte bleiben in bereits vorhandenen
kanonischen Anleitungen.

## Zusammenführung und technische Korrekturen

- Navigation und Consumer-Bereichsfilter enthalten die fertig ausgearbeiteten
  Seiten; historische Einstiege werden nicht als aktuelle Anleitung beworben.
- Querschnittsprüfungen glichen Kontoschutz, Ressourcen und Integrationen ab.
  Unter anderem wurden LDAP-Testaktualität, Deprovisioning-Ausnahmen,
  Verwaltungsrechte, IP500-Erneuerung und angebotene Freigaben korrigiert.
- Der Markdown-Export löst relative MDX-Seitenverweise mit Fumadocs
  `source.resolveHref` und dem vorhandenen Stringifier auf. HTML und Beispiele
  bleiben unverändert; sechs Regressionstests decken den Compilerpfad ab.
- Bildvergrößerung verwendet die vorhandene Fumadocs-Lightbox mit Tastaturzugang,
  Escape und deutscher Bildnavigation. Die vorherige Zoom-Variante versteckte
  ihre Tastatur-Schaltflächen. Die Kopierbestätigung ist ebenfalls übersetzt.
- Handgeschriebene deutsche Artikel erhalten `lang="de"`, auch wenn das
  übergeordnete Dashboard auf Englisch eingestellt ist.
- Gemeinsame HTTP-Anleitungen nennen überprüfte Methoden und Pfade anstelle von
  Links auf virtuelle API-Seiten, die im Website-Consumer nicht vorhanden sind.
  Die Software stellt ihre generierte Referenz weiterhin bereit.
- Der lokale Website-Bereichsfilter ist mit altem und neuem Content geprüft und
  angepasst. Sein Content-Gitlink bleibt unverändert. Kein Build oder Browserlauf
  der Website wurde als abgeschlossen ausgegeben.
- Alte OTA-/Provisioning-Notizen wurden eingeordnet; die Kennwort-Reset-Anleitung
  verlangt einen Image-Neubau nur bei alten Images ohne Wartungs-CLI.

Wiederverwendet wurden die vorhandenen MDX-Komponenten, Fumadocs-Navigation,
Suchoberfläche, Bereichsdefinitionen, OpenAPI-Verträge und Testwerkzeuge. Keine
neue Dependency und kein Business-API-/DTO-Vertrag wurden eingeführt oder verändert.

## Ausgeführte Gesamtprüfungen

Prüfungen im lokalen Software-Consumer, einschließlich des gebauten Standes:

- HTTP-/Artikelprüfung: 69 Seiten mit HTTP 200, 996 interne Artikelverweise ohne
  fehlendes Ziel oder Abschnitt. Alle 377 stabilen bisherigen Abschnittsanker sind
  erhalten; sechs dynamische Radix-Steuerungs-IDs sind keine öffentlichen Anker.
- Bilder: 42 eingebundene Artikel-Assets erreichbar, keine fehlenden Alternativtexte.
- Browser: alle 69 Seiten bei 1.440 und 390 Pixeln Breite (138 Aufrufe) ohne
  Seitenfehler, defekte Bilder oder horizontalen Seitenüberstand. Überblick und
  Diagramme auch dunkel gesichtet; Bildansicht mit Enter geöffnet und Escape
  geschlossen. Bereichswechsel durch alle sechs Bereiche und mobile Navigation
  geprüft. Globale Suche, Admin-/Benutzer-/API-Filter und Tastenkürzel verwendet.
  LDAP-Markdown kopiert und Abschnittsanker angesprungen.
- Markdown: alle 554 Operationsverträge und 5.432 lokale Schema-Verweise geprüft;
  keine defekten Referenzen, ungültigen JSON-Blöcke, relativen MDX-Seitenlinks
  oder nicht aufgelösten Bild-/Widget-Platzhalter. Der Index enthält 621 eindeutige
  veröffentlichte Ziele (67 Anleitungen plus 554 Operationen).
- `bun run build`: erfolgreich, einschließlich TypeScript. Zwei CSS-Optimierungs-
  warnungen betreffen Fumadocs `::highlight(fd-search)`. Der lokale Standalone-Lauf
  benötigt statische Assets und `contracts` wie im bestehenden Dockerfile; diese
  wurden für die Vorschau bereitgestellt. Kein Docker-Image oder Produktionshost
  wurde gebaut, verändert oder abgenommen.
- Scoped ESLint der geänderten Software-Dateien ohne Diagnose; Formatierung und
  `git diff --check` in den beteiligten Checkouts geprüft.
- Dashboard: 79 Tests in acht betroffenen Testdateien bestanden, darunter Navigation,
  Markdown-Links, Bilder/Widgets, API-Export, Suche und Feedback.
- React Doctor: 1.171 Dateien geprüft, keine blockierenden Fehler; 476 Warnungen
  im Gesamtprojekt. Dies ist kein Beleg für ein warnungsfreies Dashboard.
- Website: 145 Tests bestanden; Bereichstests zusätzlich mit der neuen Quelle im
  Speicher bestanden (45 Tests). 523 TypeScript-Dateien geprüft. Details und
  Standgrenzen im [Consumer-Bericht](reviews/2026-11-01/consumer-website.md).

## Quellenbasierte Produktabweichungen und Grenzen

Die folgenden Befunde wurden bei der Quellenprüfung sichtbar. Sie sind keine
pauschal reproduzierten Laufzeittickets. Die Texte beschreiben den belegten
Vertrag; weitergehende Softwarekorrekturen wurden nicht in eine Dokuänderung
hineingemischt. Der verlinkte Bericht enthält die konkreten Quellstellen.

| Thema                      | Befund und Umgang in der Dokumentation                                                                                                                                                                                                                            | Beleg                                                                    |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Buchungen                  | Wiederholung wird auch für mehrere Ressourcen angeboten; der kombinierte Submitpfad übernimmt sie nicht. Serien sind in der Anleitung auf eine Ressource begrenzt.                                                                                                | [P04](reviews/2026-11-01/benutzer--buchungen.md)                         |
| Profil                     | Optionale Felder werden mit null gesendet; das Backend behandelt null als Beibehalten und erst Leertext als Löschen. Eine allgemeine Löschzusage wurde entfernt.                                                                                                  | [P10](reviews/2026-11-01/ueberblick--profil.md)                          |
| Kontoschutz                | MFA-Aktivierung entfernt Passkeys. Die Letzter-Admin-Passkey-Regel kann dabei nach bereits gesetzter Zwei-Faktor-Aktivierung eingreifen. Wiederherstellungscode-Dialog und Richtlinien passen nicht durchgehend zusammen; die Implementierung erzeugt zehn Codes. | [P11](reviews/2026-11-01/ueberblick--profil-sicherheit.md)               |
| MCP-Verbindungen           | Der Erstellungsdialog erhält den vorhandenen Fehlerzustand nicht; ein Verbindungs-Limitkonflikt wird teilweise als globale Deaktivierung behandelt.                                                                                                               | [P17](reviews/2026-11-01/ueberblick--profil-mcp.md)                      |
| Geräte                     | Die aktuelle Oberfläche verwendet Aufnahme, Endpunktdiagnose und Firmwareverlauf. Alte OTA-/Provisioning-Notizen wurden als historisch markiert bzw. korrigiert; Artefakt-Upload ist kein Update-Start.                                                           | [P20](reviews/2026-11-01/administration--geraete-verwalten.md)           |
| Badges                     | Ein Importfeld bezeichnet noch ein CASE-Paket. Eine lokale Vergabe prüft Fähigkeitskriterien nicht automatisch; die Anleitung verlangt deren Prüfung.                                                                                                             | [P21](reviews/2026-11-01/administration--badges-verwalten.md)            |
| MCP-Werkzeuge              | Der UI-Hinweis zu destruktiven Aktionen nennt nur Geräte, obwohl auch Zugriffsaktionen betroffen sind. Das Werkzeug zum Löschen eines Ressourcenentwurfs und der delegierbare Berechtigungskatalog passen nicht vollständig zusammen.                             | [P23](reviews/2026-11-01/administration--mcp-verwalten.md)               |
| Einstellungen              | LDAP-/OIDC-API verlangt Settings-Rechte; Navigation und Oberfläche zusätzlich Integrations-Rechte. Die Anleitungen nennen beide Ebenen.                                                                                                                           | [P26](reviews/2026-11-01/administration--integrationen.md)               |
| Servereinstellungen        | Leere Tag-Serveradresse wird im UI abgelehnt, obwohl das Backend sie zulässt. Aussagen zu Neustart und verschlüsseltem PEM bleiben auf die belegte Schicht begrenzt.                                                                                              | [P27](reviews/2026-11-01/administration--server-einstellungen.md)        |
| Anmelderichtlinien         | Die Passkey-Regel für Administratoren schützt verbleibende Zugangsmittel; sie erzwingt keine ausschließliche Passkey-Anmeldung.                                                                                                                                   | [P28](reviews/2026-11-01/administration--sicherheit-betrieb.md)          |
| Audit                      | Datumsfilter verwenden lokale Tagesgrenzen trotz UTC-Hilfetext. Eine ältere technische Notiz behauptet einen nicht belegten Benutzeraktivitäts-Tab.                                                                                                               | [P29](reviews/2026-11-01/administration--nachweise-datenschutz.md)       |
| Zutrittsmetriken           | Vorhandene Metrikkomponenten belegen keinen aktuellen UI-Einstieg. Die Anleitung verspricht keine alten Sieben-Tage-Diagramme in der heutigen Gerätediagnose.                                                                                                     | [P30](reviews/2026-11-01/administration--zutritt-verwalten.md)           |
| Monitoring                 | Der Anmelde-Widgetpfad kann ohne Messwert null anzeigen. Einzelne Schreibaktionen der Toolbar sind nicht nach allen API-Rechten ausgeblendet; die API-Prüfung bleibt maßgeblich.                                                                                  | [P33](reviews/2026-11-01/benutzer--uebersicht-monitoring.md)             |
| Produktions-Setup          | Statischer Befund: Produktions-Compose konfiguriert HTTP-Port 8080, der Setup-Wizard fordert 5001 an; der Environment-Lock lehnt den Konflikt ab. Das ist keine praktische Abnahme aller Raspberry-Pi-Pakete.                                                     | [P34](reviews/2026-11-01/installieren--raspberry-pi.md)                  |
| Buchungsentscheidung       | Die Ablehnungsbegründung heißt im Dialog optional, wird serverseitig beim Ablehnen aber verlangt.                                                                                                                                                                 | [P42](reviews/2026-11-01/koordination--buchungen-verwalten.md)           |
| Externe Kompetenznachweise | Kein belegter produktiver Schreibpfad für SourceCredentialId: ein externer Nachweis wird nicht als automatisch anerkannter Kompetenznachweis beschrieben.                                                                                                         | [P43](reviews/2026-11-01/koordination--bewertungen.md)                   |
| Lernwegteilnahmen          | Fortschritt zählt derzeit wirksame lokale Vergaben; historische Abschlüsse bleiben erhalten. Eine Abbruchnotiz wird nicht gespeichert, und der Benutzerbogen zeigt keine Teilnahme trotz entsprechendem Hinweis.                                                  | [N03](reviews/2026-11-01/koordination--vergaben-lernwegteilnahmen.md)    |
| Rollen und Gruppen         | Neue Rolle wird sofort gespeichert. Rollenname erlaubt im UI mehr Zeichen als im Backend; einzelne Berechtigungsprüfungen und Fehlerbehandlung beim Löschen weichen ab. Gruppenbearbeitung benötigt die dokumentierten Create-/Update-Rechte.                     | [N04](reviews/2026-11-01/administration--rollen-gruppen.md)              |
| Verwaltungszuständigkeiten | Diagnose zeigt aktive Zuweisungen, keinen vollständigen effektiven Zugriff. Zuständigkeiten werden nicht automatisch auf untergeordnete Ressourcen übertragen.                                                                                                    | [N05](reviews/2026-11-01/administration--verwaltungszustaendigkeiten.md) |
| Nachweisanbieter           | Aktivierung kann sich blockieren: Test der deaktiviert gespeicherten Verbindung schlägt fehl, Aktivierung verlangt gültigen Test. OAuth-Feldlöschung und DTO-Validierung sowie Synchronisationsintervall und Scheduler sind gesondert zu prüfen.                  | [N07](reviews/2026-11-01/administration--nachweissysteme-anbinden.md)    |
| LDAP                       | TestCurrent prüft Aktualität des Fingerprints, keinen erfolgreichen Test. Die Deprovisioning-Ausnahme schützt nur direkt zugewiesene Admin-Rolle, keine Gruppen-Admins; in der Anleitung korrigiert.                                                              | [N08](reviews/2026-11-01/administration--ldap-verzeichnis.md)            |
| OIDC                       | Isolierter Test berücksichtigt Basic/Post/None, die Laufzeitkonfiguration übernimmt die Wahl der Client-Authentifizierung nicht entsprechend. Vorschau ist keine Abnahme von Registrierung, MFA oder Sperrung.                                                    | [N09](reviews/2026-11-01/administration--oidc-anmeldung.md)              |
| MQTT                       | Einzelne UI-Varianten werden vom Backend abgelehnt. ReaderAll-/Admin-Konten haben nicht dieselben ACL-Grenzen wie normale Konten; Kontoänderungen trennen Clients. Externe Veröffentlichung ist nicht freigegeben.                                                | [N10](reviews/2026-11-01/administration--mqtt-broker.md)                 |
| IP500                      | Die periodische Subscription-Erneuerung wird im aktuellen Dienst übersprungen; Wiederverbindung stellt Abonnements her. Cron-Einstellungen werden beim Start gelesen; Gateway-Aktionen sind teilweise nur API-seitig verfügbar.                                   | [N11](reviews/2026-11-01/administration--ip500-netzwerk.md)              |
| Node-RED                   | Ältere Hilfe und README weichen bei Entfernung und Deployment-Zulassung ab. Die neue Anleitung folgt dem aktuellen Deployment-Vertrag.                                                                                                                            | [N14](reviews/2026-11-01/entwickeln--automationsfluesse.md)              |

## Noch nicht praktisch abgenommen

Die alten gespeicherten E2E-Sitzungen gehören zu einer anderen lokalen Instanz;
aktuelle geeignete Testkonten waren nicht verfügbar. Deshalb wurden keine realen
Konten, Freigaben, Geräte, Anbieter oder Nachrichtenempfänger verändert. Eine
Browserprüfung der Dokumentationsdarstellung ist keine Funktionsabnahme der
beschriebenen Software.

Hardwareabläufe, Mardu Connect und Leser, Zustellung bis zu E-Mail-/Push-Empfang,
LDAP/OIDC/Nachweisanbieter, Node-RED-Deployment sowie eine leere
Produktionsinstallation und Wiederherstellung bleiben praktisch zu prüfen. Der
[abgeglichene Backlog](offene-dokumentationsaufgaben.md) enthält diese Aufgaben.

Die Agentenberichte sind zeitpunktbezogene Prüfprotokolle. Spätere Korrekturen
stehen in der Koordination und diesem Bericht; frühere Hinweise wie „Gesamtprüfung
ausstehend“ in Einzelprotokollen beschreiben deren damaligen Abschluss.
