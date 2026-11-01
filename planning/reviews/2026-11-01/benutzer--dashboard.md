# Seitenrevision: Persönliches Dashboard

## Änderungsbrief

- Seite: `docs/benutzer/dashboard.mdx`, Heimatbereich Benutzer.
- Leserfrage: Wie lese ich meine Übersicht und speichere eine eigene Widget-Anordnung?
- Vorwissen: angemeldete Person, die Buchungen, Freigaben und Einweisungen unterscheiden kann; keine Verwaltungskenntnisse nötig.
- Ergebnis: Anzeigen und ihre Grenzen verstehen, verfügbare Widgets auswählen und anordnen, Änderungen speichern oder bewusst verwerfen.
- Umfang: vorhandene Produktseite und dieser Bericht. Software und Website verwenden dieselbe MDX-Quelle.
- Plan: gültige Einleitung, Gliederung, Abgrenzungen und Abbildung behalten; Rechte, Listengrenzen, Bedienung und Speicherfehler anhand der Implementierung präzisieren. Keine neue Seite oder Komponente nötig.
- Prüfung: Quellcode und deutsche UI-Texte, gezielte Format- und Verweisprüfung. Gemeinsame Consumer-/Browserprüfung durch den Koordinator; keine neue Screenshot- oder Hardwareprüfung.

## Entscheidung

**Verbessert.** Die Seite war bereits knapp und fachlich überwiegend richtig. Die Überarbeitung entfernt die missverständliche Aussage, dass Vergrößern am Verschiebegriff erfolgt, und präzisiert bestehende Abläufe. Keine vollständige Neufassung.

## Befunde und Änderungen

- Profil-Leserechte für die Anzeige, Profil-Änderungsrechte für die Anpassung und Buchungs-Leserechte für Buchungswidgets ergänzt. Verwaltungsrechte sind dafür nicht erforderlich.
- Kommende Buchungen beginnen ab dem Ladezeitpunkt und umfassen nur bestätigte oder zur Freigabe ausstehende Buchungen; bereits laufende Buchungen sind keine kommenden Buchungen.
- Freigabenzahl umfasst direkte, aktuelle Gruppen- und Medienzuordnungen einschließlich zukünftiger und abgelaufener Freigaben. Die Liste ist auf fünf Einträge begrenzt.
- Qualifikationswidgets zeigen Einweisungen/Kompetenzvergaben, nicht alle lokalen oder importierten Nachweise. Verweis auf die vorhandene Qualifikationsseite ergänzt.
- Die drei Listen mit ihren exakten UI-Namen und dem Maximum von fünf Einträgen benannt. Die zusätzliche Ablaufanzeige bleibt bei aktuell wirksamen Vergaben mit Gültigkeitsende innerhalb von 30 Tagen.
- Anpassung an tatsächliche Bedienung angeglichen: **Widget hinzufügen**, **Widget konfigurieren**, Verschiebegriff, Größenänderung rechts unten, Pfeiltasten und Umschalt + Pfeiltasten, **Speichern**. Entfernen ändert nur die Ansicht.
- Getrennte Anordnungen für Bildschirmgrößen und mobile Standardansicht erläutert. Die bisherige pauschale Aussage, alle schmalen Ansichten seien immer einspaltig, trifft nach eigener Größenänderung nicht zwingend zu.
- **Verwerfen**, Bestätigung beim Verlassen, erhaltenen Entwurf bei Speicherfehlern und die ausdrücklich verwerfende Aktion zum Laden des gespeicherten Stands erklärt.
- Gute Inhalte erhalten: Dashboard/Start-Bezeichnung, 30-Tage-Grenze, Abgrenzung zur Hardware-Zugangsentscheidung, Detailansicht, Verweis auf Betriebsmetriken und vorhandene Abbildung mit fiktiven Daten.

## Quellen

Die genannten Symbole beziehen sich auf den zum Prüfzeitpunkt gelesenen Arbeitsstand.

