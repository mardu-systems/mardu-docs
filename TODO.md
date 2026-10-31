# Dokumentationsbestand und Arbeitsplan

Aktualisierung: 19. Oktober 2026. Die Benutzeransicht wurde auf gesonderten Auftrag
ausgearbeitet; ihr Prüfstand folgt unten. Die Bestandsbewertung und Prioritäten
vom 10. Oktober bleiben als damalige Planung erhalten. Dieser Arbeitsplan liegt außerhalb von `docs/` und ist keine
veröffentlichte Produktseite. Die konkreten Schreibaufträge stehen bei den
betroffenen Seiten; hier stehen Reihenfolge, Abdeckung und übergreifende Aufgaben.

Grundlage sind die [Doku-Regeln](AGENTS.md), alle 37 vorhandenen MDX-Seiten,
Navigation und ausgewählte Implementierungen, Controller, DTOs und Validatoren
im aktuellen lokalen Arbeitsstand. Dieser enthält noch nicht veröffentlichte
Änderungen. Es gab keine angemeldete Live-Abnahme und keine Hardwareprüfung.
Ein vorhandener Endpunkt belegt noch keinen vollständigen Ablauf im Dashboard.

## Bewertung des vorhandenen Bestands am 10. Oktober 2026

| Bereich        | Seiten | Stand vor dieser Überarbeitung                                                                                                 | Konsequenz                                                                                    |
| -------------- | -----: | ------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| Administration |     10 | Benutzerverwaltung und Badge-Bearbeitung sind ausgearbeitet, aber nicht vollständig; acht Seiten enthalten TODOs.              | Hier mit den fehlenden Verwaltungsabläufen beginnen.                                          |
| Überblick      |      6 | Die Konto-Erklärung ist ausgearbeitet; Profil enthält eine Anleitung zum Postfach. Die übrigen Inhalte sind überwiegend TODOs. | Nur die für Administratoren benötigten Grundlagen vorziehen.                                  |
| Benutzer       |      7 | Übersicht und Systemstatus sind beschrieben; sechs Seiten enthalten TODOs.                                                     | Nach der Administration schreiben; vorhandene Metriktexte prüfen.                             |
| Koordination   |      4 | Themenlisten statt durchführbarer Anleitungen.                                                                                 | Ressourcen und Buchungsregeln bereits im ersten Arbeitspaket berücksichtigen.                 |
| Installieren   |      4 | Themenlisten ohne gerätespezifische Belege.                                                                                    | Serverbetrieb für Administratoren vorziehen; Montage erst mit Hardwareunterlagen ausarbeiten. |
| Entwickeln     |      5 | Themenlisten neben der automatisch erzeugten API-Referenz.                                                                     | Technische Referenz weiterverwenden; Integrationsanleitungen später ergänzen.                 |
| Einstieg       |      1 | Wegweiser vorhanden.                                                                                                           | Bearbeitungsstand und sinnvolle Einstiege ergänzen.                                           |

32 von 37 Seiten enthielten TODOs. Die fünf Seiten ohne TODOs waren deshalb
nicht automatisch vollständig: Dazu gehören auch der allgemeine Wegweiser und
die beiden noch unvollständigen Administrator-Anleitungen.

## Was an der bisherigen Planung unbrauchbar oder irreführend ist

