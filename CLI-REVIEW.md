# Aufbau der Dokumentation zur Wartungs-CLI

Stand: 25. Oktober 2026. Gegenstand ist `mardu-admin` im lokalen Softwarestand.
Eine Veröffentlichung oder eine Zuordnung zu einer veröffentlichten Release-Version
ist damit nicht verbunden.

## Vergleich mit Anbieter-Dokumentationen

Die Beobachtungen stammen aus den verlinkten Originalquellen. Die Übertragung
auf Mardu ist eine redaktionelle Entscheidung. Fremde Befehle, Optionen und
Betriebsvoraussetzungen wurden nicht übernommen.

| Quelle                                                                                                                                           | Beobachtung                                                                                                                   | Übertragung auf Mardu                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [GitLab: Reset user passwords](https://docs.gitlab.com/security/reset_user_password/)                                                            | Voraussetzungen vor dem Ablauf, verschiedene Aufrufwege getrennt, Passwortwiederholung erklärt, Fehlerhilfe nach der Aufgabe. | Host-/Docker-Zugriff und laufende API zuerst; Menü und direkter Reset; Erfolg durch erneute Anmeldung prüfen; Einschränkungen erklären. |
| [Nextcloud: Resetting a lost admin password](https://docs.nextcloud.com/server/latest/admin_manual/configuration_user/reset_admin_password.html) | Stellt die Wiederherstellung bei fehlendem regulärem Zugang in den Mittelpunkt und zeigt den Aufruf als Dienstbenutzer.       | Einstieg mit dem Fall ohne Mardu-Login beziehungsweise Mailversand; vollständiger Docker-Aufruf als `mardu`; verdeckte Passworteingabe. |
| [Grafana: Grafana server CLI](https://grafana.com/docs/grafana/latest/administration/cli/)                                                       | Erklärt zuerst Ort und Syntax des Aufrufs und danach Befehle, Optionen sowie Konfigurationsfehler.                            | Separate Befehlsreferenz, lesende JSON-Ausgabe, Rückgabewerte und Hilfe bei Socket-/Versionsproblemen.                                  |

## Ablage und Abgleich

- `docs/administration/wartungs-cli.mdx` ist die Aufgabenanleitung.
- `docs/administration/wartungs-cli-referenz.mdx` beschreibt Befehle, Optionen und Betriebsparameter.
- Beide Seiten stehen in der Administration-Navigation; Sicherheits- und Störungsanleitungen verlinken den Einstieg.
- Der Software-Consumer benötigt beide Slugs zusätzlich in `web/lib/docs-roles.tsx`. Inhalt und Consumer-Zuordnung müssen zusammen veröffentlicht werden.
- Beschriebene Befehle, Menüpunkte, Standardwerte und Wirkungen wurden mit der implementierten CLI und den Identity-/Hosting-Komponenten abgeglichen. Vorhandene Konten werden für diese Dokumentationsarbeit nicht verändert.

Die Produktseiten bleiben auf Bedienung und Betriebsbedingungen beschränkt.
Implementierungsdetails des internen HTTP-Protokolls bleiben im Software-Repository.
