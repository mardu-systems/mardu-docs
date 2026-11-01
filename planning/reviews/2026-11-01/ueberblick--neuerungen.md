# P47: Neuerungen

## Änderungsbrief und Entscheidung

Seite: `docs/ueberblick/neuerungen.mdx`. Leserfrage: Welche Änderungen gehören
zu einer veröffentlichten Version, welche Komponenten passen zusammen und was
ist bei einem Update zu beachten? Vorwissen: Unterschied zwischen Server,
Dashboard und optionalem Node-RED. Heimatbereich: Überblick, Nachschlagezweck.

**Belegbare Teildokumentation / offene Prüfung.** Den bisherigen historischen
TODO-Entwurf durch einen begrenzten Releaseeintrag zu v0.6.0 ersetzen. Beleg sind
veröffentlichte GitHub Releases und die Tag-/Submodule-Zuordnung, keine heutigen
Änderungen. Bestehende URL, beide Abschnittsüberschriften und der Betriebsverweis
bleiben erhalten. Keine Navigationserweiterung. Geeignete Prüfungen: Format,
MDX-Kompilation, Linkziele und unveränderte Anker; Consumerprüfung beim Koordinator.

## Befunde und Umsetzung

- Beide GitHub-Releasearchive liefern je acht veröffentlichte Releases. v0.6.0
  wurde für Server am `2026-10-31T00:20:07Z`, für Dashboard am
  `2026-10-31T00:20:06Z` veröffentlicht; beide `draft=false`, `prerelease=false`.
  Das Dashboard-Release nennt ausdrücklich Backend v0.6.0. Quellen:
  [Server-Release](https://github.com/mardu-systems/mardu-rpi-api/releases/tag/v0.6.0),
  [Dashboard-Release](https://github.com/mardu-systems/web/releases/tag/v0.6.0).
  Releasehinweise sind veröffentlichte Angaben des Projekts, keine eigene
  Funktionsabnahme. Ihre Metadaten melden `immutable=false`.
- Die über GitHub-GET und lokale Git-Objekte abgeglichenen Tags zeigen auf
  Servercommit `112e51d0c73c4478ae808cf7551d496de73180b0` und Dashboardcommit
  `a4b3ed9585bd43cadbdfa094f6b3afb6ea65747d`. Der Server enthält genau diesen
  Dashboard-Gitlink. Dessen `content/docs` verweist auf
  `babe610d7dc1ceb1c6d5e18dd0e8d8757be8873a`; dieser Dokumentationsstand ist
  im Text verlinkt. Quellen: `git ls-tree v0.6.0 web`, im Web-Repo
  `git ls-tree v0.6.0 content/docs`, GitHub `git/ref/tags/v0.6.0` mit
  Auflösung der annotierten Tags und `contents/content/docs?ref=v0.6.0`.
- Das Dokumentationsrepository liefert keine eigenen GitHub Releases. Das
  verhindert die Zuordnung über den Gitlink nicht. Die heutigen uncommitteten
  Seitenänderungen wurden nicht als Releaseänderungen verwendet. Lokaler
  Docs-HEAD bei Prüfung: `611fe8dcf45ffcd16d7f85e47accd242f78d4368`.
- Die Releasezusammenfassung nennt Ressourcenübersicht, gespeicherte
  Diagrammanordnungen, Messwerthistorie und ausgewählte Korrekturen. Die
  Notwendigkeit einer Sicherung und des gemeinsamen Komponentenupdates stammt
  aus den Server-Releasehinweisen. Keine Migrationsausführung, Dauer,
  Unterbrechungsfreiheit oder Rückwärtskompatibilität erfunden.
- Gegenprüfung im veröffentlichten Code per `git show v0.6.0:<Pfad>`:
  `api/Service/ManagedResources/Boundary/HttpControllers/ResourceOverviewController.cs:18-33`
  dokumentiert Ressourcenübersicht, zusätzliche Leserechte und Grenzen gegenüber
  Kapazität und Hardwarezustand;
  `web/components/managed-resources/resource-metrics-tab.tsx:28-69` verbindet
  Übersicht, Verlauf, gespeicherte Ansichten und Rechteprüfung. Die
  Verhaltenskorrekturen werden als Releaseinhalt wiedergegeben, nicht als selbst
  mit Leserhardware getestete Abläufe.
- Wiederverwendet: bestehende MDX-Überschriften, normale Markdownverweise,
  `koordination/ressourcen.mdx#messwerte-prüfen` und
  `administration/sicherheit-betrieb.mdx#sicherung-wiederherstellung-und-update`.
  Beide Zielabschnitte gelesen. Die Betriebsseite beschreibt ausdrücklich keine
  vollständige Sicherung/Wiederherstellung oder ein Release-Update.
- `README.md:51-54` und die historischen `docs/v1/index.mdx` /
  `docs/v2/index.mdx` sind kein Produktversionsbeleg. Diese Adressen wurden weder
  in eine Historie umgedeutet noch geändert.

## Sichtbarkeit, Anker und Grenzen

`docs/ueberblick/meta.json` enthält die Seite weiterhin nicht. Die historische
URL bleibt bestehen; `web/lib/docs-roles.tsx:54` ordnet sie weiter dem Überblick
zu. `web/lib/source.ts:45-51` begrenzt veröffentlichte Ausgaben auf den kuratierten
Baum. Keine Metadaten oder Consumerlisten geändert. Die bisherigen Anker
`änderungen-einer-version` und `verhalten-nach-einem-update` bleiben durch exakt
erhaltene Überschriften bestehen. Die neue Versionsüberschrift ergänzt einen
Anker, ohne alte zu ersetzen.

Die Seite ist eine nutzbare Teilhistorie, aber bleibt im bestehenden verborgenen
Zustand. Der Koordinator entscheidet nach Consumerprüfung über Sichtbarkeit.
Es gibt weiterhin keine vollständige, praktisch geprüfte Update-, Sicherungs-
und Wiederherstellungsanleitung; die Seite benennt diese Grenze. Keine
Browserprüfung, Installation, Migration, Hardware-, Versand- oder Providerprüfung
ausgeführt. Keine Software/API/DTO geändert; keine API-Dokumentation betroffen.
Keine vollständige Releasehistorie und kein eigener Nachweis der
Containerverfügbarkeit oder des korrekten Updateverhaltens behauptet.

## Checks und geänderte Dateien

Ausgeführt und bestanden:

- Vorhandenes Prettier auf beiden eigenen Dateien mit `--ignore-path /dev/null`
  und anschließend `--check`: beide Dateien formatiert.
- Produktseite mit vorhandenem `@mdx-js/mdx` kompiliert; Frontmatter separat auf
  `title` und `description` geprüft. Kein zusätzliches H1, keine TODO-Aufträge.
- Beide bisherigen H2 mit `HEAD` verglichen: exakt erhalten. Beide relativen
  Verweise einschließlich Fragmente mit vorhandenem `github-slugger` geprüft:
  Ziele und Abschnitte vorhanden. Ausschluss aus Überblick-Metadaten bestätigt.
- `git diff --check` auf zugewiesenen Dateien: kein Befund.
- Read-only Releaseabfrage zunächst per `gh api .../releases --paginate`, danach
  über den GitHub-Connector für alle drei Repositories sowie Tagauflösung und
  Dokumentations-Gitlink. Keine Remote-Schreibaktion.

Das sind Quellen-, Syntax- und Dateiprüfungen. Consumerdarstellung, Suche und
LLM-Ausgabe sind vom Koordinator gemeinsam zu prüfen. Keine Builds oder globalen
Tests gestartet, keine Installations- oder Releaseartefakte ausgeführt.

Geändert ausschließlich:

- `web/content/docs/docs/ueberblick/neuerungen.mdx`
- `web/content/docs/planning/reviews/2026-11-01/ueberblick--neuerungen.md`
