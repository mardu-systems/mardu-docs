# N10: MQTT-Zugänge verwalten

## Entscheidung und Leserfrage

**Belegbare Teildokumentation / offene Prüfung**, Stand 2026-11-01. Neue Seite
`docs/administration/mqtt-broker.mdx`, kanonischer Heimatbereich Administration.
Leserfrage: Wie richte ich einen erreichbaren Informationsbroker und einen
begrenzten externen Lesezugang ein, prüfe ihn und entziehe ihn wieder?

`docs/administration/integrationen.mdx#mqtt` enthält einen zutreffenden Überblick,
aber keinen vollständigen Ablauf für Konto und ACL. Die verbesserte Bestandsseite
`docs/entwickeln/mqtt-events.mdx` beschreibt Clientverbindung, Filter und Payloads;
die neue Anleitung verlinkt diese Inhalte statt den Protokollvertrag zu duplizieren.
Der Zusatzseitenplan und Zusatzseitenbrief bilden den Entwurf nach Arbeitsweise B.

## Umsetzung

- Native UI unter Administration → Integrationen → Embedded MQTT; kein erfundener
  eigener Verbindungsdialog oder Verbindungstest im Administrationsformular.
- Getrennte HTTP-Rechte für Brokerkonfiguration und Integrationsschnittstellen.
- Listener-/TLS-Einrichtung, Startprofile als Entwurf, Konfigurationssperren,
  lokale Bind-Adresse und Folgen von Port-/TLS-Wechsel und Brokerneustart.
- Eigenes eingeschränktes Lesekonto, aktive `subscribe / allow`-ACL, Katalogauswahl
  mit automatisch erzeugter `+`-Wildcard und Möglichkeit der Einschränkung auf eine ID.
- Vorrang überlappender Sperren, QoS-Grenze und Retained-Verhalten, sofortige
  Auswirkungen von Dialogaktionen sowie Anmeldung und Abonnement nach Widerruf.
- Explizit: Externe Clients bleiben read-only; Admin/ReaderAll lesen `v1/info/#`
  unabhängig von eigenen ACLs. Keine Publish-Regeln, Sharedcredentials oder
  Dashboard-Anmeldedaten als MQTT-Zugang erfunden.
- Statuszähler als Diagnose, kein Empfangsnachweis; Demo-Verkehr als virtuelle Daten.
- Wiederverwendet: bestehende Markdown-Struktur, Tabellen, relative Links,
  Zertifikatsanleitung und Entwickler-Lesetest. Keine zusätzlichen Komponenten,
  Bilder, Dependencies, APIs oder DTOs. API-/DTO-Dokumentation unverändert.

## Geprüfte Quellen

Dateipfade beziehen sich auf das Software-Repository, Zeilen auf den gelesenen Stand.

