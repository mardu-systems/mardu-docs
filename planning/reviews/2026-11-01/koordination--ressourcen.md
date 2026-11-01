# Seitenrevision P25: Ressourcen einrichten

## Änderungsbrief

Leserfrage: Wie richte ich Räume und Maschinen mit Hierarchie, Buchbarkeit,
Zugriffsbedingungen, Technik und Wartung ein und prüfe das Ergebnis? Leser kennen
das Dashboard und besitzen die für ihre Aufgabe nötigen Verwaltungsrechte; sie
müssen Ressourcen, Geräte und Zugriffsfreigaben unterscheiden können. Kanonischer
Heimatbereich ist Administration; bestehende URL unter Koordination bleibt erhalten.
Die ausführliche Anleitung, gültige Schritte und Warnungen bleiben erhalten.
Statischer UI-/Backend-Abgleich korrigiert Bereichszahl, UI-Begriffe und
Löschfolgen, macht die bisher eingeklappten Folgen sichtbar und ergänzt belegte
Messwert-, Schalter- und Historienansichten. Vorhandene MDX-/Bildkomponenten bleiben
im Einsatz; keine Software-/API-/DTO-Änderung. Eigene gezielte Format-, MDX- und
Verweisprüfungen; Consumer-/Browserprüfung beim Koordinator. Keine Hardwareaktion.

## Ergebnis: verbessert

- Bestehende ausführliche Schritte zu Hierarchie, Stammdaten, Foto, Aktivierung,
  Zugriffsregeln, Hardware, Buchbarkeit, Sperren und Wartung bleiben erhalten.
  Hardwarezustand, tatsächliche Abschaltung und Zugriff werden weiterhin ausdrücklich
  von gespeicherter Konfiguration und Betriebsfreigabe unterschieden.
- Sechs Detailbereiche statt fünf, aktuelle Bezeichnungen für Zugriffsvergabe,
  weitere Zugriffsbedingungen, Neuanlage und Stilllegung. Allgemein erklärt die
  vorhandene Übersicht zu Buchbarkeit/Nutzung einschließlich „Nicht prüfbar“.
- Globale Rechte und ressourcenbezogene Regel-, Vergabe- und Hardwareverwaltung
  getrennt. Verantwortliche benötigen zum Ändern zusätzlich ManageAccess.
  Verwaltungsrechte gelten nicht automatisch für Unterressourcen und erteilen
  keinen persönlichen Zugang.
- Scope als Zugriffsbedingungen einer Ressource erklärt; Zutrittspunkt,
  Geräte-/Automationsanschluss und optionale Ausgangsressource davon abgegrenzt.
  Zusätzlicher Zugangspunkt und fehlende automatische Reaktivierung nach neuer
  Hardwarezuordnung erläutert. Direkter Schalter ersetzt keinen Freigabeaktor.
- Stilllegung/Löschung aus dem Akkordeon in sichtbaren Unterabschnitt übernommen.
  Löschvorschau und Erhaltung abgeschlossener Historie ersetzen die veraltete
  Aussage, sämtliche Buchungs-/Wartungs-/Zugriffshistorie sperre eine Löschung.
  Offene Vorgänge und aktive/fremde Abhängigkeiten bleiben genannt.
- Buchungszugriffsziele ausdrücklich auch für die gebuchte Ressource selbst;
  Hierarchie erzeugt keine automatische Zugriffszuordnung. Messwertansicht,
  eigener Zeitbezug, fehlende Daten, Zählersemantik und Leserechte ergänzt.
- Wartungsergebnis vor Abschluss ergänzt; Messwerte oder ersatzweise abgeschlossene
  Sitzungen als Datenbasis der nutzungsabhängigen Wartung erklärt.
- Workspace-Reiter Schalter/Historie ergänzt, keine erfundenen Zeitraumfilter in
  der Historien-UI (nur Ressourcen-/Planfilter; Backendzeitfilter sind kein UI-Beleg).

## Bilder

Alle vier vorhandenen PNGs mit view_image selbst angesehen; keine neuen
Screenshots erstellt. Einbindung `ressource-zugriff.png` entfernt: Sie zeigt
„Dauerhafte Vergabe“, während die aktuelle Auswahl „Zugriffsvergabe“ lautet,
und die ältere Anordnung der Regelaktivierung. Das Asset bleibt unverändert.
`ressource-allgemein.png`, `ressource-technik.png` und `ressource-wartung.png`
bleiben erhalten: Die abgebildeten Stammdatenfelder, Anschlussrollen und
Wartungsaktionen bestehen weiterhin. Der Text kennzeichnet das frühere Layout;
die älteren Kopf-Badges sind keine Bestätigung der aktuellen Betriebsbereitschaft.

