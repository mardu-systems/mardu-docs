# Zusatzseitenprüfung N01: Verfügbarkeit und Wartung koordinieren

## Änderungsbrief und Entscheidung

Leserfrage: Wie prüfe ich im laufenden Betrieb die Verfügbarkeit einer Ressource,
plane eine Unterbrechung und bearbeite fällige Wartungen? Vorausgesetzt sind eine
vorhandene Ressource und die Rechte für die konkrete Aktion. Das Ergebnis soll eine
nachvollziehbare Prüfung beziehungsweise gespeicherte Sperre oder abgeschlossene
Wartung sein; ein bestätigter Hardwarezustand ist davon getrennt.

**Entscheidung: begründete Nichtanlage; Bestandsquellen für diesen Umfang
unverändert gut.** Die geplante Datei
`docs/koordination/verfuegbarkeit-wartung.mdx` wird nicht angelegt. Die überarbeitete
Ressourcenanleitung beantwortet bereits die vollständige ressourcenbezogene
Tagesaufgabe einschließlich Einstieg, Rechten, Folgen, Ergebnisauswahl und
Historie. Globale Schließzeiten haben eine eigene ausgearbeitete Aufgabe in der
Buchungsverwaltung. Eine neue Seite würde diese Abläufe wiederholen oder nur als
zusätzliche Linkliste dienen. Der bestehende Koordinationsstart erschließt die
Ressourcenabschnitte bereits.

Kanonische Quellen bleiben:

- [Ressourcen einrichten](../../../docs/koordination/ressourcen.mdx), Heimatbereich
  **Administration**, bestehende URL unter Koordination erhalten.
- [Buchungen verwalten](../../../docs/koordination/buchungen-verwalten.mdx),
  Heimatbereich **Koordination**, Abschnitt „Globale Schließzeiten verwalten“.

## Bedarf und Bestandsabdeckung

| Tagesaufgabe                                   | Vorhandene Anleitung und überprüftes Verhalten                                                                                                                                                                        |
| ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ressource finden und aktuellen Stand einordnen | `ressourcen.mdx`: Einstieg mit Suche nach Name/Pfad und Typ-/Statusfilter; „Status und Verfügbarkeit“ erklärt Buchbarkeit und Nutzung, Prüfzeitpunkt, Aktualisierung und „Nicht prüfbar“.                             |
| Ausfall oder Unterbrechung planen              | „Ausfälle und Wartung: Betrieb unterbrechen“ beschreibt Grund/Zeitraum, getrennte Buchungs-/Betriebswirkung, Unterressourcen und Aufhebung. Ressourcen-Änderungsrechte sind genannt.                                  |
| Fällige Wartung bearbeiten                     | Derselbe Abschnitt erklärt, dass Fälligkeit noch keine Sperre ist. Start öffnet die Wartungssperre, Abschluss verlangt ein Ergebnis und schließt sie. Die Wartungssperre wird über den Wartungsvorgang abgeschlossen. |
| Wartungsgrundlage verstehen                    | Intervall-/Nutzungspläne, aktive Auswertung und Messwerte beziehungsweise abgeschlossene Sitzungen als Ersatzquelle stehen bereits dort. Keine neue Planungssystematik nötig.                                         |
| Ergebnis nachlesen                             | „Schalterübersicht und Historie nutzen“ beschreibt die Workspace-Historie für Wartungen/Ausfälle, Ressourcen-/Kennungsfilter und erhaltene Historie nach Löschung.                                                    |
| Alle Buchungsressourcen zeitweise schließen    | `buchungen-verwalten.mdx`, „Globale Schließzeiten verwalten“: Einstieg im Buchungskalender, Rechte, Einzel-/Serienanlage und -löschung, Konflikte mit vorhandenen Buchungen; keine automatische Stornierung.          |

Der aktuelle Ressourcen-Workspace bietet **Ressourcenübersicht**, **Schalter** und
**Historie**. Suche und Filter betreffen Ressourcen, Typ und Lebenszyklus. Im
geprüften Workspace gibt es keine zusätzliche ressourcenübergreifende
Fälligkeitsliste oder Tagesplan-Aktion, die einen neuen Ablauf begründen würde.
Offene Wartungen erscheinen beim jeweiligen Plan in den Ressourcendetails.

## UI- und Backendbelege

Pfade beziehen sich auf das Software-Repository; Symbole nennen die geprüften
Stellen.

- `web/app/[project]/dashboard/resources/resources-page-client.tsx`:
  `ResourcesPageClient`, `ResourcesWorkspace`, `workspaceTab`, `filtered`, `filters`
  und Workspace-Reiter; Leserechte für ManagedResources beziehungsweise
  BookingResources und Öffnen von `ResourceDetailsSheet`.
- `web/components/bookings/resource-details-sheet.tsx`: Detailbereich `operations`
  mit `ResourceOutagesPanel` und `ResourceMaintenancePanel`; nach Änderungen
  `effectiveState.reload`; Statusaktualisierung mit Prüfzeitpunkt. Die allgemeine
  Übersicht nutzt `ResourceConfigurationTrace`.
- `web/components/managed-resources/resource-configuration-trace.tsx` und
  `web/lib/managed-resources/resource-readiness.ts`: `getResourceReadiness`
  trennt Konfiguration/Sperren von konkreter Buchungs- oder Zugriffsentscheidung;
  fehlende Leserechte oder fehlgeschlagene Abfragen ergeben unbekannte Prüfung.
