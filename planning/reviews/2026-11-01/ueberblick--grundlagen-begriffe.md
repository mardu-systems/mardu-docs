# P45: Grundlagen und Begriffe

**Entscheidung: verbessert; zur gemeinsamen Consumer-Prüfung.**

Leserfrage: Welche Begriffe bezeichnen ein Nutzungsziel, seine Technik, ein Recht
oder einen Nachweis? Die Seite bleibt eine Erklärung/Nachschlagehilfe im Überblick
für Personen ohne Kenntnis des Datenmodells. Der kleine Änderungsumfang ist auf
fehlende Begriffe und ihre Abgrenzung beschränkt.

## Befund und Umsetzung

- Gerät ergänzt; Ressource, gemeinsamer Zugangsbereich/Scope, Zutrittspunkt und
  Anschluss/Endpoint präzisiert. Anschlüsse können auch aus Automationen stammen.
  Ein Raum-/Maschinenbeispiel und ein Link zur vorhandenen Ressourcenanleitung
  verdeutlichen die Zuordnung und dass Ressourcen keine Hardware voraussetzen.
- Freigabe mit der UI-Bezeichnung Zugriffsvergabe verbunden; Benutzergruppen als
  Empfänger benannt. Die Rollen einer Benutzergruppe gelten für ihre Mitglieder;
  Funktionsrechte, persönliche Nutzung und Verwaltungszuständigkeit bleiben getrennt.
- Badge/Definition/Inhaltsversion, Einweisung und technische Verifikation erklärt.
  Lokale Badge-Vergabe von signiertem Credential und Ressourcenfreigabe abgegrenzt.
  Die gute Definition der Anerkennung unverändert erhalten.
- Gültige Definitionen für Konto, Katalogangebot, Anfrage, Buchung, Tag,
  Provisionierung, Automation, Fähigkeit, Standard, Lernweg und Bewertung sowie
  Sitzungsabgrenzungen und physische Bestätigungsgrenzen inhaltlich erhalten.
  Keine API-/DTO-Verträge geändert; keine Implementierungsnamen in der Produktseite.

## Quellen

Pfade relativ zum Software-Repository; Stellen beziehen sich auf den geprüften Stand.

- `web/content/docs/docs/koordination/ressourcen.mdx:83` und `:99`:
  gemeinsame Ressourcenregel, Scope, technische Zuordnung und Beispielbegriffe.
- `web/content/docs/docs/administration/geraete-verwalten.mdx:8`:
  Controller/Anschlüsse und keine automatische Ressourcenanlage.
- `api/Service/ManagedResources/Entity/ManagedResource.cs:28`,
  `api/Service/Accesses/Entity/AccessPoint.cs:13` und
  `api/Service/Devices/Boundary/Dto/DeviceEndpointDtos.cs:8`:
  Ressourcenregel, Zutrittspunktzuordnung sowie Geräte- und Automationsanschlüsse.
- `web/content/docs/docs/ueberblick/benutzerkonten.mdx` und
  `api/framework/Infrastructure/Identity/Permissions/PermissionService.cs:96`:
  Rollen und Gruppen als Quellen von Funktionsrechten.
- `web/content/docs/docs/benutzer/kompetenzen.mdx` und
  `web/content/docs/docs/administration/badges-verwalten.mdx`:
  Einweisungen, lokale Vergaben, Definitionen und importierte/signierte Nachweise.
- `api/Service/Competencies/Entity/CompetencyGrant.cs:9` und
  `api/Service/Competencies/Entity/BadgeAward.cs:8`:
  Kompetenzanerkennung mit Status/Gültigkeit versus lokale Badge-Vergabe.
- `api/Service/OpenBadges/Application/OpenBadgesCredentialVerificationService.cs:40`
  und `api/Service/OpenBadges/Entity/CredentialVerification.cs:10`:
  zeitbezogene/providerabhängige technische Prüfung, keine Anerkennungsentscheidung.

## Eigene Checks und offene Prüfung

- MDX mit vorhandenem `@mdx-js/mdx` und `remark-gfm` kompiliert: erfolgreich.
- Prettier gezielt für die beiden eigenen Dateien mit `--ignore-path /dev/null`
  geprüft, weil die Web-Konfiguration das Doku-Submodule pauschal ausschließt.
- Vier relative Seitenverweise einschließlich des neuen Zielankers geprüft;
  alle vier bestehenden Überschriften und damit ihre Anker erhalten.
- Frontmatter und Diff/Whitespace gezielt geprüft. Keine globalen Builds,
  Softwareänderungen, Browser-, Hardware- oder Anbieterprüfung durchgeführt.
- Koordinator: gemeinsame Darstellung im Consumer, insbesondere breite
  Glossartabellen auf kleinen Bildschirmen, prüfen. Kein neuer Seitenbedarf und
  keine Navigationsänderung; bestehende Verweise bleiben erhalten.

Geänderte Dateien: `docs/ueberblick/grundlagen-begriffe.mdx` und dieser Bericht
(beide unter `web/content/docs/`).
