# Personen und Technik: Seitenrevision vom 03.11.2026

## Auftrag und Ergebnis

Leser sind Personen, die Benutzerkonten, Rollen, Gruppen, Verwaltungsrechte oder
Geräte pflegen. Vorausgesetzt sind die jeweils genannten Rechte; Hardware- oder
API-Kenntnisse sind für die Hauptaufgaben nicht nötig. Ziel sind auffindbare
Bedienwege, genaue UI-Bezeichnungen und unterscheidbare Folgen für Anmeldung,
Verwaltung und Ressourcennutzung. Heimatbereich, URLs und bestehende Anker bleiben
erhalten. Muster waren Ressourcenfreigaben und Ressourcenbuchbarkeit; vorhandene
Steps, Tabs und Tabellen werden weiterverwendet, neue Bilder nutzen ImageZoom.

Fünf Produktseiten sind angepasst, die Tag-Anleitung ist bewusst unverändert. Keine Software-,
Metadaten-, API-/DTO-, Rollen- oder Gruppenzuweisungsänderung. Die bei Beginn bereits
geänderte Geräteanleitung wurde als Ausgangspunkt erhalten.

## Benutzer und Rollen

Datei: `docs/administration/benutzer-rollen.mdx`.

**Entscheidung:** Bestehende Abläufe und Warnungen erhalten; belegte Lücken und
veraltete Metrikbezeichnungen korrigieren.

**Quellen im Software-Repository:**

- `web/app/[project]/dashboard/user-management/users/dialog/edit-user-sheet.tsx`:
  tatsächlicher Metrikreiter, Entwürfe beim Reiterwechsel, äußeres Speichern.
- Im selben Dialogverzeichnis: `user-metrics-tab.tsx`,
  `user-authorization-tab.tsx`, `edit-user-security.tsx`, `add-user-dialog.tsx`;
  daneben `registration-decision-dialog.tsx`.
