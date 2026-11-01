# P35 – Geräte in Betrieb nehmen

## Änderungsbrief

Leserfrage: Wie nehme ich einen angeschlossenen Controller an einem bestehenden
Mardu-Server auf und prüfe die Softwareeinrichtung vor dem Einsatz? Vorausgesetzt
sind Zugang zum Dashboard, Geräteunterlagen und ein bereits eingerichtetes
IP500-Netzwerk. Ergebnis ist eine nachvollziehbar geprüfte Aufnahme mit
Anschlusskonfiguration und Ressourcenzuordnung; eine physische Abnahme wird daraus
nicht abgeleitet. Heimat bleibt Installieren. Die drei vorhandenen
Abschnittsüberschriften und damit ihre Anker bleiben erhalten. Detailabläufe
bleiben in der Geräte- und Ressourcenanleitung. Montageangaben, unterstützte
Firmwarestände und echte Hardwareergebnisse sind nicht belegt.

## Entscheidung

**Belegbare Teildokumentation / offene Prüfung.** Der bisherige versteckte
TODO-Entwurf wird als begrenzter Ablauf für die Softwareeinrichtung ausgearbeitet.
Navigation, Software und andere Seiten werden nicht geändert.

## Befunde und Umsetzung

- Serverinstallation und Geräteaufnahme sind getrennt. Voraussetzung ist ein
  vorhandener Server mit registriertem, erreichbarem IP500-Edge-Router. Für andere
  Netzwerkarten wird kein Aufnahmeweg behauptet.
- Vorbereitung nennt Aufnahmedaten, Rechte, Geräteunterlagen und die vorgesehene
  Ressource. Montage- und Verdrahtungsvorgaben werden nicht aus Backendmodellen
  abgeleitet.
- Der Ablauf verlinkt die geprüfte Geräteanleitung für Import und Konfiguration
  sowie die Ressourcenanleitung für Hardwarezuordnung und Nutzungsregel. Die
  Teilanleitung wiederholt keine vollständigen Feld-/Fehlerkataloge.
- Dateiprüfung, Datensatz, Netzwerkaufnahme, automatische Modellermittlung,
  Anschlussbestätigung und physisches Ergebnis werden unterschieden.
- Bei Zertifikatsimport kommt das Modell aus HELLO; signierte Mardu-Aufnahmedaten
  können es vorgeben. Modellcode und Knotenzahlen werden gegen den Backendkatalog
  geprüft. Anschlusskonfiguration wird bei der Knotenanmeldung versendet;
  mindestens ein bereiter Anschluss genügt für den Gerätezustand Betriebsbereit.
- Keine alte Start-Provisionierungsaktion, manuelle Schlüsseleingabe oder
  OTA-Start-/Abbruchaktion beschrieben. Firmwarestand und vorhandene Historie
  werden verlinkt. Die Suche nach `start-provisioning`, `ota/start`, `ota/cancel`
  in aktueller Geräteoberfläche und Gerätekomponenten lieferte keine Treffer.
- Erhalten: URL, Titel, die Überschriften Vorbereitung und Montage, Netzwerk und
  Softwareaufnahme sowie Abnahme und damit die bisherigen Abschnittsanker.
  Vorher gab es außer Abgrenzung und Schreibaufträgen keinen ausgearbeiteten
  Ablauf und keine Bilder. Der Verweis auf die noch unfertige Seite
  `abnahme-uebergabe.mdx` wurde durch sichtbare, begrenzte Prüfkriterien ersetzt.
- Keine API-/DTO-Änderung, daher keine Anpassung technischer API-Dokumentation.

## Geprüfte Quellen

Pfade beziehen sich auf den Software-Repository-Root:

- `web/app/[project]/dashboard/device-management/dialog/unified-device-setup-dialog.tsx`,
  `handleFinish` und `canCreateDevice`: Create-Recht, Import-Payload, Erstellen.
- `web/app/[project]/dashboard/device-management/device-settings/device-properties-forms.tsx`,
  Importbereich und `includeManifest`; `web/locales/de/devices.json`,
  `device.create`, `device.form`, `device.endpoints`: aktuelle Beschriftungen.
- `api/Service/Devices/Boundary/Dto/DeviceCreationDto.cs`: technische Kennung,
  genau eine Importvariante; `api/Service/Devices/Boundary/HttpControllers/DevicesController.cs`,
  `CreateDevice`: Rechte, Aufnahmevertrag, Modell- und Ressourcenabgrenzung.
