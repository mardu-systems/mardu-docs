# Querschnittsprüfung: Profil, Identität und Verwaltungsrechte

Read-only-Prüfung der Produktseiten und ihrer Seitenberichte vom 2026-11-01
nach `AGENTS.md` und `ARBEITSWEISE.md`. Schwerpunkt: gegenseitige Aussagen zu
Konten, Rollen und Gruppen, Verwaltungszuständigkeiten, LDAP/OIDC,
Anmeldevorgaben, Sitzungen, MCP und persönlichen Nachweisquellen. Abgleich mit
den vorhandenen UI-/Backendquellen; keine Browser- oder Anbieterabnahme.

## Wesentlicher Restfehler

### LDAP: Administratorausnahme umfasst keine Gruppenrollen

- **Seite:** `docs/administration/ldap-verzeichnis.mdx:111–113`.
- **Aussage:** „Konten mit der Administratorrolle werden dabei übersprungen.“
  Zusammen mit dem auf `docs/administration/rollen-gruppen.mdx:6–9`
  beschriebenen Rollenmodell schließt das auch Personen ein, die **Admin** nur
  über eine Benutzergruppe erhalten. Für solche LDAP-Konten ist die Ausnahme
  jedoch nicht implementiert. Bei fehlendem Verzeichniseintrag kann daher trotz
  ihrer effektiven Administratorrolle die gewählte Deaktivierung oder Löschung
  ausgeführt werden. Die pauschale Schutzbehauptung ist vor einem destruktiven
  Abgleich wesentlich.
- **Belege im Software-Repository:**
  `api/framework/Infrastructure/Identity/External/LdapSyncService.cs:180–185`
  prüft ausschließlich `userManager.IsInRoleAsync(user, Admin)`; die nachfolgenden
  Zweige `:196–224` deaktivieren beziehungsweise löschen das Konto. Identity
  verwendet den normalen EF-Store
  (`api/framework/Infrastructure/Identity/IdentityExtensions.cs:19–32`). Die
  zusätzliche Zusammenführung direkter und gruppenbasierter Rollen geschieht
  dagegen ausdrücklich in
  `api/framework/Infrastructure/Identity/Permissions/PermissionService.cs:62–72,169–183`;
  dieser Dienst wird für die LDAP-Ausnahme nicht verwendet.
- **Minimaler Korrekturvorschlag:** Den Absatz ersetzen durch:
  „Diese Behandlung betrifft LDAP-Konten. Übersprungen werden Konten mit direkt
  zugewiesener Rolle **Admin**; eine ausschließlich über Benutzergruppen
  erhaltene Admin-Rolle schützt derzeit nicht vor dieser Behandlung. Prüfe diese
  Konten vor einem Abgleich mit **Deaktivieren** oder **Dauerhaft löschen**
  gesondert. Ein Rollenentzug durch Gruppenregeln ist davon zu unterscheiden.“
- **Einordnung:** Produktabweichung separat verfolgen; für diese Doku-Abnahme
  genügt die belegte Einschränkung der vorhandenen Schutzbehauptung. Kein
  Softwarefix Bestandteil dieser Prüfung.

## Übriges Ergebnis und Grenzen

Keine weiteren wesentlichen Restwidersprüche für diesen Prüfzuschnitt belegt.
Die bereits der Koordination bekannten LDAP-/OIDC-Rechte in
`server-einstellungen.mdx` und die zu starke technische Erfolgstestbedingung in
`integrationen.mdx#ldap` sind hier nicht erneut als Findings aufgenommen.
Ebenso keine erneuten Findings zu den in den Seitenberichten bereits erfassten
OIDC-Test-/Produktivunterschieden, Vorschaugrenzen, Recovery-/Passkey-Konflikten
oder OpenBadges-Aktivierungsfehlern, soweit die Anleitungen das Verhalten
einschränken und keinen erfolgreichen Ablauf für die fehlerhafte Kombination
versprechen.

Geändert wurde ausschließlich dieser Bericht. Keine Produktdateien, API-/DTO-
Dokumentation oder Software geändert; keine Tests, Builds, Commits oder externen
Aktionen ausgeführt. Codelektüre belegt die oben genannte Abweichung, keine
praktische Reproduktion.
