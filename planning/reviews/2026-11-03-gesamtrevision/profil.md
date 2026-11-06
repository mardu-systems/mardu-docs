# Profilpaket: Gesamtrevision vom 3. November 2026

Stand: **zur Prüfung**. Alle zehn zugewiesenen Seiten wurden einzeln gegen aktuelle
UI-Quellen und die jeweiligen Backend-Verträge gelesen. Sechs Seiten geändert,
vier bereits passende Seiten bewusst erhalten. Keine Software-, API-, DTO- oder
Navigationsänderung; keine Commits, Builds oder Serverstarts.

## Gemeinsame Grundlage und Prüfungen

- Auftrag und Änderungsbrief: `planning/2026-11-03-gesamtrevision.md`,
  `planning/2026-11-03-gesamtrevision-agentenbrief.md`, `AGENTS.md` und
  `ARBEITSWEISE.md`; Gestaltungsmuster: `administration/freigaben-verwalten.mdx`
  und `administration/ressourcen-buchbarkeit.mdx`.
- Fumadocs `ImageZoom`, `Step`/`Steps`, vorhandene `Callout`-Einbindung und
  Markdown-Tabellen wiederverwendet. Keine eigene Komponente oder Darstellung.
- Alle bisherigen Überschriften wurden mit `git show HEAD:docs/<seite>`
  abgeglichen: keine entfernt oder umbenannt. Damit bleiben die bisherigen
  automatisch erzeugten Heading-Anker erhalten. Relative Dateiziele und
  Bildimporte aller zehn Seiten wurden auf Existenz geprüft.
- `bun x --bun prettier --ignore-path /dev/null --check` für alle zehn Seiten
  erfolgreich. Scoped `git diff --check` erfolgreich. Abschließender Check einschließlich
  Bericht und neuen Bildimporten ebenfalls erfolgreich.
- Browser: eigene Playwright-Session `docs-revision-profil`, isoliertes Frontend
  `http://localhost:3415/docs-revision`, API-Port 35116, ausschließlich fiktive
  Seed-Daten. Mobil 390 px, Desktop 1440 px. Keine MFA-/Passkey-Aktivierung,
  keine Sitzung widerrufen, kein Token erzeugt, keine Verbindung zu einem externen
  Anbieter hergestellt, keine gespeicherten Benachrichtigungseinstellungen geändert.
- Doku-Rendering, gerenderte historische IDs, Suche, Markdown-/Agentenausgabe und
  beide Consumer werden zentral durch die Koordination geprüft. Die bisherigen
  Überschriften allein belegen diese Darstellung nicht.

## `ueberblick/benutzerkonten.mdx` — erhalten

Leserfrage: Wie entstehen Konten und wie unterscheiden sich Anmeldung,
Dashboard-Rechte und Ressourcennutzung? Bestehende Tabellen und Querverweise
beantworten die Fragen bereits ohne unnötige Komponenten.

Quellen im Software-Repository:
`api/Framework/Infrastructure/Identity/Users/Services/UserService.Invite.cs`,
`UserService.CreateUpdate.cs`,
`api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs`,
`api/Framework/Infrastructure/Identity/External/LdapSyncService.cs`,
`api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs`.
Geprüft: Einladung mit nachfolgender Freigabe, getrennte Kontobedingungen und
Rollen-/Gruppenquellen. Keine neue Anmeldung, LDAP-Synchronisierung oder externe
Kontoanlage praktisch ausgeführt; keine vollständige Zutrittsabnahme.

## `ueberblick/fehlersuche.mdx` — erhalten

Leserfrage: Welcher nächste Schritt passt zum sichtbaren Problem? Die nach
Symptomen gegliederte Fehlerhilfe bleibt erhalten; sie unterscheidet bereits
fehlende Rechte, Ladefehler, Anbieter-Verbindung, Nachweis und Ressourcenfreigabe.

Quellen: `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs`,
`api/Framework/Infrastructure/Identity/Users/Services/UserService.Password.cs`,
`api/Service/Notifications/Application/Services/NotificationChannelAvailabilityService.cs`,
`api/Service/Interoperability/Boundary/ProfileBadgeProvidersController.cs`,
`web/components/profile/profile-draft-provider.tsx`,
`web/components/integrations/openbadges/profile-provider-connections.tsx`.
Der Benachrichtigungsentwurf und sein Verwerfen-Dialog wurden praktisch geprüft;
Anmeldefehler, externe Zustellung, Buchungskonflikte und Hardwarefehler nicht neu
herbeigeführt.

