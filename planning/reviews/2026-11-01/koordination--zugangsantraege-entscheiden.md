# N02 – Zugangsanträge entscheiden

- Seite: `docs/koordination/zugangsantraege-entscheiden.mdx`
- Leserfrage: Wie prüfe und entscheide ich als zuständige Person einen Ressourcen-Zugangsantrag, und welche Freigabe beziehungsweise Rückmeldung entsteht?
- Entscheidung: **Belegbare Teildokumentation / offene Prüfung**, neue eigenständige Aufgabenanleitung zur Prüfung angelegt. Kanonische Heimat: **Koordination**. Keine praktische Abnahme behauptet.
- Bedarf: `benutzer/berechtigungsanfragen.mdx` erklärt Stellen, eigenen Status und Rücknahme. `koordination/ressourcen.mdx` erklärt Ressourcenregeln und Zuständigkeiten, aber keinen vollständigen Entscheidungsablauf. `administration/zutritt-verwalten.mdx` ist eine Metrikanleitung mit Verweisen; sie ist keine Anleitung für offene Anträge. Die neue Seite ergänzt einen anderen Arbeitsauftrag und wiederholt nicht den persönlichen Antragsablauf.

## Inhalt und Grenzen

Angelegt sind Einstieg und offene Liste, getrennte globale Rechte/Objektzuständigkeit, Empfängerprüfung, vorgelagerte Prüfung der Ressourcenbedingungen und Nachweise, Genehmigung mit Zeitraum und optionaler Notiz, Ablehnung mit Pflichtbegründung, Ergebnis und Konflikthilfe. Die Antragskarte besitzt keinen eigenen Detail-/Nachweisdialog. Die Seite erfindet weder Uploads noch automatische Kompetenzprüfung, Rollenpflicht, Benachrichtigungsversand oder Freigabe von Hardware. Die Verantwortung **Kompetenz bestätigen** erlaubt laut Service auch das Entscheiden dieses Antrags; sie ist keine allgemeine Administratorrolle.

Die Genehmigung erstellt eine direkte Personenfreigabe für die beantragte Ressource, ohne Wochenzeitfenster; sie erteilt keinen Kompetenznachweis. Beginn und Ende werden im aktuellen Dashboard vorgegeben (aktuell bis 30 Tage später) und können geändert werden. Der API-Vertrag erlaubt zwar ein offenes Ende, das aktuelle Entscheidungsformular führt aber beide Zeitwerte und erlaubt keinen belegten Ablauf für eine unbefristete Genehmigung. Deshalb dokumentiert die Seite nur die befristete UI-Aufgabe. Eine Ablehnung verändert keine vorhandene Freigabe. Abgeschlossene Vorgänge sind in der administrativen Liste nicht auswählbar; der eigene Verlauf bleibt im persönlichen Bereich sichtbar.

## Quellen

Dateipfade relativ zum Software-Repository, außer `web/content/docs/...` für Dokumentation:

