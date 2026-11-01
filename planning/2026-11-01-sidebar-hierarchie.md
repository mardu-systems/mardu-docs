# Sidebar: erkennbare Gruppen und Unterseiten

1. November 2026. Ergänzung zur Textverdichtung dieses Tages.

Nicht klickbare Gruppen sahen bisher fast wie Links aus: 14px, normale
Schriftstärke. Sie erhalten 12px, Gewicht 600, Großschreibung und einen neutralen
oberen Trenner. Links behalten ihre Schreibweise und aktive Bereichsfarbe.
Die Gruppen sind auch semantische Überschriften, keine zusätzlichen Bedienelemente.
Die Gestaltung ist in `web/DESIGN.md` festgehalten und verwendet vorhandene Tokens.

## Hierarchie

Vier native Fumadocs-Ordner ergänzen die vorhandenen Profil- und API-Unterseiten:

| Bereich        | Anklickbare Elternseite                                         | Unterseiten                           |
| -------------- | --------------------------------------------------------------- | ------------------------------------- |
| Benutzer       | [Meine Buchungen](../docs/benutzer/buchungen.mdx)               | Kalender exportieren und abonnieren   |
| Administration | [Integrationen](../docs/administration/integrationen.mdx)       | LDAP, OIDC, MQTT, IP500 und MCP       |
| Administration | [Mardu per CLI warten](../docs/administration/wartungs-cli.mdx) | Befehle und Optionen                  |
| Entwickeln     | [API und Integrationen](../docs/entwickeln/api-integration.mdx) | HTTP, MQTT, MCP und Automationsflüsse |

Überblick, Koordination und Installieren bleiben flach. Geräte und Automationen
sowie Badges und Kompetenzen bleiben eigenständige Aufgaben.

Die vier Ordner enthalten nur `meta.json`. `pagesIndex` verweist auf die vorhandene
Elternseite; die Kinder referenzieren ihre bisherigen Dateien. Kein MDX-Inhalt wurde
verschoben, keine neue Zwischen- oder Produktseite angelegt. Alle URLs, Anker und
Bereichseigentümer bleiben erhalten. Ein aktives Kind öffnet seinen Ordner;
andere Ordner beginnen eingeklappt. Der vorhandene Bereichsfilter bleibt unverändert.

Verwendet sind die offiziellen [Fumadocs-Metadaten](https://www.fumadocs.dev/docs/page-conventions#meta)
und der [Sidebar-Separator-Override](https://www.fumadocs.dev/docs/ui/layouts/docs#sidebar-components).
Keine neue Dependency, kein Business-API-/DTO-Vertrag und keine Änderung des
Dashboard-Seitenmenüs.

## Prüfung

- Vier neue Navigationsfälle zunächst fehlgeschlagen, nach Metadatenänderung bestanden.
- 83 Tests in acht Doku-Testdateien, Scoped ESLint sowie Produktionsbuild inklusive TypeScript bestanden.
- `design.md lint`: keine Fehler oder Warnungen; Impeccable-Layoutscan ohne Befund.
- Browser: Desktop 1440px und Mobil 390px, Hell und Dunkel. Alle sechs Gruppen
  nicht interaktiv, 12px/600, Kontrast mindestens 17:1. Keine seitliche Überbreite.
- Direktaufrufe von vier neuen Kindern sowie bestehendem Profil-/API-Kind:
  Gruppe automatisch offen, aktiver Eintrag sichtbar. Pfeil ohne Navigation,
  Elternlink per Tastatur und mobiler aktiver Untereintrag geprüft.
- 69 Seiten mit HTTP 200; 1.023 interne Verweise und alle 561 bisherigen stabilen
  Artikel-IDs erhalten. 42 Bilder erreichbar, keine fehlenden Alternativtexte.
- Veröffentlichungsliste weiterhin 67 Anleitungen plus 554 API-Operationen;
  verschachtelte LDAP-Anleitung über die Suche erreichbar.
- Websitefilter: 45 Tests mit aktueller gemeinsamer Quelle im Speicher bestanden.
  Website-Content-Gitlink unverändert; kein Website-Build oder Rollout.
- React Doctor: keine blockierenden Fehler; 476 bestehende Warnungen im Gesamtprojekt.

Die vorherigen Textänderungen bleiben erhalten. Commit auf anschließenden Nutzerauftrag; kein Push oder Rollout.
