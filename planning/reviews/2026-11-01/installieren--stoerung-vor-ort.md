# P37 – Störung vor Ort

## Änderungsbrief und Entscheidung

Seite: `docs/installieren/stoerung-vor-ort.mdx`; Heimat Installieren. Leserfrage:
Wie grenzt eine Person vor Ort eine Störung ein und gibt einen nachvollziehbaren
Befund weiter? Vorausgesetzt sind Geräte-Leserechte und die Angaben der eigenen
Installation; Serveradministrationswissen wird nicht vorausgesetzt.

**Belegbare Teildokumentation / offene Prüfung.** Die verborgene Entwurfsseite
ist für den statisch belegbaren Diagnoseumfang ausgearbeitet. Beobachtbares
Ergebnis: Serververbindung, Gerätemeldung, Konfigurationsauftrag, Hardwarezustand
und Zugangsbedingungen getrennt prüfen. Keine Hardwareabnahme.

Erhalten: URL, CLI-Verweis mit Einschränkung bei nicht startender API und die vier
Abschnittsanker `serverzugang-oder-serverzustand-prüfen`, `fehler-eingrenzen`,
`wiederanlauf`, `eskalation`. TODO-Schreibaufträge sind durch einen lesenden
Prüfpfad ersetzt. Änderungen an Aufnahme oder Konfiguration verweisen auf die
vorhandene Geräteanleitung. Keine Blinkcodes, Neustartfristen, Reset-/Powercycle-
oder Aktorbefehle und kein erfundener Diagnosebutton oder Logexport.

## Quellen und fachliche Befunde

Dateipfade ab Software-Repository, sofern nicht anders angegeben:

- Geräteansicht: `web/app/[project]/dashboard/device-management/device-settings/device-settings-sheet.tsx`, Tabs ab Zeile 166 und `DeviceOverviewTab`. Gerätekennung, letzte Verbindung, Firmware, MAC und Netzwerkbindung werden angezeigt; Änderungen sind an Geräte-Änderungsrechte gebunden. Exakte Bezeichnungen: `web/locales/de/devices.json`, `device.settings.tabs`, `device.settings.overview`, `device.column`.
- Online-Grenze: `web/lib/device/device-status-utils.ts:3–9` wertet `lastSeenUtc` mit fünf Minuten aus. Kein Nachweis physischer Einsatzbereitschaft.
- Anschlussidentität/Hardwareanzeige: `web/components/device/endpoint-identity.tsx:31–86`. Auftragsstatus und getrennte Aktionen Serverabruf/Auslesen: `web/components/device/device-endpoints-panel.tsx`, `reader-sensor-configuration.tsx:485–507`; Texte in `web/locales/de/devices.json:204–207, 261–273, 559–585`.
- Anschlussleserecht: `api/Service/Devices/Boundary/HttpControllers/DeviceEndpointsController.cs:21–47`. Gespeicherte Konfiguration ohne Gerätezugriff, Update-/Readbackrechte und Annahme statt Bestätigung: `api/Service/Devices/Boundary/HttpControllers/DeviceEndpointConfigurationController.cs:24–72`; gewünschter, bestätigter und rückgelesener Stand: `api/Service/Devices/Boundary/Dto/DeviceEndpointConfigurationDto.cs:3–30`.
- Bereitschaft: `api/Service/Devices/Application/Protocol/DeviceProtocolService.cs:268–300` verlangt Hardware Ready und bestätigte Konfiguration. Hardware Fault ergibt Faulted; sonst unter anderem Unknown. Unbekannt ist kein Aus-Nachweis.
- Aufnahme: `api/Service/Devices/Boundary/HttpControllers/DeviceEnrollmentController.cs`, Restart-XML/OpenAPI-Vertrag: Identitätserhalt, Sitzungs-/Aktor-/Zustellungssperren, neue Meldung und Bestätigung erforderlich. UI: `web/components/device/device-enrollment-actions.tsx:27–145`. Die Seite verlinkt Voraussetzungen und Ablauf statt sie zu kopieren.
- Diagnosemetriken: `web/app/[project]/dashboard/device-management/device-settings/device-monitoring-tab.tsx:38–76, 109–111` prüft Dashboard- und Datenquellenrechte. Geräteanleitung `administration/geraete-verwalten.mdx#diagnose-lesen` bleibt kanonisch.
- Health: `api/framework/Infrastructure/InfrastructureExtensions.cs:373–383, 464–487`, live ohne Abhängigkeitsprüfung, ready mit registrierten `ready`-Checks. Setup: `api/framework/Infrastructure/SetupModeExtensions.cs:139–145`, live 200, ready 503/setup_required. `web/app/api/healthz/route.ts:3–13` prüft nur die Webroute; keine Geräteaussage daraus abgeleitet.
- Protokollvertrag: `api/Service/Devices/Boundary/HttpControllers/DeviceProtocolController.cs:23–33` liest gespeicherte Beobachtungen, ohne das Gerät zu kontaktieren. Query und Reboot sind separate schreibberechtigte Befehle. Der Reboot-Vertrag nennt Sperren bei Sitzungen/ungeklärten Aktorzuständen und keine Abschlussgarantie. Daraus wird keine Vor-Ort-Neustartanweisung abgeleitet.
- Geräteereignisse: `api/Service/Devices/Boundary/HttpControllers/DeviceController.cs:112–156`, `api/Service/Devices/Boundary/Dto/DeviceLogFilter.cs`, `DeviceLogEntryDto.cs` belegen begrenzte gefilterte Ereignisse mit Zeit-/Korrelationsangaben. Kein Aufruf des Logs-Clients in den geprüften Geräteansichten gefunden; kein Dashboard-Logexport dokumentiert.
- Zugang: `api/Service/Accesses/Application/Services/ResourceAccessDecisionService.cs`, insbesondere `EvaluateEligibilityAsync` und `EvaluateAvailabilityAsync`, prüft Freigaben, Buchungen, Kompetenzen, Aufsicht und Verfügbarkeit getrennt von Geräteverbindung. `api/Service/Accesses/Boundary/Dto/ResourceAccessDecisionDtos.cs` trennt Entscheidung, Gründe, Ressourcen-/Endpointbezug und Sitzungs-/Ausführungsreferenzen. Vorhandene Anleitungen zu Ressourcen, persönlichen Zugangsentscheidungen und Tags verlinkt; keine neuen Verwaltungsabläufe dupliziert.
- Wiederverwendete Anleitungen: `docs/administration/geraete-verwalten.mdx`, `wartungs-cli.mdx`, `benutzer-rollen.mdx`, `tags-verwalten.mdx`, `docs/koordination/ressourcen.mdx` und `docs/installieren/raspberry-pi.mdx` im Doku-Repository, jeweils die im Seitentext verlinkten Abschnitte gelesen.