## `ueberblick/profil-benachrichtigungen.mdx` — geändert

Leserfrage: Welche Kanalwahl wird gespeichert und was braucht eine Zustellung?
Voraussetzungen für E-Mail, SMS und Web Push in einer Tabelle verdichtet,
Pflichtkanäle als sichtbaren Callout herausgestellt. Den Hinweis auf im Formular
nicht angebotene Digest-Einstellungen entfernt; er beschreibt keine ausführbare
Aufgabe. Ruhezeiten, Konfliktbehandlung und Grenzen externer Zustellung erhalten.

Quellen: `web/app/[project]/dashboard/user-management/profile/notifications/notifications-form.tsx`,
`notification-quiet-hours.tsx`, `web/locales/de/settings.json`,
`api/Service/Notifications/Boundary/HttpControllers/NotificationPreferencesController.cs`,
`api/Service/Notifications/Boundary/Dtos/NotificationPreferenceDtos.cs`,
`api/Service/Notifications/Application/Services/NotificationPreferenceService.cs`,
`NotificationChannelAvailabilityService.cs`.

Browser: Kanalverfügbarkeit und Ereignisfilter geprüft. Web Push im Entwurf
kurz ausgeschaltet; Speicherleiste, deaktivierte Ereigniskanäle und Dialog
**Ungespeicherte Änderungen?** geprüft, anschließend **Änderungen verwerfen**
bestätigt. Kein Speichern. Neuer Screenshot
`ueberblick/bilder/profil-benachrichtigungen-kanaele-aktuell.png` zeigt tatsächliche
Testkanäle und Ruhezeiten, mit `ImageZoom` eingebunden und visuell geprüft.
Kein Versand- oder Push-Abotest; E-Mail und SMS sind im Testserver nicht verfügbar.

## `ueberblick/profil-erscheinungsbild.mdx` — Darstellung verbessert

Leserfrage: Was gilt sofort im Browser, was wird am Konto gespeichert?
Kurzen, passenden Inhalt erhalten; die weiterhin passende Theme-Aufnahme mit
nativem `ImageZoom` statt einfachem Markdown-Bild eingebunden.

Quellen: `web/app/[project]/dashboard/user-management/profile/appearance/page.tsx`,
`web/hooks/use-format-settings.ts`, `web/hooks/use-accessibility.ts`,
`web/app/[project]/dashboard/user-management/profile/account/account-form.tsx`,
`web/lib/i18n.tsx`. Browser: Theme-Wahl, Bedienhilfen, Format-Auswahlen und
Browserzeitzone gelesen. Keine vollständige Persistenz-/Mehrbrowserprüfung;
Kontosprache und Kontozeitzone nicht verändert.

## `ueberblick/profil-mcp.mdx` — Darstellung und Eingabegrenzen verbessert

Leserfrage: Wie erstelle ich einen persönlichen Zugang und richte den Client ein?
Diese beiden Phasen mit nativen `Steps` gegliedert. Einmalanzeige und sofortiger
Tokenwechsel als Callouts; Pflichtname und Laufzeit präzisiert. Bestehende, gegen
UI-Code und Bildinhalt geprüfte Bilder mit `ImageZoom` eingebunden. Widerrufsfolge
und Berechtigungsgrenzen erhalten.

Quellen: `web/app/[project]/dashboard/user-management/profile/mcp/page.tsx`,
`use-profile-mcp-controller.ts`, `web/locales/de/settings.json`,
`api/Service/Mcp/Boundary/Dto/McpAgentConnectionDtos.cs`,
`api/Service/Mcp/Boundary/HttpControllers/McpAgentConnectionsController.cs`,
`api/Service/Mcp/Application/McpAgentConnectionService.cs`.
Laufzeit 1–365 Tage und zusätzliche Serverobergrenze, Rotation ohne Änderung des
Ablaufdatums sowie dauerhafter Widerruf im Code abgeglichen. Browser nach Wiederherstellung: Liste mit **0 aktive Verbindungen** sowie
Erstellen-Dialog mit Name, Laufzeit und angebotenen Berechtigungen geprüft;
**Token erstellen** ohne Eingaben deaktiviert, Dialog abgebrochen. Keine
Token-Ausgabe, Clientverbindung oder Rotation praktisch geprüft. Ein erster
Browseraufruf wurde durch eine globale, außerhalb dieses Pakets liegende
MDX-Kompilierungsstörung unterbrochen (siehe unten).

