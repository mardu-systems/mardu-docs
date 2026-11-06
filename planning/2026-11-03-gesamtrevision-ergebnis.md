# Gesamtrevision der Dokumentation: Ergebnis

Stand: 3. November 2026. Lokal umgesetzt, nicht committet oder veröffentlicht.

## Ergebnis und Umfang

Alle **74 vorhandenen handgeschriebenen Seiten** wurden einzeln gegen aktuelle
Implementierung und Leseraufgabe geprüft. **51** erhielten gezielte Inhalts-,
Darstellungs- oder Verweiskorrekturen; **23** passende Seiten blieben unverändert.
**Fünf** ausgearbeitete Anleitungen trennen bisher vermischte Aufgaben. Der Bestand
umfasst jetzt **79 Seiten**, einschließlich zweier weiterhin erreichbarer
historischer Einstiege. Die generierte HTTP-Referenz bleibt generiert.

**28 aktuelle Screenshots** ergänzen oder ersetzen belegbar veraltete Aufnahmen.
Sie stammen aus einer isolierten Testinstanz mit fiktiven Werkstattdaten.
Vorhandene passende Bilder und Systemdiagramme bleiben erhalten. Verwendet werden
native Fumadocs-Komponenten: Steps, Callout, ImageZoom und bei passenden
Alternativen Tabs. Es gibt keine neue Dependency, eigene UI-Komponente oder
allgemeine CSS-Änderung.

## Klare Aufgaben und Navigation

- Badge-Definitionen werden in der Administration gepflegt; persönliche
  [Badge-Vergaben](../docs/koordination/badge-vergaben.mdx) haben eine eigene
  Koordinationsanleitung mit ihren Rechten, Gültigkeiten und Widerrufsfolgen.
- [Automationen](../docs/administration/automationen.mdx) erklärt Runtime und
  Flow-Zugang; [Automationsanschlüsse](../docs/administration/automationen-anschluesse.mdx)
  führen durch Veröffentlichung und bestätigtes Entfernen. Die allgemeine
  Schalterbedienung bleibt an der kanonischen Ressourcenanleitung.
- Gruppen werden vollständig unter Rollen und Gruppen gepflegt. Die Benutzerseite
  erklärt die Zuordnung zu einer Person und verweist für Gruppenpflege dorthin.
- [Servereinstellungen](../docs/administration/server-einstellungen.mdx) bleibt
  Einstieg mit Suche und Speichermodell. Eigene Aufgaben erklären
  [Anmeldevorgaben](../docs/administration/anmeldevorgaben.mdx),
  [Integrationszertifikate](../docs/administration/integrationszertifikate.mdx) und
  [Monitoring/Fehlerberichte](../docs/administration/monitoring-einrichten.mdx).
- Native Fumadocs-Unterordner halten die beiden neuen Administrationsgruppen
  zusammen. Bestehende URLs und sämtliche bisherigen Artikel-IDs bleiben erhalten.
  Verweise führen direkt zur richtigen Aufgabe statt über alte Sammelseitenanker.
  Die historische Ressourcen-URL unter Koordination bleibt der Administration zugeordnet.
- Beide bestehenden Consumer-Bereichsfilter kennen die neuen Seiten; ihre
  Submodule-Verweise wurden nicht verändert. Keine leere Seite aufgenommen.

## Praktische Belege

Die Paketberichte nennen pro Seite Quellen, Änderungen, tatsächliche Prüfungen und
Grenzen. Die folgenden Abläufe liefen im isolierten Dashboard und gegen dessen
API; ein Erfolg dort ist keine Hardware- oder Anbieterabnahme:

| Bereich              | Tatsächlich geprüft                                                                                                                                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Persönliche Nutzung  | Ressourcenanfrage stellen/zurückziehen; Buchung erstellen, Beschreibung ändern und stornieren; ICS-Download; Kalenderabo abrufen, rotieren und widerrufen; Dashboard-Widget speichern und nachladen.                                               |
| Profil               | Suchdialog und Abschnittssprung; Mobilnavigation, Sitzungsfilter, Benachrichtigungsentwurf samt Verwerfen-Dialog, MCP-Dialog und Medien-Leerzustand.                                                                                               |
| Kompetenzen          | Badge erstellen und vergeben, Gültigkeitsversion ändern, bestehende Vergabe erhalten und erneuern; Lernweg anlegen, zuordnen und abschließen; Kompetenzvorschlag genehmigen und widerrufen.                                                        |
| Personen und Technik | Benutzermetriken, Zuständigkeitsvorschau und Geräteanschlüsse gelesen; keine gemeinsamen Rollen oder Hardware geändert.                                                                                                                            |
| Anbindungen          | LDAP/OIDC-Editorentwürfe ohne externe Verbindung; eigenes MQTT-Lesekonto mit gespeicherter exakter ACL; IP500-/SMTP-Formulare gelesen.                                                                                                             |
| MCP                  | Isolierte Nur-Lesen-Freigabe; eigene Verbindung mit Profile.View; initialize, tools/list und notifications_list erfolgreich; Widerruf HTTP204, alter Agent-Token anschließend HTTP401.                                                             |
| Betrieb              | Einstellungssuche, Global App mit gesperrtem Installationsschlüssel und Hot-Reload-Anzeige, Auditfilter und CSV-Download. Keine Settings-/Zertifikats-/Recovery-Änderung.                                                                          |
| Ressourcen           | Neuen Prüfraum über UI anlegen HTTP201, aktivieren HTTP200, alle sechs Detailreiter ohne API-Fehler lesen. Die am selben Tag überarbeiteten Ressourcen-, Buchungs- und Freigabenanleitungen behalten zusätzlich ihre zuvor protokollierten Belege. |

## Gemeinsame Prüfungen

| Prüfung                | Ergebnis                                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Quellen                | Alle 79 MDX-Dateien mit installiertem MDX-Compiler erfolgreich kompiliert. Scoped Formatcheck und Diff-Whitespace-Prüfung bestanden.                                                                                                                                                                                                                                                                                    |
| Build                  | Dashboard-Produktionsbuild einschließlich TypeScript erfolgreich.                                                                                                                                                                                                                                                                                                                                                       |
| Tests                  | 79 Doku-Tests in sieben Dateien erfolgreich. Sieben neue Navigationsfälle scheiterten vor der Zuordnung und bestehen danach; sie prüfen neue Seitenbesitzer und native Untergruppen.                                                                                                                                                                                                                                    |
| Links und Anker        | Alle 79 Seiten HTTP200; 1.201 interne Artikelverweise und 617 bisherige Artikel-IDs erhalten/geprüft; keine fehlenden Ziele, Abschnitte oder doppelte Artikel-IDs.                                                                                                                                                                                                                                                      |
| Bilder und Markdown    | 61 eindeutige HTML-Bildquellen und 63 Bildquellen im Markdown erreichbar, mit Alttexten. Keine rohen Steps-/ImageZoom-/Callout-/Tab-Ausdrücke oder MDX-Imports im Export.                                                                                                                                                                                                                                               |
| Browser                | 158 Ansichten: jede Seite bei 1440 und 390px ohne Seitenfehler, kaputte Bilder oder horizontalen Dokumentüberlauf. Zusätzlich fünf neue Navigationsziele in nativen Gruppen sichtbar, mobile Tastaturnavigation zur Badge-Anleitung, ImageZoom per Enter/Escape und fünf verschobene alte Anker sichtbar geprüft. Acht anspruchsvolle Seiten auch bei 320px ohne Dokumentüberlauf; dunkle Mobilansicht visuell geprüft. |
| Suche und Index        | Alle sechs Bereichsfilter liefern passende Suchtreffer; veröffentlichte Seiten im LLM-Index auffindbar. Generierte Referenz mit 559 Einträgen und einer erfolgreichen Operations-/Schema-Markdown-Stichprobe.                                                                                                                                                                                                           |
| React Doctor           | 1.213 Dateien geprüft, keine blockierenden Fehler; 484 projektweite Warnungen. Keine sachfremde Bereinigung oder Unterdrückung.                                                                                                                                                                                                                                                                                         |
| Website-Kompatibilität | 49 vorhandene Navigation-/Strukturtests mit ihrer bisherigen Quelle sowie 49 mit den neuen 79 Seiten im Speicher erfolgreich. Typprüfung: 523 Dateien ohne Fehler. Scoped ESLint beider Consumer ohne Fehler; Dashboard-Linter meldet eine bestehende Konfigurationswarnung zu animate-fade-in.                                                                                                                         |