## Checks und Prüfgrenzen

- `node web/node_modules/prettier/bin/prettier.cjs --ignore-path /dev/null --check` für beide eigenen Dateien: erfolgreich. Das explizite Ignore-Override berücksichtigt die sonst ausgeschlossene Submodule-Quelle; keine anderen Dateien formatiert.
- MDX mit vorhandenem `@mdx-js/mdx` kompiliert: erfolgreich. Mit vorhandenem `github-slugger` alle zehn relativen Links und deren Zielüberschriften sowie die vier ursprünglichen Abschnittsanker geprüft: erfolgreich. Keine TODO-/Entwurfsmarker mehr im Seitentext.
- `git -C web/content/docs diff --check -- docs/installieren/stoerung-vor-ort.mdx planning/reviews/2026-11-01/installieren--stoerung-vor-ort.md`: erfolgreich. Keine globalen Builds oder Softwaretests, da ausschließlich MDX und Bericht geändert wurden.
- Ausschließlich statische Prüfung von Code, Übersetzungen, Verträgen und Nachbaranleitungen. Keine Browser-, CLI-Laufzeit-, Netzwerk-, Provider- oder Hardwareprüfung; keine Aktionen gegen Installation oder Aktoren ausgeführt.
- Koordinator: Darstellung in Software- und Website-Consumer einschließlich Mobilansicht und Markdown-/Agentenausgabe prüfen. An einer Testinstallation die lesenden Schritte und die Trennung von Ablehnung, ungeklärter Bestätigung und physischer Wirkung nachvollziehen.
- Modellbezogene LED-/Displaycodes, Neustartfolgen und physische Wiederanlaufprüfung bleiben außerhalb des dokumentierten Umfangs, bis passende Modell-/Firmwareunterlagen und Praxisbelege vorliegen.

## Publikationsvorschlag und Dateien

Die Seite fehlt derzeit in `docs/installieren/meta.json`; der Software-Consumer
kennt ihren Slug als Bereichseigentum in `web/lib/docs-roles.tsx:159`. Navigation
hier nicht geändert. Nach Consumer-Prüfung kann der ausgearbeitete Diagnoseumfang
unter Installieren veröffentlicht werden. Der Koordinator entscheidet über
Navigation/Suche und einen Verweis vom Bereichseinstieg. Hardwaremontage und
universelle Wiederherstellung werden dadurch nicht abgenommen.

Der eingehende Verweis aus `docs/installieren/abnahme-uebergabe.mdx` bleibt gültig.
Keine zusätzlichen Seiten oder Assets benötigt. Geändert sind ausschließlich
`docs/installieren/stoerung-vor-ort.mdx` und dieser Bericht. Keine Software-, API-,
DTO- oder Navigationsänderungen; XML-/OpenAPI-Dokumentation nur als Beleg gelesen.
