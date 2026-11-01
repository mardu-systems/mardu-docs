# P54 – Administration

## Änderungsbrief

Leserfrage: Wo beginne ich mit der Verwaltung einer vorhandenen Mardu-Installation,
und welche Anleitung brauche ich für meine Aufgabe? Vorausgesetzt sind die
Dashboard-Adresse und ein eigenes Konto, aber keine Kenntnis der internen Module.
Das Ergebnis ist eine verständliche Startfolge mit einem Aufgabenwegweiser.
Heimatbereich: Administration; der Bereich ist keine Systemrolle.

Plan: Die sechs vorhandenen Aufgabengruppen erhalten, alle geprüften
Administrationsseiten und den Zusatzseitenplan abgleichen, nutzbare neue
Anleitungen zuordnen und den veralteten Schreibauftrag aus dem Produkttext
entfernen. Die historischen URLs für Ressourcen und Monitoring sowie vorhandene
Anker bleiben erhalten. N01, N12 und N15 erhalten gemäß Koordinationsentscheidung
keine neue Seite; ihre vorhandenen kanonischen Abschnitte werden verwendet.

Quellen sind die geprüften Produktseiten, ihre Einzelberichte, der Zusatzseitenplan
und die vorhandene Dashboard-/Doku-Navigation. Keine neuen Softwareabläufe,
API-Verträge oder Anmeldeversprechen werden eingeführt. Lokale Format-, Link-,
Anker- und Diffprüfungen gehören zu diesem Auftrag; gemeinsame Consumer-,
Navigations- und Browserprüfungen übernimmt die Koordination.

## Entscheidung und Änderung

**Verbessert; zur gemeinsamen Consumer-Prüfung.** Die Einstiegsseite enthält
jetzt eine kurze Startfolge: Erstsetup von vorhandener Installation unterscheiden,
Konto und Rechte prüfen, Systemstatus und gegebenenfalls E-Mail testen,
Kontowiederherstellung vorbereiten und anschließend die benötigten Funktionen
einrichten. Sie verspricht weder einen erfolgreichen Erstsetup-Lauf noch eine
physische Wirkung gespeicherter Einstellungen.

Die sechs guten Aufgabengruppen bleiben erhalten. Jede verlinkte Anleitung wird
nach ihrem Ergebnis beschrieben; bei Anbindungen steht der Verwendungszweck vor
dem Link. Der Störungseinstieg nennt zuerst Sicherheit und Betrieb, statt eine
ungeführte Gesamtliste anzubieten. Die bisherigen Aussagen, Rollenpflege,
Zuständigkeiten und weitere Server-/Anbietereinstellungen fehlten vollständig,
sind nach den neuen Seiten veraltet und wurden entfernt. Praktische Prüfgrenzen
bleiben in den Einzelberichten, nicht als Schreibauftrag auf der Einstiegsseite.

## Abgleich aller Adminseiten und Zusatzseiten

Die Aufgabenzuordnung wurde gegen Titel, Beschreibung, Einleitung und relevante
Abschnitte aller 24 übrigen MDX-Seiten in `docs/administration/` sowie die beiden
historisch außerhalb abgelegten Adminanleitungen geprüft. Alle werden im
Aufgabenwegweiser direkt erschlossen; die CLI-Referenz bleibt der Anleitung
zugeordnet. Einzelne Abläufe werden nicht erneut ausgeschrieben.

