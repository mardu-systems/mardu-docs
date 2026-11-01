# Seitenrevision P13: Meine Zutrittsmedien

## Änderungsbrief und Entscheidung

Seite: `docs/ueberblick/profil-zutrittsmedien.mdx`. Leserfrage: Welche eigenen
Karten oder Transponder sind zugeordnet, sind sie verwendbar und was ist bei
Verlust zu tun? Vorausgesetzt sind Anmeldung und Profil-Leserechte; Kenntnisse
über Enrollment oder technische NFC-Daten sind nicht erforderlich. Die Seite
bleibt die kanonische persönliche Anleitung mit bestehender URL im
Benutzerbereich. Entscheidung: **verbessert**, zur Prüfung.

Die vorhandenen Erklärungen zu Kennung, Zeitpunkten, Status und Gültigkeit sowie
die Folgen einer Verlustsperre bleiben erhalten. Der kleine Patch präzisiert den
Zugang über Kontoeinstellungen, die Suche und Fehlerhilfe sowie die Weitergabe
der Tag-ID bei Verlust. Ein veralteter Screenshot wird aus der Anleitung
entfernt. Keine Software-, Navigations-, API- oder DTO-Änderungen.

## Befunde und Quellen

- Der Einstieg heißt **Kontoeinstellungen** im Kontomenü;
  `web/components/layout/common/account-menu-items.tsx:19–27` und
  `web/locales/de/navigation.json:26–32`. **Meine Zutrittsmedien** ist ein
  Profilbereich mit Profil-Leserecht;
  `web/components/layout/settings/profile-nav.config.ts:127–140`.
- Die persönliche Ansicht liest die eigenen Medien, filtert nach Name oder
  Tag-ID, bietet Seitennavigation, **Neu laden** und bei Fehlern **Erneut
  versuchen**. Sie übergibt keine Änderungsaktionen an die gemeinsame Darstellung:
  `web/components/profile/profile-access-media.tsx:22–124`. Der Backend-GET
  verlangt `Permissions.Profile.View` und liest anhand der angemeldeten Person:
  `api/Service/Tags/Boundary/HttpControllers/ProfileTagsController.cs:31–38`.
- Die gemeinsame `TagSummary` zeigt Tag-ID, Kopieraktion, Erstellungs- und
  Änderungsdatum, kombinierte Gültigkeit, Verluststatus und Verlustzeitpunkt:
  `web/components/tags/tag-summary.tsx:22–105`. Statusbezeichnungen stammen aus
  `web/lib/tags/status.ts:4–9`; Texte aus
  `web/locales/de/resources.json:501–523` und
  `web/locales/de/devices.json:682–744`. Die Unterscheidung zwischen
  Datensatzanlage und Benutzerzuweisung ist im DTO ausdrücklich dokumentiert:
  `api/Service/Tags/Boundary/Dto/TagDtos.cs:73–81`.
- Die Benutzerverwaltung bietet **Als verloren melden** mit
  `Permissions.Tags.Update`; keine persönliche Portalaktion:
  `web/app/[project]/dashboard/user-management/users/dialog/user-tags-tab.tsx:53–58,105–118`
  und `api/Service/Tags/Boundary/HttpControllers/TagsController.cs:96–113`.
  `TagsService.ReportLostAsync` speichert den ersten Verlustzeitpunkt und
  deaktiviert den Datensatz, ohne ihn zu löschen; `PatchAsync` verhindert eine
  Reaktivierung: `api/Service/Tags/Application/Services/TagsService.cs:62–114`.
  Die bestehende Erklärung zu fortbestehenden Nutzungen wird durch den
  Endpointvertrag bestätigt. Die Serverprüfung verweigert verlorene, inaktive
  oder zeitlich ungültige Tags:
  `api/Service/Accesses/Boundary/EventConsumers/ProtocolDeviceAccessConsumer.cs:24–32`.
- Der vorhandene Screenshot wurde als lokale Datei betrachtet. Er zeigt die
  frühere Darstellung **Kennung** und getrennte Gültigkeitsfelder ohne Kopieraktion
  und Zeitpunkte. Sein Verweis und die zugehörige Bildunterschrift werden entfernt;
  die Asset-Datei bleibt unverändert. Das Bild ist kein aktueller UI-Nachweis.
- Im Backlog `planning/offene-dokumentationsaufgaben.md` besteht kein eigener
  Auftrag für diese Profilseite. Nachbarseiten `docs/ueberblick/profil.mdx` und
  `docs/benutzer/zutritt.mdx` wurden als Kontext gelesen. Die Trennung zwischen
  Medienstatus und Freigabe/Einweisung bleibt erhalten.

## Checks und Praxisgrenzen

Ausgeführt: gezielter Prettier-Formatcheck für beide zugewiesenen Dateien
(`--ignore-path /dev/null`, weil der Consumer das Doku-Submodule standardmäßig
ignoriert), Diff-/Whitespaceprüfung, Existenzprüfung des relativen Seitenlinks
und Prüfung auf unveränderte Überschriftenanker. Das Tabellenformat wurde mit
dem vorhandenen Prettier korrigiert. Keine globalen Builds oder Softwaretests,
da ausschließlich Dokumentation geändert wurde.

Nur statischer Abgleich und Sichtprüfung des bestehenden Bildes. Keine
angemeldete Browserprüfung, keine Karten-/Readerprüfung, keine Verlustmeldung
ausgeführt. Keine praktische Abnahme behauptet. Rendering im Software- und
Website-Consumer, Markdown-Ausgabe sowie mobile Darstellung prüft der Koordinator. Für ein neues
Bild wird ein aktueller Screenshot mit fiktiven Daten benötigt; die Anleitung
bleibt ohne Bild vollständig lesbar.

## Koordination und geänderte Dateien

Die bestehenden Anker `medien-finden-und-lesen` und
`fehlendes-oder-verlorenes-medium` bleiben erhalten. Der bestehende relative Link
nach `../benutzer/zutritt.mdx` bleibt bestehen. Kein neuer Seitenbedarf und keine
Änderung an Navigation oder Nachbarseiten erforderlich. Das veraltete Asset kann
nach Prüfung weiterer Verwendungen separat ersetzt oder bereinigt werden.

- `web/content/docs/docs/ueberblick/profil-zutrittsmedien.mdx`
- `web/content/docs/planning/reviews/2026-11-01/ueberblick--profil-zutrittsmedien.md`