| Quelle                                                                                                            | Relevante Stellen / Beleg                                                                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `web/components/layout/sidebar/dashboard-navigation.ts`                                                           | 236–239: Integrationen-Einstieg mit `Integrations.View`, native Zielroute `/dashboard/admin/integrations/mqtt`.                                                                    |
| `web/app/[project]/dashboard/admin/integrations/mqtt/page.tsx`                                                    | 125–141: Profile und konkrete Vorgaben; 194–320: direkt ausgeführte Konto-/Passwort-/ACL-Aktionen; 331–675: Status, Listener, TLS, Demo, Konten, Katalog; 676–734: native Dialoge. |
| `web/app/[project]/dashboard/admin/integrations/mqtt/use-mqtt-broker-settings-controller.ts`                      | 104–173: getrenntes Laden von Settings, Status, Zertifikaten, Konten, Katalog; 198–213: Sperren beachten; 226–287: Neuladen, Speichern, Neustart.                                  |
| `web/app/[project]/dashboard/admin/integrations/mqtt/mqtt-broker.utils.ts`                                        | 71–113: Pflichtfeldprüfungen, Port, Zertifikatsauswahl, Demo-ID und Intervall.                                                                                                     |
| `web/components/integrations/mqtt/mqtt-users-card.tsx`                                                            | Kontenliste, Bearbeiten, ACLs, Passwort und bestätigtes Löschen.                                                                                                                   |
| `web/components/integrations/mqtt/mqtt-user-create-dialog.tsx`                                                    | Benutzername/Passwort, Kontotyp, Aktiv, Beschreibung; eingeschränkter Vorgabetyp.                                                                                                  |
| `web/components/integrations/mqtt/mqtt-user-dialog.tsx`                                                           | Kontotyp, Aktiv und Beschreibung; Benutzername bleibt nur lesbar.                                                                                                                  |
| `web/components/integrations/mqtt/mqtt-user-password-dialog.tsx`                                                  | Neues Passwort wird gesetzt; keine Passwortabfrage.                                                                                                                                |
| `web/components/integrations/mqtt/mqtt-acl-dialog.tsx`                                                            | Regelliste mit Filtern, Status, Bearbeiten und bestätigtem Löschen.                                                                                                                |
| `web/components/integrations/mqtt/mqtt-acl-editor-dialog.tsx`                                                     | 63–108: vorhandene Werte, ausschließlich `subscribe`; Katalog/Topic-Filter, allow/deny, Aktiv, QoS und Retained-Schalter.                                                          |
| `web/components/integrations/mqtt/mqtt-acl-filter.ts`                                                             | Platzhalter → `+`; Validierung auf Informationsbaum, kein globaler Filter.                                                                                                         |
| `web/components/integrations/mqtt/mqtt-runtime-overview.tsx`                                                      | Laufzeitzustände, Endpoint, Zähler, letzte Fehlermeldung, Status aktualisieren und bestätigter Neustart; keine Client-Empfangsbestätigung.                                         |
| `web/locales/de/settings.json`                                                                                    | 1572 ff. `settings.mqtt`, 1940 ff. `integrations.mqtt`: UI-Bezeichnungen, Hinweise, Dialogtitel.                                                                                   |
| `api/Service/Devices/Boundary/HttpControllers/MqttInfoBrokerSettingsController.cs`                                | 37/68: Settings View/Update; 54–62 und 187–200: Feldsperren; 74–105: IP-/TLS-Zertifikatsprüfung; Speichern in vorhandene Konfigurationsabschnitte.                                 |
| `api/Framework/Infrastructure/Settings/SettingsEnvironmentLock.cs`                                                | ENV-/DotEnv-Sperrquelle und Zurückweisen gesperrter Änderungen.                                                                                                                    |
| `api/Framework/Infrastructure/Network/Broker/Boundary/MqttUsersController.cs`                                     | 34/46 View, 59 Create, 94/117 Update, 137 Delete auf Integrations; 67–68/98–99: gültige Kontotypen; Cache-/Sitzungswiderruf nach Mutation.                                         |
| `api/Framework/Infrastructure/Network/Broker/Boundary/MqttAclsController.cs`                                      | View/Create/Update/Delete auf Integrations; ausschließlich subscribe, allow/deny, Filter- und QoS-Validierung; Widerruf nach allen Mutationen.                                     |
| `api/Framework/Infrastructure/Network/Broker/Boundary/MqttBrokerStatusController.cs`                              | 20: Integrations View für Status; 32: Integrations Update für Neustart.                                                                                                            |
| `api/Framework/Infrastructure/Network/Broker/DbMqttAclService.cs`                                                 | 31–45: explizite anonyme Konfiguration; 97–105 und 139–140: breite Kontotypen erhalten erzeugte Freigabe statt eigener ACLs; 130–135: nur aktive Subscribe-ACLs.                   |
| `api/Framework/Infrastructure/Network/Broker/MqttInfoPolicy.cs`                                                   | 53–110: Filterabdeckung, deny-Vorrang, QoS-Minimum, Retained-Unterdrückung.                                                                                                        |
| `api/Framework/Infrastructure/Network/Broker/MqttServerHostedService.cs`                                          | 82–118: automatischer Neustart nach Änderung; 232–267: TLS-/Klartextlistener; 416–432: externe Publishes abweisen; 530–553: Status; 555–596: betroffene Sitzungen entfernen.       |
| `api/Framework/Infrastructure/Network/Broker/AclCacheBuster.cs`                                                   | Invalidierung des Benutzercaches ruft Broker-Widerruf auf.                                                                                                                         |
| `api/Framework/Infrastructure/Network/Broker/Configuration/MqttBrokerSettings.cs`                                 | Bind-Adresse, Port, TLS, anonyme Zugriffe, Wildcard-Option, reservierte Client-IDs.                                                                                                |
| `api/Service/Devices/Application/MqttInfoBrokerSettings.cs`                                                       | Pflicht-Demo-ID, 5–3.600 Sekunden, TLS/Zertifikat.                                                                                                                                 |
| `api/Service/Devices/Application/Publishing/DeviceInfoHeartbeatHostedService.cs`                                  | Demo-Nachrichten und virtuelle Geräte-ID, nur bei verfügbarem Broker.                                                                                                              |
| `docs/administration/server-einstellungen.mdx#zertifikate` und `docs/entwickeln/mqtt-events.mdx` im Doku-Submodul | Bestehende Zertifikatsanleitung, Protokoll-/Payloadgrenzen und begrenzter Lesetest.                                                                                                |