| Befund                                                                                                              | Beleg                                                                                                                                                                                                                                                                                                                 | Korrektur                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Themen wie „LDAP anbinden“ nennen weder Ergebnis noch Voraussetzungen oder Fehlerfälle.                             | Bisherige Integrations- und Einstellungsseiten.                                                                                                                                                                                                                                                                       | Pro Aufgabe Rechte, Voraussetzungen, Schritte, Ergebnis und Fehler dokumentieren.                                                    |
| Backup wird wie eine nutzbare Dashboard-Funktion eingeplant.                                                        | [Backup-Seite](../../app/[project]/dashboard/admin/server/database-backup/page.tsx) zeigt „aktuell nicht freigegeben“; der Navigationseintrag ist auskommentiert.                                                                                                                                                     | Verfügbarkeit ausdrücklich nennen; externen Sicherungs- und Wiederherstellungsablauf prüfen.                                         |
| „Zwei-Faktor-Pflicht je Rolle“ ist zu weit gefasst.                                                                 | [AuthPolicySettings](../../../api/Framework/Core/Auth/AuthPolicySettings.cs) enthält Administratorpflichten; Benutzer haben eigene Sicherheitsaktionen.                                                                                                                                                               | Administratorpflichten und kontobezogene Vorgaben beschreiben; keine beliebigen Rollenregeln versprechen.                            |
| „Wiederherstellungscodes überwachen“ und „fremde Sitzungen beenden“ setzen eine passende Verwaltungsansicht voraus. | [Benutzercontroller](../../../api/Framework/Infrastructure/Identity/Users/Boundary/UserController.cs) hat Code-Neuerzeugung, Anmeldehistorie und Passkeys; [Profilsitzungen](../../../api/Framework/Infrastructure/Identity/Users/Boundary/ProfileSessionsController.cs) beziehen sich auf den angemeldeten Benutzer. | API-Verfügbarkeit, UI-Verfügbarkeit und Selbstbedienung getrennt prüfen. Keine Übersicht über fremde Codes oder Sitzungen behaupten. |
| MCP vermischt Serverrichtlinie und persönliche Agentenzugänge.                                                      | [MCP-Verbindungen](../../../api/Service/Mcp/Boundary/HttpControllers/McpAgentConnectionsController.cs) sind Profil-Selbstbedienung.                                                                                                                                                                                   | Serverrichtlinie in Integrationen, eigene Tokens im Profil und Client-Anbindung unter Entwickeln erklären.                           |
| Ressourcenmodell und objektbezogene Zutrittsverwaltung fehlen weitgehend.                                           | [Ressourcenarchitektur](../../../docs/managed-resource-architecture.md) und [Ressourcen-API](../../../docs/managed-resource-api.md).                                                                                                                                                                                  | Ressource, Zugangsbereich, Zutrittspunkt, Geräte-Endpunkt, Zuordnung und delegierte Verwaltungsrechte erklären.                      |
| „Badges verwalten“ erklärt Vergaben nur in wenigen Sätzen.                                                          | [Vorhandene Anleitung](docs/administration/badges-verwalten.mdx).                                                                                                                                                                                                                                                     | Vergabe, Erneuerung, Widerruf, Veröffentlichungen und Fehler als eigene Aufgaben ausarbeiten.                                        |
| Integrationen fehlen in der Themenliste.                                                                            | [Integrationsnavigation](../../components/layout/settings/integrations-nav.config.ts) enthält Ausstellung, Synchronisierung, Anbieter, Anerkennung und Vergaben für Open Badges sowie Automationen.                                                                                                                   | Alle vorhandenen Einstellungsbereiche erfassen; Zuständigkeiten für Inhalte, Anbieter und eigene Konten trennen.                     |
| Buchungsadministration wird nur als Koordinationsaufgabe betrachtet.                                                | [Buchungseinstellungen](../../components/layout/settings/booking-settings-nav.config.ts) enthalten Gruppenregeln und Schließzeiten.                                                                                                                                                                                   | Einrichtung der Buchbarkeit, Regeln und Schließzeiten gehört zur ersten Administrator-Runde.                                         |
| Die Zielgruppenbereiche wirken wie fest eingebaute Systemrollen.                                                    | [Doku-Rollen](../../lib/docs-roles.tsx) sind Navigation; die API verwendet einzelne Berechtigungen.                                                                                                                                                                                                                   | Bereiche als Lesereinstiege beschreiben; Rechte je Aktion nennen.                                                                    |
| Es gibt bereits konkrete Findbarkeitsfehler.                                                                        | `badges-verwalten` fehlt in der Administrator-Slugliste; `benutzerkonten` fehlt im Überblick-Wegweiser. Der bisherige Link von Administration zu `zutritt` zielte in den falschen Ordner.                                                                                                                             | Slugliste als Consumer-Aufgabe korrigieren; Wegweiser und fehlerhaften Zutrittslink im Docs-Bestand berichtigen.                     |
| README beschreibt `v1`/`v2`, die im vorhandenen Bestand nicht existieren.                                           | [README](README.md), [Navigation](docs/meta.json), [Doku-Quelle](../../lib/source.ts).                                                                                                                                                                                                                                | Aktuelle Zielgruppenstruktur dokumentieren; Versionierung erst bei tatsächlicher Einführung beschreiben.                             |
| Screenshots ersetzen teilweise die Erklärung von Voraussetzungen und Fehlern.                                       | Vorhandene Benutzer- und Badge-Seiten haben Bilder, aber noch offene Aufgaben.                                                                                                                                                                                                                                        | Nur unterstützende Bilder aufnehmen; Testdaten und Komponenten-Fixtures kenntlich machen; Rechte und Folgen als Text ergänzen.       |
| Standardsätze, „typische Wochenabläufe“ und pauschale Fristen helfen ohne Produktbezug wenig.                       | Bisherige Bereichs-TODOs und Datenschutzseite.                                                                                                                                                                                                                                                                        | Konkrete Aufgaben priorisieren; organisatorische Vorgaben und gesetzliche Fristen nicht als Produkteigenschaft erfinden.             |

## Reihenfolge: Administration zuerst

P0 korrigiert falsche Erwartungen und die Navigation. P1 deckt die Verwaltung
einer üblichen Installation ab. P2 ergänzt optionale Anbindungen und vertiefte
Anleitungen. Ein Thema ist erst erledigt, wenn es anhand der Abschlusskriterien
unten geprüft wurde.