## `ueberblick/profil-nachweisquellen.mdx` — erhalten

Leserfrage: Wann melde ich mich beim Anbieter an und wann hinterlege ich einen
persönlichen API-Zugang? Die Anleitung trennt beide Wege, Import und Anmeldung
bereits korrekt. Verbindungswechsel, Trennen und Folgen bleiben erhalten.

Quellen: `web/app/[project]/dashboard/user-management/profile/openbadges/page.tsx`,
`use-openbadges-link.ts`,
`web/components/integrations/openbadges/profile-provider-connections.tsx`,
`web/locales/de/badges.json`,
`api/Service/Interoperability/Boundary/ProfileBadgeProvidersController.cs`,
`api/Service/OpenBadges/Boundary/ProfileOpenBadgesLinkController.cs`.
Browser: Tab **Anbieter** mit **Keine Anbieter verfügbar** und Tab **Persönlicher
API-Zugang** mit Benutzerreferenz, Tokenfeld und deaktiviertem **Prüfen und
verbinden** ohne Eingaben geprüft. Kein externer Anbieter konfiguriert;
Anmeldung, Prüfung eines persönlichen Tokens und Import nicht praktisch abgenommen.

## `ueberblick/profil-sicherheit.mdx` — Folgen hervorgehoben

Leserfrage: Wie ändere ich einen Anmeldeweg, ohne den Zugang zu verlieren?
Passkey-Deaktivierung bei 2FA-Aktivierung und Austausch aller Recovery-Codes
mit sichtbaren Warn-Callouts an der betreffenden Aktion hervorgehoben.
Vorhandene Bilder mit `ImageZoom` eingebunden; sonst gute Abläufe erhalten.

Quellen: `web/app/[project]/dashboard/user-management/profile/authentication/page.tsx`,
`two-factor-setup.tsx`, `disable-two-factor-button.tsx`,
`web/components/profile/change-email-dialog.tsx`, `passkey-card.tsx`,
`RecoveryCodesDialog.tsx`,
`api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs`,
`api/Framework/Infrastructure/Identity/Users/Services/UserService.TwoFactor.cs`,
`UserService.Password.cs`, `UserService.EmailChange.cs`.
Browser: Sicherheitskarten und vorhandene Aktionen gelesen. Kein QR-Code oder
Recovery-Codesatz erzeugt, keine E-Mail versandt, kein Passwort oder Faktor
geändert. WebAuthn-/Anbieterabnahme bleibt offen.

## `ueberblick/profil-sitzungen.mdx` — aktuelle Bedienung und neues Bild

Leserfrage: Wie erkenne und widerrufe ich eine eigene Sitzung?
Den veralteten Select **Alle Geräte** durch die aktuelle Gerätefilter-Bedienung
ersetzt und mobile Sortierauswahlen ergänzt. Folge von **Alle abmelden** als
Warn-Callout. Screenshot durch
`ueberblick/bilder/profil-sitzungen-aktuell.png` ersetzt und mit `ImageZoom`
eingebunden. Bild zeigt die echte isolierte Laufzeit mit markierter eigener und
weiteren Testsitzungen; fehlende Browser-/OS-Angaben wurden nicht nachgezeichnet.

Quellen: `web/app/[project]/dashboard/user-management/profile/sessions/page.tsx`,
`api/Framework/Infrastructure/Identity/Users/Boundary/ProfileSessionsController.cs`.
Browser: aktuelle Liste, Suche, Filterbutton, Kennzeichnung **Aktuell**, deaktiviertes
**Dieses Gerät**, Widerrufsaktionen und Screenshot geprüft. Keine Sitzung
widerrufen, insbesondere keine gemeinsam verwendete Testsitzung. Weitere
API-Anfragen nach Widerruf nicht praktisch geprüft.

## `ueberblick/profil-zutrittsmedien.mdx` — erhalten

Leserfrage: Wie erkenne ich mein Medium, seine Gültigkeit und einen Verluststatus?
Die vorhandene kompakte Anleitung und Statustabelle stimmen mit den gelesenen
Quellen überein; keine rein dekorative Komponente hinzugefügt.

