# Prüfung der Benutzer-Dokumentation

Stand: 19. Oktober 2026. Gegenstand ist die Web-Selbstbedienung im lokalen
Arbeitsstand. Die native App und eine Veröffentlichung gehören nicht zu dieser Runde.

## Vergleich mit anderen Dokumentationen

Die folgenden Beobachtungen stammen aus den verlinkten Originalanleitungen.
Die Übertragung auf Mardu ist eine redaktionelle Entscheidung; Funktionsumfang,
Tarife oder Anmeldeverfahren der Vergleichsprodukte werden nicht übernommen.

| Quelle                                                                                                                                                      | Auffälliger Aufbau                                                                                                     | Für Mardu übernommen                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| [Vercel: Einstieg](https://vercel.com/docs/getting-started-with-vercel)                                                                                     | Ziel, Voraussetzungen, nummerierter Ablauf und nächste Schritte; Referenzen getrennt.                                  | Einstieg vor Einzelthemen; Ergebnisse und passende Folgeaufgaben verlinken.                      |
| [GitHub: Hello World](https://docs.github.com/en/get-started/using-github/hello-world)                                                                      | Ein vollständiger Beispielablauf mit erkennbarem Ergebnis statt einer Funktionsliste.                                  | Auf der Benutzerübersicht von Anmeldung und Profil über Ressourcen bis zur Buchung führen.       |
| [Slack: Neue Benutzer](https://slack.com/help/articles/218080037-Getting-started-for-new-Slack-users/)                                                      | Profil und persönliche Benachrichtigungen gehören zum Einstieg; kurze Aufgaben verweisen auf ausführliche Hilfe.       | Kurzer erster Durchlauf; Kontohilfe und Posteingang als eigene Aufgaben.                         |
| [Notion: Posteingang](https://www.notion.com/en-gb/help/updates-and-notifications) und [Versandoptionen](https://www.notion.com/help/notification-settings) | Posteingang bearbeiten und Zustellpräferenzen sind getrennte Anleitungen.                                              | Bestehende Trennung beibehalten und in beide Richtungen verlinken.                               |
| [GitLab: Benutzerkonto](https://docs.gitlab.com/user/profile/)                                                                                              | Je Änderung konkrete Menüwege, Voraussetzungen und Auswirkungen.                                                       | Profil nach Aufgabe gliedern; Kontodaten, Sicherheit und Verbindungen getrennt erklären.         |
| [Nextcloud: Benutzerhandbuch](https://docs.nextcloud.com/server/latest/user_manual/en/)                                                                     | Benutzerhandbuch und administrative/technische Themen haben unterschiedliche Einstiege.                                | Persönliches Dashboard vom Systembetrieb trennen; vorhandenen Metriktext erhalten.               |
| [Confluence: Arbeiten organisieren](https://support.atlassian.com/confluence-cloud/docs/create-and-organize-work-in-confluence-cloud/)                      | Aufgabenorientierte Themen; administrative Einrichtung steht außerhalb der täglichen Nutzung.                          | Benutzerfokus auf eigene Aufgaben beschränken; Verwaltungsrechte und Wechsel gesondert erklären. |
| [Skedda: Mitarbeiteranleitung](https://support.skedda.com/en/articles/5351844-skedda-employee-user-guide)                                                   | Ressource wählen, Verfügbarkeit prüfen, buchen, Bestätigung erkennen, Details bearbeiten; Desktop und Mobil erläutert. | Buchungsablauf samt Status und Folgeaktionen erklären; beide Bildschirmgrößen prüfen.            |

Es wurden acht Produktdokumentationen und ihre verlinkten Einstiegs-/Detailseiten
verglichen. Umfangreiche Marketing-FAQ-Sammelseiten dienen nicht als Vorlage für
unsere Bedienungsanleitungen. Mardu erhält keine fremden Funktionen oder
Berechtigungsmodelle, nur weil sie in einer anderen Anleitung vorkommen.

## Reihenfolge und wiederkehrender Seitenaufbau

Für neue Mitglieder steht auf der Startseite dieser Weg:

1. Am richtigen Standort anmelden und eigene Profildaten prüfen.
2. Ressource finden und Voraussetzungen einschließlich Einweisungen prüfen.
3. Falls nötig Zugriff anfragen und die Entscheidung abwarten.
4. Buchen und Bestätigung beziehungsweise Freigabebedarf erkennen.
5. Bei Bedarf einen Kalender anbinden und Mitteilungen einstellen.

Für wiederkehrende Nutzung bleibt die Seitenleiste an den Portalbereichen
orientiert: Einstieg, Dashboard, Ressourcen, Anfragen, Buchungen, Kalender,
Qualifikationen, Posteingang und Störungshilfe. Danach folgen **Profil und Hilfe**.
Optionale Nachweisquellen und MCP-Verbindungen stehen hinter den alltäglichen
Kontoeinstellungen. Bestehende URLs bleiben erhalten.

Die Anleitungen beschreiben, soweit für die Aufgabe nötig:

- Ziel und Einstieg in der Oberfläche.
- Voraussetzungen und Rechte vor der Aktion.
- Schritte mit tatsächlichen UI-Bezeichnungen.
- Erkennbares Ergebnis und Wirkung des Speicherns oder Widerrufs.
- Relevante Fehler und Grenzen der Selbstbedienung.
- Einen passenden nächsten Schritt statt einer zweiten vollständigen Referenz.

Nicht jede Seite erhält künstlich alle Überschriften. Eine Begriffsseite bleibt
eine Erklärung; eine Anleitungsseite bleibt auf ihre Aufgabe beschränkt.

## Echte Mitgliedsprüfung

Für die Prüfung wurde über die vorhandene lokale Benutzer-API ein eigenes
Testkonto mit fiktiven Daten angelegt. Es erhält die vorhandene Rolle **Basic**
mit zwölf effektiven Rechten, darunter persönliche Profil-, Buchungs- und
Katalogrechte. Es besitzt keine Verwaltungsrechte. Es wurden keine Rechte an
bestehenden Rollen geändert und keine Einladungen verschickt.

Nachgewiesen wurden:

- Anmeldung mit dem eigenen Passwort und Einstieg ins persönliche Dashboard.
- Profiländerung speichern und durch erneutes Laden bestätigen.
- Einen eigenen Testtermin anlegen, ihn in der Benutzeroberfläche und den Details
  öffnen und als ICS exportieren.
- Einen persönlichen Kalenderlink erzeugen und eigene Termine daraus abrufen.
- Link ersetzen und Ablehnung des alten Links prüfen.
- Zugang widerrufen und Ablehnung des widerrufenen Links prüfen.
- Testtermin stornieren und den gespeicherten Stornierungsstatus erneut lesen.
- Export mehrerer eigener Serien mit allen zehn Testterminen aus fünf Serien;
  alle erzeugten Testtermine sind anschließend storniert.
- Entwurfswarnungen bei Profil- und Buchungsänderungen sowie Mitgliedszugriff auf
  Dashboard-Editor und Zugriffsanfrageformular.

Die Testbuchung bleibt als stornierter Verlauf sichtbar. Das getrennte lokale
Testkonto bleibt für weitere Prüfungen bestehen. Zugangsdaten und Kalenderlinks
liegen nicht in der Dokumentation oder im Repository.

Beim direkten Aufruf der verpflichtenden Recovery-Code-Seite ohne eingerichtete
2FA lehnt die API die Erzeugung ab. Die Anleitung nennt diese Voraussetzung.
Der gemeinsame Dialog behandelt auch die abgewiesene automatische Erzeugung als
sichtbaren Fehler. Der zweite Live-Befund betraf die erste Darstellung gespeicherter
Themes; Profil und Theme-Menü verwenden dafür nun dieselbe Hydrationsbehandlung.

## Website und gemeinsamer Inhalt

Die öffentliche URL `https://www.mardu.de/docs/benutzer` lieferte bei dieser
Prüfung HTTP 404. Die bestehende Website-Konfiguration deaktiviert Dokumentation
standardmäßig. Eine lokale Prüfung mit `MARDU_DE_ENABLE_DOCS=true` aktiviert nur
den Testprozess; sie veröffentlicht oder ändert keine Produktionskonfiguration.

Der Website-Checkout enthielt noch das anfängliche Grundgerüst mit V1-/V2-Ordnern.
Die aktuellen kanonischen Inhalte wurden in seinen vorhandenen Doku-Mount
übernommen. Die alten Versionsdateien bleiben für bestehende URLs erhalten und
werden nicht als aktuelle Veröffentlichung dargestellt. Die Website verwendet
das vorhandene Fumadocs-Layout und die Fokus-/Baumlogik des Web-Consumers mit dem
websiteeigenen Logo und dem vorhandenen Suchendpunkt.

Der konkrete Abschlussstand der Browser- und Build-Prüfungen steht im
[Arbeitsplan](TODO.md). Reale Hardware, externe Anmeldedienste, externe Nachweisanbieter
und eine Zustellung an reale E-Mail-/SMS-/Push-Empfänger sind davon getrennt.

Der bei der Erstprüfung gefundene Secret-Fallback in `payload.config.ts` wurde im
anschließenden Auftrag entfernt und mit Regressionstests geprüft. Die vollständige
Website-Reactprüfung läuft ohne Fehler durch; 160 bestehende Warnungen bleiben.
Der aktuelle Prüfstand steht im oben verlinkten Arbeitsplan.

## Screenshot-Ergänzung vom 19. Oktober 2026

20 neue Screenshots ergänzen 14 Benutzer- und Profilanleitungen. Die Aufnahmen
stammen aus der vorhandenen Weboberfläche auf dem lokalen Docker-Stand, mit
einem angemeldeten Mitglied, deutscher Sprache und hellem Farbschema. Die
vorhandenen Qualifikationsbilder und die mobile Profilübersicht bleiben erhalten.

| Anleitung                      | Neue Aufnahmen                                                         |
| ------------------------------ | ---------------------------------------------------------------------- |
| Dashboard                      | Kennzahlen und Listen mit eigenen Beispieldaten.                       |
| Buchungen                      | Eigene Liste, Erstellungsformular und Details mit Stornierungsbereich. |
| Kalender                       | Aktives Abo mit Ersetzen und Widerrufen, ohne persönlichen Link.       |
| Zugänge & Ressourcen           | Eigene Freigabe, Katalog und mobile Ressourcenkarte.                   |
| Berechtigungsanfragen          | Offener und genehmigter eigener Antrag, Rücknahmeaktion.               |
| Benachrichtigungen             | Persönliche Buchungs- und Nachweismeldungen statt Betriebsalarme.      |
| Profil                         | Kontaktformular und Profilbildbereich ohne Foto.                       |
| Anmeldesicherheit              | Passwortdialog und Zwei-Faktor-Bereich vor der Schlüsselerzeugung.     |
| Sitzungen                      | Aktuelle und weitere fiktive Sitzung mit getrennten Aktionen.          |
| Zutrittsmedien                 | Aktive Karte und deaktivierter Transponder mit Gültigkeit.             |
| Benachrichtigungseinstellungen | Kanäle und Ruhezeiten.                                                 |
| Erscheinungsbild               | Mobile Theme-Auswahl und Bedienhilfen.                                 |
| Nachweisquellen                | Verbindungswege bei noch nicht angebotenem Anbieter.                   |
| MCP                            | Tatsächlich deaktivierte Serverfunktion.                               |

Für gefüllte Listen wurden ausschließlich die Antworten der eigenen Datenabfragen
im Aufnahmebrowser durch fiktive Beispieldaten ersetzt: Alex Mustermann,
`alex@example.invalid`, Holzwerkstatt und Lasercutter. Sitzungs-IP-Adressen stammen
aus dem Dokumentationsnetz `192.0.2.0/24`. Die Oberfläche und ihre Zustandsdarstellung
wurden nicht nachgezeichnet. Die Bildunterschriften kennzeichnen die Beispiele;
diese Aufnahmen belegen keine neue Backend- oder Hardwareprüfung.

Im Aufnahmebrowser wurden keine Änderungen gespeichert, keine Anfragen versandt,
keine Sitzungen beendet und keine realen Kalenderlinks oder Anmeldeschlüssel
erzeugt. Die vorhandene Fumadocs-Bilddarstellung und die jeweiligen `bilder/`-Ordner
werden weiterverwendet. Bilder und Texte wurden in beide vorhandenen Consumer-Mounts
übernommen; Veröffentlichung und neue Commits sind davon getrennt.

Prüfung: 50 MDX-Dateien einschließlich historischer Einstiege kompilieren;
210 lokale Verweise und 42 Bildverweise ohne Befund. Alle Bilder der 14 geänderten
Anleitungen laden auf der Website und im neu gebauten Docker-Webcontainer bei
1440 und 390 Pixeln, ohne seitliches Überlaufen oder Laufzeitfehler. Der
Docker-Produktionsbuild einschließlich Typecheck ist erfolgreich; alle vier
Compose-Dienste sind gesund. Die vorhandenen 41 Web-Navigationstests und 26
Website-Dokumentationstests sind erfolgreich. Die tatsächlichen Aufnahmen wurden
zusätzlich auf sichtbare Inhalte und fehlende Zugangsdaten geprüft.
