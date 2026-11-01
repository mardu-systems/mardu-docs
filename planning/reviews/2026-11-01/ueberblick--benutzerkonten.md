# P44 – Benutzerkonten, Rollen und Zugänge

## Änderungsbrief

Leserfrage: Wie hängen das Konto einer Person, Dashboard-Rechte und die Nutzung
von Ressourcen zusammen? Leser kennen noch keine Mardu-Begriffe; sie sollen die
Zuordnungen unterscheiden können. Heimat bleibt **Überblick**. Die bestehende
Erklärung mit ihren drei getrennten Prüfungen, Kontoentstehung und Deaktivierung
bleibt erhalten. Nach statischem Abgleich mit Identity, Zugriffsentscheidung und
Qualifikationsportal werden nur die fehlende Buchungsabgrenzung und der
Unterschied zwischen Einweisung und Badge ergänzt; die nicht mehr belegte
Zutrittspunktgruppen-Erklärung entfällt. Vorhandene Überschriften und URL bleiben
erhalten. Prüfen: gezieltes Format, MDX-Kompilierung, Links und bestehende Anker;
Consumer-Darstellung übernimmt der Koordinator. Keine Software- oder API-Änderung.

## Entscheidung: verbessert

Die Seite erklärt bereits verständlich Person/Konto, Anmeldung, Rollenrechte und
Ressourcennutzung. Diese Grundstruktur, alle sechs Überschriften und vorhandenen
Anker bleiben erhalten. Kontoentstehung, Mehrfachzuweisung von Rollen,
Deaktivierung und persönliche Sicht wurden gegen Code geprüft und beibehalten.

Die Sammelzeile „Fähigkeiten und Badges“ wurde in gültige lokale Einweisungen und
Badges/importierte Nachweise aufgeteilt. Buchungen werden als Reservierungen mit
gesonderter möglicher Zugriffswirkung erklärt. „Zugänge“ heißt in der Tabelle nun
„Ressourcenfreigaben“ und nennt die unterstützten Empfänger. Ein kurzer Absatz
erklärt die Kombination von Freigabe, Buchung und weiteren Bedingungen. Persönliche
Detailanleitungen werden direkt verlinkt, statt ihre Abläufe zu wiederholen.
Bei externen Anmeldungen wird die fortbestehende Zuordnung zum Mardu-Konto klarer.

Die Erklärung zu Zutrittspunktgruppen wurde entfernt: Die aktuelle Entscheidung
verwendet Ressourcen und Personen-/Gruppen-/Tagfreigaben, während die alten
Gruppenlader leere Ergebnisse liefern. Verbliebene Übersetzungen oder alte
Komponenten allein belegen keine verwendbare Funktion. Keine neue technische
Begriffsebene, Komponenten oder Bilder ergänzt.

## Fachliche Quellen

Alle Pfade beziehen sich auf das Software-Repository.

- `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:689` und
  `:729`: Kontostatus, Bestätigung und zusätzliche Anmeldebedingungen.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.Invite.cs:14`,
  `UserService.CreateUpdate.cs:215` und
  `api/Framework/Infrastructure/Identity/SelfRegistration/Services/SelfRegistrationService.cs:55`:
  Einladung, Passwortanlage, Registrierung und Freigabe.
- `api/Framework/Infrastructure/Identity/External/LdapSyncService.cs:49` und `:91`,
  `api/Framework/Infrastructure/Auth/Application/OidcBrokerService.cs:319` und
  `:378`: externe Kontoanlage und richtlinienabhängige Freigabe.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.cs:385` und
  `UserService.CreateUpdate.cs:481`: extern verwaltete Felder;
  `api/Framework/Infrastructure/Identity/Users/Entity/OidcExternalIdentity.cs:23`:
  Verknüpfung mit einem Mardu-Benutzer.
- `api/Framework/Infrastructure/Identity/Permissions/PermissionService.cs:111`
  und `:170`: direkte Rollen, Gruppenrollen und Quellen.
  `web/app/[project]/dashboard/user-management/users/dialog/user-authorization-tab.tsx:313`
  und `web/locales/de/users.json:156`: „Effektive Berechtigungen“.