Quellen: `web/components/profile/profile-access-media.tsx`,
`web/components/tags/tag-summary.tsx`, `web/lib/tags/status.ts`,
`api/Service/Tags/Boundary/HttpControllers/ProfileTagsController.cs`,
`api/Service/Tags/Boundary/HttpControllers/TagsController.cs`,
`api/Service/Tags/Application/Services/TagsService.cs`,
`api/Service/Accesses/Boundary/EventConsumers/ProtocolDeviceAccessConsumer.cs`.
Browser: Seite mit **Karten & Transponder**, Suchfeld, **Neu laden** und
abschließendem Leerzustand **Keine Zutrittsmedien zugeordnet** geprüft.
Statusdarstellung und Verlustfolge durch Codeabgleich, nicht durch eine neue
praktische Medien-/Leserprüfung belegt. Kein NFC-Medium oder physischer Leser
geprüft.

## `ueberblick/profil.mdx` — falschen Suchablauf korrigiert und verdichtet

Leserfrage: Wo finde und speichere ich eigene Angaben und Einstellungen?
Die frühere Beschreibung eines direkten Suchfelds und einer zweiten Dialogansicht
stimmte nicht mehr mit der UI überein. Auf den tatsächlichen Ablauf **Profil
durchsuchen → Suchdialog → Abschnitt** reduziert. Rechte, getrenntes Speichern,
Suchumfang, Tastaturbedienung und Entwurfsschutz erhalten.

Alte Navigationsaufnahme ohne Suchbutton durch
`ueberblick/bilder/profil-navigation-mobil-aktuell.png` ersetzt. Neues Bild zeigt
den echten mobilen Profilbereich ohne Devtools-Überlagerung. Kontaktbild mit
überholtem E-Mail-Hinweis entfernt; die beschrifteten aktuellen Felder benötigen
keine eigene weitere Abbildung. Weiterhin passenden Avatar-Ausschnitt mit
`ImageZoom` erhalten.

Quellen: `web/components/profile/profile-settings-layout.tsx`,
`web/components/layout/settings/settings-search.tsx`,
`profile-nav.config.ts`, `web/lib/settings/search.ts`,
`web/hooks/use-settings-search-query.ts`,
`web/app/[project]/dashboard/user-management/profile/profile-form.tsx`,
`account/account-form.tsx`, `web/components/profile/profile-avatar-editor.tsx`,
`avatar-editor.tsx`,
`api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs`.
Browser: Mobilnavigation sowie Suchdialog mit **Handynummer**, passender Treffer
**Kontaktinformationen** und anschließender Navigation nach
`/portal/profile/details#contact-info` geprüft. Kontaktfelder und getrennte
Speicheraktionen gelesen. Keine Kontodaten oder Bilder gespeichert.

## Separater Produktbefund

`web/lib/users/nullable.ts` bildet geleerte Angaben über `toNullable(...)` auf
`null` ab. Die Profilformulare `profile-form.tsx` und `account/account-form.tsx`
verwenden diesen Mapper. Der aktuelle Vertrag in `ProfileController.UpdateProfile`
und die Implementierung in `UserService.CreateUpdate.cs` behalten bei `null`
den gespeicherten Wert; erst ein Leerstring entfernt optionale Angaben.
Das Leeren beispielsweise von Telefonnummer oder Anzeigename kann damit im
Formular als erfolgreich gespeichert erscheinen, ohne den gespeicherten Wert
zu entfernen. Keine Softwareänderung im Doku-Auftrag und keine zusätzliche
Löschfunktion dokumentiert. Durch Quellenvergleich belegt, nicht durch Mutation
des gemeinsam genutzten Testkontos reproduziert; dem Koordinator gemeldet.

## Transiente Prüfunterbrechungen

Globale MDX-Kompilierung wurde während paralleler Arbeit zweimal unterbrochen:
fehlendes `server-einstellungen-global-aktuell.png`, später eine ungültige MDX-Zeile
67 in `administration/verwaltungszustaendigkeiten.mdx`. Beides liegt außerhalb der
zugewiesenen Dateien; keine Fremddatei geändert. Beide Störungen wurden zentral
behoben und die Browserprüfung erfolgreich fortgesetzt. Ein automatischer
Mehrseiten-Leselauf traf außerdem eine laufende Navigation und wurde nicht als
Prüfnachweis gezählt. Erfolgreiche Einzelprüfungen stehen jeweils oben.