## Quellen

Pfade relativ zum Software-Repository, relevante Symbole/Abschnitte:

- `web/components/bookings/resource-details-sheet.tsx`: `tabs`, `ResourceConfigurationTrace`,
  getrennte dirty/busy-Zustände, zusätzlicher Tab `metrics`.
  `web/app/[project]/dashboard/resources/resources-page-client.tsx`: Hierarchie,
  Suche/Filter, Workspace-Reiter, `onResourceDeleted`/Historienbezug.
- `web/components/managed-resources/resource-identity-settings.tsx`:
  `ResourceIdentitySection`, `ResourceDangerZone`, `ResourceUsageSection`;
  `resource-configuration-trace.tsx` und `web/lib/managed-resources/resource-readiness.ts`:
  Buchbarkeit und Nutzung, Voraussetzungen, Nicht-prüfbar-Zustände.
  `web/hooks/use-resource-identity.ts`: Speichern, Konflikte und Löschvorschau.
- `api/Service/ManagedResources/Boundary/Dto/ManagedResourceDtos.cs` und
  `Application/Services/ManagedResourceService.cs`: `CreateAsync`, `UpdateAsync`,
  `ValidateParentAsync`, `EnsureAncestorsAreActiveAsync`, `EnsureSiblingNameIsUniqueAsync`,
  `ChangeLifecycleCoreAsync`, `DeactivateResourceConfigurationAsync`,
  `EnsureControlsCanBeDeactivatedAsync`: Grenzen, Hierarchie, Status und Stilllegung.
- `api/Service/ManagedResources/Application/Services/ManagedResourceDeletionImpactProvider.cs`:
  `GetReportAsync` unterscheidet gelöschte eigene Konfiguration, erhaltene abgeschlossene
  Historie sowie offene/fremde Abhängigkeiten. Ergänzend
  `api/Service/Accesses/Infrastructure/DeletionImpact/AccessDeletionImpactContributor.cs`:
  `GetImpactsAsync`, offene Sitzungen/Anträge/Bestätigungen und erhaltene Zugriffsprotokolle.
  `ResourceHistoryDeletionCleanup.cs`: ursprüngliche Ressourcenbezüge bei Löschung.
- `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessController.cs`:
  globale RequiredPermission-Attribute. `Application/Services/ResourceAccessAdministrationService.cs`:
  `GetPolicyAsync`, `UpdatePolicyCoreAsync`, `AssignHardwareAsync`,
  `CreateAccessPointAsync`, `UpdateAccessPointAsync`, Vergabemethoden und
  ressourcenbezogene Prüfungen (ViewTopology, ManagePolicy, ManageAccess, ManageHardware).
  `ResourceAccessAuthorizationService.cs`: `FindMatches`, `GetAcceptedActions`;
  keine automatische Hierarchievererbung.
- `web/components/access/resource-scope-editor.tsx`, `access-point-editor.tsx`,
  `access-point-endpoint-bindings-panel.tsx`: Regelbedingungen, Ausgangsressource,
  technischer Schlüssel, gemeinsame Hardwarezuordnung und Aktivierung.
  `web/locales/de/resources.json`: aktuelle UI-Werte einschließlich
  `authorizationModes`, `policyAdvanced`, `createAdditionalPoint`, `pointEnabled`.
- `web/components/bookings/booking-resource-settings.tsx`: `toBookingResourceRequest`,
  `BookingAccessTargets`, Zeitzone, Rechte und gespeicherte Werte;
  `booking-access-targets.tsx`: aktive Regeln, Buchungsnachweis, explizite Zielauswahl.
  `api/Service/Bookings/Boundary/HttpControllers/ManagedBookingResourcesController.cs`:
  BookingResources.View/Create/Update;
  `Application/Services/ManagedBookingResourceService.cs`: `Apply`, gespeicherte AccessTargets.
