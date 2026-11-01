# N14 – Einen Node-RED-Flow entwickeln und prüfen

- Seite: `docs/entwickeln/automationsfluesse.mdx`.
- Entscheidung: **belegbare Teildokumentation / offene Prüfung**; neue eigenständige Anleitung, zur Prüfung, keine praktische Abnahme.
- Kanonischer Heimatbereich: **Entwickeln**.
- Leserfrage: Wie entwickle ich mit der bereits eingerichteten Verbindung einen eigenen lesenden Flow, verstehe seine Nachrichten und prüfe das Deploy-Ergebnis?
- Vorwissen: Node-RED-Nodes verbinden, `msg.payload` und `msg.topic` zuordnen; eine vorhandene Testressource und betriebsbereite Verbindung stehen bereit.

## Bedarf und Zuschnitt

Die Bestandsseite `administration/automationen.mdx` beantwortet Einrichtung, Verbindungsreparatur, Anschlussveröffentlichung, Zuordnung und Entfernung. Sie beschreibt keinen vollständigen lesenden Entwicklungsablauf mit Ressourcenauswahl, Zustandsschema, Catch-Pfad und Debug-Prüfung. Die neue Seite ergänzt diese eigenständige Aufgabe. Die vorhandene Vorlage `examples/zustand-lesen.json` belegt den Aufbau Inject → Zustand lesen → Debug; ihre importierten Beispielzugangsdaten und teilweise alten Kommentarformulierungen wurden nicht übernommen. Die Anleitung verwendet direkt angelegte Nodes mit der vorhandenen Verbindung und eine fiktive verwaltete Ressource.

Die Seite führt vom manuellen Lesen über Schemaabfrage zu `Zustands-Änderung` und `Verbindungs-Status`. Der zusätzliche kurze Nachrichtenvergleich erklärt die tatsächlich vorhandenen Eingangs-, Ausgangs- und Statuswege einschließlich CloudEvent-Hülle und Abschlusskorrelation. Keine Anleitung zum Schalten, keine Freigabeentscheidung, kein echter Flowdeploy und keine hypothetischen Protokollpacks. Gerätemeldung, Aktionsannahme, Aktionsabschluss, Verfügbarkeit und physische Bestätigung bleiben getrennt.

## Quellen und relevante Stellen

Pfade ohne Präfix sind relativ zum Software-Repository.

- `integrations/node-red/nodes/mardu.html:1658`: Hilfe **Zustand lesen**, Ressourcenreferenz, Vorgabenpriorität, unterstützte Typen und Ausgabe.
- `integrations/node-red/nodes/mardu.html:1332`: Dialogbezeichnungen **Mardu**, **Ressourcentyp**, **Ressource**, **Weitere laden**, **Ressourcen-ID**.
- `integrations/node-red/nodes/mardu.html:1759` und `:1792`: Katalogpagination und **Schema lesen**.
- `integrations/node-red/nodes/mardu.html:1848`, `:1862`, `:1744`: **Mardu-Ereignis**, **Zustands-Änderung**, **Verbindungs-Status**; Nachrichtshülle, REST-Nachladen und 30-Sekunden-Abgleich.
- `integrations/node-red/nodes/mardu.html:1688`, `:1728`, `:1830`: **Aktion ausführen**, **Aktion beendet**, **Aktions-Status**; `end-session`, Annahme und Abschluss, `executionId`-Pfad und Ergebnisstatus.
- `integrations/node-red/nodes/mardu.html:1573`, `:1629`, `:1956`, `:2358`: Checkpointübernahme/-entscheidung, Catch-Verarbeitung, unterstützte Beobachtungsfelder und Unterschied zum Schaltauftrag.
- `integrations/node-red/src/index.ts:215`, `:378`, `:394`: reale Implementierung von Lesen, exaktem Ereignisfilter, Start-/MQTT-/periodischem Abruf und Versionserkennung. Automatische Abruffehler werden gewarnt; keine erfundene Catch-Ausgabe für diese Quelle.
- `integrations/node-red/src/runtime/resources.ts:14`: tatsächliche REST-Pfade für Zustand, Schema und Ausführungsstatus.
- `integrations/node-red/src/runtime/connection.ts:85` und `:266`: getrennte REST-/MQTT-Statusdaten und Statusdarstellung.
- `api/Service/Automations/Boundary/HttpControllers/AutomationResourcesController.cs:14`: eigene Laufzeitauthentifizierung und Lese-/Schemaendpunkte.
- `api/Service/Automations/Application/Services/AutomationResourceService.cs:105`, `:265`, `:303`: Schema, Lebenszyklus/`online` für verwaltete Ressourcen sowie verborgenes 404 bei deaktivierter oder nicht authentifizierter Laufzeit.
- `api/Service/Automations/Boundary/Dto/AutomationResourceStateDtos.cs:44`: Zustandshülle mit optionalem Beobachtungszeitpunkt und redigierten Werten.
- `api/Service/Automations/Application/AutomationActionRegistry.cs:45`: Katalogfähigkeiten sind kein Nachweis einer ausführbaren Aktion; `Application/Executors/MachineEndSessionAutomationExecutor.cs:22` belegt den registrierten `managed-resource`-/`end-session`-Executor.
- `api/Service/Automations/NodeRed/Application/Services/NodeRedEditorSessionService.cs:30`: Personenbezogene Editor-Sitzung, View-Recht und getrenntes CanUpdate.
- `web/app/[project]/dashboard/automations/page.tsx`: eingebetteter Editor und Sitzungslebenszyklus; `web/locales/de/settings.json:2210` und `:2226`: aktuelle Zugangsrechte und **Node-RED öffnen**.
- `integrations/node-red/editor/deployment-lifecycle.js:120`: Vorschau, bestätigte Übernahme und Abfrage eines unklaren Deploy-Ergebnisses ohne erneutes Absenden.
- `api/Service/Automations/NodeRed/Application/Services/NodeRedDeploymentProxyHandler.cs:39`: aktueller Revisionsvertrag, gemeinsame Deploy-Sperre, Ergebnisabgleich.
- `integrations/node-red/examples/zustand-lesen.json`, `examples/README.md`: vorhandener lesender Aufbau und Abgrenzung Simulation/Gerätebetrieb.
- `integrations/node-red/test/mardu-nodes.mjs:398`, `:498`, `:509`: statisch gelesene bestehende Tests zu Referenzauflösung, Ereignisfilter, Verbindungsstatus und Versionsunterdrückung.
- `integrations/node-red/test/core-runtime-regressions.mjs:204`, `:244`, `:379`: statisch gelesene Tests zu Wiederaufnahme nach fehlendem Hinweis/initialem Fehler, Catch-Details und fehlender Version.

