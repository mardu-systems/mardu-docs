# Seitenrevision P19: Zugangs-Tags verwalten

## Änderungsbrief und Entscheidung

Seite: `docs/administration/tags-verwalten.mdx`. Leserfrage: Wie ordne ich einer
Person eine Karte über Mardu Connect zu, prüfe oder benenne sie und sperre oder
ersetze sie bei Verlust? Vorausgesetzt sind ein vorhandenes Benutzerkonto und
die jeweiligen Verwaltungsrechte; NFC- und API-Kenntnisse werden im Hauptablauf
nicht vorausgesetzt. Heimat bleibt Administration, URL und Anker bleiben erhalten.

Entscheidung: **unverändert gut** nach statischem Abgleich. Die bereits gegen
Dashboard, Backend und Connect überarbeitete Anleitung hat keine belegte
inhaltliche Lücke ergeben. Keine kosmetische Neufassung. Produktseite,
Store-Verweise, Warnungen, Beispiel und seit `611fe8d` verwendete
Fumadocs-Framework-Image-Komponenten bleiben unverändert. Nur dieser Bericht
wird angelegt; keine Software-, Navigations-, API- oder DTO-Änderung.

## Befunde und Quellen

Die folgenden Pfade sind relativ zum Software-Repository; Connect-Quellen liegen
unter `/Users/lucaschoeneberg/Documents/GitHub/mardu_connect/`.

- **Rechte und unmittelbares Speichern:** Konto einschließlich Tags wird mit
  `Permissions.Users.View` gelesen: `api/framework/Infrastructure/Identity/Users/Boundary/UserController.cs:41–46`
  und `api/framework/Infrastructure/Identity/Users/Services/UserService.cs:319,501–550`.
  Enrollment verlangt `Tags.Update`; Umbenennen/Verlust ebenfalls, Löschen
  `Tags.Delete`: `api/Service/Tags/Boundary/HttpControllers/TagEnrollmentController.cs:24–47`
  und `TagsController.cs:66–142`. Die UI-Aktionen und unabhängigen Requests stehen
  in `web/app/[project]/dashboard/user-management/users/dialog/user-tags-tab.tsx:50–157`,
  `edit-user-sheet.tsx:645–674,733–767` sowie
  `web/components/tags/tag-rename-dialog.tsx:51–68` und `tag-loss-dialog.tsx:42–50`.
  Die bestehende Rechtetabelle und Warnung zum Abbrechen des Benutzerformulars
  bleiben zutreffend.
- **Anmeldung und Rückmeldung:** `TagEnrollmentService.cs:48–96` im selben
  Services-Verzeichnis erzeugt fünf Minuten gültige DESFire-EV2-Anmeldedaten.
  `web/lib/stores/tag-store.ts:37–67` übergibt ausschließlich Person und optionalen
  Namen, daher fehlen beide Gültigkeitsgrenzen; `TagEnrollmentService.cs:234–247`
  erzeugt den aktiven Tag mit diesen gespeicherten Werten. Name, Längenprüfung,
  manuelle QR-Daten, Abschluss und lokaler Abbruch stehen in
  `web/components/tags/enroll-tag-wizard.tsx:119–145,220–269,302–365`.
  `web/locales/de/devices.json:643–751` bestätigt die verwendeten UI-Bezeichnungen.
  Für fremde Benutzergruppen verlangt
  `api/Service/Tags/Boundary/Hubs/UserTagHub.cs:23–26,53–85` die Admin-Rolle;
  `tag-store.ts:89–99,135–175` erklärt die getrennte REST-Anmeldung und
  Live-Rückmeldung. Die dokumentierte Einschränkung ist notwendig.
- **Connect und Fehlerhilfe:** `lib/features/enrollment/logic/enrollment_controller.dart:76–90`
  übernimmt die Serveradresse aus dem QR-Code. `presentation/pages/enroll_info_page.dart:49–63`
  und `home_page.dart:349–405` bestätigen **Schreiben starten**, Fehlermeldung und
  Wiederholung. `enrollment_controller.dart:247–345` speichert den ausstehenden
  Abschluss erst nach Kartenprüfung, wiederholt nur COMPLETE und hält den Zustand
  im laufenden Controller. Verwerfen setzt weder Karte noch Server zurück.
  `presentation/pages/success_page.dart:96–132,209–241,290–320` bestätigt
  **Synchronisierung ausstehend**, **Erneut synchronisieren**, **Vorgang beenden**,
  **Abschluss verwerfen** und **Abgeschlossen**. Die Warnungen vor erneutem
  Beschreiben und vor einem App-Neustart bleiben erhalten.
