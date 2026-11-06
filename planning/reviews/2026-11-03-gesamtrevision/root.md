# Koordinator: Einstiege und zuletzt überarbeitete Anleitungen

Die 16 Seiten werden einzeln geprüft. Gute neue Ressourcen-, Buchungs- und
Freigabenanleitungen bleiben erhalten. Bilder/Diagramme stammen aus den bereits
protokollierten Arbeiten dieses Tages; sie sind keine neu behauptete Hardwareabnahme.
Die aktuelle Revision ändert an diesen Anleitungen nur Verweise aus Nachbarseiten.

## Einzelentscheidungen

| Seite                                             | Entscheidung und Begründung                                                                                                                 |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `administration/freigaben-verwalten.mdx`          | Bewusst erhalten: Vorheriger gezielter Auftrag samt fünf erfolgreicher Bearbeitungsfälle und PostgreSQL-Regressionsprüfung bleibt erhalten. |
| `administration/index.mdx`                        | Verbessert: Einrichtung und Betrieb mit direkten Links zu den neuen Aufgabenanleitungen getrennt.                                           |
| `administration/ressourcen-aendern-entfernen.mdx` | Bewusst erhalten: Die frisch getrennte Anleitung enthält Rechte, konkrete Schritte, Prüfergebnis, Fehlerhilfe und passende aktuelle Grafik. |
| `administration/ressourcen-buchbarkeit.mdx`       | Bewusst erhalten: Die frisch getrennte Anleitung enthält Rechte, konkrete Schritte, Prüfergebnis, Fehlerhilfe und passende aktuelle Grafik. |
| `administration/ressourcen-wartung.mdx`           | Bewusst erhalten: Die frisch getrennte Anleitung enthält Rechte, konkrete Schritte, Prüfergebnis, Fehlerhilfe und passende aktuelle Grafik. |
| `administration/ressourcen-zustand.mdx`           | Bewusst erhalten: Die frisch getrennte Anleitung enthält Rechte, konkrete Schritte, Prüfergebnis, Fehlerhilfe und passende aktuelle Grafik. |
| `administration/ressourcen-zutritt.mdx`           | Bewusst erhalten: Die frisch getrennte Anleitung enthält Rechte, konkrete Schritte, Prüfergebnis, Fehlerhilfe und passende aktuelle Grafik. |
| `index.mdx`                                       | Bewusst erhalten: Die sechs aufgabenbezogenen Einstiege und Rechteabgrenzung sind bereits knapp.                                            |
| `koordination/buchungen-verwalten.mdx`            | Bewusst erhalten: Aktuelle UI-Schritte, drei Bilder, Anfragenentscheidung und Schließzeitfolgen sind bereits präzise.                       |
| `koordination/index.mdx`                          | Verbessert: Links für Zustand, Wartung und Buchbarkeit direkt auf die kanonischen Anleitungen statt alte Sammelseitenanker gesetzt.         |
| `koordination/ressourcen.mdx`                     | Bewusst erhalten: Die frisch getrennte Anleitung enthält Rechte, konkrete Schritte, Prüfergebnis, Fehlerhilfe und passende aktuelle Grafik. |
| `ueberblick/grundlagen-begriffe.mdx`              | Verbessert: Anschlussbeispiel direkt mit der passenden technischen Anleitung verbunden.                                                     |
| `ueberblick/index.mdx`                            | Bewusst erhalten: Systemmodell, optionale Technik und zwei verständliche Diagramme passen zu den aktuellen Domänen.                         |
| `ueberblick/neuerungen.mdx`                       | Verbessert: Messwerteverweis direkt auf die aktuelle Anleitung gesetzt; Releaseaussagen beibehalten.                                        |
| `v1/index.mdx`                                    | Bewusst erhalten: Historischer Einstieg bleibt erreichbar und verweist ohne Versionsversprechen auf aktuelle Doku.                          |
| `v2/index.mdx`                                    | Bewusst erhalten: Historischer Einstieg bleibt erreichbar und verweist ohne Versionsversprechen auf aktuelle Doku.                          |

## Quellen und Abgleich

- Bereichsbesitz und virtuelle Ordner: `web/lib/docs-roles.tsx`,
  `docs/meta.json`, `docs/administration/ressourcen-anleitungen/meta.json`.
  Die Ressourcenhauptseite gehört trotz historischer Koordinations-URL zur Administration.
- Ressourcen: `web/components/bookings/resource-details-sheet.tsx`,
  `web/components/managed-resources/resource-identity-{fields,settings}.tsx`,
  `resource-effective-state.tsx`, `resource-switch-panel.tsx`,
  `resource-metrics-tab.tsx`, `resource-history-panel.tsx`;
  `web/components/bookings/{booking-resource-settings,resource-outages-panel,resource-maintenance-panel}.tsx`.
- Backend: `api/Service/ManagedResources/Application/Services/ManagedResourceService.cs`,
  zugehörige HTTP-Controller für Lebenszyklus, Zustand, Messwerte, Zuordnungen
  und Schalter; `api/Service/Accesses/Application/Services/ResourceAccessAdministrationService.cs`
  und `api/Service/Bookings/Boundary/HttpControllers/`.
- Buchungsentscheidungen: `web/app/[project]/dashboard/bookings/requests/booking-admin-center.tsx`.
- Veröffentlichtes v0.6.0 am 31.10.2026 über GitHub-Connector direkt gegen beide
  offiziellen Releasequellen gelesen:
  [Server](https://github.com/mardu-systems/mardu-rpi-api/releases/tag/v0.6.0),
  [Dashboard](https://github.com/mardu-systems/web/releases/tag/v0.6.0).
  Verfügbarkeit, Messwertlayouts, Migrationen und Updatehinweise stimmen überein.

## Praktische Prüfung und Grenzen

In der frischen isolierten Werkstatt-Testinstanz wurde `Doku-Prüfraum` über
`Ressource anlegen` mit Typ Raum als Entwurf angelegt (HTTP 201). Die sechs
Detailreiter Allgemein, Nutzung & Zugriff, Technik, Buchbarkeit, Ausfälle und
Wartung sowie Messwerte entsprechen weiterhin den Ressourcenanleitungen.
Die Aktivierung wurde im Bestätigungsdialog ausgeführt (HTTP 200, Version 1, Status Aktiv). Alle sechs Detailreiter wurden danach lesend geöffnet, mit passenden Bereichsüberschriften und ohne API-Fehler. Kein Schalter oder Hardwareanschluss wurde eingerichtet.

Kein physischer Schaltauftrag und kein Gerätetest. Die früheren Tagesprotokolle
für Ressourcen, Buchungen und Freigaben behalten ihren eigenen tatsächlichen
Prüfumfang. Der .NET-Gesamttest-Hänger aus dem vorherigen Auftrag wird hier weder
behoben noch als bestandener Test umgedeutet. Die neue Revision ändert keine
Software, APIs oder DTOs.

Gemeinsame Format-, Render-, Link-/Anker-, Bild-, Such- und Markdownprüfungen
stehen im Gesamtbericht; vor deren Abschluss keine vollständige Consumerabnahme.