| Reihenfolge | Priorität | Arbeitspaket und Ablage                                                                                                                      | Fehlender Umfang                                                                                                                                               |
| ----------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1           | P0        | Doku-Einstieg und Grundlagen                                                                                                                 | Entwurfsstatus, Glossar, Konten versus Rollen versus Zugänge, vorhandene Links und Consumer-Navigation.                                                        |
| 2           | P1        | [Benutzer und Rollen](docs/administration/benutzer-rollen.mdx)                                                                               | Rollen erstellen und bearbeiten, Berechtigungen ändern, Gruppen erstellen/löschen, Sicherheitsaktionen, Kontoquellen und Zusammenführung prüfen.               |
| 3           | P1        | [Servereinstellungen](docs/administration/server-einstellungen.mdx) und [Sicherheit und Betrieb](docs/administration/sicherheit-betrieb.mdx) | Einstellungen speichern, gesperrte Felder, Neustartbedarf, Registrierung, Admin-Anmeldepflichten, Mail, Zertifikate und Wiederherstellungsgrenzen.             |
| 4           | P1        | [Ressourcen](docs/koordination/ressourcen.mdx) und [Buchungen verwalten](docs/koordination/buchungen-verwalten.mdx)                          | Ressourcenhierarchie, Zustände, Buchbarkeit, Gruppenregeln, Schließzeiten, Ausfälle und Wartung; von der Administration direkt verlinken.                      |
| 5           | P1        | [Geräte verwalten](docs/administration/geraete-verwalten.mdx)                                                                                | Anlage, Zuordnung, Provisionierung, Endpunkte, Einstellungen, Status, Firmware-Artefakte, Updateabbruch und Löschfolgen.                                       |
| 6           | P1        | [Zutritt verwalten](docs/administration/zutritt-verwalten.mdx)                                                                               | Ressource und Zugangsbereich konfigurieren, Hardware zuordnen, Rechte delegieren, Freigaben erteilen, Anträge entscheiden, Sitzungen und Zustellstatus prüfen. |
| 7           | P1        | Tags: zunächst [Geräte verwalten](docs/administration/geraete-verwalten.mdx)                                                                 | Smartphone-App/Leser-Voraussetzungen, Anmeldung, abgelaufene Anmeldung, Zuordnung, Sperrung und Ersatz. Bei Ausarbeitung eigene Anleitung vorsehen.            |
| 8           | P1        | [Badges verwalten](docs/administration/badges-verwalten.mdx) und [Bewertungen](docs/koordination/bewertungen.mdx)                            | Fähigkeiten, Definitionen, Vergaben, Lernwege, Bewertungen, Anerkennung und veröffentlichte Definitionen; Verknüpfung mit Zutrittsbedingungen erklären.        |
| 9           | P1        | [Nachweise und Datenschutz](docs/administration/nachweise-datenschutz.mdx)                                                                   | Audit lesen/exportieren, Datenarten und belegte Aufbewahrung, Kontolöschung versus Historie, organisatorische Auskunfts- und Löschprozesse.                    |
| 10          | P1        | [Sicherheit und Betrieb](docs/administration/sicherheit-betrieb.mdx), später eigene Betriebsanleitung                                        | Externe Sicherung und Wiederherstellung, Release-Update, Wartungsfenster, Funktionsprüfung, Störungen und Übergabe.                                            |
| 11          | P2        | [Integrationen](docs/administration/integrationen.mdx)                                                                                       | MQTT, LDAP, OIDC, IP500/Gateways, Open-Badges-Ausstellung und Anbieter; fehlende Betriebsvarianten pro Anbindung.                                              |
| 12          | P2        | [Automationen](docs/administration/automationen.mdx)                                                                                         | Adapter einrichten, Ressourcenrechte, Editor, Deploy, Flow-Freigabepflicht, Verbindung reparieren und Fehler.                                                  |
| 13          | P2        | MCP und Benachrichtigungen                                                                                                                   | Serverrichtlinie und persönliche Agententokens; Zustellkanäle, Pflichtkanäle, Ruhezeiten und fehlgeschlagene Zustellung.                                       |
| 14          | P1/P2     | Lernweg und Nachschlageinhalte für Administratoren                                                                                           | Ein durchgängiges Beispiel von Benutzer über Ressource und Gerät bis zum erlaubten/verweigerten Zugang; danach Feld-/Statusreferenzen und Fehlerhilfe.         |

Die Einstellungsbereiche E-Mail, LDAP, OIDC und Tags liegen teilweise unter
Servereinstellungen, obwohl sie thematisch Anbindungen betreffen. Anleitungen
müssen den tatsächlichen Menüpfad nennen; die Doku-Zuordnung ersetzt ihn nicht.

## Übergreifende TODOs für die Administrator-Runde