- `web/components/metrics/entity-metrics-view.tsx`,
  `web/components/users/passwordless-admin-card.tsx`,
  `web/locales/de/{users,common,auth}.json`.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.{Invite,Roles,CreateUpdate,TwoFactor}.cs`,
  `api/Framework/Infrastructure/Identity/Groups/UserGroupService.cs`,
  `api/Framework/Infrastructure/Identity/Passwordless/Boundary/PasswordlessController.cs`
  und `PasswordlessLoginService.cs` im übergeordneten Verzeichnis.

**Änderungen:** Metriken über den nachgewiesenen Benutzereinstieg beschrieben;
„Widget hinzufügen“, „Alle Widgets hinzugefügt“, „Ansicht speichern“ und
„Messwerte aktualisieren“ statt alter Kennzahltexte. Sofortige Ansichtsspeicherung
von äußerem Formularspeichern unterschieden. Passwortlosen Zugang per E-Mail und
Zwei-Personen-Freigabe mit Rechten, Bestätigung und Linkfolge ergänzt. Dekorative
Breitenwrapper und die für die Aufgabe entbehrliche Profilbild-Layoutaufnahme
entfernt. Bestehenden Anker `prüfstand-und-grenzen` beim sachlicheren Schluss
„Weitere Verwaltung“ erhalten.

**Browser:** Benutzer Jonas Sommer geöffnet; Metrikreiter mit leeren aktuellen
Daten, Ansicht bearbeiten und neue Beschriftungen geprüft. Sicherheit zeigt Code
senden, Freigabecode erstellen und Anfrage freigeben. Gruppendetails und
Mitgliederauswahl geöffnet. Keine Ansicht gespeichert, keine E-Mail oder
Freigabe angefordert, keine Kontodaten oder Mitgliedschaften geändert.

**Bild:** `docs/administration/bilder/personen-technik-benutzermetriken-2026-11-03.png`,
1440 × 1100 Browserfenster, Ausschnitt des Benutzerfensters. Tatsächlicher leerer
Verlauf; keine erfundenen Entscheidungen. Bild visuell geprüft und mit Alttext
über ImageZoom eingebunden.

## Rollen und Gruppen verwalten

Datei: `docs/administration/rollen-gruppen.mdx`.

**Entscheidung:** Gruppenpflege hier zusammenführen. Die Seite trennt globale
Rechte, Gruppenmitgliedschaft und Nutzungsfreigabe. Rollenanlage, Duplizieren,
Systemschutz und Löschfolgen bleiben erhalten; Gruppenanlage, Bearbeitung,
Mitglieder-/Rollenauswahl und Löschung stehen jetzt vollständig auf dieser Seite.

**Quellen:** `web/components/roles/{role-detail,role-list,role-overview-table}.tsx`,
`web/lib/stores/roles-store.ts`,
`web/app/[project]/dashboard/user-management/settings/{user-group-form-dialog,user-group-details-sheet}.tsx`,
`web/locales/de/users.json`,
`api/Framework/Infrastructure/Identity/Roles/{RoleService.cs,Boundary/RolesController.cs}`,
`api/Framework/Infrastructure/Identity/Groups/{UserGroupService.cs,Boundary/UserGroupsController.cs}`,
`api/Framework/Core/Identity/Request/{CreateOrUpdateRoleRequest,UpdateRolePermissionsRequest,UserGroupRequests}.cs`.

**Browser:** Rollenübersicht, Systemrolle Basic mit schreibgeschütztem Namen und
Rechten sowie sichtbarer Duplizieraktion; Benutzergruppe Werkstattleitung mit
Übersicht, Mitglieder- und Rollenreiter sowie Mitgliederauswahl/Anwenden geprüft.
Keine Rolle dupliziert, angelegt oder gelöscht, keine Gruppe geändert. Die
Gruppenlöschfolgen und Namensgrenzen wurden im Code abgeglichen, nicht ausgeführt.

## Verwaltungszuständigkeiten

Datei: `docs/administration/verwaltungszustaendigkeiten.mdx`.

**Entscheidung:** Inhalt beibehalten, Vorschau als aktuellen visuellen Beleg ergänzen.

**Quellen:** `web/app/[project]/dashboard/access-management/scopes/page-client.tsx`,
`web/components/access/{responsibility-binding-dialog,access-scope-diagnostics-dialog}.tsx`,
`web/locales/de/access.json`,
`api/Service/Accesses/Boundary/HttpControllers/AccessScopeAssignmentsController.cs`,
`api/Service/Accesses/Application/Services/{AccessScopeAssignmentService,AccessScopeProfilePresets}.cs`.
Globalrechte, ManagePolicy am Ziel, Weitergabe nur eigener Aktionen, Profilumfang,
Zeitraum, Widerruf und Diagnosesicht sind durch diese Quellen gedeckt.

**Änderung und Browser:** Aktuelle Vorschau für Benutzergruppe Werkstattleitung,
Holzwerkstatt, Grant administrator und Pflichtbegründung aufgenommen; Empfänger-,
Ressourcen- und Profilauswahl bis zur Vorschau praktisch durchlaufen. Aktivieren
war nach Begründung verfügbar; der Assistent wurde ohne Aktivieren geschlossen.
Kein Nachweis einer ausgeführten Vergabe oder eines Widerrufs.

**Bild:** `docs/administration/bilder/personen-technik-zustaendigkeit-vorschau-2026-11-03.png`,
visuell geprüft, ImageZoom mit Alttext. Eine erste Aufnahme enthielt während
paralleler Bearbeitung einen globalen MDX-Fehler und wurde vollständig durch die
saubere Aufnahme ersetzt.

## Zugangs-Tags

Datei: `docs/administration/tags-verwalten.mdx`.

**Entscheidung:** Unverändert gut. Bestehender Steps-Ablauf, Store-Badges,
Verlustwarnung und differenzierte Wiederherstellungshilfe bleiben erhalten.

**Quellen:** `web/app/[project]/dashboard/user-management/users/dialog/user-tags-tab.tsx`,
`web/components/tags/{enroll-tag-wizard,tag-summary,tag-rename-dialog,tag-loss-dialog}.tsx`,
`web/lib/stores/tag-store.ts`, `web/locales/de/devices.json`,
`api/Service/Tags/Boundary/HttpControllers/{TagEnrollmentController,TagsController}.cs`,
`api/Service/Tags/Boundary/Hubs/UserTagHub.cs`,
`api/Service/Tags/Application/Services/{TagEnrollmentService,TagsService}.cs`.
Zusätzlich die aktuellen Connect-Quellen unter
`/Users/lucaschoeneberg/Documents/GitHub/mardu_connect/lib/features/enrollment/`:
`logic/enrollment_controller.dart` und
`presentation/pages/{enroll_info_page,success_page}.dart`. Insbesondere die
Wiederholung nur des Serverabschlusses, der flüchtige Zustand in der laufenden
App und die deutschen Aktionsnamen sind erneut direkt gelesen; der ältere
Prüfbericht wurde nur zum Auffinden der Quellen verwendet.

**Browser:** Benutzer → Tags und erster Schritt von Zugangs-Tag zuweisen mit
optionalem Namen und 100-Zeichen-Hinweis geprüft. Vor Weiter abgebrochen; keine
Serveranmeldung erzeugt, kein QR-Code aufgenommen. Fünf-Minuten-Gültigkeit,
Admin-Grenze der Live-Rückmeldung, Sperre und Löschung sind Codebelege. Keine
Smartphone-, NFC-, Karten-, Leser-, App-Store- oder Verlustprüfung.

## Geräte

Datei: `docs/administration/geraete-verwalten.mdx`.

**Entscheidung:** Bestehende überarbeitete Anleitung erhalten, konkrete UI-Abweichungen
korrigieren und Anschlüsse zeigen.

**Quellen:**

- `web/app/[project]/dashboard/device-management/{device-management-page-client.tsx,device-settings/device-settings-sheet.tsx,device-settings/device-monitoring-tab.tsx}`.
- `web/components/device/{device-endpoints-panel,device-ota-history-panel}.tsx`,
  `web/components/metrics/{entity-metrics-view,metric-history-controls}.tsx`,
  `web/lib/device/device-status-utils.ts`, `web/locales/de/{devices,common}.json`.
- `api/Service/Devices/Boundary/HttpControllers/{DevicesController,DeviceController,DeviceEnrollmentController,DeviceEndpointConfigurationController,DeviceOtaHistoryController}.cs`.

**Änderungen:** Äußere Aktion heißt Änderungen speichern. Historienfilter präzisiert:
Geräteauswahl und Status gelten sofort; manuelle Ursprungs-ID und Zeitraum haben
jeweils Anwenden. Diagnose mit Einstieg, 24-Stunden-Vorgabe, Auflösung, Lücken,
Aktualisieren und kontoweit gespeicherter Geräteansicht beschrieben; vom festen
Sieben-Tage-Zeitraum der Benutzerstatistik unterschieden. Anschlussbild erklärt
fehlende bzw. ausstehende Bestätigung und unbekannten Hardwarezustand.

**Browser:** Testgerät door-r-holz geöffnet; Übersicht, Anschlüsse mit Leser/Aktor,
Ressourcenzuordnung, Auftragsstatus und Diagnose mit Letzte 24 Stunden/Automatisch
geprüft. Kein Auftrag gesendet oder gespeichert. Historienfilter und
Aufnahme-/Löschverhalten wurden im aktuellen Code gelesen, nicht ausgeführt.

**Bild:** `docs/administration/bilder/personen-technik-geraete-anschluesse-2026-11-03.png`,
visuell geprüft und mit Alttext eingebunden. Gerät ist offline und zeigt keine
bestätigte physische Funktion. Kein Controller, Edge-Router oder Leser wurde
angebunden; keinerlei Hardwareabnahme.

## Zugangsmetriken

Datei: `docs/administration/zutritt-verwalten.mdx`.

**Entscheidung:** Genaue Einstiegshilfe und aktuelle Aktualisieren-Aktion;
Kennzahlen, UTC-Erklärung und Sichtbarkeitsgrenzen bleiben erhalten.

**Quellen:** `web/app/[project]/dashboard/user-management/users/dialog/{edit-user-sheet,user-metrics-tab}.tsx`,
`web/components/metrics/{entity-metrics-view,access-activity-metrics}.tsx`,
`web/hooks/use-access-activity-metrics.ts`, `web/locales/de/{access,common,users}.json`,
`api/Service/Accesses/Boundary/Dto/ResourceAccessActivityMetricsDto.cs`,
`api/Service/Accesses/Application/Services/ResourceAccessActivityService.Metrics.cs`,
`api/Service/Accesses/Gateway/ResourceAccessActivityMetricsQuery.cs`.

**Änderungen und Browser:** Personen → Benutzer → Konto → Metriken praktisch
bestätigt. Die Seite behauptet keinen Einstieg über den historischen
Zutrittspunkt-Metrikreiter. Messwerte aktualisieren und abweichende Beschriftung
der Standardanzeige erklärt. Der leere Verlauf mit null Ereignissen, Strich bei
Erfolgsquote und null aktiven Sitzungen wurde im Browser gesehen. Nicht mit
positiven Protokolldaten, eingeschränkten Rechten oder einer laufenden physischen
Nutzung geprüft.

## Prüfungen und Grenzen

- Gezielte Format-, MDX-, Link-/Anker-/Bild- und Whitespaceprüfungen: siehe
  abschließende Prüfergebnisse unten.
- Browser: eigene Playwright-Sitzung `docs-revision-personen`, isolierter Zugang
  `http://localhost:3415/docs-revision`, deutscher Text, helles Theme, fiktive
  Daten. Nur lesende Schritte und nicht gespeicherte Dialogentwürfe.