- `api/Service/Network/Stacks/Ip500/Association/Application/DeviceAssociationService.cs`,
  `StartDeviceAssociationAsync` und `TryDiscoverModelAsync`: Routervoraussetzung,
  IP500-Grenze, Modellermittlung und Synchronisierung der Anschlüsse.
- `api/Service/Devices/Configuration/DeviceProtocolSettings.cs`, `MatchesHello`:
  Modellcode und erwartete Knotenzahlen.
- `api/Service/Devices/Application/Protocol/DeviceProtocolService.Registration.cs`,
  `HandleHelloAsync` und `ResolveDesiredConfiguration`: Konfiguration bei Anmeldung,
  erneute Bestätigung erforderlich; `DeviceProtocolService.cs`,
  `UpdateReadinessAsync` und `IsNodeReady`: Einzelanschluss-/Gesamtbereitschaft.
- `web/components/device/device-endpoints-panel.tsx`, `canUpdateDevice` und
  Konfigurationsaktionen; `api/Service/Devices/Boundary/HttpControllers/DeviceEndpointConfigurationController.cs`,
  `GetAsync`/`PutAsync`: Lesen/Ändern getrennt, angenommener Auftrag ist keine Bestätigung.
- `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessController.cs`,
  `AssignHardware`: Hardwareverwaltung erforderlich, Zugriffsregel unverändert.
- `web/components/device/device-enrollment-actions.tsx` und
  `api/Service/Devices/Boundary/HttpControllers/DeviceEnrollmentController.cs`:
  erneute Netzwerkaufnahme/Abbruch sind eigene Aktionen; kein Ersatz für Anschlussprüfung.
- Kanonische Inhalte: `web/content/docs/docs/administration/geraete-verwalten.mdx`
  und `web/content/docs/docs/koordination/ressourcen.mdx`; Kontext:
  `docs/installieren/index.mdx`, `abnahme-uebergabe.mdx`, `meta.json` im selben
  Docs-Submodul und `web/lib/docs-roles.tsx`.

## Eigene Prüfungen und Grenzen

- Beide eigenen Dateien mit vorhandenem `bun fmt` formatiert; beim abschließenden
  Check wird `--ignore-path=/dev/null` verwendet, weil die Web-Ignore-Datei das
  Docs-Submodul sonst ausnimmt.
- MDX-Inhalt mit installiertem `@mdx-js/mdx` kompiliert (Frontmatter vorher
  abgetrennt): Syntax gültig.
- Alle acht relativen MDX-Verweise einschließlich Zielabschnitten durch Lesen der
  Zielquellen geprüft. Drei ursprüngliche Überschriften erhalten. Keine TODOs
  oder leeren Aufgabenlisten im Produkttext.
- Dateibezogener `git diff --check` im Docs-Submodul.
- Keine Browser-, Website-Consumer-, Hardware- oder Firmwareprüfung durchgeführt;
  keine globalen Tests, Builds, Hardwarebefehle oder externen Schreibaktionen.
  MDX-Kompilierung belegt keine Consumerdarstellung oder physische Abnahme.

## Publikationsvorschlag / Koordination

Die Seite kann nach gemeinsamer Consumerprüfung als begrenzte Anleitung zur
Softwareeinrichtung angeboten werden. Sie ist keine Montageanleitung und keine
Abnahmevorlage. Bis zur Prüfung keine Abnahmebehauptung. Der Koordinator
entscheidet über Aufnahme in `installieren/meta.json`, passende Einordnung im
Bereichsstart und Consumerfilter; diese Dateien bleiben hier unverändert.

Für die vollständige Inbetriebnahme bleiben gerätespezifische Anschlussunterlagen,
belegte Hardware-/Firmwarekombinationen und eine echte Prüfung mit Edge-Router,
Controller, Leser/Aktor sowie erlaubtem/verweigertem Zugriff erforderlich. Die
Nachbarseite Abnahme und Übergabe bleibt beim zuständigen Auftrag. Keine weitere
Produktseite oder neues Bild erforderlich für den hier belegten Umfang.

## Geänderte Dateien

- `web/content/docs/docs/installieren/inbetriebnahme.mdx`
- `web/content/docs/planning/reviews/2026-11-01/installieren--inbetriebnahme.md`