- [ ] P0: `badges-verwalten` in der vorhandenen Consumer-Rollennavigation berücksichtigen und mit den bestehenden Doku-Navigationstests prüfen.
- [ ] P0: Alle noch offenen Seiten als Entwurf erkennbar halten; eine reine TODO-Seite nicht als fertige Hilfe oder Release-Dokumentation darstellen.
- [ ] P1: Den tatsächlichen Admin-Einstieg ergänzen: erste Anmeldung, Setup versus bereits eingerichtete Installation, Rechte, Mailtest und nächster Arbeitsablauf. In `administration/index.mdx` beginnen.
- [x] P1: Administrator-Aufgaben zu Ressourcen, Buchungen und Bewertungen direkt aus der Administration verlinkt; die vorhandenen Seiten bleiben ihre gemeinsame Ablage.
- [ ] P1: Beim Ausarbeiten lange Sammelseiten nach Hauptzweck teilen, zum Beispiel `rollen-verwalten.mdx`, `tags-verwalten.mdx`, `betrieb-wiederherstellung.mdx`, Feld- und Statusreferenzen. Bestehende URLs erhalten und ergänzende Seiten in `meta.json` und der Consumer-Slugliste aufnehmen. Diese Dateien sind noch nicht angelegt.
- [ ] P1: Ein überprüfbares Tutorial mit fiktiver Person, Ressource und Gerät durchführen: Rollen zuweisen, Zugang konfigurieren, erlaubte und abgelehnte Entscheidung erklären. Hardwareprüfung gesondert kennzeichnen.
- [ ] P1: Für jede Anbindung Voraussetzungen, Rechte, minimale Einrichtung, Verbindungstest, laufenden Betrieb, Abschalten und typische Fehler dokumentieren.
- [ ] P1: Für jedes veränderbare Einstellungsfeld Format, Einheit, erlaubte Werte, Pflicht/optional, Leeren, Default-Quelle, Änderungsauswirkung und Neustartbedarf belegen. UI-Startwerte sind keine verlässlichen Serverdefaults.
- [ ] P1: Anmelde-, Zutritts- und Editor-Sitzungen durchgehend unterscheiden; erlaubte Entscheidung, gespeicherter Befehl und bestätigte Hardwareaktion getrennt benennen.
- [ ] P1: Destruktive und sofort ausgeführte Aktionen vor dem Schritt erklären; Teilfehler beim Speichern und veraltete Änderungsstände behandeln.
- [ ] P1: Screenshots mit vorhandener UI und fiktiven Daten prüfen; Sprache, Theme und Ausschnitt je Ablauf gleich halten, Fixture-Darstellungen nennen und unbenutzte Bilder erst nach Referenzprüfung bereinigen.
- [ ] P1: Technische Verträge aus OpenAPI/XML und bestehenden technischen Dokumenten wiederverwenden. Request/Response, Rechte, Pflichtfelder, Null/Leer, Validierung, Statuscodes und Fehlerbeispiele beim Ergänzen der Entwicklerreferenzen prüfen; generierte Dateien nicht von Hand ändern.
- [ ] P1: Produktseiten und technische Pläne unterscheiden. `docs/` und `roadmap/` im Software-Repo sind Quellen zur Prüfung, kein Beleg, dass eine geplante Funktion schon verfügbar ist. Historische Geräteprotokolle mit ihrem Versionsstand behandeln.
- [ ] P1: Doku und Consumer am selben überprüften Arbeits-/Release-Stand testen; die Website ist ein weiterer Consumer und wurde hier nicht ausgeführt. Commit, Push und Veröffentlichung benötigen einen entsprechenden Auftrag.
- [ ] P2: Den Doku-Feedbackweg und einen Standort-Ansprechpartner beschreiben, ohne eine eingebaute Support- oder Ticketfunktion vorauszusetzen.

## Geplante Folgearbeiten aus der Bestandsaufnahme vom 10. Oktober

| Bereich      | Nach der Administrator-Runde zu schreiben                                                                                                                                 | Abhängigkeit                                                                                                     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Überblick    | Begriffe, Anmeldungshilfe, eigenes Profil, Passkeys/2FA/Codes, Sitzungen, persönliche MCP-/Badge-Konten, Benachrichtigungseinstellungen, tatsächliche Release-Neuerungen. | Sicherheitsrichtlinie und unterstützte Anmeldewege müssen feststehen.                                            |
| Benutzer     | Erstes Anmelden, Standalone/Projektwechsel, eigene Buchung, eigener Zugang und Antrag, Tags, Kompetenznachweise/Lernwege, verfügbare Geräteanzeigen.                      | Die verwalteten Abläufe müssen belegt und ihre Selbstbedienungsgrenzen klar sein.                                |
| Koordination | Buchungsentscheidungen, Ressourcenzustände und Wartung, Kompetenzbewertung und Anerkennung externer Nachweise.                                                            | Ressourcen- und Bewertungsthemen sind wegen Administratorbedarf teilweise vorgezogen.                            |
| Installieren | Montage/Verkabelung pro Gerät und Firmware, Netzwerkeinbindung, Inbetriebnahme, Abnahmekriterien, dokumentierter Neustart und Störung vor Ort.                            | Hersteller-/Firmwareunterlagen, geeignete Hardware und Testzugang; LED-Codes nicht aus Backendannahmen ableiten. |
| Entwickeln   | Authentifizierung und Fehlervertrag, gültige HTTP-Beispiele, MQTT-Topics/Payloads/ACLs, SignalR-Ereignisse, MCP-Client, Automation-Nodes und Protokollkompatibilität.     | Vorhandene technische Referenzen und generierte API verwenden; fiktive Beispiele ausführen.                      |
| Betrieb      | Produktionsbereitstellung, TLS/Ingress, Persistenz, Update/Migration, Sicherung/Wiederherstellung, Ausfall von DB/MQTT/Node-RED, Log-/Metrikdiagnose.                     | Eine konkrete unterstützte Betriebsform testen; vorhandene Produktionsdokumente abgleichen.                      |

Die überarbeiteten TODOs aller Zielgruppen sind Schreibaufträge. Bei noch nicht
abgeglichenem Verhalten verlangen sie ausdrücklich eine Verfügbarkeitsprüfung,
statt Funktionen, Statuswerte, Fristen oder Rückfragen zu versprechen.

Die Zeilen **Überblick** und **Benutzer** sind durch die Benutzerrunde vom 19. Oktober für die vorhandene Web-Selbstbedienung ausgearbeitet. Release-Neuerungen,
administrative Lernwege und die übrigen Zielgruppen bleiben separate Aufgaben.

## Quellen für die nächste Ausarbeitung

Die Regeln gelten aus [AGENTS.md](AGENTS.md). Zusätzlich zu den vorhandenen
Produktseiten wurden unter anderem diese Implementierungen und Verträge geprüft:

- Identität: [Rollen](../../../api/Framework/Infrastructure/Identity/Roles/Boundary/RolesController.cs), [Gruppen](../../../api/Framework/Infrastructure/Identity/Groups/Boundary/UserGroupsController.cs), [Benutzer](../../../api/Framework/Infrastructure/Identity/Users/Boundary/UserController.cs), [Autorisierung](../../../docs/user-authorization.md).
- Einstellungen: [Globale Einstellungen](../../../api/Service/Admin/Settings/Application/GlobalAppSettings.cs), [Auth-Policy-Controller](../../../api/Service/Admin/Settings/Boundary/HttpControllers/AuthPolicySettingsController.cs), [Zertifikate](../../../api/Framework/Infrastructure/Certificates/Boundary/CertificatesController.cs), [Servernavigation](../../components/layout/settings/server-nav.config.ts).
- Ressourcen und Zugang: [Ressourcenvertrag](../../../docs/managed-resource-api.md), [Ressourcenmodell](../../../docs/managed-resource-architecture.md), [Buchungsregeln](../../../api/Service/Bookings/Boundary/Dto/BookingPolicyDtos.cs), [Zutrittscontroller](../../../api/Service/Accesses/Boundary/HttpControllers).
- Geräte und Tags: [Geräteaktionen](../../../api/Service/Devices/Boundary/HttpControllers/DeviceController.cs), [Löschvorschau](../../../api/Service/Devices/Boundary/Dto/DeviceDeletionPreviewDto.cs), [Tag-Anmeldung](../../../api/Service/Tags/Boundary/HttpControllers/TagEnrollmentController.cs), [Geräteeinbindung](../../../docs/device-onboarding-flow.md).
- Kompetenzen: [Katalogvertrag](../../../docs/competency-catalog-api.md), [Bewertungen](../../../docs/competencies-and-assessments.md), [Anbieter und Veröffentlichungen](../../../docs/standard-exchange-and-provider-connections.md).
- Betrieb und Integrationen: [Audit-Controller](../../../api/Framework/Infrastructure/Identity/Audit/Boundary/AuditTrailController.cs), [MQTT-Benutzer](../../../api/Framework/Infrastructure/Network/Broker/Boundary/MqttUsersController.cs), [Automation-Vertrag](../../docs/automation-settings-and-editor.md), [Flow-Verwaltung](../../../api/Service/Automations/NodeRed/Boundary/HttpControllers/NodeRedFlowsController.cs), [MCP](../../../docs/mcp.md).

## Wann ein Arbeitspaket fertig ist

- [ ] Zielgruppe und ein Hauptzweck nach Diátaxis sind erkennbar; Überschrift und Navigation führen zur gesuchten Aufgabe.
- [ ] Rechte, Voraussetzungen, UI-Bezeichnungen, Eingaben, Ergebnis und relevante Fehler sind gegen UI und Backend geprüft.
- [ ] Verfügbares Verhalten, Einschränkungen und Pläne sind unterschieden. Ein fehlender Testzugang wird genannt.
- [ ] Beispielablauf ist nachvollziehbar und mit fiktiven Daten geprüft; schwer rückgängig zu machende Folgen stehen vor der Aktion.
- [ ] Ergänzende Erklärungen und Referenzen sind verlinkt; lange Anleitungen enthalten keine vollständige zweite API-Dokumentation.
- [ ] MDX, Frontmatter, interne Links/Anker, Bilder, `meta.json` und Consumer-Rollennavigation sind geprüft; betroffene Seiten wurden soweit möglich gerendert.
- [ ] TODOs werden erst nach dieser Abnahme abgehakt oder entfernt; „Text vorhanden“ genügt nicht.

## Prüfung dieser Bestandsüberarbeitung

- [x] Alle 37 MDX-Seiten gelesen und ihre Aufgabenlisten aktualisiert; Administrator-Aufgaben priorisiert und ungeprüftes Verhalten als Prüfauftrag formuliert.
- [x] Vorhandene ausgearbeitete Benutzer-, Badge-, Konto- und Metriktexte erhalten; die vorhandene Postfach-Anleitung ebenfalls erhalten.
- [x] README an die vorhandene Struktur angepasst, den Konto-Wegweiser ergänzt und den falschen Zutrittslink korrigiert.
- [x] Formatprüfung für 39 Textdateien und `git diff --check` erfolgreich.
- [x] Alle 37 MDX-Seiten kompiliert; Frontmatter und zusätzliche H1 geprüft.
- [x] 194 lokale Seiten-/Datei-/Anker-/Bildverweise, 20 Bild-Alternativtexte und sieben Navigationsdateien geprüft. `entwickeln/API` ist ein bewusst virtuell erzeugter OpenAPI-Ordner.
- [x] Die acht vorhandenen Tests für die Consumer-Doku-Rollennavigation erfolgreich ausgeführt.

Die statische Prüfung findet weiterhin `administration/badges-verwalten` als
fehlenden Eintrag in der Consumer-Slugliste. Die vorhandenen Tests decken diese
konkrete Auslassung noch nicht ab; der P0-Auftrag bleibt offen. Live-Rendering,
angemeldete Abläufe, Website-Consumer und Hardware wurden nicht geprüft. Es wurden
keine API-/DTO-Verträge, Anwendungskomponenten oder Bilder verändert.

## Benutzerrunde vom 19. Oktober 2026