Die öffentliche Website wurde weder auf die neue Content-Quelle umgestellt noch
neu gebaut oder im Browser abgenommen. Ihr Filter ist kompatibel geprüft; der
getestete neue Seitenstand ist in der Dashboard-Vorschau auf Port 3400 verfügbar.

## Getrennte Produktbefunde und Prüfgrenzen

Diese Revision hat keine Business-APIs, DTOs oder Produktfunktionen geändert.
Bekannte oder neu belegte Abweichungen stehen in den jeweiligen Paketberichten:

- Leere optionale Profilfelder werden als null gesendet und daher serverseitig
  beibehalten. Die Anleitung verspricht keine allgemeine Löschwirkung.
- UI-Hilfetexte zur ersten Badge-Version und Speicherung einer Metrikansicht
  stimmen nicht vollständig mit dem beobachteten Verhalten überein. Die Doku
  nennt das geprüfte Ergebnis. Ein Lernweg-Status zeigt einen fehlenden Übersetzungsschlüssel;
  der Katalog-Anfragedialog enthält einen überzähligen Trenner.
- Der bestehende Setup-Konflikt zwischen gesperrtem Produktionsport 8080 und
  Wizardwert 5001 bleibt offen. Der Installationshinweis bleibt sichtbar.
- Der Audit-CSV-Download lieferte eine Datei, aber die UI meldete fehlende gültige
  Vollständigkeitsmetadaten. Das ist keine bestätigte vollständige Exportabnahme.
- LDAP/OIDC-Anbieter, externe Nachweisquellen, SMTP-Zielpostfach, SMS/WebPush,
  externes Kalenderprogramm und MQTT-Empfang durch einen externen Client sind
  nicht als erfolgreich abgenommen markiert. Ein OIDC-Entwurf blieb im isolierten
  Runtime mangels lesbarer Versionskennung nicht speicherbar.
- Node-RED-Flowdeploy, Mardu-Connect-/NFC-Anmeldung, physische Leser/Aktoren,
  Raspberry-Pi-Installation, TLS-Wechsel und Wiederherstellung benötigen passende
  Dienste, Hardware und eigene Belege. Vorhandene Beispiele ersetzen sie nicht.
- Während dieser Revision entstanden unabhängige Activity-Änderungen in Backend,
  Frontend und generierten Verträgen. Sie wurden nicht zurückgesetzt oder von
  dieser Dokuaufgabe verändert. Die isolierte API verwendet das zuvor gebaute
  korrigierte Image; sie ist keine Abnahme dieser parallelen Produktentwicklung.
- Der .NET-Gesamttest-Hänger des vorherigen Freigabenauftrags bleibt getrennt
  protokolliert und wird hier nicht als bestanden ausgegeben.

Die isolierte Testinstanz und ihre temporären Zugangsdaten wurden nach Abschluss
entfernt; die Doku-Vorschau bleibt erreichbar. Keine Commits, Pushes, Gitlink-Bumps,
Notion-Änderungen oder Veröffentlichung durch diesen Auftrag.

## Vollständiges Seiteninventar

Die Entscheidung bezieht sich auf den Stand beim Beginn dieses Auftrags, nicht
auf sämtliche früheren uncommitteten Änderungen. Ein angepasster Verweis zählt als
gezielte Anpassung, nicht als vollständige Neufassung.

