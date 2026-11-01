# N07 · Nachweissysteme anbinden

## Änderungsbrief

- Leserfrage: Wie stellt die Administration einen Nachweisanbieter bereit, welcher Zugang passt und wie werden Import, Ausstellung und Anerkennung voneinander abgegrenzt?
- Vorwissen: Zugang zur Anbieterregistrierung und zur eigenen Mardu-Administration; keine Kenntnis der zwei getrennten Integrationswege vorausgesetzt.
- Ergebnis und Heimat: eigene Aufgabenanleitung in Administration. `integrationen.mdx` ist der Wegweiser; `profil-nachweisquellen.mdx` bleibt die persönliche Anmeldung, `badges-verwalten.mdx` die Definition und lokale Vergabe. Keine ausreichend vollständige bestehende Einrichtungsanleitung gefunden.
- Plan: UI-/Backend-Verträge vergleichen; belegte Konto-Anbieter-Einrichtung beschreiben; serverweite Einstellungen und deren tatsächliche Prüfgrenze dokumentieren; Quellen, Format, MDX und Verweise gezielt prüfen.
- Umfang: nur die zugewiesene neue MDX-Datei und dieser Bericht; Navigation/Browserprüfung durch Koordination. Keine Softwareänderung, kein Build, keine externe Aktion.

## Entscheidung

**Belegbare Teildokumentation / offene Prüfung.** Die Konto-Anbieter-Registrierung ist als eigenständiger UI-Ablauf belegt. Die serverweite Synchronisation besitzt Einstellungen und Aktionen, aber die aktuelle Kombination aus Frontend-Aktivierungsprüfung und Backend-Verbindungsprobe blockiert eine erstmalige Aktivierung. Dafür wird keine erfolgreiche Einrichtungsfolge behauptet.

## Befunde und Umsetzung

- Zwei Wege nach Leserziel getrennt: OAuth-Konto-Anbieter für persönliche OB3-Quellen und serverweite, providerspezifische Synchronisation mit technischen Zugangsdaten.
- Rechte für Integrationen (Anzeigen, Anlegen, Bearbeiten), separate Profilrechte und getrennte Mardu-Ausstellereinstellungen genannt. Die Dokumentationsrolle Administration ist keine Berechtigung.
- Konto-Anbieter: deaktivierten Eintrag speichern, exakte Rückleitungs-URL beim Anbieter registrieren, wieder öffnen und aktivieren; HTTPS-Endpunkte und tatsächliche Client-Authentifizierungen beschrieben. Kein erfundener Testknopf.
- Konto-Anbieter-Secret: leer behält den gespeicherten Wert; neuer Wert ersetzt ihn. Wechsel auf öffentlichen Client entfernt das Secret und muss zur Anbieterregistrierung passen. Änderungen verlangen erneute persönliche Anmeldung; Deaktivierung blockiert Anmeldung/Abruf, löscht keine importierten Nachweise.
- Synchronisation: belegte Authfelder, Geheimnisaktionen, Richtungen, Intervalle, Test des gespeicherten Standes, manueller Import und Ergebnisgrenzen beschrieben. Kein universeller OB3-Adapter, keine automatische Anerkennung, kein periodischer Export behauptet.
- Anerkennungsregeln erzeugen im serverweiten Import gegebenenfalls Pending-Vorschläge; der persönliche OB3-Import erzeugt Credentials mit unbekannter kryptografischer Prüfung und keinen solchen Kompetenzvorschlag. Zuständige bestehende Anleitung verlinkt.
- Keine API-/DTO-Änderung; vorhandene OpenAPI-/XML-Verträge als Belege verwendet.

## Quellen

Alle folgenden Pfade beziehen sich auf das Software-Repository.

