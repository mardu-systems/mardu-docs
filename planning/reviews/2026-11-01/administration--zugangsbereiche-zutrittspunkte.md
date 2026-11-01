# N15: Ressourcenzugang mit Zutrittspunkten einrichten

## Entscheidung: begründete Nichtanlage

Die Leserfrage lautet: Wie richte ich für einen Raum oder eine Maschine die
Zugriffsregel und die zugehörigen Leser-/Aktoranschlüsse ein und prüfe den
gespeicherten Zustand? Die dafür nötige Ressourcenanlage und Geräteeinrichtung
werden vorausgesetzt beziehungsweise aus der vorhandenen Anleitung verlinkt.

Die inzwischen ausgearbeitete Bestandsanleitung **Ressourcen einrichten** beantwortet
diese Aufgabe bereits verständlich. Die zusätzliche Produktdatei
`docs/administration/zugangsbereiche-zutrittspunkte.mdx` wird daher nicht angelegt.
Eine zweite Anleitung würde denselben Ablauf und dieselben Voraussetzungen
duplizieren. Der kanonische Heimatbereich ist **Administration**; die bestehende
Datei und ihre URL unter `koordination/` bleiben erhalten.

Kanonische Ziele:

- [Nutzung und Zugriff: Nutzung erlauben](../../../docs/koordination/ressourcen.mdx#nutzung-und-zugriff-nutzung-erlauben)
- [Technik: Anschlüsse zuordnen](../../../docs/koordination/ressourcen.mdx#technik-anschlüsse-zuordnen)
- [Buchbarkeit: Reservierungen ermöglichen](../../../docs/koordination/ressourcen.mdx#buchbarkeit-reservierungen-ermöglichen)

## Abdeckung und Quellen

Die geprüfte Bestandsseite beschreibt Rechte vor Änderungen, die gemeinsame Regel
aller Zutrittspunkte, die erste gemeinsame Leser-/Aktorzuordnung, weitere Punkte
mit technischem Schlüssel und optionaler Ausgangsressource, explizite Punktauswahl,
Aktivierung sowie Ersetzen und Lösen. Raum und Maschine werden anhand von
Holzwerkstatt und Säge unterschieden. Sie trennt gespeicherte Konfiguration,
persönliche Zugriffsentscheidung und physische Einsatzbereitschaft.

| Aussage / Aufgabe                                                                                                | Geprüfte aktuelle Quelle                                                                                                                                                                                                                     |
| ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aktiver Einstieg über Ressourcenübersicht und Ressourcendetails                                                  | `web/app/[project]/dashboard/resources/resources-page-client.tsx:47–88`; `web/components/bookings/resource-details-sheet.tsx:301–354` rendert `ResourceAccessPanel` mit `view="rules"` beziehungsweise `view="points"`.                      |
| Vorhandene Anleitung deckt Rechte und Speicherkonflikte ab                                                       | `web/content/docs/docs/koordination/ressourcen.mdx:15–30`.                                                                                                                                                                                   |
| Scope ist die ressourcenbezogene Zugriffsregel; keine zusätzliche Ressourcen- oder Handlungsauswahl              | Bestandsseite `:83–97`; `web/components/access/resource-access-panel.tsx:244` und `web/components/access/resource-scope-editor.tsx` verwenden die Ressourcenkennung für die Regel.                                                           |
| Berechtigungsnachweis und tatsächlich angebotene Bedingungen                                                     | `web/components/access/resource-scope-editor.tsx:176–180,188–269,310–365`; `web/locales/de/resources.json:90–120`: vier Nachweisarten, Kompetenz mit Inaktivitätsgrenze, drei Aufsichtsoptionen und optionaler erforderlicher Schaltausgang. |
| Aktivierung prüft aktive Ressource und vollständige aktive Zutrittspunkte                                        | `api/Service/Accesses/Application/Services/ResourceAccessAdministrationService.cs:77–110,608–624`; `AccessPointTopologyPolicy.cs:7–16`.                                                                                                      |
| Erste Zuordnung erzeugt bei Bedarf einen Punkt und speichert Leser und Aktor gemeinsam; keine Änderung der Regel | `web/components/access/access-point-endpoint-bindings-panel.tsx:102–160`; `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessController.cs:53–65`; `ResourceAccessAdministrationService.cs:139–205`.                               |
| Weitere Punkte, Auswahl und Bearbeitung                                                                          | `web/components/access/resource-access-panel.tsx:108–238`; `web/components/access/access-point-editor.tsx:49–155`; UI-Texte in `web/locales/de/resources.json:145–156,273–284`.                                                              |
| Kompatible, freie Anschlüsse und fehlende Anschlussdaten                                                         | `web/components/access/access-point-endpoint-bindings-panel.tsx:80–100,129–130,262–350`; `api/Service/Accesses/Application/Services/AccessEndpointRolePolicy.cs:15–57`; `ResourceAccessAdministrationService.cs:150–189,748–764`.            |
| Getrennte globale und ressourcenbezogene Verwaltungsrechte                                                       | `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessController.cs:41–56,78–94`; `api/Service/Accesses/Boundary/Hypermedia/ResourceAccessHypermediaEnrichers.cs:58–112`; `ResourceAccessAdministrationService.cs:82–92,146–147`.     |
| Lösen und Deaktivierung unvollständiger Punkte; aktive Sitzungen, ausstehende Befehle und Versionskonflikte      | `ResourceAccessAdministrationService.cs:449–491`; Controller `:147–160`; Bestandsseite `:118–126`.                                                                                                                                           |

Die alte Seite `docs/administration/zutritt-verwalten.mdx` ist die Anleitung zum
Lesen der Zugangsmetriken und verweist für die Einrichtung bereits auf die
Ressourcenanleitung. Sie ist kein Beleg für einen eigenständigen alten
Verwaltungsdialog.

## Fachliche Grenzen

- **Keine Zutrittspunktgruppen-Anleitung:** Die aktuellen Ladehilfen in
  `web/lib/access/async-loaders.ts:294–341` geben für Gruppen und deren Mitglieder
  leere Seiten zurück. Die vorhandenen alten Gruppentypen und Komponenten belegen
  keinen verfügbaren Gruppierungsablauf.
- **Keine automatische Zugriffspolitik aus Hardware:** Die Hardwareoperation
  verändert weder Nachweisart noch Aktivierung der Ressourcenregel. Die
  Bestandsseite nennt dies ausdrücklich.
- **Zeiten gehören zum jeweiligen vorhandenen Ablauf:** Der Regel-Editor enthält
  keine allgemeine Wochenzeitenkonfiguration. Die Bestandsseite ordnet Zeitfenster
  den Vergaben und Buchungsverfügbarkeit der Buchbarkeit zu. Detailanweisungen zu
  Vergaben bleiben dem separaten Seitenauftrag vorbehalten.
- **Keine zusätzliche Zuständigkeitsanleitung:** Die Bestandsseite nennt die zum
  Einrichten benötigten Rechte und unterscheidet sie von Kompetenzbestätigung und
  Aufsicht. Die ausführliche Zuweisung von Verwaltungsrechten ist ein eigener
  Auftrag.

## Eigene Checks und offene Praxisprüfung

- Vorgaben, Arbeitsweise, offene Dokumentationsaufgaben und aktuelle Bestandsseiten
  gelesen; gegen aktive Komponenten, deutsche UI-Texte, Controller, Hypermedia-
  Rechte und Serviceprüfungen abgeglichen.
- Die drei relativen kanonischen Links und ihre Überschriften in der Bestandsdatei
  mit einem lokalen Python-Check geprüft; fehlende Neuanlage und nachgestellte
  Leerzeichen ebenfalls geprüft. `git diff --check` ohne Befund;
  `web/node_modules/.bin/prettier --check` für den Bericht erfolgreich.
  Nur diese Berichtsdatei angelegt; keine Produktdatei, Navigation,
  Übersetzungen oder Software verändert.
- Keine Tests, Builds, Serverstarts oder Hardwareaktionen ausgeführt. Keine
  Browser- oder Consumerabnahme behauptet.
- Offen für die koordinierte Praxisprüfung: Einrichtung eines Raums und einer
  Maschine im aktuellen Dashboard, fehlende beziehungsweise belegte Anschlüsse,
  zusätzlicher zunächst inaktiver Punkt, Versionskonflikt, Austausch und Lösen mit
  synthetischen Daten. Physische Leserreaktion, Aktorausführung,
  Konfigurationsbestätigung und Verhalten bei nicht erreichbarer Hardware müssen
  separat an der tatsächlich verwendeten Hardware geprüft werden.

## Querverweise für den Koordinator

N15 im Zusatzseitenplan auf die vorhandenen Ressourcenabschnitte abbilden, statt
eine neue Adresse in die Navigation aufzunehmen. Aus der späteren
Vergaben-Anleitung und der Verwaltungsrechte-Anleitung können kontextbezogene
Verweise dorthin führen. Bestehende Ressourcen-, Geräte- und Automationsverweise
bleiben nutzbar; keine Links auf noch nicht vorhandene Neuseiten ergänzt.

Geänderte Datei: ausschließlich dieser Bericht. API-/DTO-Dokumentation bleibt
unverändert, da keine API geändert wurde. Ergebnis: **begründete Nichtanlage;
kanonische Bestandsanleitung vorhanden, praktische Abnahme weiterhin getrennt**.