| Seite                                                                                                      | Entscheidung      | Quellen und Prüfgrenzen                                                       |
| ---------------------------------------------------------------------------------------------------------- | ----------------- | ----------------------------------------------------------------------------- |
| [administration/anmeldevorgaben.mdx](../docs/administration/anmeldevorgaben.mdx)                           | Neu ausgearbeitet | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/automationen-anschluesse.mdx](../docs/administration/automationen-anschluesse.mdx)         | Neu ausgearbeitet | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [administration/automationen.mdx](../docs/administration/automationen.mdx)                                 | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [administration/badges-verwalten.mdx](../docs/administration/badges-verwalten.mdx)                         | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/koordination_kompetenzen.md) |
| [administration/benachrichtigungen-verwalten.mdx](../docs/administration/benachrichtigungen-verwalten.mdx) | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/anbindungen.md)              |
| [administration/benutzer-rollen.mdx](../docs/administration/benutzer-rollen.mdx)                           | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/personen_technik.md)         |
| [administration/freigaben-verwalten.mdx](../docs/administration/freigaben-verwalten.mdx)                   | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [administration/geraete-verwalten.mdx](../docs/administration/geraete-verwalten.mdx)                       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/personen_technik.md)         |
| [administration/index.mdx](../docs/administration/index.mdx)                                               | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [administration/integrationen.mdx](../docs/administration/integrationen.mdx)                               | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/anbindungen.md)              |
| [administration/integrationszertifikate.mdx](../docs/administration/integrationszertifikate.mdx)           | Neu ausgearbeitet | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/ip500-netzwerk.mdx](../docs/administration/ip500-netzwerk.mdx)                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/anbindungen.md)              |
| [administration/kompetenzen-lernwege.mdx](../docs/administration/kompetenzen-lernwege.mdx)                 | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/koordination_kompetenzen.md) |
| [administration/ldap-verzeichnis.mdx](../docs/administration/ldap-verzeichnis.mdx)                         | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/anbindungen.md)              |
| [administration/mcp-verwalten.mdx](../docs/administration/mcp-verwalten.mdx)                               | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/anbindungen.md)              |
| [administration/monitoring-einrichten.mdx](../docs/administration/monitoring-einrichten.mdx)               | Neu ausgearbeitet | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/mqtt-broker.mdx](../docs/administration/mqtt-broker.mdx)                                   | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/anbindungen.md)              |
| [administration/nachweise-datenschutz.mdx](../docs/administration/nachweise-datenschutz.mdx)               | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/nachweissysteme-anbinden.mdx](../docs/administration/nachweissysteme-anbinden.mdx)         | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/koordination_kompetenzen.md) |
| [administration/oidc-anmeldung.mdx](../docs/administration/oidc-anmeldung.mdx)                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/anbindungen.md)              |
| [administration/ressourcen-aendern-entfernen.mdx](../docs/administration/ressourcen-aendern-entfernen.mdx) | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [administration/ressourcen-buchbarkeit.mdx](../docs/administration/ressourcen-buchbarkeit.mdx)             | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [administration/ressourcen-wartung.mdx](../docs/administration/ressourcen-wartung.mdx)                     | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [administration/ressourcen-zustand.mdx](../docs/administration/ressourcen-zustand.mdx)                     | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [administration/ressourcen-zutritt.mdx](../docs/administration/ressourcen-zutritt.mdx)                     | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [administration/rollen-gruppen.mdx](../docs/administration/rollen-gruppen.mdx)                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/personen_technik.md)         |
| [administration/server-einstellungen.mdx](../docs/administration/server-einstellungen.mdx)                 | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/sicherheit-betrieb.mdx](../docs/administration/sicherheit-betrieb.mdx)                     | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/tags-verwalten.mdx](../docs/administration/tags-verwalten.mdx)                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/personen_technik.md)         |
| [administration/verwaltungszustaendigkeiten.mdx](../docs/administration/verwaltungszustaendigkeiten.mdx)   | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/personen_technik.md)         |
| [administration/wartungs-cli-referenz.mdx](../docs/administration/wartungs-cli-referenz.mdx)               | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/wartungs-cli.mdx](../docs/administration/wartungs-cli.mdx)                                 | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/zertifikate-https.mdx](../docs/administration/zertifikate-https.mdx)                       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [administration/zutritt-verwalten.mdx](../docs/administration/zutritt-verwalten.mdx)                       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/personen_technik.md)         |
| [benutzer/benachrichtigungen.mdx](../docs/benutzer/benachrichtigungen.mdx)                                 | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/berechtigungsanfragen.mdx](../docs/benutzer/berechtigungsanfragen.mdx)                           | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/buchungen.mdx](../docs/benutzer/buchungen.mdx)                                                   | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/dashboard.mdx](../docs/benutzer/dashboard.mdx)                                                   | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/erste-schritte.mdx](../docs/benutzer/erste-schritte.mdx)                                         | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/geraete-status.mdx](../docs/benutzer/geraete-status.mdx)                                         | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/index.mdx](../docs/benutzer/index.mdx)                                                           | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/kalender.mdx](../docs/benutzer/kalender.mdx)                                                     | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/kompetenzen.mdx](../docs/benutzer/kompetenzen.mdx)                                               | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/uebersicht-monitoring.mdx](../docs/benutzer/uebersicht-monitoring.mdx)                           | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [benutzer/zutritt.mdx](../docs/benutzer/zutritt.mdx)                                                       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/benutzer.md)                 |
| [entwickeln/api-integration.mdx](../docs/entwickeln/api-integration.mdx)                                   | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [entwickeln/automationsfluesse.mdx](../docs/entwickeln/automationsfluesse.mdx)                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [entwickeln/http-api.mdx](../docs/entwickeln/http-api.mdx)                                                 | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [entwickeln/index.mdx](../docs/entwickeln/index.mdx)                                                       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [entwickeln/mcp-anbindung.mdx](../docs/entwickeln/mcp-anbindung.mdx)                                       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [entwickeln/mqtt-events.mdx](../docs/entwickeln/mqtt-events.mdx)                                           | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/entwickeln_automationen.md)  |
| [index.mdx](../docs/index.mdx)                                                                             | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [installieren/abnahme-uebergabe.mdx](../docs/installieren/abnahme-uebergabe.mdx)                           | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [installieren/inbetriebnahme.mdx](../docs/installieren/inbetriebnahme.mdx)                                 | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [installieren/index.mdx](../docs/installieren/index.mdx)                                                   | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [installieren/raspberry-pi.mdx](../docs/installieren/raspberry-pi.mdx)                                     | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [installieren/stoerung-vor-ort.mdx](../docs/installieren/stoerung-vor-ort.mdx)                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/betrieb_installieren.md)     |
| [koordination/badge-vergaben.mdx](../docs/koordination/badge-vergaben.mdx)                                 | Neu ausgearbeitet | [Paketbericht](reviews/2026-11-03-gesamtrevision/koordination_kompetenzen.md) |
| [koordination/bewertungen.mdx](../docs/koordination/bewertungen.mdx)                                       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/koordination_kompetenzen.md) |
| [koordination/buchungen-verwalten.mdx](../docs/koordination/buchungen-verwalten.mdx)                       | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [koordination/index.mdx](../docs/koordination/index.mdx)                                                   | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [koordination/ressourcen.mdx](../docs/koordination/ressourcen.mdx)                                         | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [koordination/vergaben-lernwegteilnahmen.mdx](../docs/koordination/vergaben-lernwegteilnahmen.mdx)         | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/koordination_kompetenzen.md) |
| [koordination/zugangsantraege-entscheiden.mdx](../docs/koordination/zugangsantraege-entscheiden.mdx)       | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/koordination_kompetenzen.md) |
| [ueberblick/benutzerkonten.mdx](../docs/ueberblick/benutzerkonten.mdx)                                     | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/fehlersuche.mdx](../docs/ueberblick/fehlersuche.mdx)                                           | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/grundlagen-begriffe.mdx](../docs/ueberblick/grundlagen-begriffe.mdx)                           | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [ueberblick/index.mdx](../docs/ueberblick/index.mdx)                                                       | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [ueberblick/neuerungen.mdx](../docs/ueberblick/neuerungen.mdx)                                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [ueberblick/profil-benachrichtigungen.mdx](../docs/ueberblick/profil-benachrichtigungen.mdx)               | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/profil-erscheinungsbild.mdx](../docs/ueberblick/profil-erscheinungsbild.mdx)                   | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/profil-mcp.mdx](../docs/ueberblick/profil-mcp.mdx)                                             | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/profil-nachweisquellen.mdx](../docs/ueberblick/profil-nachweisquellen.mdx)                     | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/profil-sicherheit.mdx](../docs/ueberblick/profil-sicherheit.mdx)                               | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/profil-sitzungen.mdx](../docs/ueberblick/profil-sitzungen.mdx)                                 | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/profil-zutrittsmedien.mdx](../docs/ueberblick/profil-zutrittsmedien.mdx)                       | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [ueberblick/profil.mdx](../docs/ueberblick/profil.mdx)                                                     | Gezielt angepasst | [Paketbericht](reviews/2026-11-03-gesamtrevision/profil.md)                   |
| [v1/index.mdx](../docs/v1/index.mdx)                                                                       | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
| [v2/index.mdx](../docs/v2/index.mdx)                                                                       | Bewusst erhalten  | [Paketbericht](reviews/2026-11-03-gesamtrevision/root.md)                     |