Auftrag: die vorhandene Benutzeransicht des Webportals vollständig innerhalb der
bestehenden Fumadocs-Struktur beschreiben und den Fokus **Benutzer** anpassen.
Diese Runde dokumentiert den lokalen Arbeitsstand; sie veröffentlicht keinen
Release und ändert weder Backend-Verträge noch Funktionen der nativen App.

### Abdeckung

- [x] Einstieg und Anmeldung einschließlich vorgeschalteter Sicherheitsabläufe,
      Projektkontext, Desktop-/Mobilnavigation und Verwaltungswechsel.
- [x] Persönliches Dashboard, Widget-Konfiguration, Speicherung, Konflikte und Datenfehler.
- [x] Ressourcen und eigene Freigaben, Gültigkeit, Zeitfenster, Voraussetzungen und
      Grenzen gegenüber einer Hardware-Zutrittsentscheidung.
- [x] Eigene Berechtigungsanfragen mit allen Bearbeitungsständen und Rücknahme.
- [x] Eigene Buchungen, Wiederholungen, kombinierte Ressourcen, Änderungen,
      Stornierungsumfang, Anwesenheit und Fehler-/Entwurfszustände.
- [x] Einmaliger Kalenderexport und persönliches Kalenderabo: Erstellen, einmalige
      Linkanzeige, Ersetzen, Widerruf, Erreichbarkeit und Abrufintervall.
- [x] Einweisungen, lokale Vergaben sowie importierte/signierte Nachweise getrennt
      mit Wirksamkeit, Prüfstatus, Gültigkeit, Details und Original-Download.
- [x] Persönlicher Posteingang mit Lesestatus, Archiv, Wiederherstellung, Filtern
      und rechtenabhängiger Empfängersicht; Versandpräferenzen separat.
- [x] Profilbild und Kontodaten, E-Mail/Passwort, 2FA, Wiederherstellungscodes,
      Passkeys, Sitzungen, Zutrittsmedien, Darstellung, Nachweisquellen und MCP.
- [x] Grundlagen, Kontowegweiser, allgemeine Einstiege und Fehlerhilfe aktualisiert.
- [x] Vorhandene Profil-URLs erhalten. Gemeinsame Anleitungen bleiben aus
      **Überblick** erreichbar und aktivieren eindeutig **Benutzer**. Aufgaben stehen
      vor **Profil und Hilfe**. Systemmetriken bleiben unter ihrer bisherigen URL
      erhalten und gehören im Consumer zum Verwaltungsfokus.
- [x] Drei Screenshots der vorhandenen UI mit fiktiven Mitgliedsdaten ergänzt;
      Ansicht am Desktop und Handy geprüft. Das vorhandene Postfachbild bleibt erhalten.

Die 48 Produktseiten enthalten elf neue Anleitungen. Die 19 Seiten des
Benutzerfokus (einschließlich Einstieg und gemeinsamer Profil-/Hilfeseiten) sind
für die vorhandene Web-Selbstbedienung ausgearbeitet. Aufgaben anderer Zielgruppen
werden dadurch nicht als abgeschlossen bewertet. Nicht angebotene Vorgänge wie
Verlustsperre, Ersatzbestellung, Ticketsystem oder Schulungsverwaltung sind als
Grenzen beschrieben.

### Prüfstand und Grenzen

- [x] Alle 48 MDX-Seiten kompiliert; Frontmatter, zusätzliche H1, `meta.json`,
      187 lokale Seiten-/Datei-/Anker-/Bildverweise und 23 Bild-Alternativtexte geprüft.
- [x] 100 Tests in den fünf vorhandenen Testdateien für Doku-Navigation, Portalrahmen,
      Qualifikationen, Ressourcen und persönliches Dashboard erfolgreich; davon 29
      Doku-Navigationstests einschließlich neuer Seiten, eindeutiger Fokuszuordnung
      und erhaltener gemeinsamer Einstiege.
- [x] Typecheck und ESLint für die geänderte Consumer-Navigation erfolgreich.
      Auch die gesamte Web-Lintprüfung endet ohne Fehler, mit 14 bestehenden Warnungen.
- [x] Produktionsbuild erfolgreich, einschließlich TypeScript-Prüfung.
- [x] 23 Doku-Routen jeweils bei 1440 und 390 Pixeln geprüft: HTTP 200,
      keine offenen Schreibaufträge auf den geprüften Seiten, kein seitliches Überlaufen
      und keine Laufzeitfehler. Neue Bildbeispiele zusätzlich visuell geprüft.
- [x] Client-Navigation von Überblick zu Profil und Anmeldesicherheit geprüft:
      bestehende URLs und Benutzerfokus bleiben erhalten. Der bisherige Systemmetriken-Link
      bleibt im Verwaltungsfokus erreichbar.
- [x] Übersetzungsprüfung erfolgreich: deutsche und englische Kataloge mit je 5904 Schlüsseln.
- [x] React-Prüfung erfolgreich, keine Fehler; 540 bestehende Warnungen im gesamten
      Web-Arbeitsstand. Diese Dokumentationsrunde ist keine Bereinigung dieser Warnungen.
- [x] Angemeldeter Leseabgleich mit dem vorhandenen Administratorkonto über acht
      Portal-/Profilrouten. Es wurden keine Kontodaten, Buchungen oder Zugänge verändert.