- **Abbruch und Ablauf:** `TagEnrollmentService.cs:99–145` und
  `TagEnrollmentController.cs:50–90` belegen API-Stornierung und Token-Erneuerung.
  Der Dashboard-Abbruch setzt nur den lokalen Store zurück, ohne Cancel-Request
  (`enroll-tag-wizard.tsx:339–365`, `tag-store.ts:69–79`).
  `api/Service/Tags/Application/Services/TagDeletionImpactProvider.cs:52–63`
  blockiert die Löschung beteiligter Konten bei unvollständigen Anmeldungen.
- **Verlust, Ersatz und Löschung:** `api/Service/Tags/Application/Services/TagsService.cs:62–110`
  verhindert Reaktivierung und erhält den ersten Verlustzeitpunkt.
  `TagsController.cs:96–113` beschreibt ausdrücklich unveränderte laufende
  Sitzungen und NFC-Daten. Die Serverentscheidung prüft Verlust, Status,
  Eigentümer und Zeitraum:
  `api/Service/Accesses/Boundary/EventConsumers/ProtocolDeviceAccessConsumer.cs:24–39`.
  `TagEnrollmentService.cs:234–247` verweigert registrierte Chip-Kennungen und
  verändert beim Ersatz keinen alten Tag. Benutzer- und Tag-Freigaben werden
  getrennt verglichen: `api/Service/Accesses/Application/Services/ResourceAccessDecisionService.cs:1004–1014`.
  Löschvorschau und Bestätigung sind in `TagsController.cs:133–164` und
  `TagsService.cs:113–128` belegt. Die Anleitung verspricht weder Kartenreset noch
  automatische Ersatzübertragung oder Offline-Sperrbestätigung.
- **Anzeige und technische Daten:** `web/components/tags/tag-summary.tsx:22–133`
  trennt Status und Zeitraum, bietet das Kopieren der Tag-ID und kennzeichnet
  technische Angaben als gespeicherte Daten. Die entsprechende Erklärung bleibt.
- **Store-Links und App-Links:** Die vorhandenen
  [App-Store](https://apps.apple.com/de/app/mardu-connect/id6771269028)- und
  [Google-Play](https://play.google.com/store/apps/details?id=de.mardu.connect&hl=de)-Adressen
  antworteten bei lesenden HTTP-Abfragen am 01.11.2026 jeweils mit HTTP 200;
  die gelesenen Antworten enthalten Mardu GmbH, Apple auch den Titel Mardu Connect.
  Das Web-Lesewerkzeug konnte beide Seiten nicht abrufen; die HTTP-Prüfung
  erfolgte anschließend mit curl. Androids Paketkennung ist zusätzlich in
  `android/app/build.gradle.kts:42,64` belegt. Dashboard-App-Link und native
  URL-Zuordnungen passen zusammen: `web/lib/tags/enrollment-app-link.ts:3`,
  Connect `android/app/src/main/AndroidManifest.xml:40–41` und
  `ios/Runner/Runner.entitlements:5–8`. `ios/Runner/Info.plist:34` belegt den
  Hinweis auf lokalen Netzwerkzugriff. Keine Installation oder Store-Aktion.

## Checks, Grenzen und Koordination

- Erfolgreicher gezielter Prettier-Check der Produktseite und dieses Berichts
  mit dem vorhandenen `web/node_modules/prettier/bin/prettier.cjs`, ausdrücklich
  `--ignore-path /dev/null` für das sonst ignorierte Doku-Submodule.
- Erfolgreiche lokale Prüfung aller 13 relativen Seiten-/Ankerlinks mit dem
  vorhandenen `github-slugger`; beide importierten Store-SVGs existieren.
  Die zwei Framework-Image-Verwendungen und der Import bleiben erhalten.
- Diff-/Whitespaceprüfung nur der zugewiesenen Dateien; Produktseite unverändert.
  Keine globalen Builds, Softwaretests oder Softwareänderungen.
- Nachbarseiten `administration/benutzer-rollen.mdx`,
  `koordination/ressourcen.mdx` und `ueberblick/profil-zutrittsmedien.mdx` wurden
  im relevanten Zusammenhang gelesen. Der Backlog enthält keinen eigenen
  offenen Seitenauftrag für Tags; die allgemeine Verwaltungsinventur bleibt
  Aufgabe des Koordinators. Kein neuer Seitenbedarf und kein Linkfehler gefunden.

Nur statische Code-/Textprüfung und öffentliche HTTP-Leseabfragen. Keine
angemeldete Browserprüfung, kein echter Connect-Durchlauf, keine Karte, kein
Leser und keine Verlust-/Löschaktion. Store-Erreichbarkeit belegt keine
Installierbarkeit oder Übereinstimmung der ausgelieferten App mit dem lokalen
Quellcode. Gemeinsames Rendering in beiden Consumern, Markdown-Ausgabe der
Store-Badges, mobile Ansicht und reale Enrollment-/Leserprüfung bleiben beim
Koordinator beziehungsweise bei der Installation. Keine praktische Abnahme.

Geänderte Datei:
`web/content/docs/planning/reviews/2026-11-01/administration--tags-verwalten.md`.
