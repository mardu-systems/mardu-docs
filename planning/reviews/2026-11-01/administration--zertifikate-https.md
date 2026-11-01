# N13: HTTPS-Zertifikatswechsel vorbereiten und prüfen

## Änderungsbrief und Bedarfsentscheidung

- Leserfrage: Welcher Dienst liefert mein HTTPS-Zertifikat aus, wo muss ein
  Wechsel erfolgen und wie erkenne ich, dass die neue Verbindung funktioniert?
- Leser: Personen mit Verantwortung für eine bestehende Installation; für einen
  Listenerwechsel sind zusätzlich Host-/Deployment-Zugriff und Kenntnis der
  tatsächlich verwendeten Adresse nötig.
- Eigenständiger Bedarf bestätigt: `server-einstellungen.mdx#zertifikate` erklärt
  Upload, Ersetzen und Löschen bereits ausreichend. `sicherheit-betrieb.mdx`
  behandelt Ablaufkontrolle; `installieren/raspberry-pi.mdx` erklärt die
  HTTPS-Erstinstallation hinter Caddy. Es fehlt der zusammenhängende Ablauf zum
  Zuordnen der HTTPS-Gegenstelle und zur Prüfung eines Wechsels, insbesondere beim
  direkten Kestrel-Listener.
- Kanonische Heimat: Administration, neue Seite
  `docs/administration/zertifikate-https.mdx`. Speicherverwaltung bleibt unter
  `server-einstellungen.mdx#zertifikate`; die Caddy-Erstinstallation bleibt unter
  `installieren/raspberry-pi.mdx`.
- Plan: nur die fehlende Zuordnungs-/Wechselprüfung ausarbeiten; bestehende
  Speicheranleitung verlinken; Kestrel-Dateikonfiguration, Proxy und Clientvertrauen
  trennen. Keine neue TLS-Architektur und kein eigener ACME-/PKI-Ablauf.
- Prüfziel: statischer Quellenabgleich, MDX-/Markdown-Format und lokale Verweise.
  Consumer-Rendering und reale HTTPS-Prüfung übernimmt die gemeinsame Abnahme.

## Befund und Umsetzung

- Entscheidung: **belegbare Teildokumentation / offene Prüfung**. Eigenständige
  Anleitung angelegt; statisch geprüft, keine praktische Abnahme behauptet.
- Neue Seite erklärt die tatsächliche TLS-Gegenstelle, Rechte und
  Deployment-Voraussetzungen, den direkten Kestrel-Dateiwechsel mit Neustart sowie
  die getrennte Prüfung von Zertifikat, Clientvertrauen und Funktion.
- Keine Wiederholung des Uploaddialogs. Kein angenommener Dashboard-Dialog für
  Kestrel oder Proxy; keine eigene Zertifikatsausstellung, ACME-/PKI-Anleitung,
  generelle automatische Erneuerung oder neue Betriebsarchitektur.
- Bestehende Speicheraktionen und Integrationsanleitungen wiederverwendet. Keine
  API-/DTO-/Softwareänderung; daher keine API-/DTO-Dokumentation angepasst.

## Quellen

Pfade beziehen sich auf das Software-Repository; die Produktseiten liegen im
Doku-Submodul. Relevante Stellen wurden gelesen:

- `web/content/docs/docs/administration/server-einstellungen.mdx:121–163`:
  kanonischer Upload-/Ersetzen-/Löschen-Ablauf und Grenze zur TLS-Konfiguration.
- `web/content/docs/docs/administration/sicherheit-betrieb.mdx`, Abschnitt
  **Zertifikatsablauf prüfen**: bestehende Ablaufkontrolle und fehlende vollständige
  Zuordnung aktiver Verbindungen; Abschnitt **Eine Störung eingrenzen**:
  Aussagegrenzen der Health-Endpunkte.
- `web/content/docs/docs/installieren/raspberry-pi.mdx:138–149`: Caddy auf `443`,
  interner API-HTTP-Port `8080`, Persistenz und separate MQTT-TLS-Einrichtung.
- `api/server/Program.cs:50–146`: Kestrel-Listener, HTTPS-Port, Dateipfad und
  Passwort, Content-Root-Auflösung und selbstsignierter Fallback. Die Datei wird
  in der Listener-Konfiguration beim Start geladen; kein Store-ID-Lookup.
- `api/server/Hosting/PersistentHttpsCertificateProvider.cs:9–61`: persistentes
  selbstsigniertes Fallback-Zertifikat; kein Bezug zur Dashboard-Zertifikatsliste.