- [x] Mitgliedsdarstellung für Qualifikationen und mobile Profilnavigation mit
      fiktiven API-Antworten geprüft; dabei kein Verwaltungswechsel sichtbar.
- [x] Nachprüfung mit einem eigens angelegten lokalen Mitgliedskonto durchgeführt;
      der konkrete Umfang und verbleibende externe Voraussetzungen stehen unten.
- [x] Website-Consumer lokal mit dem aktuellen Inhalt und aktivierter bestehender
      Doku-Funktion geprüft; öffentliche Website separat geprüft, siehe unten.
- [ ] Physischer Zutritt und externe Anbieter: nicht ausgeführt.

Vorhandene API-/DTO-Dokumentation und UI-Komponenten wurden als Quellen verwendet;
keine APIs, DTOs oder Dependencies verändert. Prüfungen belegen den aktuellen lokalen
Arbeitsstand, keinen veröffentlichten Software-/Dokumentationsstand. Commit,
Submodule-Verweise, Push und Veröffentlichung bleiben einem entsprechenden Auftrag
vorbehalten.

## Nachprüfung mit Mitgliedskonto und Website

Die ausführliche Auswertung samt Quellenvergleich steht in
[BENUTZER-REVIEW.md](BENUTZER-REVIEW.md). Acht Produktdokumentationen wurden
verglichen. Übernommen sind ein geführter Einstieg, Voraussetzungen vor der Aktion,
erkennbare Ergebnisse und passende Weiterführungen. Die Schnellnavigation bleibt
an den persönlichen Aufgaben ausgerichtet; optionale Verbindungen stehen hinten.

- [x] Ein separates lokales Mitglied mit der vorhandenen Rolle Basic angelegt,
      zwölf effektive Rechte geprüft und über die tatsächliche Passwortanmeldung
      angemeldet. Andere Rollen und Konten wurden nicht verändert.
- [x] Vier Portalbereiche und zehn Profil-/Sicherheitsrouten jeweils bei 1440 und
      390 Pixeln geprüft: 28 erfolgreiche Routenaufrufe, kein Verwaltungswechsel,
      keine administrativen Datenabfragen und nach den Korrekturen keine Laufzeitfehler
      oder seitliches Überlaufen.
- [x] Eigene Profiländerung gespeichert und nach erneutem Laden bestätigt.
- [x] Neue Buchung samt Details, Einzel-ICS, eigenem Kalenderfeed, einmaliger
      Linkerzeugung, Ersetzung und Widerruf geprüft. Ersetzter und widerrufener Link
      werden abgewiesen. Der Testtermin wurde storniert und sein Status erneut gelesen.
- [x] Mehrere reale eigene Serien angelegt; der Export enthält alle zehn expliziten
      Testtermine aus fünf Serien. Sämtliche erzeugten Testtermine sind storniert.
- [x] Ungespeicherte Profil- und Buchungsänderungen lösen die bestehende Warnung aus;
      Verwerfen erlaubt den Wechsel. Dashboard-Editor und Anfrageformular öffnen mit
      den vorhandenen Komponenten für das Mitglied.
- [x] Qualifikationen, Freigaben, Zutrittsmedien und Posteingang mit dem echten
      Mitgliedskontext geprüft. Das neue Mitglied hat dort zunächst keine eigenen
      Vergaben oder Nachrichten. Tests für gefüllte Statusvarianten bleiben ergänzend
      erforderlich; leere Daten belegen keine tatsächliche externe Ausstellung.
- [x] Zwei Live-Befunde in gemeinsamen Profilbausteinen korrigiert: gespeicherte
      Theme-Auswahl und browserabhängige Formatvorschauen erst nach Hydration anzeigen;
      abgewiesene automatische Recovery-Code-Erzeugung ohne unbehandelte Promise-Ablehnung.
      Regressionstests und erneute Desktop-/Mobilprüfung erfolgreich.
- [x] 107 Webtests in sieben Testdateien und sämtliche 110 Website-Tests in 29
      Dateien erfolgreich. Davon prüfen 25 Website-Tests die Doku-/Fokusstruktur.
- [x] Typechecks beider Consumer und Übersetzungsprüfung erfolgreich. Web-Reactprüfung
      ohne Fehler, weiterhin 540 Warnungen im gesamten Arbeitsstand. Website-Lint ohne
      Fehler; bei den korrigierten Web-Komponenten keine Lintfehler.
- [x] Beauftragte Folgekorrektur des CMS-Befunds: Den fest eingebauten Ersatz für
      `PAYLOAD_SECRET` in `apps/mardu-de/payload.config.ts` entfernt. Fehlende, leere
      und ausschließlich aus Leerraum bestehende Werte verhindern das Laden der
      Konfiguration; gesetzte Werte bleiben unverändert. Vier Regressionstests
      prüfen diesen gemeinsamen Eingang. Vor der Korrektur drei erwartete Fehler,
      danach vier erfolgreiche Tests. Eine unabhängige Prüfung fand keinen
      konkreten verbleibenden Umgehungsweg oder Rückschritt.
- [x] Vollständiger Website-Reactcheck nach dieser Korrektur erfolgreich: 425 Dateien,
      keine Fehler, weiterhin 160 Warnungen. Keine Regeln unterdrückt. Alle 114
      Website-Tests in 30 Dateien sowie Lint, Typecheck und Produktionsbuild erfolgreich.
      Schlüsselanforderung für Entwicklung, Build, Laufzeit und CLI im Website-README
      und in der Deployment-Dokumentation ergänzt. Keine API-/DTO-Änderung.