- `api/Service/Accesses/Application/Services/ResourceAccessDecisionService.cs:752`,
  `:820` und `:1004`: Freigabe/Buchung, lokale Kompetenzanerkennung, Aufsicht und
  Empfänger Person/Benutzergruppe/Tag.
- `api/Service/Bookings/Gateway/BookingSpecifications.cs:23`: bestätigte Buchung
  nur mit explizitem Ressourcen-Zugriffsziel und passendem Zeitraum als Nachweis.
- `api/Service/Competencies/Entity/CompetencyGrant.cs:10` und
  `BadgeAward.cs:8`; `web/components/portal/portal-qualifications.tsx:51` und
  `web/locales/de/competencies.json:339`: Einweisungen, lokale Badges und
  importierte/signierte Nachweise sind getrennt; kein automatischer Ressourcenzugang.
- `api/Service/Accesses/Boundary/EventConsumers/ProtocolDeviceAccessConsumer.cs:24`:
  Tag-Zuordnung, Status und Gültigkeit vor der personenbezogenen Entscheidung.
- `api/Framework/Infrastructure/Identity/Users/Services/UserService.cs:324`:
  Deaktivierung ändert den Kontostatus; keine unmittelbare Beendigung bestehender
  Sitzungen oder Entfernung der Zuordnungen.
- `api/Service/Accesses/Application/Services/ResourceAccessAuthorizationService.cs:26`
  und `api/Service/Notifications/Application/Services/NotificationAudienceService.cs:108`:
  Verwaltungszuständigkeiten und Empfänger von Betriebsereignissen werden getrennt
  von persönlicher Nutzung geprüft.
- `api/Service/Bookings/Application/Services/BookingService.cs:34` und
  `web/components/portal/portal-qualifications.tsx:51`: persönliche Datenansichten.
- `web/lib/access/async-loaders.ts:294`: alte Zutrittspunktgruppen-Lader liefern
  leere Ergebnisse; kein belegbarer aktueller Bedienweg für diese Seitenerklärung.

Kontext: bestehende Anleitungen `benutzer/kompetenzen.mdx`, `benutzer/zutritt.mdx`,
`benutzer/buchungen.mdx`, `administration/benutzer-rollen.mdx` und
`koordination/ressourcen.mdx`. Der gemeinsame Backlog enthält keinen eigenen
offenen Auftrag für diese Überblicksseite.

## Ausgeführte Prüfungen und Grenzen

- Einzeldatei-Kompilierung mit installiertem `@mdx-js/mdx` und `remark-gfm`: bestanden.
- Lokale Link- und Fragmentprüfung: alle 12 Verweise auflösbar; alle sechs
  bestehenden Überschriftenanker erhalten.
- Gezielter vorhandener Prettier mit `--ignore-path /dev/null --check` für beide
  Dateien: bestanden. Der explizite Override ist nötig, weil der Software-Consumer
  das Docs-Submodule generell ignoriert.
- `git -C web/content/docs diff --check -- docs/ueberblick/benutzerkonten.mdx planning/reviews/2026-11-01/ueberblick--benutzerkonten.md`:
  bestanden.

Nur statisch geprüft. Keine angemeldete Browserprüfung, Anbieteranmeldung,
Hardwareprüfung oder Consumer-Abnahme behauptet. Der Koordinator prüft die
Darstellung der erweiterten Begriffstabelle, insbesondere mobil, sowie die
Consumer-Navigation. Website-Consumer nicht ausgeführt. Keine Backend-/Frontend-
Builds, globalen Tests oder Softwareänderungen; API-/DTO-Dokumentation unverändert.

Koordinationshinweis: Alte Zutrittspunktgruppen-Texte existieren noch in
Übersetzungen und Hilfskomponenten. Daraus hier keine weitere Anleitung ableiten;
Bereinigung wäre ein separater Softwareauftrag. Kein zusätzlicher Seitenbedarf.

## Geänderte Dateien

- `web/content/docs/docs/ueberblick/benutzerkonten.mdx`
- `web/content/docs/planning/reviews/2026-11-01/ueberblick--benutzerkonten.md`