- Kein globaler Build oder Serverstart, kein Commit, kein Stash oder Reset.
- Gemeinsames Produktrendering, Mobilansicht, Suche, Markdown-Ausgabe und zweite
  Consumer-Prüfung verbleiben beim Koordinator. Keine vollständige praktische
  Abnahme aller Benutzer-, Rollen-, Tag- oder Geräteabläufe behauptet.
- Produktbefund gemeldet: `user.metrics.sharedViewHint` behauptet weiterhin nur
  das äußere Speichern. Die aktuelle Oberfläche bietet zusätzlich die unmittelbar
  ausführende Aktion Ansicht speichern. Nur die Anleitung wurde berichtigt.

### Abschließende Prüfergebnisse

- `bun x --bun prettier --ignore-path /dev/null --check` für alle sechs
  Produktseiten und diesen Bericht: erfolgreich.
- `git diff --check -- <eigene sechs Seiten und Bericht>` im Doku-Repository:
  erfolgreich.
- Isolierte Kompilierung aller sechs Seiten mit installiertem `@mdx-js/mdx`:
  erfolgreich; kein globaler Build.
- Lokaler Quellencheck mit installiertem `github-slugger`: 59 relative Verweise,
  fünf Bildimporte und 97 bestehende Abschnittsanker gegen die Vorher-Snapshots
  geprüft; keine fehlenden Ziele oder verlorenen Anker. Das ist eine statische
  Prüfung und ersetzt nicht das gemeinsame Rendering des Koordinators.

