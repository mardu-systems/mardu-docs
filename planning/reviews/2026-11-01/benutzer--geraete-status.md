# Seitenrevision: benutzer/geraete-status

## Änderungsbrief

Mitglieder sollen bei verweigerter oder fehlerhafter Nutzung die Anzeigen im
Portal einordnen und der zuständigen Stelle verwertbare Angaben melden können.
Die Seite bleibt im Benutzerbereich und behält URL und beide Abschnittsanker.
Die vorhandene Trennung zwischen Freigabe, Buchung und physischem Zustand bleibt
erhalten. Ergänzt werden belegte Kataloganzeigen und vorhandene Aktionen;
eine allgemeine Offline-Anzeige wird nicht als Portal-Funktion dargestellt.
Quellen sind Portal-Komponenten, deutsche Übersetzungen sowie Katalog-DTO und
Ressourcenzustandsdienst. Geprüft werden Format, Verweise und MDX-Kompilation;
Browser, Website-Consumer und Hardware bleiben beim Koordinator bzw. der
Praxisprüfung.

## Entscheidung und fachlicher Befund

**Verbessert, zur Prüfung.** Leserfrage: „Warum kann ich eine Ressource trotz
Freigabe oder Buchung nicht nutzen, und was melde ich bei einer Störung?“

- Den tatsächlichen Einstieg **Zugänge & Ressourcen → Ressourcen entdecken**,
  mobile Bezeichnung, Katalog-Leserechte sowie **Details**, **Neu laden** und
  **Erneut versuchen** ergänzt.
- **Verfügbar** und **Nicht verfügbar** anhand der ausgewerteten Aktivzustände
  und Sperrzeiten erklärt. Der Katalog verwendet `AllowsOperation`, weder eine
  Live-Geräteprüfung noch eine Prüfung freier Buchungskapazität.
- Die bisherige Tabellenzeile „Gerät offline oder Meldung veraltet“ ließ eine
  solche Anzeige im Mitgliederportal vermuten. Ersetzt durch die belegten
  Kataloganzeigen und einen sichtbaren Hinweis auf deren technische Grenze.
- Hinweise zu benötigtem Zugang und Einweisungen ergänzt, Einzelheiten zu
  Freigaben und Buchungen bei den vorhandenen Nachbaranleitungen belassen.
- **Zugriff anfragen** als Freigabeantrag eingeordnet; die technische
  Störungsmeldung bleibt ein organisatorischer Kontaktweg des Standorts.
- Gute bestehende Inhalte erhalten: Portalstatus bestätigt keine physische
  Freischaltung, Konto-/Projektprüfung, Angaben für eine Meldung, Schutz von
  Zugangsdaten und persönlichen Kalenderlinks sowie Verweise auf Diagnose und
  Betriebsmetriken.
- Auf der zugewiesenen Seite waren keine Screenshots eingebunden. Kein Bild
  entfernt, kein Asset geändert, für diese Textanleitung kein Ersatzbild nötig.

## Quellen

Alle Pfade beziehen sich auf die Wurzel des Software-Repositories.

| Aussage                                                                                             | Geprüfte Quelle                                                                                                                                            |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Portalbereiche und getrennte Rechte                                                                 | `web/components/portal/portal-resources.tsx:50–62`; `web/components/access/resource-catalog-workspace.tsx:63–69`                                           |
| Einstieg und mobile Bezeichnung                                                                     | `web/components/portal/portal-navigation.ts:15–20`; `web/locales/de/navigation.json:117,138`; `web/locales/de/resources.json:477–478`                      |
| Status, Voraussetzungen und getrennte Nachweise                                                     | `web/components/access/access-catalog-presentation.tsx:48–105`; `web/locales/de/access.json:489–613`                                                       |
| Verfügbarkeit ist Betriebsfreigabe; Voraussetzungen sind keine persönlichen Qualifikationsnachweise | `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:80–131`; `api/Service/Accesses/Boundary/Dto/ResourceAccessCatalogDtos.cs:26–67` |
| Aktivstatus der Ressource und Vorfahren, wirksame Sperrzeiten, getrennte Buchungs-/Betriebswirkung  | `api/Service/ManagedResources/Application/Services/ResourceOperationServices.cs:257–298`                                                                   |
| Katalog-Recht und eigener Freigabeantrag                                                            | `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessCatalogController.cs:26–61`                                                                   |
| Details, Neu laden, Anfrage und Rücknahme                                                           | `web/components/access/resource-catalog-workspace.tsx:163–173,236–285,310–341,392–408`; `web/components/collection/collection-toolbar.tsx:6,87–91`         |
| Zeitstatus und eigene Freigaben                                                                     | `web/components/portal/profile-access-grants.tsx:126–145`; `web/locales/de/resources.json:489–503`                                                         |
| Exakte Reload-/Retry-Bezeichnungen                                                                  | `web/locales/de/common.json:43,52`                                                                                                                         |

Der vorhandene Backlog `planning/offene-dokumentationsaufgaben.md` enthält keinen
eigenen Auftrag für diese Seite. Seine Aufgaben zu Monitoring und technischer
Zugangsdiagnose bleiben bei den jeweiligen Anleitungen.

## Prüfungen und Grenzen

- Statischer Abgleich von UI, Übersetzungen, DTO, Berechtigungen und
  Ressourcenzustandsberechnung durchgeführt.
- Die beiden Überschriften **Anzeigen einordnen** und **Eine Störung eingrenzen**
  bleiben unverändert; bestehende Anker und URL bleiben erhalten.
- Lokale Linkziele auf vorhandene Dateien geprüft; kein neuer Navigationspunkt.
- MDX mit vorhandenem `@mdx-js/mdx` und `remark-gfm` kompiliert.
- Gezielter Formatcheck mit vorhandenem Prettier; das reguläre `bun fmt`
  überspringt das Submodule aufgrund von `web/.prettierignore` und ist deshalb
  für diese Dateien kein Formatnachweis.
- Keine Software-/API-Änderung; bestehende DTO/XML-Dokumentation nur als Quelle
  verwendet. Keine Änderung der API-Dokumentation erforderlich.
- Keine Browser-, Website-Consumer-, Hardware- oder Providerprüfung. Die
  Darstellung der geänderten Tabelle und die Portalansichten mit unterschiedlichen
  Rechten sowie Betriebs-/Sperrzuständen sind beim Koordinator noch praktisch zu
  prüfen. Die Seite ist damit nicht als abgenommen markiert.

## Koordination und geänderte Dateien

Kein zusätzlicher Seiten- oder Screenshotbedarf festgestellt. Die vorhandenen
Nachbarseiten bleiben die Quellen für Freigaben, Buchungen, Anträge,
Gerätediagnose und Betriebsmetriken. Standortzuständigkeit und Kontaktweg sind
Organisationsangaben, keine aus dem Code ableitbaren Produktfunktionen.

- `web/content/docs/docs/benutzer/geraete-status.mdx`
- `web/content/docs/planning/reviews/2026-11-01/benutzer--geraete-status.md`
