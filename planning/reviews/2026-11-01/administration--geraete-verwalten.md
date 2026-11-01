# Seitenrevision: Geräte verwalten

## Änderungsbrief

Seite: `docs/administration/geraete-verwalten.mdx` (P20), Heimatbereich Administration.
Leserfrage: Wie nehme ich einen Controller auf, prüfe seine Anschlüsse und ersetze oder lösche ihn?
Die Lesenden kennen das Dashboard und ihre Ressourcen, benötigen aber die Unterscheidung
zwischen Datensatz, Netzwerkaufnahme, Gerätebestätigung und physischer Wirkung.

Ziel: Bestehende ausführliche Anleitung erhalten, veraltete Anschlussbeschriftungen
gegen aktuelle UI/Übersetzungen berichtigen, den belegten Firmware-Verlauf ergänzen.
Keine Softwareänderung und keine Anleitung für nicht vorhandene OTA-Aktionen.
Vorhandene Steps, Links, URL und Überschriftenanker bleiben bestehen.

Prüfumfang: statischer UI-/Backend-/Vertragsabgleich, lokale MDX-/Link-/Diff-Prüfung.
Browser-, Website-Consumer- und Hardwareprüfung bleiben beim Koordinator bzw. der
betreuenden Installation. Die ältere Anschlussabbildung muss ersetzt werden.

## Entscheidung: verbessert, zur Prüfung

- Aufnahme, erneuter Import, Netzwerkneustart/-abbruch, fünfminütige Online-Schwelle,
  anschlussbezogene Bereitschaft, Hardwareersatz und Löschfolgen bleiben erhalten.
- Veraltete Anschlussaktionen berichtigt: **An Gerät senden**, **Letzter Auftragsstatus**,
  **Details und Verwaltung**, **Serverstand aktualisieren**, **Vom Gerät bestätigt**.
  Unterschiede zwischen Leser- und Aktorbeschriftungen ausdrücklich benannt.
- Nicht gesendete Formularänderungen und **Änderungen verwerfen** ergänzt;
  Metadaten-Speichern, Sollkonfiguration, Gerätebestätigung und Auslesen getrennt.
- Erneuter Import startet eine bereits erfolgte Aufnahme nicht neu. Der vorhandene
  Einstieg **Erneut ins Netzwerk aufnehmen** bleibt erhalten. Automatischer
  Schlüsselaustausch bleibt beschrieben; keine manuelle Schlüsselübertragung ergänzt.
- Firmwareversion und vorhandene globale OTA-Historie mit Filter, Details und erhaltenen
  Einträgen gelöschter Geräte ergänzt. Keine Update-Start-/Abbruchanleitung erfunden.
- Dashboard-Leserecht für Diagnose sowie Neuladen einer veralteten Löschvorschau ergänzt.
- Die ältere Anschlussabbildung aus der Seite entfernt: Sie zeigt **Speichern**, **Neu laden**,
  **Konfiguration**, **Vom Gerät übernommen** sowie alte Laufzeitgrenzen und eine alte
  direkte Ressourcenzuordnung im Gerätekopf. Das Asset selbst bleibt unverändert.
- Den redaktionellen Hinweis zur fehlenden erneuten Hardwareprüfung aus dem Aufnahmeablauf
  entfernt und hier dokumentiert; die notwendige Funktionsprüfung an der Installation
  steht weiter im Produkttext.

## Geprüfte Quellen

Pfade sind relativ zum Software-Repository; Zeilen beziehen sich auf den geprüften Stand.

