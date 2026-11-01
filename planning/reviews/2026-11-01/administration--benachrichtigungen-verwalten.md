# Seitenrevision P24: Benachrichtigungen einrichten und prüfen

## Änderungsbrief

Leserfrage: Wie bereite ich Zustellkanäle vor, prüfe SMTP und untersuche fehlende
Mitteilungen? Zielgruppe sind Personen mit Einstellungsrechten und Kenntnis der
Mailanbieter-Zugangsdaten. Heimatbereich bleibt Administration. Die bereits
praktisch geprüfte Anleitung und ihre SMTP-Schritte bleiben erhalten. Der
statische Abgleich präzisiert nur die Grenze zwischen hinterlegten Digest-Werten
und vorhandener Profiloberfläche sowie zwischen technischen Zustellstatus und
sichtbaren Dashboardinformationen. Keine Produkt-, API- oder DTO-Änderung.

## Ergebnis: verbessert

- SMTP-Schritte, STARTTLS/Zertifikatsvoraussetzung, Anmeldungspflicht,
  Passwortbeibehaltung, Hot Reload, Rechte und Trennung von SMTP-Übergabe und
  tatsächlichem Empfang sind weiterhin belegt und erhalten.
- Zusammenfassungen werden als gegebenenfalls bereits hinterlegte Einstellung
  erklärt. Das Profilformular bietet weder Modus/Zeit noch Browser-Aboverwaltung.
- Die Fehlersuche unterscheidet technische Zustellstatus von den im Dashboard
  verfügbaren Kennungen und aggregierten Metriken; kein erfundener Einzelstatus-
  oder Wiederholungsdialog. Ein Versandauftrag belegt keinen externen Empfang.
- Ereignisregeln, Pflichtkanal für Passwortänderung, Verfügbarkeit vor Pflicht,
  Ruhezeiten, sofortiger In-App-Inhalt und minütliche Worker-Verarbeitung stimmen
  mit den Quellen überein. Keine neue Struktur oder neue Komponenten erforderlich.

## Quellen

Pfade relativ zum Repository, relevante Symbole beziehungsweise Abschnitte:

- `web/app/[project]/dashboard/admin/server/mail-settings/page.tsx`:
  `MailSettingsAdminPage`, Felder und gespeicherter Testversand;
  `use-mail-settings-controller.ts`: `save`, `sendTest`;
  `mail-settings.utils.ts`: `buildMailSettingsPayload`.
- `api/Service/Admin/Settings/Boundary/HttpControllers/MailSettingsController.cs`:
  `Get`, `Update`, `Test` (Settings.View/Update, Passwortbeibehaltung, Hot Reload).
  `api/Framework/Infrastructure/Mailing/SmtpMailService.cs`: `SendAsync`
  (STARTTLS, Pflichtzugangsdaten, Ergebnis nach SMTP-Senden).
- `api/Service/Notifications/Application/Services/NotificationChannelAvailabilityService.cs`:
  `IsProviderAvailable`, `HasVerifiedEndpointAsync` (SMTP/VAPID/SMS und Bestätigung).
- `api/Service/Notifications/Application/Catalog/NotificationCatalog.Security.cs`:
  `security.password.changed`; `NotificationCatalog.cs`: aktive Definitionen.
  `Application/Policy/NotificationPolicyEngine.cs`: `EvaluateChannel`
  (Anbindung/Empfänger vor Pflicht, Ruhezeit, E-Mail-Digest).
- `web/app/[project]/dashboard/user-management/profile/notifications/notifications-form.tsx`:
  `preferenceFormValues`, Kanal-/Ereignisformular; bestehende Werte bleiben erhalten,
  keine Digest- oder Browser-Abo-Bedienung. Abgleich mit P15-Seite
  `docs/ueberblick/profil-benachrichtigungen.mdx`.
- `api/Service/Notifications/Boundary/HttpControllers/NotificationPreferencesController.cs`:
  `GetCatalog`, Profilrechte; `NotificationsController.cs`: eigener Posteingang.
  `PushSubscriptionsController.cs`: vorhandene API, keine behauptete Dashboardaktion.
- `api/server/Hosting/NotificationHostingExtensions.cs`: minütliche Jobs.
  `api/Service/Notifications/Application/Workers/EmailDeliveryWorker.cs`,
  `DailyDigestWorker.cs`, `WebPushDeliveryWorker.cs`: Zustellversuche, Rechte-
  und Empfängerprüfung, Wiederholungen, Entfernen ungültiger Push-Abos.
- `web/components/notifications/notification-inbox-sheet.tsx`: `Technical Details`
  enthält Kennungen, keinen individuellen Versandstatus.
  `api/Service/Observability/Application/BusinessOperationsMetricsProvider.cs`
  und `Boundary/HttpControllers/DashboardMetricsController.cs`: aggregierte Metriken,
  Dashboard.View und Quellenrechte.
- Frühere praktische Prüfung: `web/docs/mcp-notifications-runtime-verification-2026-10-31.md`
  (lokales Mailpit mit STARTTLS/Anmeldung, Pflicht-E-Mail, SMTP-Fehler,
  Passwortbeibehaltung). Diese Ergebnisse wurden gelesen, nicht erneut durchgeführt.

## Prüfungen und Grenzen

Ausgeführt: vorhandenes Prettier mit `--check` auf beiden eigenen Dateien;
`git diff --check` ohne Befund. Lokaler Dateiabgleich bestätigt alle fünf relativen
Verweise einschließlich Zielanker, vorhandenes Frontmatter und unveränderte
Überschriften gegenüber HEAD. Das ist keine gerenderte Consumerprüfung.
Keine eigene Browser-, Hardware-, Push-, SMS- oder SMTP-Prüfung und kein Versand.
Die frühere Mailpit-Prüfung belegt keinen Empfang bei externen Mailanbietern.
Consumerdarstellung und gemeinsame Navigation prüft der Koordinator.

URLs, alle bestehenden Überschriften und Anker bleiben erhalten. Vorhandene
Querverweise werden wiederverwendet; kein zusätzlicher Seiten- oder Assetbedarf.

Geänderte Dateien:

- `web/content/docs/docs/administration/benachrichtigungen-verwalten.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--benachrichtigungen-verwalten.md`