- [x] React-Prüfung der geänderten Website-Dateien erfolgreich: keine Befunde.
- [x] Aktuellen kanonischen Inhalt in den vorhandenen Website-Mount übernommen;
      die alten Versionsdateien und URLs bleiben erhalten. Fumadocs, Logo, Suche und
      vorhandene Fokus-/Baumlogik wiederverwendet.
- [x] Im lokalen Website-Consumer 23 Doku-Routen jeweils auf Desktop und Handy geprüft;
      keine Entwurfsmarker auf diesen Seiten, kein Überlaufen und keine Laufzeitfehler.
      Fokuswechsel, Profil-URLs, Suche, neue Inhalte und Bilder funktionieren.
- [x] Bestehende Website-URLs `/docs/v1` und `/docs/v2` liefern weiterhin HTTP 200.
- [x] Öffentliche Website geprüft: `/docs/benutzer` liefert HTTP 404. Dokumentation ist
      in der bestehenden Website-Konfiguration standardmäßig deaktiviert. Für den
      lokalen Test wurde nur der Prozess mit `MARDU_DE_ENABLE_DOCS=true` gestartet.
- [x] Produktionsbuilds beider Consumer erfolgreich abgeschlossen, einschließlich
      TypeScript-Prüfung und statischer Seitenerzeugung im Website-Consumer.
- [x] Doku-Einstieg im gemeinsamen Kontomenü ergänzt: Im Portal öffnet er direkt
      `/docs/benutzer`, in der Verwaltung `/docs/administration`. Die Verwaltungs-Sidebar
      verwendet ebenfalls diesen Einstieg; keine Rollenprüfung und kein Projektpräfix
      für Doku-URLs. Bestehende Navigation und Menükomponenten wiederverwendet.
- [x] Folgeprüfung des Einstiegs: Mitglied im Portal, Administrator im Portal und
      Administrator in der Verwaltung jeweils auf Desktop und Handy erfolgreich
      geprüft. Alle sechs Fälle öffnen den passenden Fokus im neuen Tab. Eine zunächst
      abgelaufene lokale Verwaltungssitzung wurde vor der erfolgreichen Prüfung erneuert.
      21 Navigations-/Portaltests, Typecheck, betroffene Lintprüfungen,
      Übersetzungsprüfung und Produktionsbuild erfolgreich. Der volle Web-Reactcheck
      bleibt ohne Fehler bei 540 bestehenden Warnungen.
- [x] Website nach CMS-Korrektur erneut geprüft: 23 Doku-Routen in beiden
      Bildschirmgrößen ohne Entwurfsmarker, seitliches Überlaufen oder Laufzeitfehler;
      Fokuswechsel und bestehende Profil-/Metrik-URLs funktionieren. Der anonyme
      bestehende CMS-Endpunkt `/api/users/me` antwortet lokal mit HTTP 200.

Die Testzugänge werden nicht mit der Dokumentation ausgeliefert. Der lokale
Testbenutzer bleibt für Folgeprüfungen bestehen. Zugriffsanfragen wurden als
Formular geprüft, ohne eine Bearbeitungsentscheidung anderer Personen zu simulieren.

## Redaktionelle Prüfung des übrigen Bestands

- [x] Alle 48 Produktseiten auf Wiederholungen geprüft; 22 Seiten inhaltlich
      gestrafft. Übersichtslisten, Profilverweise und wiederholte Erklärungen
      gekürzt; die Zugangsmetriken stehen unter Administration an einer Stelle.
      Voraussetzungen, Warnungen, Entwurfskennzeichnungen, URLs und Abschnittsanker
      bleiben erhalten. Die gemeinsamen Dokumentationsregeln halten dieses Vorgehen fest.
- [x] Bei der Browserprüfung einen bestehenden Auflösungsfehler gefunden:
      Fumadocs verarbeitet relative MDX-Verweise nur mit `./` oder `../` als
      Seitenverweise. 93 Verweise korrigiert; insgesamt 36 Produktseiten angepasst.
      Der ergänzte Test verwendet den vorhandenen Fumadocs-Loader und prüft die
      Verweise des aktuellen Inhalts, ohne historische Versionen umzuschreiben.
- [x] Alle 48 Seiten in der Website bei 1440 und 390 Pixeln geprüft: HTTP 200,
      passende Überschriften, aufgelöste Seitenverweise, kein seitliches Überlaufen
      und keine Laufzeitfehler. Der Sprung zur Metrikreferenz funktioniert mit Anker.
- [x] 48 MDX-Seiten, 189 lokale Link-/Bildziele, 23 Bilder und die Navigation
      geprüft; keine Befunde. 26 Doku-Tests und die gesamte Website-Suite mit 115
      Tests erfolgreich; Typecheck und Lint der ergänzten Testdatei erfolgreich.
      Externe Anmelde-/Nachweisanbieter, echte Passkey-Geräte, zugestellte E-Mails/SMS/Push
      und Hardware sind nicht live abgenommen. Diese Grenzen werden nicht als bestandene
      Ende-zu-Ende-Abläufe gezählt. Es wurden keine API-/DTO-Verträge oder Dependencies
      verändert und keine Änderungen veröffentlicht.