| Gruppe                      | Vorhandene Ziele / Zusatzseitenplan                                                                                                                                                                                                                                                                                                                                                     |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Personen und Berechtigungen | `benutzer-rollen.mdx`, `rollen-gruppen.mdx` (N04), `verwaltungszustaendigkeiten.mdx` (N05). Globale Rollenrechte, objektbezogene Verwaltung und Nutzung getrennt.                                                                                                                                                                                                                       |
| Ressourcen und Zutritt      | `../koordination/ressourcen.mdx`, `freigaben-verwalten.mdx` (N16), `tags-verwalten.mdx`. N01 und N15 werden nicht neu angelegt: Wartung steht unter Ressourcen `#ausfälle-und-wartung-betrieb-unterbrechen`, Regeln unter `#nutzung-und-zugriff-nutzung-erlauben`, Zutrittspunkte unter `#technik-anschlüsse-zuordnen`.                                                                 |
| Kompetenzen und Nachweise   | `kompetenzen-lernwege.mdx` (N06), `badges-verwalten.mdx`, `nachweissysteme-anbinden.mdx` (N07). N03 ist als laufende Lernwegbegleitung im verlinkten Koordinationsstart erschlossen.                                                                                                                                                                                                    |
| Geräte und Automationen     | `geraete-verwalten.mdx`, `automationen.mdx`. N14 ist eine Entwicklungsaufgabe und bleibt über die Automationsanleitung erschlossen.                                                                                                                                                                                                                                                     |
| Anbindungen                 | `integrationen.mdx`, `ldap-verzeichnis.mdx` (N08), `oidc-anmeldung.mdx` (N09), `mqtt-broker.mdx` (N10), `ip500-netzwerk.mdx` (N11), `mcp-verwalten.mdx`. Nachweissysteme sind bei Kompetenzen zugeordnet, E-Mail unter Betrieb.                                                                                                                                                         |
| Betrieb                     | `server-einstellungen.mdx`, `sicherheit-betrieb.mdx`, `zertifikate-https.mdx` (N13), `benachrichtigungen-verwalten.mdx`, `../benutzer/uebersicht-monitoring.mdx`, `zutritt-verwalten.mdx`, `nachweise-datenschutz.mdx`, `wartungs-cli.mdx`, `wartungs-cli-referenz.mdx`. N12 wird nicht neu angelegt: Anmelderichtlinie bleibt kanonisch in Servereinstellungen und Sicherheit/Betrieb. |

N02 (Zugangsanträge) ist eine Koordinationsaufgabe und über den dortigen
Bereichsstart erschlossen. Damit sind alle N01–N16 abgeglichen, ohne eine Seite
nur aufgrund ihres Planeintrags zu verlinken. Der Zusatzseitenplan führt weiterhin
den ursprünglichen Arbeitsstatus; seine Pflege liegt außerhalb dieses Auftrags.

## Quellen und relevante Stellen

Pfade relativ zum Software-Repository; Seitenpfade in der obigen Tabelle relativ
zu `web/content/docs/docs/administration/`.

- `web/components/layout/sidebar/dashboard-navigation.ts:46–160,210–247`:
  Systemstatus, Personen, Kompetenzen, Ressourcen, Freigaben und Administration
  sind vorhandene Aufgaben mit eigenen Leserechten. Geplante Menüeinträge werden
  nicht zu dokumentierten Verwaltungsabläufen erklärt.
- `web/components/layout/settings/server-nav.config.ts:44–142`:
  vorhandene Einstiege für globale Werte, Auth Policy, IP500, Zertifikate, LDAP
  und OIDC samt getrennten Settings-/Integrationsrechten.
- `web/components/layout/settings/integrations-nav.config.ts:38–65`:
  Informationsbroker und MQTT-Konten sind ein eigener Integrationsbereich.
- `api/Service/Admin/Settings/Boundary/HttpControllers/AuthPolicySettingsController.cs:30–79`:
  Lesen und Ändern der vorhandenen Auth Policy benötigen Settings-Rechte;
  Tokenlaufzeiten sind als neustartpflichtig gekennzeichnet. Kein neuer
  Kontoschutzvertrag wird aus dem Aufgabenwegweiser abgeleitet.
- `web/lib/docs-roles.tsx:103–151` und
  `web/content/docs/docs/administration/meta.json`:
  Ressourcen und Monitoring gehören trotz alter URL zur Administration. Die
  neue Seite benennt das ausdrücklich und erhält beide Adressen.
