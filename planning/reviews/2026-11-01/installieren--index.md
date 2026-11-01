# P55 – Installieren

## Änderungsbrief

Leserfrage: Welche Anleitung brauche ich für Serveraufbau, Aufnahme eines
vorhandenen Geräts, Funktionsprüfung und Übergabe oder eine Störung vor Ort?
Vorausgesetzt sind die Unterlagen und Zugänge der konkreten Installation;
Detailvoraussetzungen stehen an den verlinkten Aufgaben. Heimat bleibt
`installieren/index`.

Nach Lektüre der vier ausgearbeiteten Nachbarseiten: kurze Orientierung behalten,
die neuen Anleitungen in der Arbeitsreihenfolge verlinken und den überholten
Planungshinweis ersetzen. Bestehende Überschriften, URLs und explizite Anker
erhalten. Geräte-Montage und Kompatibilität bleiben von Softwareeinrichtung und
Funktionsprüfung getrennt. Keine Software- oder Navigationsänderung.

## Entscheidung und Umsetzung

**Verbessert.** Der Bereichsstart führt jetzt vom Serveraufbau zur Geräteaufnahme,
zur Funktionsprüfung mit Protokoll und Übergabe und schließlich zur Störungshilfe.
Er bleibt eine Orientierung und wiederholt keine Detailabläufe.

- Neue direkte Verweise auf die ausgearbeiteten Seiten `inbetriebnahme`,
  `abnahme-uebergabe` und `stoerung-vor-ort`. Die Voraussetzung eines vorhandenen
  Servers und erreichbaren IP500-Edge-Routers ist beim Gerätepfad erkennbar.
- Der veraltete Hinweis auf fehlende physische Abnahme und Übergabecheckliste
  entfällt. Stattdessen werden getrennte Prüfung von Softwareangaben,
  Geräterückmeldungen und physischer Beobachtung sowie offene Mängel genannt.
- Keine Montage-, Stromversorgungs- oder Kompatibilitätsanleitung behauptet:
  Diese Fragen verweisen auf die Unterlagen des konkreten Geräts und Stands.
- Der Serverpfad verweist vor dem Einstieg ausdrücklich auf die bekannte
  Einschränkung des Erstsetups. Es wird kein erfolgreicher Pi-Start behauptet.
- Vorhandene Kurzorientierung, alle bisherigen Linkziele und drei Überschriften
  sowie die expliziten IDs `in-diesem-bereich` und
  `offene-dokumentationsaufgaben` bleiben erhalten. Den historischen zweiten
  Anker bewahrt der Text ohne sichtbaren Planungsauftrag.
- Vorhandene Markdown-/MDX-Struktur und kanonische Geräte-/Ressourcenanleitungen
  wiederverwendet; Bereichswechsel bei diesen Verweisen benannt. Ergänzend ist
  Sicherheit und Betrieb aus Administration erreichbar.

## Geprüfte Quellen und Beleggrenzen

Dokumentpfade beziehen sich auf `web/content/docs`, Softwarepfade auf die
Repositorywurzel.

- `docs/installieren/raspberry-pi.mdx`, Voraussetzungen und Abschnitt
  `4. Starten und einrichten`: Installationsumfang und dokumentierte
  Erstsetup-Einschränkung.
- `deploy/production/docker-compose.prod.yml:60` setzt intern HTTP-Port 8080;
  `web/components/setup/setup-wizard.tsx:311` übermittelt 5001;
  `api/Framework/Infrastructure/Configuration/Setup/SetupOrchestrator.cs:401`
  und `:521–534` prüfen den Wert gegen eine Umgebungs-Sperre. Diese Stellen
  selbst gelesen. Der bereits von P34 gemeldete Konflikt ist eine statische
  Ableitung für diese Quellkombination, kein pauschaler Release- oder Pi-Befund.
- `docs/installieren/inbetriebnahme.mdx`, Einleitung, Netzwerk und
  Softwareaufnahme sowie Abnahme: angeschlossener Controller, eingerichtetes
  IP500-Netzwerk, Server und Edge-Router; getrennte Prüfung der Anschlüsse.
- `api/Service/Devices/Boundary/Dto/DeviceCreationDto.cs`, Manifest/Certificate
  und Validierung: genau eine Aufnahmequelle, keine freie Hardwarezusage.
- `api/Service/Devices/Application/Services/DeviceEndpointConfigurationService.cs:41–76`,
  `GetAsync` und `UpdateAsync`: gespeicherte Konfiguration, Geräterückmeldung
  und asynchroner Konfigurationsauftrag werden getrennt abgebildet. Eine
  gespeicherte Einstellung bestätigt keine physische Wirkung.
- `docs/installieren/abnahme-uebergabe.mdx`, Funktionsprüfung sowie Protokoll
  und Übergabe: durchführbare Prüfschritte und manuelles Protokoll; ausdrücklich
  keine Montage- oder Normprüfung und keine Abnahme einer konkreten Anlage.
- `docs/installieren/stoerung-vor-ort.mdx`, Serverprüfung, Fehler eingrenzen,
  Wiederanlauf und Eskalation: nutzbare Störungshilfe statt Planungsseite.
- `docs/installieren/meta.json`: derzeit nur Raspberry-Pi-Anleitung sichtbar;
  neue verlinkte Seiten sind vorhanden. Metadaten wurden nicht geändert.

## Ausgeführte Checks

- Vorhandenes Prettier aus `web/node_modules/.bin/prettier` mit
  `--ignore-path /dev/null` nur auf beide eigenen Dateien angewandt; anschließende
  Formatprüfung erfolgreich. Das Docs-Submodul wird sonst ignoriert.
- `@mdx-js/mdx` aus vorhandenen Consumer-Dependencies: Seite kompiliert.
- Statischer Dateicheck: Frontmatter mit Titel und Beschreibung, kein H1 und
  keine TODO-Schreibaufträge; alle elf relativen Verweise samt verwendetem
  Zielanker aufgelöst. Alle fünf bisherigen Überschriften/IDs gegen `HEAD`
  erhalten.
- `git diff --check` im Doku-Submodul nur für die beiden eigenen Dateien:
  erfolgreich.
- Keine API-/DTO- oder Softwareänderung; keine API-Dokumentation anzupassen.

## Offen für den Koordinator

Consumer-Rendering, mobile Darstellung, gemeinsame Navigation und Erreichbarkeit
der neuen Aufgaben in beiden Consumern prüfen. Keine Browserprüfung, kein
globaler Build und keine reale Pi-/Hardwareprüfung ausgeführt. Eine konkrete
Installationsabnahme braucht passende Release-Images und Geräteunterlagen sowie
die tatsächlichen Prüfungen vor Ort; der Bereichsstart bestätigt sie nicht.
Kein zusätzlicher Seitenbedarf aus diesem Patch. Nachbarseiten und Metadaten
bleiben unangetastet.

## Geänderte Dateien

- `web/content/docs/docs/installieren/index.mdx`
- `web/content/docs/planning/reviews/2026-11-01/installieren--index.md`
