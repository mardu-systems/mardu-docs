# Offene Prüfungen nach der Seitenrevision

Stand: 1. November 2026. Die frühere Schreibauftragsliste wurde gegen die
[Seitenrevision](2026-11-01-seitenrevision-ergebnis.md) abgeglichen. Quellen,
Änderungen und Einschränkungen sind in den einzelnen Seitenberichten dokumentiert.
Die Liste beschreibt Prüfbedarf; sie ist kein Bestandteil der Produktanleitungen.

## Geschlossene Schreibaufträge

Die fehlenden Abläufe für Badge-Definitionen, Vergabe, Erneuerung, Widerruf,
Veröffentlichung und Import stehen in [Badges verwalten](../docs/administration/badges-verwalten.mdx).
Kompetenzen und Lernwege, Anbieteranbindung sowie laufende Teilnahmen haben
getrennte Anleitungen. Die Zuständigkeiten und Querverweise sind ergänzt.

Systemstatus und persönliche Dashboards wurden gegen Datenquellen, Rechte,
Zeitbereiche und Aggregationen abgeglichen. Veraltete Zugangsdiagramme werden
nicht mehr als aktuelle Oberfläche ausgegeben. Die Verwaltungseinstiege erklären
Setup gegenüber vorhandenen Installationen, Startprüfung und nächste Aufgaben.

Ressourcen, Bereiche, Zutrittspunkte, Bedingungen und Endpunkte stehen unter
[Ressourcen einrichten](../docs/koordination/ressourcen.mdx). Freigaben,
Verwaltungszuständigkeiten und Antragsentscheidungen haben eigene Anleitungen;
Zutrittsentscheidungen und Sitzungen bleiben unter Zutritt verwalten. Der
Geräte- und Messwertabgleich ist erfolgt. Node-RED hat einen eigenen Flow-Leitfaden.
Entwicklerverweise sind mit den aktuellen OpenAPI-Operationen abgeglichen.

Diese Textarbeit ist abgeschlossen. Sie ersetzt die folgenden praktischen
Abnahmen nicht.

## Praktische Abnahme in geeigneter Testinstallation

- [ ] Benutzer- und Verwaltungsabläufe mit aktuellen Testkonten und getrennten
      Berechtigungen durchspielen: Konto/Rolle/Gruppe, Ressource, Freigabe, Antrag,
      Buchung, Badge, Lernweg, Dashboard und MCP-Verbindung. Vorhandene gespeicherte
      E2E-Sitzungen passen nicht zur aktuellen Instanz.
- [ ] MFA, Passkeys, Wiederherstellung, Sitzungswiderruf und erzwungene Richtlinien
      mit isolierten Konten prüfen. Die im Ergebnisbericht erfassten Produktabweichungen
      zuerst berücksichtigen.
- [ ] Benachrichtigungen je Kanal bis zum externen Empfang prüfen: In-App,
      E-Mail und Web-Push mit aktiver Konfiguration, Pflichtkanälen, Ruhezeiten und
      Zustellfehlern. Ein Versandauftrag allein belegt keinen Empfang.
- [ ] LDAP, OIDC, externe Nachweisquellen und MQTT mit kontrollierten Diensten
      abnehmen. Ergebnis und Aktualität eines Tests getrennt prüfen; Änderungen an
      Bestandskonten vermeiden. Bekannte Aktivierungs-/Authentifizierungsabweichungen
      stehen im Ergebnisbericht.
- [ ] Einen Node-RED-Flow mit zugelassener Verbindung und Ressource deployen;
      erlaubte und verweigerte Aktion sowie Ereigniszustellung prüfen.
- [ ] Tag-Anmeldung mit Mardu Connect, unterstützter Karte und realem Leser bis
      zum Zutritt prüfen. Ebenso Geräteaufnahme, Endpunkte, Sitzungsende und
      Gerätebestätigung mit passender Firmware abnehmen.
- [ ] Raspberry-Pi-/Produktionsinstallation, HTTPS, Sicherung und Wiederherstellung
      auf leerer Testumgebung prüfen. Den statischen Portkonflikt zwischen
      Produktions-Compose und Setup-Wizard vor dieser Abnahme klären.
- [ ] Hardware-/Firmware-Kompatibilitätsliste anhand Hersteller- und Laborbelegen
      ergänzen. Aktuelle Quellen reichen nicht für allgemeine Kompatibilitätszusagen.
- [ ] Falls neue UI-Bilder benötigt werden, diese aus der aktuellen Testoberfläche
      aufnehmen. Irreführende vorhandene Bilder wurden aus den Anleitungen entfernt;
      es wurden keine Ersatzoberflächen erfunden.

## Ergänzende technische Dokumentation

- [ ] SignalR als eigene Integration nur bei konkretem Bedarf ausarbeiten:
      öffentliche Hubs, Authentifizierung, Gruppen, Ereignisse, Wiederverbindung und
      erlaubte Clients gegen den aktuellen Vertrag prüfen. Bestehende interne
      Echtzeitverbindungen begründen keine allgemeine öffentliche API-Zusage.
- [ ] Ein durchgängiges Lern-Tutorial mit fiktiver Person und Ressource erst nach
      erfolgreicher Testinstallation aufzeichnen. Die einzelnen Aufgaben sind bereits
      dokumentiert; ein praktischer Gesamtdurchlauf steht noch aus.

## Consumer und Veröffentlichung

- [ ] Docs-Revision und Consumer-Commits gemeinsam prüfen und veröffentlichen.
      Die lokale Website verwendet noch ihren bisherigen Content-Gitlink. Ihr Filter
      wurde für beide Stände geprüft, die neue Quelle dort nicht ausgerollt.
- [ ] Website nach dem Content-Update bauen und im Browser prüfen. Die dortigen
      Tests und Typprüfungen sind keine Browserabnahme der Website.

Softwareabweichungen mit Quellenbelegen stehen im
[Ergebnisbericht](2026-11-01-seitenrevision-ergebnis.md). Daraus wurden keine
externen Tickets oder Meldungen erstellt.