- `web/components/layout/sidebar/dashboard-navigation.ts:123–151` und `web/locales/de/navigation.json:76–81`: **Zutritt → Zugriffsanträge**, Menü-Leserecht.
- `web/app/[project]/dashboard/access-management/requests/page.tsx:1–5`: tatsächlicher Routeneinstieg.
- `web/app/[project]/dashboard/access-management/requests/requests-page-client.tsx:45–130`: Standardzeitraum, globale Lese-/Änderungsrechte, nur `Pending`, Versionsübergabe, Erfolg/Laden und Fehlerausgabe.
- Dieselbe Datei `:170–246` und `:250–323`: Kartenangaben, angebotene Aktionen, Pagination, Zeitraum, Notiz/Begründung, Länge und Bestätigung. Kein eigener Antragsdetaildialog oder Kompetenzstatus vorhanden.
- `web/locales/de/access.json:547–566`: konkrete deutsche Aktions- und Feldnamen. Die dortige Behauptung „revisionssicher“ wurde nicht als Produkteigenschaft übernommen.
- `api/Service/Accesses/Boundary/HttpControllers/ResourceAccessRequestsController.cs:22–60`: globale `Accesses.View`/`Accesses.Update`, Erfolg und dokumentierte Fehlerantworten.
- `api/Service/Accesses/Application/Services/ResourceAccessCatalogService.cs:202–219`: Liste aus `ViewAccessRelations`-Zielen plus Ressourcenverantwortung `CompetencyApprover`.
- Dieselbe Datei `:242–310`: Genehmigung erstellt User-Grant mit angefragter Ressource/Person und Zeitraum; Antrag und Vergabe werden transaktional gespeichert; Ablehnung aktualisiert nur den Antrag.
- Dieselbe Datei `:337–399`: Entscheidungszuständigkeit `ManageAccess` oder `CompetencyApprover`, Prüfung auf offenen Stand und Version, Konflikt bei konkurrierendem Speichern.
- `api/Service/Accesses/Application/Services/ResourceAccessAuthorizationService.cs:125–168,230–242`: Einzelressource versus gesamter Zugriffsbereich, keine Hierarchievererbung, Lesen von Vergaben auch über `ManageAccess`.
- `api/Service/Accesses/Boundary/Hypermedia/ResourceAccessHypermediaEnrichers.cs:504–541`: Entscheidungsaktionen nur bei offenem Status und Zuständigkeit; zusätzliche globale Update-Berechtigung.
- `api/Service/Accesses/Boundary/Dto/ResourceAccessCatalogDtos.cs:72–155`: gespeicherte Entscheidung, Pflicht/Optionalität, 1024 Zeichen, exklusive Endzeit, Versionskonflikt.
- `api/Service/Accesses/Entity/AccessGrant.cs:19–31`: neue Vergabe ohne zusätzliche Wochenzeitfenster.
- `web/locales/de/resources.json:132–139`: UI-Bezeichnung **Kompetenz bestätigen**.
- `web/components/portal/profile-access-requests.tsx:145–194`: persönliche Anzeige von Entscheidung, Bearbeitungsdatum und Rückmeldung.
- `web/content/docs/docs/benutzer/berechtigungsanfragen.mdx`, `web/content/docs/docs/benutzer/zutritt.mdx`, `web/content/docs/docs/koordination/ressourcen.mdx`, `web/content/docs/docs/koordination/bewertungen.mdx`, `web/content/docs/docs/administration/zutritt-verwalten.mdx`: Abgrenzung und bestehende gemeinsame Anleitungen.

## Prüfungen und verbleibende Arbeit

- Statische Prüfung der genannten UI-, Übersetzungs-, Backend- und Vertragsquellen; keine realen Anträge entschieden.
- Prettier-Prüfung mit vorhandenem `web/node_modules/.bin/prettier --ignore-path /dev/null --check` für beide Dateien bestanden. Expliziter Ignore-Override, weil das Web-Projekt das Dokumentations-Submodul sonst ausnimmt.
- MDX-Syntax mit dem vorhandenen `@mdx-js/mdx` kompiliert: bestanden. Kein Consumer-Build oder Rendering.
- Frontmatter (Titel/Beschreibung), kein zusätzliches H1 sowie alle vier relativen Links einschließlich beider Zielanker mit lokalem Python geprüft: bestanden.
- Keine Softwareänderung, API-/DTO-Änderung, Navigation, Commits, Serverstarts oder Builds. Keine Tests verändert oder ausgeführt.
- Offen für Koordinator: Rendern in Dashboard-/Website-Consumer, Mobilansicht, Tastatur, Zeitzonendarstellung der Zeitfelder; realer Test mit getrennten Sicht-/Entscheidungsrechten, beiden Zuständigkeitswegen, erfolgreicher Genehmigung/Ablehnung und konkurrierender Entscheidung beziehungsweise Rücknahme. Anschließend persönlichen Verlauf und erzeugte Freigabe gegenprüfen. Kein Hardware-/Anbieterzugriff erforderlich, um diesen Dashboard-Ablauf zu prüfen; eine reale Tür-/Maschinenfreigabe wäre eine gesonderte Prüfung.
- Querverweise: Neue Seite bei Koordination aufnehmen; aus Ressourcenregel und persönlicher Antragsanleitung bei Bedarf auf diese Koordinationsaufgabe verweisen. Eine benachbarte neue Freigaben-Anleitung erst nach Anlage verknüpfen. Bestehende Links der neuen Seite zeigen ausschließlich auf bereits vorhandene Seiten.

Geänderte Dateien: ausschließlich neue Produktseite und dieser Bericht.