- `api/Service/ManagedResources/Application/Services/ResourceOperationServices.cs`:
  `StartAsync`/`CompleteAsync` öffnen/schließen die Wartungssperre;
  `MaintenanceAutomationService.cs`: `ProcessDueMaintenanceAsync`, `GetUsageCountAsync`,
  `GetOperatingHoursAsync` (Messwertvorrang, Ersatz durch abgeschlossene Sitzungen).
  `Boundary/Dto/ResourceOperationDtos.cs`: Trigger-/Einheitenvalidierung.
  `web/components/bookings/resource-maintenance-panel.tsx`: Ergebnisauswahl;
  `resource-outages-panel.tsx`: Sperrwirkungen und Aufhebung.
- `web/components/managed-resources/resource-metrics-tab.tsx`,
  `web/lib/managed-resources/resource-metric-view.ts`:
  Dashboard-/Quellenrechte, Zeitraum/Auflösung, getrennte aktuelle Übersicht,
  Lücken und Antwortgrenzen. `api/Service/ManagedResources/Boundary/HttpControllers/ResourceMetricsController.cs`:
  dokumentierte Historiensemantik; `ResourceOverviewController.cs`: zusätzliche
  Rechte für Sitzungen/Buchungen und keine Aggregation von Unterressourcen.
- `web/components/managed-resources/resource-switch-panel.tsx`,
  `resource-switches-workspace.tsx`: einzelne/Sammelschaltaufträge und Bedienbarkeit.
  `api/Service/ManagedResources/Boundary/HttpControllers/ResourceSwitchController.cs`
  und `Application/Services/ResourceSwitchService.cs`: globale Update-Rechte,
  ManageHardware/OperateHardware; `ResourceSwitchSafetyPolicy.cs`: bestätigtes Aus
  und Aktualität. `ResourceHistoryPanel` in `resource-history-panel.tsx`:
  Wartungs-/Ausfallhistorie, Kennungsfilter und historische Details.
- Nachbarseiten `web/content/docs/docs/administration/automationen.mdx`,
  `geraete-verwalten.mdx`, `zutritt-verwalten.mdx`; interner Kontext
  `web/docs/managed-resources-frontend.md`, `resource-access-frontend.md`.

## Prüfungen und Grenzen

Ausgeführte Checks:

- Prettier für genau die beiden eigenen Dateien mit `--ignore-path /dev/null`
  ausgeführt und abschließend mit `--check` geprüft (Submodule ist sonst ignoriert).
- Eigene MDX-Seite mit dem vorhandenen `@mdx-js/mdx` kompiliert.
- Frontmatter, fehlendes zusätzliches H1, alle bisherigen Überschriften gegen HEAD,
  relative Seitenlinks samt Zielankern sowie drei verbliebene Bildimporte geprüft.
- `git -C web/content/docs diff --check -- docs/koordination/ressourcen.mdx planning/reviews/2026-11-01/koordination--ressourcen.md`.

Keine eigene Browser-,
Hardware-, Node-RED-, Provider- oder Schreibprüfung durchgeführt. Keine Server
oder Builds gestartet. Code-/Vertragsabgleich ist keine praktische Abnahme;
Consumerdarstellung, responsive Ansicht und gemeinsame Navigation prüft der
Koordinator. Für die drei erhaltenen Bilder sollte bei Gelegenheit derselbe
fiktive Datensatz im aktuellen Layout neu aufgenommen werden; sie werden hier
nicht als aktuelle praktische Prüfung ausgegeben.

Alle bisherigen Überschriften/URLs bleiben erhalten, ergänzte Unterabschnitte
fügen neue Anker hinzu. Relative Seitenlinks und vorhandene Bildkomponente
werden wiederverwendet. Kanonischer Heimatbereich Administration trotz alter
Koordinations-URL; Navigation/Bereichsfilter gehören zum Koordinator.

Zusatzseitenbedarf: Eine eigene Anleitung für die Vergabe und Diagnose von
Verwaltungszuständigkeiten, Zugangsanträge und Sitzungseingriffe fehlt weiterhin
(siehe vorhandenen Backlog Zutrittsverwaltung und Hinweis auf der Nachbarseite).
Diese Fragen werden auf dieser Einrichtungsseite nicht als vollständig abgedeckt
behauptet. Kein zwingender neuer Seitenschnitt nur für diesen Patch.

Geänderte Dateien:

- `web/content/docs/docs/koordination/ressourcen.mdx`
- `web/content/docs/planning/reviews/2026-11-01/koordination--ressourcen.md`