- `web/content/docs/docs/installieren/raspberry-pi.mdx:92–137`:
  Erstsetup, initiales Konto und Anmeldung; bekannter Portkonflikt bleibt in der
  kanonischen Installationsanleitung, kein Erfolgsversprechen im Bereichsstart.
- `web/content/docs/docs/administration/benutzer-rollen.mdx:17–31,92–106,156–191,310–325`:
  Konto-/Aufgabenrechte, Kontofreigabe, Rollen und Gruppen sowie Kontostatus.
- `web/content/docs/docs/administration/verwaltungszustaendigkeiten.mdx:6–46`:
  Verwaltungszuständigkeit und Ressourcennutzung sind getrennt.
- `web/content/docs/docs/administration/sicherheit-betrieb.mdx:11–50,105–134`
  und `benachrichtigungen-verwalten.mdx:40–89`: neue Anmeldung und Wiederherstellung
  vor strengeren Vorgaben, Störungseingrenzung, Mailtest und Empfangsprüfung.
- `web/content/docs/docs/koordination/ressourcen.mdx:83–165`:
  Regeln, technische Zuordnung, Buchbarkeit und Wartung. Die obigen N01-/N15-Ziele
  bleiben kanonisch.
- `web/content/docs/planning/2026-11-01-zusatzseiten.json` und
  `planning/reviews/2026-11-01/administration--anmeldung-kontoschutz.md`:
  Planumfang N01–N16 und begründete Nichtanlage N12. Die Koordination bestätigt
  ebenfalls die Nichtanlage N01/N15.

## Verweise, Prüfungen und Grenzen

Erhalten: alle sechs Aufgabenüberschriften sowie `#empfohlene-reihenfolge`,
`#weitere-verwaltungsaufgaben`, `#offene-dokumentationsaufgaben` und der bisher
automatisch erzeugte Anker `#umfang-der-anleitungen` (nun explizit).
Keine Bilder oder neuen MDX-Komponenten nötig. Keine Software-, API-/DTO- oder
OpenAPI-Änderung.

Die Koordination muss neue nutzbare Seiten weiterhin in `meta.json` und den
Consumer-Sluglisten freischalten sowie die Bereichszuordnung beider Consumer
prüfen. Diese Dateien wurden nicht geändert. Insbesondere stehen die neuen Ziele
im gelesenen Metadatenstand noch nicht vollständig in der Sidebar; direkte
MDX-Verweise ersetzen diese gemeinsame Navigationsprüfung nicht.

Eigene Checks:

- Vorhandenes Prettier für beide eigenen Dateien ausgeführt, danach `--check`:
  erfolgreich.
- Die einzelne Einstiegsseite mit vorhandenem `@mdx-js/mdx` kompiliert:
  erfolgreich; kein globaler Build.
- 33 lokale Verweise einschließlich Zielanker mit Dateiauflösung und vorhandenem
  `github-slugger` geprüft: alle vorhanden. Alle historischen Anker erhalten.
- Vollständigkeitsabgleich: alle 24 übrigen Admin-MDX-Seiten direkt verlinkt;
  alle vorgesehenen und vorhandenen Admin-Zusatzseiten abgedeckt; keine Links
  auf die bewusst nicht angelegten N12/N15. N01 und N15 verwenden vorhandene
  Ressourceninhalte, N02/N03 den Koordinationsstart, N14 die Automationsanleitung.
- `git diff --check` für die Einstiegsseite und Diffprüfung des neuen Berichts:
  keine Whitespace-Befunde.

Keine eigene Browser-, Hardware-, Anbieter- oder Consumer-Abnahme. Die
Startfolge ist ein Wegweiser und kein praktisch durchgeführtes Ende-zu-Ende-
Tutorial. Der gewünschte Musterablauf mit Person, Ressource, Gerät und erlaubter
bzw. verweigerter Entscheidung bleibt eine gesonderte Aufgabe.

Geänderte Dateien ausschließlich:

- `web/content/docs/docs/administration/index.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--index.md`