| Aussage                                                                                                                   | Code-/UI-/Vertragsquelle                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Dashboard/Start und Navigation                                                                                            | `web/components/portal/portal-navigation.ts`, `portalNavigation`; `web/locales/de/navigation.json`, `nav.portal`                                                                                                                               |
| Rechte für Anzeige, Anpassung und Buchungswidgets; Hinzufügen, Speichern, Verwerfen, Aktualisieren und Konfliktbehandlung | `web/components/portal/member-dashboard.tsx`, `MemberDashboard` und `MemberDashboardWorkspace`; `api/Service/Observability/Boundary/HttpControllers/ProfileDashboardController.cs`, `GetAsync`, `UpdateAsync`, `GetCatalog`                    |
| Eigene Daten, Widgetkatalog und Standardanordnung                                                                         | `api/Service/Observability/Application/MemberPortalDashboard.cs`, `Widgets`, `GetCatalog`, `CreateDefault`; `api/Service/Observability/Application/PersonalDashboardService.UserMetrics.cs`, `GetMemberPortalAsync`, `UpdateMemberPortalAsync` |
| Grenzen der Anzeigen                                                                                                      | `web/components/portal/member-metric-view.ts`, `memberMetricView`: Filter auf Startzeit und Buchungsstatus, `totalCount`, `isEffective`, `slice(0, 5)`, 30-Tage-Filter                                                                         |
| Datenquellen und Aktualisierung                                                                                           | `web/components/portal/use-member-metrics.ts`, `useMemberMetrics`: eigene Buchungen, Profil-Freigaben mit Seitengröße fünf, Profil-Kompetenzvergaben                                                                                           |
| Eigene Gruppen-/Medienfreigaben und fehlende Hardwareentscheidung                                                         | `api/Service/Accesses/Boundary/HttpControllers/ProfileAccessGrantsController.cs`, `GetAsync`; `api/Service/Accesses/Application/Services/ProfileAccessGrantService.cs`, `ListOwnAsync`                                                         |
| Einweisungen gegenüber anderen Nachweisen                                                                                 | `api/Service/Competencies/Boundary/HttpControllers/ProfileCompetenciesController.cs`, `GetAsync`; `docs/benutzer/kompetenzen.mdx`                                                                                                              |
| Verschieben und Größe ändern                                                                                              | `web/app/[project]/dashboard/_components/editable-dashboard-grid.tsx`, `EditableDashboardGrid`; `web/app/[project]/dashboard/_components/dashboard-widget-card.tsx`, `handleLayoutKey` und Widgetaktionen                                      |
| Konfiguration und Details                                                                                                 | `web/app/[project]/dashboard/_components/dashboard-client.tsx`, `WidgetConfigurationDialog`; `web/app/[project]/dashboard/_components/dashboard-widget-card.tsx`, Detaildialog                                                                 |
| Getrennte Anordnungen                                                                                                     | `web/app/[project]/dashboard/_lib/dashboard-layout.ts`, `updateGridItem`, `replaceGridLayout`; `web/app/[project]/dashboard/_components/use-dashboard-breakpoint.ts`, `breakpointForWidth`                                                     |
| Entwurf und Verwerfbestätigung                                                                                            | `web/components/profile/profile-draft-provider.tsx`, `ProfileDraftBoundary`, `useProfileDraft`; `web/locales/de/devices.json`, `device.settings.discard`; `web/locales/de/navigation.json`, `nav.portal.metrics`                               |

## Prüfungen und offene Grenzen

- Statische Prüfung der genannten Frontend-, Backend- und Übersetzungsquellen durchgeführt.
- Vorhandenes `docs/benutzer/bilder/dashboard-desktop.png` visuell gelesen: Die gezeigten sechs Standardwidgets und Bedienelemente passen zum beibehaltenen Seitentext. Datierte Beispieldaten sind keine aktuelle Messung oder neue praktische Prüfung.
- Formatprüfung beider eigenen Dateien mit dem vorhandenen Prettier aus `web/node_modules/.bin/prettier` und ausdrücklich aufgehobener Consumer-Ignore-Regel für diese beiden Submodule-Dateien. Formatabweichungen wurden ausschließlich dort korrigiert; anschließender `--check` erfolgreich.
- `git -C web/content/docs diff --check -- docs/benutzer/dashboard.mdx planning/reviews/2026-11-01/benutzer--dashboard.md`: erfolgreich.
- Relative Seitenverweise und vorhandene Bilddatei anhand des Dateisystems geprüft; vier verschiedene Seitenziele und eine Bilddatei vorhanden. Alle drei bestehenden H2-Überschriften unverändert; keine eingehenden Abschnittsverweise auf diese Seite im Produktquellenbaum gefunden.
- Keine Browserprüfung, keine Consumer-Darstellungsprüfung, keine Hardware-/Providerprüfung durchgeführt. Keine praktische Abnahme behauptet.
- Koordinator: persönliche Dashboard-Seite in beiden Consumern rendern; Anpassen am Desktop und Handy sowie Tastaturbedienung und Speicherfehler-/Konfliktablauf praktisch prüfen. Vorhandenes Bild wurde nicht als aktuelle Browserabnahme gewertet.
- URL und drei vorhandene Abschnittsüberschriften bleiben erhalten. Keine Navigationsänderung und kein zusätzlicher Seitenbedarf.
- API-/DTO-Verträge unverändert; keine angepasste API-Referenz erforderlich.

## Geänderte Dateien

- `docs/benutzer/dashboard.mdx`
- `planning/reviews/2026-11-01/benutzer--dashboard.md`