## Eigene Prüfungen

- Beide eigenen Dateien mit dem vorhandenen Prettier 3 aus `web/node_modules` formatiert und explizit geprüft; Submodule wird mit `--ignore-path /dev/null` berücksichtigt.
- Neue Produktseite mit dem vorhandenen `@mdx-js/mdx` im Speicher kompiliert; kein Build/Serverstart und keine generierten Dateien.
- Relative Produktlinks und die beiden verwendeten Adminanker lokal auf Existenz geprüft; JSON-Beispiel syntaktisch geparst.
- `git diff --check --no-index /dev/null <Datei>` für beide Neudateien als Whitespace-Prüfung; Exit 1 wegen neuer Inhalte ist erwartet, keine Whitespace-Diagnose.
- Keine Softwareänderung und keine Teständerung; Backend-/Node-RED-Tests wurden gelesen, nicht ausgeführt. Keine API-/DTO-Vertragsänderung; vorhandene XML-/OpenAPI-Verträge wurden als Quellen wiederverwendet.

## Offene Prüfung und Hinweise an die Koordination

- Consumer-Rendering, mobile Darstellung, Navigation und Markdown-/Agentenausgabe der neuen Seite im gemeinsamen Lauf prüfen. Navigation/Consumerlisten sind ausdrücklich nicht Teil dieses Agentenpatches.
- Der beschriebene Leseablauf benötigt einen Browserdurchlauf mit Testressource und verwalteter Laufzeit: Auswahl und Folgeseiten, Lesen/Schema, Catch-Ausgabe, erster Snapshot und erneuter Abgleich. Es wurde kein Flow deployt und kein Zustand einer realen Installation gelesen.
- Kein Hardware-/Anbieterversprechen; der Beispielablauf benötigt keine Hardware oder externe Protokollverbindung. Die zusätzlichen Aktions-/Beobachtungskontrakte wurden ausschließlich statisch belegt.
- Vorschläge für Querverweise: aus `entwickeln/index`, `administration/automationen` und dem vorhandenen privaten-Automation-Hinweis in `entwickeln/mqtt-events` auf diese Entwicklungsanleitung verweisen. Nur der Koordinator bearbeitet diese Seiten und Navigation.
- Quellenkonflikte nicht in die Anleitung übernommen: `examples/README.md` enthält noch einen Schritt „Anschluss … stilllegen“, während der aktuelle bestätigte Deploy den Lebenszyklus behandelt. Die Hilfe zu **Beobachtung melden** behauptet im letzten Absatz ebenfalls, Entfernen/Deploy löse keine Zuordnung; aktueller Deploy-Editor und Backend widersprechen dem. Diese Alttexte sollten getrennt überprüft werden.
- Der Protokollkatalog nennt für Managed MQTT `MQTT.js 5.15.2`, `integrations/node-red/package.json` verwendet `5.16.0`. Deshalb keine Paketversion oder behauptete Protokollkompatibilität aus dem Katalog als Teil der neuen Aufgabe übernommen; ein Versionsabgleich bleibt Softwarepflege.

## Geänderte Dateien

- `web/content/docs/docs/entwickeln/automationsfluesse.mdx`
- `web/content/docs/planning/reviews/2026-11-01/entwickeln--automationsfluesse.md`