- `web/components/bookings/resource-outages-panel.tsx`: `canUpdate`, `add`,
  Zeitraum oder „Bis zur Aufhebung“, mindestens eine Wirkung, optional
  Unterressourcen; Aufhebung nur ohne `maintenanceOccurrenceId`, mit Bestätigung
  und Versionsprüfung. `resource-maintenance-panel.tsx`: planbezogene offene
  Vorgänge, `executeOccurrence`, Ergebniswahl vor Abschluss, Änderungsrechte.
- `web/locales/de/bookings.json`: `booking.structure` für „Ausfälle und Wartung“,
  „Buchungen sperren“, „Betrieb und Zugriff sperren“, „Wartung fällig“,
  „Wartung starten“, „Wartung abschließen“ und die Ergebniswerte.
- `api/Service/ManagedResources/Boundary/HttpControllers/ManagedResourcesController.cs`:
  `ListOutages`, `ListMaintenancePlans`, `ListMaintenanceOccurrences` und
  `EffectiveState` verlangen `ManagedResources.View`; Anlegen/Aufheben, Planpflege
  und `MaintenanceOccurrencesController.Start`/`Complete` verlangen
  `ManagedResources.Update`.
- `api/Service/ManagedResources/Application/Services/ResourceOperationServices.cs`:
  `ResourceOutageService.CreateAsync` validiert Zeitraum/Wirkung und speichert
  eine Sperre; `CancelAsync` schützt Wartungssperren und veraltete Versionen.
  `EffectiveResourceStateService.BuildState` wertet Status, Vorfahren und wirksame
  Sperren aus. `MaintenanceService.StartAsync` erstellt eine Sperre für Buchung
  und Betrieb; `CompleteAsync` verlangt einen gestarteten Vorgang, gültiges
  Ergebnis und Version und beendet nur dessen Sperre.
- `api/Service/ManagedResources/Application/Services/MaintenanceAutomationService.cs`:
  `ProcessDueMaintenanceAsync` erzeugt fällige Vorgänge, keine Sperren;
  `GetUsageCountAsync`/`GetOperatingHoursAsync` verwenden Messwerte vorrangig und
  abgeschlossene Sitzungen als Ersatz. Es ist kein physischer Abschaltauftrag.
- `web/components/managed-resources/resource-history-panel.tsx`: Reiter
  Wartungen/Ausfälle, Ressourcen-/Planfilter und historische Detailansicht.
- `web/components/bookings/admin/booking-closures-sheet.tsx`: `canView` und
  `canUpdate` für BookingAdministration; ohne Änderungsrecht schreibgeschützt.
  `api/Service/Bookings/Boundary/HttpControllers/BookingPoliciesController.cs`:
  `ListClosures`, `CreateClosure`, `DeleteClosure` und `DeleteClosureSeries`.
  `api/Service/Bookings/Application/Services/BookingCalendarClosureService.cs`:
  `CreateAsync` lehnt Überschneidungen mit aktiven Buchungen ab, statt sie zu
  stornieren; Einzel-/Serienlöschung sind getrennt.

## Querverweise für den Koordinator

Keine neue Navigation und keinen neuen Slug aufnehmen. Der Koordinationsstart
verlinkt Status und Verfügbarkeit sowie Ausfälle und Wartung bereits. Als kleine
Ergänzung dort genügt ein Verweis auf
`./buchungen-verwalten.mdx#globale-schließzeiten-verwalten`, sobald diese
Bestandsseite in die gemeinsame Veröffentlichung aufgenommen wird.

Die produktseitigen bestehenden Anker bleiben unverändert. Kein Link auf eine
noch nicht angelegte Zusatzseite erforderlich. Keine Änderung an den
Bestandsseiten im Rahmen dieses Auftrags vorgenommen.

## Checks und offene Praxisprüfung

- Quellenabgleich von Bestandsanleitungen, deutschem UI-Katalog, Komponenten,
  Controllerrechten und ausführenden Services durchgeführt.
- Formatprüfung des eigenen Berichts mit vorhandenem Prettier; relative
  Berichtlinks und die vier für Querverweise relevanten Überschriften geprüft.
- `git diff --check` für den eigenen Bericht ausgeführt. Keine neue MDX-Datei;
  deshalb kein zusätzlicher MDX-Kompilierungscheck erforderlich.

Nur statische Prüfung, keine praktische Abnahme: Die gemeinsame angemeldete
Consumerprüfung sollte Leserechte/Änderungsrechte getrennt, Statusaktualisierung,
Sperrwirkungen, Wartungsabschluss und Schließzeitkonflikt prüfen. Responsive
Darstellung und Website-Consumer bleiben beim Koordinator. Ob Hardware
ausgeschaltet ist und ob abgeschlossene Sitzungen die reale Nutzung abbilden,
muss mit der jeweiligen Installation geprüft werden. Keine echten Buchungs-,
Wartungs- oder Hardwareaktionen ausgeführt; keine Server, Builds oder Caches
verändert.

Geändert ausschließlich dieser Bericht:
`web/content/docs/planning/reviews/2026-11-01/koordination--verfuegbarkeit-wartung.md`.
Bestehende Produktanleitungen und ihre Patterns wiederverwendet; keine Software-,
API- oder DTO-Änderung und keine Anpassung der Vertragsdokumentation.