## Strukturkorrektur nach unabhängigem Review

Die ausführliche Gruppenpflege wurde aus `benutzer-rollen.mdx` nach
`rollen-gruppen.mdx` übernommen und ergänzt. Nach der Gruppenanlage geht es direkt
zur lokalen Mitglieder-/Rollenauswahl; der bisherige Rückverweis zur Benutzerseite
entfällt. Der neue Ablauf beschreibt Übersicht, Mitglieder auswählen, Rollen
auswählen, Anwenden als Entwurf, Speichern sowie die Folgen des Entfernens und
möglicher Teilspeicherung. Namensprüfung und Create-plus-Update-Rechte bleiben
am kanonischen Ort. Die einzelne Person wird weiterhin über die Benutzerdetails
zu Rollen und bestehenden Gruppen zugeordnet.

Dafür erneut direkt gelesen: `UserGroupsController.cs`, `UserGroupRequests.cs`,
`UserGroupService.cs` und
`web/app/[project]/dashboard/user-management/settings/{user-group-details-sheet,user-group-form-dialog,user-group-row-actions}.tsx`.
Der Vertrag ersetzt Mitglieder- und Rollenlisten, speichert Gruppenangaben,
Mitglieder und Rollen nacheinander und lässt leere Auswahlen zu. Die Anleitung
behauptet keine atomare Gesamtänderung.

Auf der Benutzerseite bleiben die alten Anker `benutzergruppen-verwalten`,
`verlorenen-tag-sperren` und `tag-datensatz-löschen` als Sprungziele für die
kanonischen Verweise bestehen. Wiederholte Tag-Verlust-/Löschhinweise und der
zweite Metrik-Leseablauf sind verdichtet; beide Nutzeraufgaben bleiben direkt
verlinkt. Die eigene Aufgabe Metrikansicht anpassen samt aktuellem ImageZoom-Bild
bleibt erhalten. Für Zeitbezug, Zahlen und Sichtbarkeitsgrenzen führt ein Verweis
zur Metrik-Anleitung. Keine neue Seite oder Metadatenänderung.

Die ursprünglichen Browserbelege für Gruppenreiter und Mitgliederauswahl bleiben
gültig; in dieser Strukturkorrektur wurden keine weiteren Gruppenänderungen
praktisch ausgeführt. Erneute Format-, isolierte MDX-, Link-/Bild-/Anker- und
Whitespaceprüfung sind im Abschluss der Korrektur festgehalten.

### Parallel geänderte Aktivitätsoberfläche

Beim letzten Abgleich bindet `edit-user-sheet.tsx` weiterhin `UserMetricsTab` ein;
`use-access-activity-metrics.ts` lädt weiterhin `resourceAccessLogsMetrics` mit
RequesterId. Der parallel geänderte `ResourceActivityWorkspace` verwendet dagegen
`resourceAccessActivityList` und eigene Filter unter `resource-activity-query.ts`.
Die Metrikanleitung wird deshalb nicht zur Anleitung dieser Aktivitätstabelle
umgeschrieben. Die Browserbelege stammen aus dem bereitgestellten isolierten
API-Stand vor diesen parallelen Activity-Vertragsänderungen. Neue Activity-APIs,
Filter und Sitzungsaktionen sind hier weder praktisch geprüft noch abgenommen;
entsprechende Unterschiede zwischen aktuellem Checkout und Test-Image bleiben
eine gesonderte Prüfgrenze. Fremde Softwaredateien wurden nicht geändert.

### Checks der Strukturkorrektur

- Gezieltes Prettier-Check für beide erneut geänderten Seiten und den Bericht:
  erfolgreich.
- Isolierte MDX-Kompilierung von Benutzer- und Rollen-/Gruppenseite: erfolgreich.
- Scoped `git diff --check`: erfolgreich.
- Erneuter statischer Check aller sechs Paketseiten: 61 relative Verweise,
  fünf Bildimporte und alle 97 ursprünglichen Abschnittsanker ohne Fehler.