| Aussage                                                                        | Quelle / relevante Stellen                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Vorhandene Abdeckung und Aufgabenabgrenzung                                    | `web/content/docs/docs/administration/integrationen.mdx`, Abschnitt „Open Badges und externe Anbieter“; `.../ueberblick/profil-nachweisquellen.mdx`; `.../administration/badges-verwalten.mdx`; `.../koordination/bewertungen.mdx`, „Externe Nachweise anerkennen“; `planning/offene-dokumentationsaufgaben.md:21`. |
| UI-Einstieg und Rechte                                                         | `web/components/layout/settings/integrations-nav.config.ts:86–145`; `web/components/integrations/openbadges/openbadges-navigation.tsx:21–58`; `web/locales/de/settings.json:658–667`.                                                                                                                               |
| Konto-Anbieter-Felder, Speichern und Callback                                  | `web/components/competencies/badge-providers.tsx:32–38,176–307`; `web/components/competencies/shared.tsx:156–237`; `web/locales/de/badges.json:346–389`.                                                                                                                                                            |
| Konto-Anbieter-Validierung, Geheimnis und Konfigurationsversion                | `api/Service/Interoperability/Boundary/BadgeProviderDtos.cs:6–24`; `.../Boundary/BadgeProvidersController.cs:12–34`; `.../Application/BadgeProviderAdministration.cs:23–72`.                                                                                                                                        |
| PKCE, Rechteumfang, erneute Anmeldung nach Konfigurationswechsel               | `api/Service/Interoperability/Application/BadgeOAuthConnectionService.cs:38–115`; `.../BadgeOAuthTransport.cs:29–47,85–126`; `.../BadgeProviderSynchronization.cs:22–34`; `.../Boundary/ProfileBadgeProvidersController.cs`.                                                                                        |
| Import und Anerkennungsgrenze der Konto-Anbieter                               | `api/Service/Interoperability/Application/BadgeProviderSynchronization.cs:35–68`; `.../BadgeEvidenceExchange.cs:17–61` (Identität, gespeicherte Credentials, `VerificationUnknown`; keine Kompetenzvergabe).                                                                                                        |
| Serverweite UI, Geheimnisaktionen und Richtungen                               | `web/app/[project]/dashboard/admin/integrations/openbadges/external/page.tsx:235–750`; `.../openbadges-settings.presentation.ts:37–73`; `.../openbadges-settings.utils.ts:75–113,198–294`; `web/locales/de/badges.json:2–228`.                                                                                      |
| Speichern, Validieren, Sync-Voraussetzungen                                    | `web/app/[project]/dashboard/admin/integrations/openbadges/use-openbadges-settings-controller.ts:190–300,364–367`; `api/Service/OpenBadges/Boundary/OpenBadgesIntegrationController.cs`; `.../Boundary/OpenBadgesSyncController.cs`.                                                                                |
| Backend-Speichern und Prüfprobe                                                | `api/Service/OpenBadges/Application/OpenBadgesIntegrationService.cs:34–98,278–297`; `api/Framework/Infrastructure/Configuration/Setup/SetupIntegrationProbes.cs:266–359`.                                                                                                                                           |
| Geheimnis-Löschgrenze                                                          | `api/Service/OpenBadges/Boundary/Dto/OpenBadgesIntegrationDtos.cs:209–245` (OAuth: leere Client-ID/Secret bei Update immer ungültig); `.../Application/OpenBadgesIntegrationService.cs:52–71`; Frontend-Payload in `openbadges-settings.utils.ts:80–113`.                                                           |
| Persönlicher Token, Identitätsprüfung, Ergebniszählung und externe Ausstellung | `api/Service/OpenBadges/Application/OpenBadgesSyncService.cs:35–180`; `.../OpenBadgesGateway.cs:52–145,207–215`; `.../OpenBadgesCompetencyProjectionService.cs:22–104`.                                                                                                                                             |
| Intervall und notwendiger Neustart                                             | `api/Service/OpenBadges/Boundary/OpenBadgesIntegrationController.cs:39–40`; `api/Server/Program.cs:297–320` (Registrierung bei Start, Begrenzung auf 59 Minuten); `web/locales/de/badges.json:164–169`.                                                                                                             |

## Belegte Produktwidersprüche zur getrennten Nachverfolgung