| Aussage                                                                                 | Quelle                                                                                                                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Anlegen mit Zertifikat oder signierten Aufnahmedaten, Modell-Erkennung und Wiederimport | `api/Service/Devices/Boundary/HttpControllers/DevicesController.cs:61`, `api/Service/Devices/Boundary/Dto/DeviceCreationDto.cs:8`, `api/Service/Network/Stacks/Ip500/Association/Application/DeviceAssociationService.cs:67` und `:105`                                                                                                     |
| Dialog, technische Kennung, Pflichtimport                                               | `web/app/[project]/dashboard/device-management/dialog/unified-device-setup-dialog.tsx:98`, `web/app/[project]/dashboard/device-management/device-settings/device-properties-forms.tsx:257`, `web/locales/de/devices.json:85` und `:113`                                                                                                     |
| Aufnahme-Neustart und Abbruch, Rechte, Fehler, Erhalt von Identität und Zuordnungen     | `api/Service/Devices/Boundary/HttpControllers/DeviceEnrollmentController.cs:24`, `api/Service/Network/Stacks/Ip500/Association/Application/DeviceAssociationService.Enrollment.cs:24`, `:72`, `:126`; `web/components/device/device-enrollment-actions.tsx:38`                                                                              |
| Automatischer Aufnahmestatus/Schlüsselaustausch                                         | `api/Service/Network/Stacks/Ip500/Association/Application/DeviceAssociationService.cs:272`, `:429`; `web/locales/de/devices.json:596`                                                                                                                                                                                                       |
| Online-Schwelle, Einrichtungsanzeige und Bereitschaft                                   | `web/lib/device/device-status-utils.ts:3`, `:11`; `api/Service/Devices/Application/Protocol/DeviceProtocolService.cs:238`; `api/Service/Devices/Application/Protocol/DeviceProtocolService.Registration.cs:111`                                                                                                                             |
| Übersicht, erlaubte Tabs, Aktualisieren von Metadaten                                   | `web/app/[project]/dashboard/device-management/device-settings/device-settings-sheet.tsx:92`, `:145`, `:168`, `:449`                                                                                                                                                                                                                        |
| Anschlussaktionen, Zustände und Details                                                 | `web/components/device/device-endpoints-panel.tsx:219`, `:1124`, `:1156`, `:1174`, `:1246`; `web/components/device/reader-sensor-configuration.tsx:166`, `:304`, `:356`, `:368`, `:486`; `web/locales/de/devices.json:260` und `:558`                                                                                                       |
| Anschlussrechte und Lösch-/Ausleseauftrag                                               | `api/Service/Devices/Boundary/HttpControllers/DeviceEndpointConfigurationController.cs:26`, `:36`, `:46`, `:55`                                                                                                                                                                                                                             |
| Ressourcenzuordnung und Austausch                                                       | `docs/koordination/ressourcen.mdx:100` im Docs-Submodule (bestehende kanonische Anleitung); dortige Verweise und Voraussetzungen erhalten                                                                                                                                                                                                   |
| Firmwareversion aus Gerätemeldung                                                       | `api/Service/Devices/Application/Protocol/DeviceProtocolService.Registration.cs:139`                                                                                                                                                                                                                                                        |
| Historie, Filter, Details und Geräte-Leserecht                                          | `web/app/[project]/dashboard/device-management/device-management-page-client.tsx:225`, `:265`; `web/components/device/device-ota-history-panel.tsx:58`, `:122`, `:168`; `api/Service/Devices/Boundary/HttpControllers/DeviceOtaHistoryController.cs:18`, `:26`; `api/Service/Devices/Boundary/Dto/DeviceOtaHistoryDto.cs:8`                 |
| Diagnose benötigt Dashboard-Leserecht und Datenquellenrechte                            | `web/app/[project]/dashboard/device-management/device-settings/device-monitoring-tab.tsx:34`, `:47`, `:87`                                                                                                                                                                                                                                  |
| Löschen: Rechte, Vorschau, Bestätigung, Netzwerkabmeldung, erhaltene Historie           | `api/Service/Devices/Boundary/HttpControllers/DeviceController.cs:71`, `:83`; `api/Service/Devices/Application/Services/DeviceService.CreationUpdate.cs:153`; `api/Service/Devices/Application/Services/DeviceDeletionImpactProvider.cs:27`; `web/app/[project]/dashboard/device-management/data-table/device-data-table-row-action.tsx:35` |

## Quellendrift für den Koordinator

- Der ältere Root-AGENTS-Hinweis nennt `start-provisioning` als verbliebenen Admin-Einstieg.
  Die aktuellen Controller und der generierte Client enthalten diesen Aufruf nicht.
  Belegt sind `POST /api/v1/device/{deviceId}/enrollment/restart` und
  `DELETE /api/v1/device/{deviceId}/enrollment` mit `Devices.Update`.
  Der Koordinator hat bestätigt, den aktuellen Vertrag zu dokumentieren.
- `web/docs/ota-frontend-contract-v1.md:53`, `:83`, `:106` beschreibt Status-, Start-
  und Abbruchendpunkte, die im aktuellen `DeviceController` und generierten Client
  fehlen. Die bei `:280` bis `:282` genannten Dateien `lib/device/ota.ts`,
  `components/device/device-ota-panel.tsx` und
  `app/[project]/dashboard/device-management/devices/[deviceId]/page.tsx` sind nicht vorhanden.
  Der aktuelle Controller hat unter `DeviceController.cs:175` und `:203` ausschließlich
  Firmware-Artefakt-Upload/-Liste; diese starten laut OpenAPI keinen Geräte-Updatevorgang.
  Das Settings Sheet bietet unter `device-settings-sheet.tsx:168` nur Übersicht,
  Anschlüsse und Diagnose an. Übersetzungsschlüssel für alte OTA-Aktionen sind kein UI-Beleg.
  Kein pauschaler Schluss auf fehlende Firmwareunterstützung der Hardware.
- Screenshot-Ersatz mit aktueller Anschlusskarte für Leser/Aktor nötig; Bedarf an
  den Koordinator gemeldet. Keine neue Bildschirmaufnahme oder Hardwareabnahme behauptet.

## Eigene Prüfungen und offene Praxisprüfungen

- Erfolgreich: MDX-Kompilierung dieser Seite mit vorhandenem `@mdx-js/mdx`.
- Erfolgreich: neun lokale Seiten-/Ankerverweise mit vorhandenem `github-slugger`
  gegen vorhandene Ziele geprüft. Vorhandene Überschriften und damit deren Anker erhalten.
- Erfolgreich: Prettier für beide eigenen Dateien mit `--ignore-path /dev/null`
  (der normale Consumer-Check ignoriert das Submodule) und gezieltes `git diff --check`.
- Keine Tests, globalen Builds, Browser-/Server-/Hardware- oder Provideraktionen ausgeführt.
- Offen: Consumer-Rendering im Software- und Website-Consumer, mobil und in beiden Themes;
  reale Aufnahme, Konfigurationsübernahme, Auslesen, Austausch mit Aus-Bestätigung und
  Netzwerkabmeldung beim Löschen; Historie nach Geräte-Löschung praktisch prüfen.
- Keine neuen Seiten oder Navigationsänderungen nötig. Bestehende Links auf Ressourcen
  und Tags bleiben erhalten; zentralen Quellendrift und Screenshotbedarf nachverfolgen.
- API-/DTO-Dokumentation unverändert: ausschließlich Produktanleitung und Bericht bearbeitet.

## Geänderte Dateien

- `web/content/docs/docs/administration/geraete-verwalten.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--geraete-verwalten.md`
