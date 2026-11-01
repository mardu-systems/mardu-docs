# P15 – Benachrichtigungseinstellungen

Änderungsbrief: Anleitung für angemeldete Personen, die ihre eigenen Kanäle,
Ereignisse, Ruhezeiten und Stummschaltungen einstellen. Heimat bleibt Überblick,
URL und bestehende Überschriften/Anker bleiben erhalten. Vorhandene Speicher- und
Rechtehinweise werden bewahrt; Einstieg, Zustellvoraussetzungen, Ruhezeitwirkung
sowie Grenzen von Browserpush und Zusammenfassungen werden anhand UI/Backend
präzisiert. Prüfung: statischer Quellenabgleich, gezielter Format- und Linkcheck;
Browser-/Providerprüfung übernimmt die gemeinsame Abnahme.

**Entscheidung: verbessert; zur gemeinsamen Prüfung.** Gültige Rechte-,
Schnellauswahl- und Entwurfshinweise erhalten. Präzisiert wurden Kanal- und
Ereignisauswahl, Pflichtkanäle trotz ausgeschaltetem Hauptkanal, bestätigte
Kontaktdaten, Ruhezeitwirkung, Mute-Auswahl und Aufheben, Speicherkonflikt sowie
Entwurfsverlust bei Rechteänderung. Browser-Abos und Digest sind als im Formular
nicht bedienbar eingegrenzt, statt nicht vorhandene Einrichtungsschritte zu nennen.

## Quellen im Software-Repository

- Einstieg: `web/components/layout/common/account-menu-items.tsx:19–41`,
  `web/locales/de/navigation.json:32`,
  `web/components/layout/settings/profile-nav.config.ts:141–155`.
- Gemeinsames Portalformular:
  `web/app/[project]/portal/profile/notifications/page.tsx:1`.
  Formular `web/app/[project]/dashboard/user-management/profile/notifications/notifications-form.tsx`:
  Zeilen 99–125 erhalten vorhandene Kanal-/Digestwerte; 236–247 laden nach
  Rechteänderung neu; 365–390 Schnellauswahl; 394–449 validieren/speichern mit
  ETag und erhalten bei Fehler den Entwurf; 541–574 Konflikt/Verwerfen/Speichern;
  579–724 Kanal- und Mute-Auswahl. Gesamtes Formular: keine Digeststeuerung oder
  Browser-Abo-Verwaltung. `web/components/profile/profile-draft-provider.tsx:96–197`
  schützt interne Wechsel, Neuladen und soweit abbrechbar Browserhistorie.
- Rechte und Katalog:
  `api/Service/Notifications/Boundary/HttpControllers/NotificationPreferencesController.cs:38–69,137–192`
  (Profile View/Update, aktuelle Empfangsrechte, Anbieterstatus).
  `api/Service/Notifications/Application/Services/NotificationChannelAvailabilityService.cs:35–56`
  (bestätigte E-Mail/Telefonnummer bzw. gespeichertes Push-Abo).
- Wirkung: `api/Service/Notifications/Application/Policy/NotificationPolicyEngine.cs:51–146`
  prüft Anbieter/Endpunkt vor Pflichtkanal; danach Hauptkanal, Ereignis, Mute,
  E-Mail-Digest und Ruhezeit.
  `api/Service/Notifications/Application/Services/NotificationProcessor.cs:183–252`
  hält In-App sichtbar und unterdrückt dessen Echtzeithinweis während Ruhezeiten.
  `web/lib/notifications/notification-realtime-client.ts:90–135` koppelt Ton an
  den Echtzeithinweis. Beispielkatalog:
  `api/Service/Notifications/Application/Catalog/NotificationCatalog.Security.cs:7–25`
  und `NotificationCatalog.Access.cs:7–25`.
- Backendgrenzen: `api/Service/Notifications/Boundary/HttpControllers/PushSubscriptionsController.cs:45–102`
  bietet separate Abo-APIs; keine Registrierung durch die Kanalauswahl.
  `api/Service/Notifications/Application/Services/NotificationPreferenceService.cs:44–132`
  schützt Revision und erhält ausgeblendete Ereignis-/Mutepräferenzen.

## Checks und Grenzen

- `bun fmt --check` nur für die beiden zugewiesenen Dateien: erfolgreich.
- `git diff --check`: erfolgreich. Bestehende drei Überschriften/Anker erhalten;
  relativer Link zum vorhandenen Posteingangsabschnitt geprüft.
- Keine Software-/API-/DTO-Änderung, daher keine angepasste Vertragsdokumentation
  und keine Builds oder Softwaretests. Keine Nachrichten ausgelöst.
- Nur statischer Quellenabgleich. Gemeinsame Consumerprüfung: Seite rendern und
  den Kontomenü-Einstieg sowie Speichern/Verwerfen/Konflikt praktisch prüfen.
  Browser-Erlaubnis, Abo und realer Push-/Mail-/SMS-Empfang bleiben ungeprüft.
- Koordination: Nachbarseite `docs/ueberblick/profil.mdx` hat noch den Einstieg
  „Mein Profil“; dortige Überarbeitung abstimmen. Bestehender eingehender Anker
  aus `docs/administration/benachrichtigungen-verwalten.mdx` bleibt gültig.
  Kein Bedarf für eine weitere Produktseite aus diesem Auftrag.

Geändert: `docs/ueberblick/profil-benachrichtigungen.mdx` und dieser Bericht.