1. **Aktivierung der Synchronisation über Dashboard blockiert:** Der Controller erlaubt Validieren nur bei unverändert gespeichertem Stand und verlangt für eine Aktivierung eine erfolgreiche Validierung der Verbindungsdaten. `ToRuntimeSettings` übernimmt das gespeicherte `Enabled`; `OpenBadgesSetupProbe.ProbeAsync` lehnt jedoch `!request.Enabled` vor jedem Verbindungsversuch ab. Der UI-Hinweis „deaktiviert speichern, validieren, aktivieren“ ist damit nicht ausführbar. Keine Umgehung über API/Secrets als Produktanleitung empfohlen. Aktive bestehende Anbindungen lassen sich hingegen mit unveränderten Verbindungsdaten validieren; das manuelle Synchronisieren bleibt für sie dokumentierbar.
2. **OAuth-Zugangsdaten löschen:** Die UI bietet Client-ID/Secret löschen an; das DTO lehnt die dadurch übertragenen leeren Werte bei `UpdateClientId`/`UpdateClientSecret` im OAuth-Modus unabhängig vom Aktivstatus ab. Produkttext beschreibt diese Grenze statt erfolgreiches Löschen zu versprechen. Der Direct-Token-Service-Token besitzt diesen DTO-Block nicht. Ein Deployment kann zusätzlich Laufzeitwerte als Fallback liefern; daher keine Behauptung einer vollständigen Geheimnisbereinigung durch die UI.
3. **Richtungen bei deaktiviertem Speichern:** Backend schreibt alle drei Richtungen als `request.Enabled && ...`; das Abschalten setzt sie zurück. Bei einer späteren Wiederaktivierung müssen sie erneut gewählt werden. Im Text vor dem Abschalten genannt.
4. **Intervall:** UI/DTO lassen 1–1440 zu; Scheduler begrenzt bei Start auf 1–59. Neustart ist auch für die erstmalige automatische Jobregistrierung relevant. Im Text keine tägliche Synchronisierung über einen 1440-Minuten-Wert versprochen.

## Prüfungen und Grenzen

- Statische Prüfung der genannten UI-, Übersetzungs-, DTO-, Berechtigungs- und Servicequellen durchgeführt.
- Vorhandenes Prettier ausschließlich für die beiden eigenen Dateien ausgeführt; anschließend gezielter Check bestanden.
- MDX ohne Frontmatter mit dem vorhandenen `@mdx-js/mdx` kompiliert: bestanden. Alle vier relativen Seitenverweise einschließlich der beiden Fragmentziele mit vorhandenem `github-slugger` aufgelöst: bestanden. Kein TODO-/Checkbox-Schreibauftrag im Produkttext.
- `git -C web/content/docs diff --check` auf die beiden eigenen Pfade: bestanden. Da beide Dateien neu und ungetrackt sind, wurden ihre Inhalte zusätzlich unmittelbar durch Format-/MDX-/Linkprüfung erfasst.
- Keine Browser-/Consumer-, Hardware- oder reale Anbieterprüfung, kein Serverstart/Build. Erforderlich bleiben: Konto-Anbieter-Testregistrierung mit korrekter öffentlicher Backendadresse und Callback, je unterstützter Authmethode; Zustimmung/erneute Anmeldung nach Änderung, deaktivierter Anbieter und partieller Import; aktive Synchronisation mit persönlichem Testkonto, ausgelassenen Konten und Anerkennungsvorschlag; Scheduler nach Neustart.
- Aktivierungsblock und OAuth-Löschblock benötigen getrennte Softwarekorrektur samt Tests. Die Seite gilt nicht als abgenommen.

## Querverweise für die Koordination

- Neue Seite unter „Kompetenzen und Nachweise“ in Administration aufnehmen und aus `integrationen.mdx#open-badges-und-externe-anbieter` verlinken.
- Profilquelle, Bewertungen und Badges bleiben ihre kanonischen Ziele; Rückverweise auf diese administrative Einrichtung können dort ergänzt werden.
- Eigenständiger Bedarf für Betrieb des nativen Mardu-Ausstellers bleibt außerhalb dieses Auftrags; kein Link auf eine noch nicht vorhandene Seite.

## Geänderte Dateien

- `web/content/docs/docs/administration/nachweissysteme-anbinden.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--nachweissysteme-anbinden.md`