- `docker-compose.https.yml:1–20`: lokales HTTPS-Overlay, `/certs`-Mount,
  Datei-/Passwortvariablen und feste Container-Portzuordnung `7443`.
- `deploy/production/docker-compose.prod.yml:1–18,55–69` und
  `deploy/production/Caddyfile:1–13`: Caddy-Proxy, Ports `80`/`443`, interne
  Upstreams und deaktiviertes Kestrel-HTTPS. Kein manueller Uploadpfad in Mardu.
- `web/components/layout/settings/server-nav.config.ts:90–103`,
  `web/lib/settings/config.ts:80–89`,
  `web/locales/de/navigation.json:86` sowie
  `web/locales/de/settings.json:1774–1840`: Einstieg **Server-Zertifikate**,
  Leserecht und genaue Dialogtexte einschließlich **Ersetzen** und
  **Selbstsigniertes Zertifikat zulassen**.
- `web/app/[project]/dashboard/admin/server/certificates/page.tsx:101–167,250–350`
  und `web/components/server/certificates-card.tsx:108–219`: vorhandene
  Speicheraktionen, Zertifikatsliste und angezeigte Metadaten; keine Auswahl des
  aktiven Kestrel-/Proxy-Zertifikats.
- `api/framework/Infrastructure/Certificates/Boundary/CertificatesController.cs:19–75`:
  `Settings.View` für Liste/Metadaten, `Settings.Update` für Upload/Ersetzen/Löschen.
- `api/framework/Infrastructure/Certificates/Application/CertificateService.cs:36–125`:
  Speicherung, Beibehaltung der ID beim Ersetzen und Dateiauflösung für Verbraucher.
- `api/framework/Infrastructure/Identity/External/LdapConnectionBuilder.cs:64–88`,
  `api/framework/Infrastructure/Certificates/Application/ExternalServerCertificateTrustService.cs:66–94`
  und `api/framework/Infrastructure/Network/Broker/MqttServerHostedService.cs:703–727`:
  getrennte Nutzung als CA-Vertrauen für LDAP/OIDC beziehungsweise als
  Brokerzertifikat für MQTT. Daraus folgt kein Browser-Vertrauensspeichereintrag.

## Eigene Checks und Prüfgrenzen

- Vollständiger statischer Abgleich der beschriebenen Zuständigkeiten,
  Konfigurationsschlüssel, UI-Namen und Zertifikatsspeicherrechte mit den genannten
  Quellen.
- `web/node_modules/.bin/prettier --check --ignore-path /dev/null` mit genau den
  beiden eigenen Dateien: bestanden (nach Formatierung der MDX-Tabelle).
- Lokaler Python-Check: Frontmatter mit Titel/Beschreibung, kein zusätzliches H1,
  alle vier relativen MDX-Links samt vorhandenen Zielankern bestanden. Kein
  Consumer-Rendering aus dieser Textprüfung abgeleitet.
- Keine Änderungen an Zertifikaten, Listenern, Netzwerk, Deployment oder
  externen Systemen. Keine Builds, Serverstarts, Commits oder Softwareänderungen.
- Offen: Consumer-Rendering in Software und Website (auch mobil), Browserprüfung
  an einer Testinstallation, tatsächlich ausgeliefertes Zertifikat nach einem
  Kestrel-Wechsel, Trust-Verhalten verwendeter Endgeräte und Proxy-/Anbieterbetrieb.
  Kein realer Raspberry-Pi- oder Zertifikatsaussteller-Test.
- Für Caddy wird ausschließlich die vorhandene TLS-Zuständigkeit beschrieben.
  Erneuerung, Ausstellerfehler und ein manueller Caddy-Zertifikatswechsel sind kein
  praktisch geprüfter Umfang dieser Seite.

## Hinweise an die Koordination

- Neue Seite unter Administration eintragen; Consumer-Filter und Suche prüfen.
- Als Querverweis aus `server-einstellungen.mdx#zertifikate` und
  `sicherheit-betrieb.mdx#zertifikatsablauf-prüfen` geeignet. Im Installationsbereich
  kann nach der Erklärung von internem HTTP und Caddy auf diese Wechselprüfung
  verwiesen werden.
- Alle ausgehenden Produktlinks zeigen auf bestehende Seiten. Keine Links auf
  parallel erst entstehende Zusatzseiten aufgenommen.

## Geänderte Dateien

- `web/content/docs/docs/administration/zertifikate-https.mdx`
- `web/content/docs/planning/reviews/2026-11-01/administration--zertifikate-https.md`