## Produktabweichungen und offene Prüfungen

- Die Kontotypauswahl bietet `Anonymous` und `None` an, das Backend lehnt beide
  bei Create/Update mit 400 ab. Deshalb keine Anleitung für diese UI-Optionen;
  anonymer Zugang ist als Serverkonfiguration erklärt.
- `mqtt-user-dialog.tsx:35–37` initialisiert den Editierentwurf mit
  ReaderRestricted/Aktiv/leerer Beschreibung. Die Übernahme des gewählten Kontos
  liegt nur in `handleOpenChange(true)` (54–60), der Dialog wird aber bereits offen
  bedingt gemountet (`page.tsx:676–683`). Im Browser prüfen, ob beim ersten Öffnen
  die bestehenden Werte erscheinen; andernfalls kann Speichern unbeabsichtigt
  Kontotyp/Status/Beschreibung ändern. Die Anleitung fordert vor Speichern deren
  Kontrolle; keine Softwareänderung in diesem Auftrag.
- Broker-Speichern kann erfolgreich sein, während der asynchron nachlaufende
  Brokerneustart scheitert. Live-Status/Startfehler und externer Lesetest bleiben
  als getrennte Prüfschritte erforderlich.
- Nicht durchgeführt: Browser-/Mobile-/Theme-Render in Software und Website,
  praktische Dialogprüfung, Brokerstart/-neustart, echter MQTT-Client, TLS-Vertrauen,
  Netzwerk-/Containererreichbarkeit, ACL-Widerruf an einer offenen Sitzung,
  Raspberry-Pi-/Geräteprüfung. Keine Abnahme aus Codelektüre.

## Eigene Checks

- Statischer Abgleich von UI, Übersetzungen, Controllerrechten, Brokerpolicy und
  Widerrufspfad; keine externen Mutationen, Softwaretests, Builds oder Serveraktionen.
- `web/node_modules/.bin/prettier --ignore-path /dev/null --check` für beide
  zugewiesenen Dateien: erfolgreich. Der explizite Ignore-Pfad ist nötig, weil
  `web/.prettierignore` das Doku-Submodul ausschließt. Der MDX-Parser lief dabei mit.
- Lokaler Python-Dokumentcheck: alle sechs relativen Links einschließlich ihrer
  Ankerziele vorhanden; Frontmatter mit Titel/Beschreibung und Struktur ohne H1
  geprüft. Keine erfundene CI-Prüfung, nur ein lokaler Inhaltscheck.
- `git diff --no-index --check /dev/null` je neuer Datei: keine Whitespace-Fehler.
- Scoped Git-Status: ausschließlich die zwei zugewiesenen neuen Dateien geprüft.
  Navigation und beide Consumer bleiben bei der Koordination.

## Koordination und Querverweise

- Neue Seite in Administration-Navigation und nötigen Consumerlisten aufnehmen.
- `administration/integrationen.mdx#mqtt`: neue Anleitung als Ziel für Einrichtung
  und Kontoverwaltung ergänzen; Überblick kann kurz bleiben.
- `entwickeln/mqtt-events.mdx`: vorhandenen Administrationslink auf die neue
  kanonische Anleitung umstellen; Protokoll und Payloads dort erhalten.
- Keine Links auf andere neue Zusatzseiten gesetzt. Bestehende Links führen zu
  Integrationen, Zertifikaten und Entwickler-MQTT.

## Geänderte Dateien

- `web/content/docs/docs/administration/mqtt-broker.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--mqtt-broker.md`
