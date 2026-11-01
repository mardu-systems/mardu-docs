# Mardu-Dokumentation: Navigation und Einstieg

Stand: 1. November 2026, nach kritischer Revision. **Strukturvorschlag zur Besprechung**, keine freigegebene
Navigation. Alle sechs Bereiche bleiben erhalten. Vorhandene Anleitungen und URLs
werden weiterverwendet. Für die neue Navigation ist diese Fassung der aktuelle
Vorschlag; die Bestandsbefunde und offenen Sachprüfungen in `TODO.md` bleiben
erhalten. Eine Produktabnahme folgt daraus nicht.

Der [ausgeschriebene Überblick](../drafts/2026-11-01-mardu-verstehen.md) gehört zu
diesem Vorschlag. Die [kritische Prüfung](./2026-11-01-dokumentationsstruktur-review.md)
hält die Schwächen der ersten Fassung und ihre Korrekturen fest. Diese Dateien
liegen außerhalb der veröffentlichten Inhalte.

## Leitentscheidung

Die Dokumentation beantwortet zuerst **„Wie hängt Mardu zusammen?“**, danach
**„Was möchte ich erledigen?“**. Ressourcen und Personen bilden das gemeinsame
Begriffsmodell. Die Bereiche sind Lesereinstiege; sie vergeben keine Rechte und
entsprechen nicht zwingend den Rollen oder Menüs im Dashboard.

| Bereich        | Frage der Leser                                         | Grenze zum Nachbarbereich                                                           |
| -------------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Überblick      | Was verwaltet Mardu, und wie hängen die Teile zusammen? | Erklärungen und Wegweiser; keine Sammlung aller Einstellungen.                      |
| Benutzer       | Wie erledige ich meine eigene Aufgabe?                  | Eigene Buchungen, Freigaben, Nachweise, Verbindungen und Kontodaten.                |
| Koordination   | Wie organisiere ich Ressourcen und ihre Nutzung?        | Verfügbarkeit, konkrete Buchungs-/Zugangsanfragen, Bewertungen und Vergaben.        |
| Administration | Wie richte ich die Installation ein und betreibe sie?   | Konten/Rechte, Ressourcenregeln, Nachweismodelle, Technik, Anbindungen und Betrieb. |
| Installieren   | Wie bringe ich Server und Hardware vor Ort zum Laufen?  | Erstaufbau, Inbetriebnahme und Übergabe; laufende Konfiguration verlinken.          |
| Entwickeln     | Wie integriere ich Software in Mardu?                   | Protokolle, Verträge und ausführbare Beispiele.                                     |

Eine Person kann mehrere Einstiege brauchen. Die Einordnung beschreibt den Zweck
der Anleitung und behauptet keine festen Systemrollen. Eine zuständige Person
kann beispielsweise Ressourcen konfigurieren und anschließend Buchungen entscheiden.

## Korrektur gegenüber der ersten Fassung

Die erste Fassung ordnete alle 54 vorhandenen Seiten ein, prüfte aber die
Aufgabenabdeckung zu wenig. Der Zielbaum berücksichtigt jetzt auch vorhandene
Funktionen ohne ausreichende Anleitung. Neue Seiten sind begründete Zuschnitte,
keine sofort anzulegenden Platzhalter und keine festgelegte Gesamtzahl.

| Aufgabe                                                           | Kanonischer Einstieg                                                               | Anschluss für andere Leser                                                                                        |
| ----------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Ressource anlegen, Technik, Zugriff und Buchbarkeit konfigurieren | Administration → Ressourcen einrichten; vorhandene Quelle und URL weiterverwenden. | Koordination verlinkt konkrete Abschnitte für Änderungen der Einrichtung.                                         |
| Verfügbarkeit, Sperren und fällige Wartung im Alltag organisieren | Koordination → Verfügbarkeit und Wartung.                                          | Konfiguration und physische Durchführung zur jeweils passenden Anleitung verlinken.                               |
| Ressourcenregel und Verwaltungszuständigkeiten festlegen          | Administration → Zutritt / Verwaltungszuständigkeiten.                             | Koordination braucht den passenden Umfang für konkrete Entscheidungen.                                            |
| Einen Zugangsantrag oder eine Buchung entscheiden                 | Koordination → Zugangsanträge / Buchungen verwalten.                               | Administration verlinkt diese Aufgaben; Benutzer verfolgt den eigenen Antrag.                                     |
| Rollen und Benutzergruppen samt Gruppenregeln pflegen             | Administration → Rollen und Gruppen.                                               | Eine vorhandene Rolle am Konto zuweisen bleibt Teil der Benutzerverwaltung.                                       |
| Kompetenzen, Kriterien und Lernwege definieren                    | Administration → Kompetenzen und Lernwege.                                         | Koordination bewertet Personen und verwaltet konkrete Vergaben/Einschreibungen; Benutzer liest den eigenen Stand. |
| Externe Nachweisanbieter und Anerkennungsregeln einrichten        | Administration → Nachweissysteme anbinden.                                         | Eine konkrete Anerkennungsentscheidung gehört zur Koordination; eigene Verbindung nach Benutzer.                  |
| MQTT-Broker, Benutzer und ACLs verwalten                          | Administration → MQTT verwalten.                                                   | Entwickeln beschreibt Clientverbindung, Topics und Payloads.                                                      |
| Benachrichtigungen zustellen oder persönlich nutzen               | Administration richtet Kanäle ein und prüft Zustellung.                            | Benutzer liest Mitteilungen und wählt persönliche Einstellungen.                                                  |

Eine Anleitung hat eine kanonische Quelle. Andere Bereiche dürfen sie bei einer
konkreten Aufgabe verlinken. Bereichswechsel werden dabei sichtbar benannt. Ob eine
Person eine Aktion ausführen darf, bestimmen die tatsächlichen Rechte und
Zuordnungen; die Dokumentationsstruktur erteilt keine Berechtigung.

## Recherche und Abwägung

Aus der Online-Recherche übernehmen wir folgende Prinzipien. Ihre Anwendung auf
Mardu ist ein Vorschlag; sie wurde noch nicht mit neuen Nutzern getestet.

| Quelle                                                                                                    | Übernahme für Mardu                                                                                                                            |
| --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| [Google: Zielgruppe und Vorwissen](https://developers.google.com/tech-writing/one/audience)               | Der Überblick schließt die Wissenslücke über Ressourcen und Personen, bevor er Fachbegriffe voraussetzt.                                       |
| [Diátaxis: Kompass](https://diataxis.fr/compass/)                                                         | Erklärung, Lernen, Erledigen und Nachschlagen unterscheiden. Die Typen bestimmen die einzelne Seite, nicht vier zusätzliche Hauptordner.       |
| [Vercel: Dokumentationsnavigation](https://vercel.com/docs)                                               | Beschriftete Aufgabengruppen und eine erkennbare Referenz bieten Orientierung. Wir übernehmen das Muster, nicht Umfang oder Produktkategorien. |
| [GOV.UK: Nutzerbedürfnisse](https://www.gov.uk/service-manual/user-research/start-by-learning-user-needs) | Titel an konkreten Fragen ausrichten; Zuordnung anschließend mit Suchaufgaben prüfen.                                                          |
| [GOV.UK: Akkordeons](https://design-system.service.gov.uk/components/accordion/)                          | Wichtiges sichtbar lassen. Seiten mit Überschriften gliedern; Akkordeons nur bei belegtem Nutzen.                                              |
| [Google: zugängliche Dokumentation](https://developers.google.com/style/accessibility)                    | Diagramme zusätzlich erklären; Orientierung darf nicht ausschließlich visuell oder von Farbe abhängig sein.                                    |

Drei mögliche Richtungen wurden abgewogen:

- **Dashboard-Menü spiegeln:** vertraute Begriffe, aber wechselnde UI-Strukturen
  und Berechtigungen erklären das System nicht. Nicht als Ordnungsprinzip gewählt.
- **Nur nach Funktionen sortieren:** bündelt Themen, vermischt aber eigene Nutzung
  und Verwaltung. Nicht als Gesamtstruktur gewählt.
- **Sechs Einstiege mit Aufgabengruppen:** erhält gute Seiten und bestehende
  Adressen, macht Zuständigkeiten sichtbar. **Empfehlung für diese Runde.**

## Befunde im Bestand

Die Bestandsaufnahme erfasst alle handgeschriebenen aktuellen MDX-Seiten und ihre
Navigation. Die kritische Revision prüft zusätzlich Dashboard-Navigation,
Einstellungsbereiche und ausgewählte Implementierungen/Verträge. Die
[Belegliste](./2026-11-01-dokumentationsstruktur-review.md#geprüfte-produktquellen)
nennt die Quellen und Grenzen. Generierte API-Seiten bleiben ein Referenzbaum.

- Bereichsstarts sind überwiegend Linklisten; ein gemeinsames Systembild fehlt.
- Persönliche Profilseiten liegen unter `ueberblick/`, gehören sichtbar aber zu
  Benutzer. Ihre URLs können bleiben; sie müssen nicht beide Sidebars verlängern.
- **Badges verwalten** steht in der Admin-`meta.json`, fehlt aber in der
  Admin-Slugliste. **Raspberry-Pi-Installation** hat dieselbe Abweichung bei
  Installieren. Eine Seitenliste allein garantiert keinen sichtbaren Eintrag.
- **Übersicht und Systemstatus** liegt unter `benutzer/`, ist bereits dem
  Verwaltungsfokus zugeordnet und gehört dort unter Betrieb.
- Mehrere Starts und Anleitungen enthalten noch Schreibaufträge. Eine neue
  Reihenfolge macht diese Inhalte nicht fertig.
- **Automationen und KI-Anbindung** mischt MCP, Node-RED und Echtzeit. Einrichtung
  und Protokollbeispiele brauchen getrennte Zuständigkeiten.
- Die frühere Gesamtzahl im README ist überholt. Die Zuordnung unten dient als
  Inventar dieses Plans, nicht als Fertigstellungsnachweis.

## Navigation für alle Bereiche

Der Bereichswähler folgt **Überblick → Benutzer → Koordination → Administration →
Installieren → Entwickeln**. Das ist keine verpflichtende Lesereihenfolge.

Jeder Bereich zeigt seine Startseite als ersten anklickbaren Eintrag. Längere
Listen erhalten Zwischenüberschriften, keine leeren Landingpages. Zusammengehörige
Unterbäume wie Profileinstellungen und API-Referenz dürfen eingeklappt werden. Die rechte
Inhaltsübersicht bleibt für Abschnitte der geöffneten Seite zuständig.

`/docs` bleibt ein kurzer Wegweiser zu den sechs Einstiegen und wird kein siebter
Bereich. Bereichsstarts nennen ihren Zweck, häufige Aufgaben und passende
Querverweise. Jede Anleitung hat einen Heimatbereich und kann aus anderen Aufgaben verlinkt werden. Querverweise
nennen den Zielbereich; das Öffnen wechselt dorthin.

**Leseschlüssel:** Einrückungen bezeichnen Sidebar-Gruppen, keine neuen Ordner.
„Geplant“ erscheint erst mit nutzbarem Inhalt. Alle anderen Einträge verwenden
bestehende URLs; die Zuordnung dazu folgt im Seiteninventar.

### Überblick

```text
Mardu verstehen
Personen, Rollen und Freigaben
Begriffe nachschlagen
Neuerungen [nur mit belegtem Release-Inhalt]
```

Der Überblick erklärt in einer zusammenhängenden Startseite Ressourcen, Personen
und optionale Funktionen mit zwei Grafiken. Die zunächst vorgeschlagenen Seiten
„Ressourcen und Funktionen“ und „Systembestandteile“ entfallen in der ersten
Fassung: Der Startentwurf deckt ihren Zweck bereits ab. Bei späterer Aufteilung
muss jede Vertiefung eine eigene Leserfrage beantworten. Persönliche Aufgaben
führen nach Benutzer. Fehlender Release-Inhalt bleibt intern, statt eine leere
Neuerungen-Seite in der Sidebar zu zeigen; die bestehende Adresse bleibt erreichbar.

### Benutzer

```text
Benutzer: Start
Erste Schritte
  Eigene Aufgaben
  ├─ Zugänge und Ressourcen
  ├─ Meine Buchungen
  ├─ Zugriff anfragen
  ├─ Meine Qualifikationen
  ├─ Meine Zutrittsmedien
  ├─ Benachrichtigungen lesen
  ├─ Persönliches Dashboard
  ├─ Ressourcenzustand und Störungen
  └─ Kalender exportieren und abonnieren
  Profil und Einstellungen [aufklappbar, vorhandene Profilübersicht als Einstieg]
  ├─ Eigenes Profil
  ├─ E-Mail und Anmeldesicherheit
  ├─ Eigene Sitzungen
  ├─ Benachrichtigungseinstellungen
  ├─ Erscheinungsbild und Anzeigeformate
  ├─ Persönliche Nachweisquellen
  └─ Eigene MCP-Verbindungen
Hilfe
```

Häufige Nutzungsaufgaben bleiben direkt erreichbar. Die Medienseite steht bei der
Nutzung, damit Kartenverlust nicht unter Kontoeinstellungen gesucht werden muss.
Das vorhandene Profil ist der Einstieg zu persönlichen Einstellungen. Spezialfälle
wie MCP-Verbindungen werden dort angeboten, statt gleichrangig mit jeder
Hauptaufgabe die Sidebar zu verlängern. Welche Aufgaben häufiger sind, ist eine
Arbeitshypothese für den Lesertest. Aufklappbare Navigation ist von Akkordeons im
Seiteninhalt zu unterscheiden; notwendige Handlungsschritte bleiben sichtbar.

### Koordination

```text
Koordination: Start
Verfügbarkeit und Wartung koordinieren [geplant]
Buchungen verwalten
Zugangsanträge entscheiden             [geplant]
Bewertungen durchführen
Vergaben und Lernwegteilnahmen         [geplant]
```

Hier stehen konkrete Vorgänge für zuständige Personen. Die technische und
regelbezogene Ressourcen-Einrichtung bekommt Administration als Heimat. Die
bestehende Ressourcenanleitung unter ihrer bisherigen URL wird weiterverwendet.
Bis die neuen Aufgabenanleitungen ausgearbeitet sind, führt der Koordinationsstart
mit beschrifteten Links zu den passenden bestehenden Abschnitten. Es entstehen
keine leeren Seiteneinträge. Eine konkrete Anerkennung und die Einrichtung ihrer
Regeln werden getrennt erklärt; unterstützte Verfahren müssen jeweils geprüft sein.

### Administration

```text
Administration: Start
  Personen und Berechtigungen
  ├─ Benutzerkonten verwalten
  ├─ Rollen und Gruppen verwalten                 [geplant]
  └─ Verwaltungszuständigkeiten vergeben          [geplant]
  Ressourcen und Zutritt
  ├─ Ressourcen einrichten                       [vorhandene URL bleibt]
  ├─ Zutritt verwalten
  └─ Zugangs-Tags verwalten
  Kompetenzen und Nachweise
  ├─ Kompetenzen und Lernwege einrichten          [geplant]
  ├─ Badges verwalten
  └─ Nachweissysteme anbinden                     [geplant]
  Geräte und Automationen
  ├─ Geräte verwalten
  └─ Automationen
  Externe Anbindungen
  ├─ Externe Systeme anbinden                    [Einstieg]
  ├─ LDAP-Verzeichnis anbinden                    [geplant]
  ├─ Anmeldung über OpenID Connect                [geplant]
  ├─ MQTT verwalten                              [geplant]
  ├─ IP500-Netzwerk anbinden                      [geplant]
  └─ MCP für Agenten freigeben
  Betrieb, Sicherheit und Daten
  ├─ Servereinstellungen
  │  ├─ Anmeldung und Kontoschutz                 [geplant]
  │  └─ Zertifikate und HTTPS                     [geplant]
  ├─ Benachrichtigungen einrichten und prüfen
  ├─ Übersicht und Systemstatus
  ├─ Sicherheit und Betrieb
  ├─ Audit und Datenschutz
  └─ Mardu per CLI warten
     └─ Wartungs-CLI: Befehle und Optionen
```

Die sechs Gruppen beschreiben Aufgabenfelder. Der Baum ist eine Zielstruktur für
belegte Funktionen und noch auszuarbeitende Anleitungen. Erst fertige Seiten
werden sichtbar. Vorhandene Seiten können bis zur Ausarbeitung neuer Anleitungen
mehrere Aufgaben abdecken; das gilt insbesondere für Rollen/Gruppen, Integrationen
und Sicherheit. Ein aufklappbarer Einstellungs-/Referenzzweig wird nur mit nutzbaren
Unterseiten umgesetzt; dafür werden keine zusätzlichen leeren Indexseiten erzeugt.

Admin-MQTT bleibt eine Betriebsanleitung; Clientprotokolle stehen unter Entwickeln.
LDAP/OIDC-Weiterleitungsrouten begründen keine zusätzlichen Funktionsvarianten.
„Audit und Datenschutz“ verwendet die vorhandene Seite `nachweise-datenschutz`;
Kompetenznachweise werden im gleichnamigen Aufgabenfeld erklärt.

**Kein Backup-Dialog im Zielbaum:** Die vorhandene Produktseite ist ein Platzhalter.
Sicherung/Wiederherstellung ist ein wichtiger betrieblicher Bedarf, aber erst nach
Klärung eines unterstützten und praktisch geprüften Verfahrens als Anleitung
aufzunehmen. Der Oberbegriff „Sicherheit und Betrieb“ verspricht dafür noch keinen
funktionierenden Dashboard-Ablauf. Dasselbe gilt für ein noch zu prüfendes
Updateverfahren. Neue Navigationspunkte dürfen keine Produktlücke verdecken.

Die drei Einträge unter **Kompetenzen und Nachweise** haben verschiedene Zwecke:
Fähigkeiten und Lernwege festlegen, eine Badge-Definition samt Inhaltsversionen
pflegen und einen externen Anbieter anbinden. Die erste Anleitung verweist für
die Badge-Erstellung auf die vorhandene Badge-Anleitung. Sie schreibt denselben
Assistenten nicht erneut aus. Konkrete Bewertungen, Vergaben und Teilnahmen
verlinken von dort nach Koordination.

### Installieren

```text
Installieren: Start
Server auf dem Raspberry Pi installieren
Geräte in Betrieb nehmen
Abnahme und Übergabe
Störung vor Ort
```

Die kurze Reihenfolge bleibt. Der Einstieg unterscheidet Neuaufbau und Anschluss
an einen vorhandenen Server. Unterstützte Plattform, Version, Netzwerk und
Übergabe an den laufenden Betrieb müssen erkennbar sein. Andere Plattformen oder
Betriebsverfahren werden nicht aus bloß vorhandenen Docker-/Deploy-Dateien als
abgenommene Installationswege abgeleitet.

### Entwickeln

```text
Entwickeln: Start
Integration planen
  Schnittstellen
  ├─ HTTP-API nutzen
  ├─ MQTT-Ereignisse beziehen
  ├─ MCP-Client anbinden
  └─ Eigene Automationsflüsse entwickeln [geplant]
  Referenz
  └─ HTTP-API-Referenz [generiert, eingeklappt]
```

Der Bereich richtet sich zuerst an Integratoren. Der Start benennt diesen Umfang
und verlinkt für Beiträge an Mardu auf die vorhandenen Entwickleranweisungen des
Software-Repositories. Eine vollständige Contributor-Dokumentation wird durch
diese vier Protokoll-/Integrationswege nicht behauptet. Runtime-Freigabe und
Berechtigungen für Automationen bleiben bei Administration; eigene Flüsse brauchen
hier ein überprüfbares Beispiel samt Rückmeldung und Fehlerfall.

## Grobe Inhalte und bestehende URLs

Pro Seite folgen vier Inhaltspunkte, durch Semikolon getrennt. Das ist ein
Arbeitsrahmen, keine Pflichtvorlage für vier Abschnitte. „Beibehalten“ bedeutet
wiederverwenden, nicht erneut abgenommen. Links zeigen auf die jetzigen Quellen;
Titel können sich ändern, URLs und verwendete Anker bleiben erhalten.

### Wegweiser und Überblick

| Seite / Quelle                                                                                               | Vier Inhaltspunkte                                                                                                | Vorgehen                                                                                    |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [Dokumentation](../docs/index.mdx)<br>`/docs`                                                                | Bereich wählen; neue Leser zum Überblick; Nutzung und Verwaltung unterscheiden; Grenzen des Dokumentationsstands. | Kürzen, kein zweiter Überblick.                                                             |
| [Mardu verstehen](../docs/ueberblick/index.mdx)<br>`/docs/ueberblick`                                        | Ressourcen und Personen; optionale Funktionen; Systembestandteile im Diagramm; nächste eigene Aufgabe.            | Ausgeschriebener Entwurf liegt separat vor.                                                 |
| [Personen, Rollen und Freigaben](../docs/ueberblick/benutzerkonten.mdx)<br>`/docs/ueberblick/benutzerkonten` | Konto und Anmeldung; Rollen und Gruppen; Ressourcenfreigaben und Nachweise; Herkunft und Sperrung von Zugängen.   | Bestehende Erklärung erhalten.                                                              |
| [Begriffe](../docs/ueberblick/grundlagen-begriffe.mdx)<br>`/docs/ueberblick/grundlagen-begriffe`             | Ressourcen und Anschlüsse; Konto/Rolle/Gruppe/Freigabe; Kompetenz/Definition/Vergabe; Sitzungen und Zustände.     | Als Nachschlageseite fokussieren.                                                           |
| [Neuerungen](../docs/ueberblick/neuerungen.mdx)<br>`/docs/ueberblick/neuerungen`                             | Eindeutiger Softwarestand; Verhaltensänderungen; nötige Umstellungen; aktualisierte Anleitungen.                  | Erst belegte Release-Inhalte veröffentlichen, bisheriger Schreibauftrag ist keine Historie. |

### Benutzer

| Seite / Quelle                                                                                                                      | Vier Inhaltspunkte                                                                                      | Vorgehen                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [Benutzer: Start](../docs/benutzer/index.mdx)<br>`/docs/benutzer`                                                                   | Erste Nutzung; Ressourcen nutzen; Kontoeinstellungen; Hilfe und Verwaltungswechsel.                     | Gute Aufgabenlinks erhalten.                               |
| [Erste Schritte](../docs/benutzer/erste-schritte.mdx)<br>`/docs/benutzer/erste-schritte`                                            | Server und Zugang; anmelden; Profil prüfen; erste Aufgabe und Abmelden.                                 | Beibehalten.                                               |
| [Persönliches Dashboard](../docs/benutzer/dashboard.mdx)<br>`/docs/benutzer/dashboard`                                              | Eigene Anzeigen; Zeitbezug der Werte; Anordnung ändern; speichern oder verwerfen.                       | Beibehalten.                                               |
| [Zugänge und Ressourcen](../docs/benutzer/zutritt.mdx)<br>`/docs/benutzer/zutritt`                                                  | Eigene Freigaben; Ressourcenkatalog; Bedingungen lesen; fehlenden Zugriff klären.                       | Von Admin-Zutrittsverwaltung trennen.                      |
| [Zugriff anfragen](../docs/benutzer/berechtigungsanfragen.mdx)<br>`/docs/benutzer/berechtigungsanfragen`                            | Ressource wählen; Anfrage begründen; Entscheidung verfolgen; offenen Antrag zurückziehen.               | Beibehalten.                                               |
| [Meine Buchungen](../docs/benutzer/buchungen.mdx)<br>`/docs/benutzer/buchungen`                                                     | Freien Zeitraum finden; reservieren; ändern/stornieren; Genehmigung und Check-in.                       | Beibehalten.                                               |
| [Kalender exportieren und abonnieren](../docs/benutzer/kalender.mdx)<br>`/docs/benutzer/kalender`                                   | Export oder Abo; Abo einrichten; Aktualisierung verstehen; privaten Link ersetzen/widerrufen.           | Beibehalten.                                               |
| [Meine Qualifikationen](../docs/benutzer/kompetenzen.mdx)<br>`/docs/benutzer/kompetenzen`                                           | Einweisungen; lokale Vergaben; importierte/signierte Nachweise; Gültigkeit und Korrektur.               | Beibehalten.                                               |
| [Ressourcenzustand und Störungen](../docs/benutzer/geraete-status.mdx)<br>`/docs/benutzer/geraete-status`                           | Verfügbarkeit lesen; gemeldeten Zustand einordnen; Störung beschreiben; zuständige Stelle erreichen.    | Keine Admin-Gerätediagnose ergänzen.                       |
| [Eigenes Profil](../docs/ueberblick/profil.mdx)<br>`/docs/ueberblick/profil`                                                        | Persönliche Angaben; Profilbild; Pflichtangaben; weitere Kontoeinstellungen.                            | Kurze Übersicht erhalten.                                  |
| [E-Mail und Anmeldesicherheit](../docs/ueberblick/profil-sicherheit.mdx)<br>`/docs/ueberblick/profil-sicherheit`                    | E-Mail/Passwort ändern; zweiten Faktor einrichten; Wiederherstellungscodes sichern; Passkeys verwalten. | Beibehalten.                                               |
| [Eigene Sitzungen](../docs/ueberblick/profil-sitzungen.mdx)<br>`/docs/ueberblick/profil-sitzungen`                                  | Sitzung erkennen; einzelne widerrufen; andere beenden; unbekannte Anmeldung klären.                     | Beibehalten.                                               |
| [Meine Zutrittsmedien](../docs/ueberblick/profil-zutrittsmedien.mdx)<br>`/docs/ueberblick/profil-zutrittsmedien`                    | Zugeordnete Medien; Status/Gültigkeit; Verlust melden; Ersatz anfragen.                                 | Einrichtung zur Admin-Anleitung verlinken.                 |
| [Persönliche Nachweisquellen](../docs/ueberblick/profil-nachweisquellen.mdx)<br>`/docs/ueberblick/profil-nachweisquellen`           | Angebotenen Anbieter wählen; Zugang verbinden; Herkunft und Importstatus; Verbindung trennen.           | Unterstützungsgrenzen prüfen.                              |
| [Eigene MCP-Verbindungen](../docs/ueberblick/profil-mcp.mdx)<br>`/docs/ueberblick/profil-mcp`                                       | Begrenzten Zugang erstellen; einmaligen Token übernehmen; Client eintragen; erneuern/widerrufen.        | Distill-/Polish-Ergebnis erhalten.                         |
| [Benachrichtigungen lesen](../docs/benutzer/benachrichtigungen.mdx)<br>`/docs/benutzer/benachrichtigungen`                          | Posteingang öffnen; lesen; archivieren/rückgängig; fehlende Meldung einordnen.                          | Beibehalten.                                               |
| [Benachrichtigungseinstellungen](../docs/ueberblick/profil-benachrichtigungen.mdx)<br>`/docs/ueberblick/profil-benachrichtigungen`  | Kanäle/Ereignisse; Pflichtmeldungen; Ruhezeiten/Stummschaltung; speichern/verwerfen.                    | Von Lesen und Serverzustellung abgrenzen.                  |
| [Erscheinungsbild und Anzeigeformate](../docs/ueberblick/profil-erscheinungsbild.mdx)<br>`/docs/ueberblick/profil-erscheinungsbild` | Theme; Zeitzone; Zahlen-/Datumsformat; Bedienhilfen.                                                    | Beibehalten.                                               |
| [Hilfe](../docs/ueberblick/fehlersuche.mdx)<br>`/docs/ueberblick/fehlersuche`                                                       | Anmeldung; Zugriff; Buchung/Kalender; Nachweise/Medien/Mitteilungen.                                    | Nach Symptom gliedern, aus betroffenen Aufgaben verlinken. |

### Koordination

| Seite / Quelle                                                                                                  | Vier Inhaltspunkte                                                                                                  | Vorgehen                                         |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| [Koordination: Start](../docs/koordination/index.mdx)<br>`/docs/koordination`                                   | Verantwortungsbereich; Verfügbarkeit prüfen; Anfragen entscheiden; Bewertung/Vergabe.                               | Schreibauftrag durch Wegweiser ersetzen.         |
| [Buchungen verwalten](../docs/koordination/buchungen-verwalten.mdx)<br>`/docs/koordination/buchungen-verwalten` | Kalender/Schließzeiten; Anfragen entscheiden; Buchungen ändern; Gruppenlimits als Voraussetzung nachschlagen.       | Entwurf gegen reale Abläufe ausarbeiten.         |
| [Bewertungen durchführen](../docs/koordination/bewertungen.mdx)<br>`/docs/koordination/bewertungen`             | Bewertungsauftrag finden; Voraussetzungen/Nachweise; Entscheidung erfassen; Ergebnis und weitere Vergabe einordnen. | Verfügbare Verfahren und Zuständigkeiten prüfen. |

### Administration

| Seite / Quelle                                                                                                                                             | Vier Inhaltspunkte                                                                                                         | Vorgehen                                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| [Administration: Start](../docs/administration/index.mdx)<br>`/docs/administration`                                                                        | Einrichtungsaufgaben wählen; Personen/Zugänge; Technik/Anbindungen; Betrieb und Koordination.                              | Keine universelle Einrichtungspflicht für alle Funktionen.                                                                 |
| [Benutzerkonten verwalten](../docs/administration/benutzer-rollen.mdx)<br>`/docs/administration/benutzer-rollen`                                           | Konten anlegen; Kontenstatus; Rollen/Gruppen/Rechte; externe Quellen und verbleibende Zuweisungen.                         | Kontenpflege erhalten; Rollen-/Gruppenpflege in eigene geplante Anleitung, Zuweisung am Konto hier behalten.               |
| [Ressourcen einrichten](../docs/koordination/ressourcen.mdx)<br>`/docs/koordination/ressourcen`                                                            | Anlegen/strukturieren; Zugriff und Technik; Buchbarkeit; Sperren/Wartung/Stilllegung.                                      | Admin-Heimat bei gleicher URL; Betriebsaufgaben später nach Koordination ausgliedern und alte Anker als Verweise erhalten. |
| [Zutritt verwalten](../docs/administration/zutritt-verwalten.mdx)<br>`/docs/administration/zutritt-verwalten`                                              | Ressourcenregel/Zutrittspunkt; Zuständigkeiten; Freigaben/Anträge; Sitzungen/Protokolle.                                   | Mit Ressourcenanleitung abgleichen, Konfiguration nicht doppeln.                                                           |
| [Zugangs-Tags verwalten](../docs/administration/tags-verwalten.mdx)<br>`/docs/administration/tags-verwalten`                                               | Connect-App und Karte; anmelden/zuweisen; Verlust sperren; Ersatz und Fehler.                                              | Distill-/Polish-Ergebnis erhalten, Hardwareabnahme bleibt offen.                                                           |
| [Badges verwalten](../docs/administration/badges-verwalten.mdx)<br>`/docs/administration/badges-verwalten`                                                 | Definition/Version erstellen; Kriterien/Voraussetzungen; aktivieren/veröffentlichen; Folgen für Vergaben.                  | Definitionen von persönlichen Vergaben trennen, Entwurf vervollständigen.                                                  |
| [Audit und Datenschutz](../docs/administration/nachweise-datenschutz.mdx)<br>`/docs/administration/nachweise-datenschutz`                                  | Datenarten/Aufbewahrung; Audit suchen/exportieren; Auskunft/Berichtigung/Löschung; öffentlich geteilte Inhalte.            | Produktverhalten von organisatorischen und rechtlichen Vorgaben trennen.                                                   |
| [Geräte verwalten](../docs/administration/geraete-verwalten.mdx)<br>`/docs/administration/geraete-verwalten`                                               | Aufnehmen/verbinden; Anschlüsse konfigurieren; Ressource zuordnen; Diagnose/Austausch/Löschen.                             | Vorhandene Anleitung erhalten, Montage zur Installation verlinken.                                                         |
| [Automationen](../docs/administration/automationen.mdx)<br>`/docs/administration/automationen`                                                             | Runtime aktivieren; Editor öffnen; Anschluss veröffentlichen/zuordnen; Aktion und Rückmeldung prüfen.                      | Parallele Überarbeitung weiterverwenden, nicht überschreiben.                                                              |
| [Externe Systeme anbinden](../docs/administration/integrationen.mdx)<br>`/docs/administration/integrationen`                                               | Anbindung/Datenrichtung wählen; LDAP/OIDC; Nachweisanbieter; testen und trennen.                                           | Einstieg erhalten; LDAP/OIDC/MQTT/IP500/Nachweise mit eigenen Admin-Aufgaben, Protokolle zusätzlich nach Entwickeln.       |
| [MCP für Agenten freigeben](../docs/administration/mcp-verwalten.mdx)<br>`/docs/administration/mcp-verwalten`                                              | Serverfreigabe/Rechte; persönlicher Lesezugang; Schreibrechte/Grenzwerte; einschränken/abschalten.                         | Distill-/Polish-Ergebnis erhalten.                                                                                         |
| [Servereinstellungen](../docs/administration/server-einstellungen.mdx)<br>`/docs/administration/server-einstellungen`                                      | Globale Werte; speichern/Neustart; gesperrte Angaben; Anmelde-/Zertifikatsverfahren verlinken.                             | Referenzdetails verlinken, nicht jede Option im Einstieg aufzählen.                                                        |
| [Benachrichtigungen einrichten und prüfen](../docs/administration/benachrichtigungen-verwalten.mdx)<br>`/docs/administration/benachrichtigungen-verwalten` | Kanäle vorbereiten; E-Mail testen; Ereignis bis Empfang; Pflichtkanäle/Fehler.                                             | Vorhandene Anleitung erhalten, externe Zustellung nicht pauschal abgenommen.                                               |
| [Übersicht und Systemstatus](../docs/benutzer/uebersicht-monitoring.mdx)<br>`/docs/benutzer/uebersicht-monitoring`                                         | Zeitraum/Diagramme; System-/Ressourcenwerte; fehlende Daten; Alarm und Diagnose.                                           | Unter Admin-Betrieb einordnen, URL erhalten.                                                                               |
| [Sicherheit und Betrieb](../docs/administration/sicherheit-betrieb.mdx)<br>`/docs/administration/sicherheit-betrieb`                                       | Sicherheitsaufgaben zuordnen; administrative Zugriffe; Störungen/Wiederanlauf; belegte Betriebsverfahren und ihre Grenzen. | Kein Backup-/Updateversprechen; vorhandene GUI-Sicherung ist Platzhalter, externe Verfahren zuerst klären.                 |
| [Mardu per CLI warten](../docs/administration/wartungs-cli.mdx)<br>`/docs/administration/wartungs-cli`                                                     | Lokalen Zugriff vorbereiten; Konto wiederherstellen; Sitzungen widerrufen; Serverzustand prüfen.                           | Aufgabenanleitung beibehalten.                                                                                             |
| [Wartungs-CLI: Befehle und Optionen](../docs/administration/wartungs-cli-referenz.mdx)<br>`/docs/administration/wartungs-cli-referenz`                     | Aufrufe/Optionen; Rechte/Konfiguration; JSON-Ausgabe; Rückgabewerte/Fehler.                                                | Referenz erhalten, keine zweite Schrittanleitung.                                                                          |

### Installieren

| Seite / Quelle                                                                                                         | Vier Inhaltspunkte                                                                                | Vorgehen                                                      |
| ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| [Installieren: Start](../docs/installieren/index.mdx)<br>`/docs/installieren`                                          | Neuer oder vorhandener Server; Serveraufbau; Hardwareaufnahme; Übergabe und Hilfe.                | Unterstützte Wege benennen.                                   |
| [Server auf dem Raspberry Pi installieren](../docs/installieren/raspberry-pi.mdx)<br>`/docs/installieren/raspberry-pi` | Voraussetzungen/Paket; Zugang zu Images; Konfiguration/Start; Erstzugang und Prüfung.             | Vorhandene Anleitung in Bereichsfilter aufnehmen.             |
| [Geräte in Betrieb nehmen](../docs/installieren/inbetriebnahme.mdx)<br>`/docs/installieren/inbetriebnahme`             | Vorbereitung/Montage; Strom/Netzwerk; Softwareaufnahme; Anschluss- und Funktionstest.             | Hardwarevarianten und elektrische Zuständigkeiten prüfen.     |
| [Abnahme und Übergabe](../docs/installieren/abnahme-uebergabe.mdx)<br>`/docs/installieren/abnahme-uebergabe`           | Vereinbarte Funktionen; physischer Test; Protokoll/Zugänge; Verantwortliche und Restpunkte.       | Konkrete Prüfnachweise statt allgemeiner Erfolgssätze.        |
| [Störung vor Ort](../docs/installieren/stoerung-vor-ort.mdx)<br>`/docs/installieren/stoerung-vor-ort`                  | Strom/Netzwerk/Server; Gerät/Zutrittspunkt; kontrollierter Wiederanlauf; Supportdaten/Eskalation. | Befehle und Folgen prüfen, nicht pauschal Neustart empfehlen. |

### Entwickeln

| Seite / Quelle                                                                                     | Vier Inhaltspunkte                                                                                           | Vorgehen                                              |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- |
| [Entwickeln: Start](../docs/entwickeln/index.mdx)<br>`/docs/entwickeln`                            | Integrationsziel; Schnittstelle wählen; Testzugang/Rechte; Referenz finden.                                  | Kurzer Wegweiser.                                     |
| [Integration planen](../docs/entwickeln/api-integration.mdx)<br>`/docs/entwickeln/api-integration` | HTTP/MQTT/MCP vergleichen; Identität/Rechte; unterstützte Datenflüsse; Test und Betrieb.                     | Entscheidungshilfe statt zweiter Protokollreferenz.   |
| [HTTP-API nutzen](../docs/entwickeln/http-api.mdx)<br>`/docs/entwickeln/http-api`                  | Authentifizierung; erster Leseaufruf; Mutation/Validierung; Fehler/Parallelität/Pagination soweit vorhanden. | Beispiele gegen OpenAPI und Server prüfen.            |
| [MQTT-Ereignisse beziehen](../docs/entwickeln/mqtt-events.mdx)<br>`/docs/entwickeln/mqtt-events`   | Verbindung/TLS; Benutzer/ACL; Topic/Payload; Empfang/Fehler.                                                 | Nur belegte Topics und Zustellsemantik dokumentieren. |
| [MCP-Client anbinden](../docs/entwickeln/mcp-anbindung.mdx)<br>`/docs/entwickeln/mcp-anbindung`    | URL/Bearer-Token; Protokollinitialisierung; Werkzeugaufruf; Widerruf/Fehler/Grenzwerte.                      | MCP fokussieren, Node-RED-Verwaltung verlinken.       |

## Ergänzender Aufgabenbedarf

Die Bestandszuordnung oben beschreibt vorhandene Quellen. Diese zusätzlichen
Zuschnitte schließen belegte Lücken oder trennen überladene Aufgaben. Sie sind
**geplant, nicht geschrieben oder praktisch abgenommen**. Die Zieladressen sind
Vorschläge, keine Links zu existierenden Seiten. P0 klärt das Fundament, P1 die
Kernabläufe und P2 optionale Vertiefungen. Nicht alle Seiten müssen vor der ersten
Navigationsverbesserung entstehen; nutzbare Bestandsabschnitte dienen bis dahin als
Quellen. Beim Ausgliedern bleiben alte Anker als beschriftete Verweise erhalten.

| Bereich / geplante Seite                             | Vorgeschlagene Zieladresse                         | Vier Inhaltspunkte                                                                                                     | Beleg / Grenze                                                                                                                | Reihenfolge |
| ---------------------------------------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ----------- |
| Administration: Rollen und Gruppen verwalten         | `/docs/administration/rollen-gruppen`              | Rollen/Rechte bearbeiten; Gruppen anlegen/pflegen; Mitglieder/Gruppenrollen; verbleibende Rechte und Gruppenlimits.    | Rollen- und Gruppenoberfläche; bisherige Kontenanleitung deckt das ausdrücklich nicht vollständig ab.                         | P0          |
| Administration: Verwaltungszuständigkeiten vergeben  | `/docs/administration/verwaltungszustaendigkeiten` | Zielbereich wählen; Person/Gruppe/Rolle zuordnen; Rechteumfang/Gültigkeit prüfen; diagnostizieren und widerrufen.      | Scopes-Oberfläche und Diagnose vorhanden; Vererbung/Delegationsgrenzen im Vertrag prüfen.                                     | P0          |
| Administration: Kompetenzen und Lernwege einrichten  | `/docs/administration/kompetenzen-lernwege`        | Katalog/Kompetenz definieren; Kriterien und Versionen; Lernweg zusammenstellen; Folgen für bestehende Teilnahmen.      | Kompetenz-Workspace und LearningPathsController vorhanden; Beispiele benötigen praktische Abnahme.                            | P1          |
| Administration: Nachweissysteme anbinden             | `/docs/administration/nachweissysteme`             | Aussteller/Anbieter einrichten; unterstützte Datenflüsse; Identitäts-/Anerkennungsregeln; Synchronisation/Prüfgrenzen. | Anbieter-, Anerkennungs- und Ausstellungsseiten vorhanden; Remote-Prüfung nicht pauschal als vollständig verfügbar behandeln. | P2          |
| Administration: LDAP-Verzeichnis anbinden            | `/docs/administration/ldap`                        | Verbindung/TLS testen; Attribute zuordnen; Synchronisation und Konflikte; Änderungen/Trennung und Kontoauswirkung.     | Eigene Einstellungsseite, alte Integrationsroute leitet dorthin weiter.                                                       | P1          |
| Administration: Anmeldung über OpenID Connect        | `/docs/administration/oidc`                        | Anbieter/Callback konfigurieren; Claims und Kontoanlage; Testanmeldung; Änderung/Abschaltung und Wiederzugang.         | Eigene Einstellungsseite; Wiederzugangsfolgen vor Anleitung praktisch prüfen.                                                 | P1          |
| Administration: MQTT verwalten                       | `/docs/administration/mqtt-verwalten`              | Broker/Betriebsform; Benutzer und Zugangsdaten; ACLs; Verbindung und verweigertes Abonnement prüfen.                   | Broker-/Benutzerbereiche in integrations-nav.config.ts; Client-Payloads bleiben Entwicklerreferenz.                           | P1          |
| Administration: IP500-Netzwerk anbinden              | `/docs/administration/ip500`                       | Betriebsform prüfen; Verbindung konfigurieren; Gateway-/Gerätestatus; Abgleich und Fehler.                             | Konfigurationsseite mit API-Aufrufen vorhanden; realer Gatewaytest steht gesondert aus.                                       | P2          |
| Administration: Anmeldung und Kontoschutz            | `/docs/administration/anmeldung-kontoschutz`       | Registrierungs-/Freigaberegeln; erforderliche Anmeldeverfahren; Änderungen und bestehende Konten; Wiederzugang prüfen. | Auth-Policy-Einstellungen vorhanden; persönliche Einrichtung des Faktors bleibt Benutzeranleitung.                            | P1          |
| Administration: Zertifikate und HTTPS                | `/docs/administration/zertifikate`                 | Zertifikatszweck bestimmen; bereitstellen/zuordnen; Ablauf und Erneuerung; Erreichbarkeit nach Änderung prüfen.        | Zertifikatsbereich vorhanden; konkrete unterstützte Verfahren zuerst abgleichen.                                              | P1          |
| Koordination: Verfügbarkeit und Wartung koordinieren | `/docs/koordination/verfuegbarkeit-wartung`        | Zustand einordnen; Sperre planen/aufheben; Wartung starten/abschließen; Buchungs-/Zugriffsfolgen prüfen.               | Vorhandene Ressourcenanleitung; später ausgliedern und dortige Anker als Verweise erhalten.                                   | P1          |
| Koordination: Zugangsanträge entscheiden             | `/docs/koordination/zugangsantraege`               | Antrag/Zuständigkeit; Bedingungen/Nachweise; genehmigen/ablehnen; resultierende Freigabe prüfen.                       | Antragsoberfläche vorhanden; bisheriger Zutrittsentwurf noch unvollständig.                                                   | P1          |
| Koordination: Vergaben und Lernwegteilnahmen         | `/docs/koordination/vergaben-lernwege`             | Person und Ziel wählen; Vergabe/Gültigkeit; Einschreibung/Fortschritt; Abschluss/Widerruf und Anerkennung.             | Vergabe-Workspace und Lernwegvertrag vorhanden; konkrete Verfahren einzeln prüfen.                                            | P1          |
| Entwickeln: Eigene Automationsflüsse entwickeln      | `/docs/entwickeln/automationsfluesse`              | Testumgebung/Rechte; Ein-/Ausgänge und Fluss; Anschluss veröffentlichen/zuordnen; Rückmeldung und Fehler prüfen.       | Bestehende Runtime-/Automationsanleitung als Grundlage; braucht ausführbares Beispiel statt neuem Protokollversprechen.       | P2          |

Die generierte **HTTP-API-Referenz** unter `/docs/entwickeln/API/…` bleibt ein
Referenzbaum: Endpunkte; Request/Response; Rechte/Validierung; Statuscodes und
Modelle. Quelle im Software-Consumer ist `contracts/backend-swagger-docs.json`.
Keine Handbearbeitung oder Einzelplanung aller generierten Endpunktseiten.

Die historischen [v1](../docs/v1/index.mdx)- und [v2](../docs/v2/index.mdx)-Einstiege
bleiben erreichbar, ohne aktuelle Sidebar-Einträge: historische Adresse erhalten;
zum aktuellen Einstieg führen; keine Softwareversion behaupten; Inhalte nicht
duplizieren. Eine Versionsnavigation braucht ein belegtes Release-Modell.

## Überblick und Grafiken

Der [Entwurf](../drafts/2026-11-01-mardu-verstehen.md) erklärt Ressourcen und
Personen, zeigt einen Raum ohne Hardware neben einer angebundenen Maschine,
unterscheidet Freigabe/Buchung/Nachweis/Identifikation und ordnet die Bestandteile
des Systems ein. Zwei Mermaid-Diagramme zeigen Beziehungen und Systemgrenzen.
Sie sind keine Datenbankstruktur und kein garantierter Ablauf jeder Installation.
Keine Akkordeons, Einstellungslisten oder Screenshot-Sammlung im Einstieg.

Wichtige Grenzen aus der Codelektüre: `BookingResource` kann auch ohne verknüpfte
`ManagedResource` bestehen. Das gemeinsame Ressourcenmodell ist eine Orientierung,
kein behauptetes Datenbankschema aller Buchungen. Externe Nachweisquellen bedeuten
keine unbegrenzte Badge-Kompatibilität: `RemoteW3cBadgeProvider` implementiert
beispielsweise derzeit keine vollständige Prüfung externer Signaturen,
Ausstellervertrauen und Widerrufsstatus.

## Umsetzung nach der Strukturentscheidung

1. **Consumer prüfen:** Software ist hier untersucht. Die Website konsumiert
   dieselben Inhalte, ihre Navigation wurde für diesen Plan nicht ausgeführt.
2. **Quellen gemeinsam anpassen:** `docs/*/meta.json` ordnet die Seiten;
   `web/lib/docs-roles.tsx` filtert und bestimmt den aktiven Bereich. Vorhandene
   Fumadocs-Mittel wiederverwenden; keine zusätzliche, parallel gepflegte
   Gesamtstruktur im Produkt einführen.
3. **Zwischenüberschriften erhalten:** Die installierte Fumadocs-Version unterstützt
   `"---Personen und Zugänge---"` in `meta.json`. Der aktuelle Filter übernimmt nur
   Seiten und Ordner und verwirft Separator-Knoten. Gruppen zusammen mit sichtbaren
   Seiten erhalten; leere Gruppen entfernen.
4. **Bereichsstart zeigen:** Beim Abflachen des Bereichsordners wird dessen Index
   derzeit nicht als erster Eintrag übernommen. Ihn ausdrücklich zeigen; aktive
   Bereichserkennung und eindeutige Baum-IDs erhalten.
5. **Profil logisch zuordnen:** Bestehende Profil-URLs unter `ueberblick/` erhalten,
   im Benutzerbereich in die passenden Gruppen einordnen. Die bisherige Sortierung
   „Ordner ans Ende“ darf diese Reihenfolge nicht zerstören.
6. **Zuordnung vervollständigen:** Badges und Raspberry-Pi-Anleitung aufnehmen;
   Ressourcen-Einrichtung und Monitoring Administration zuordnen, ihre URLs erhalten.
   Überblick bekommt keine zusätzliche Profil-Sidebar. Querverweise nennen den
   Zielbereich; heutige URL-basierte Bereichserkennung erhält nicht automatisch
   den vorherigen Lesekontext.
7. **Grafiken darstellen:** Im untersuchten Software-Consumer ist keine Mermaid-
   Komponente registriert. Vor Veröffentlichung in beiden Consumern die Darstellung
   ergänzen oder aus Mermaid erzeugte SVGs verwenden. Ein Codeblock allein genügt nicht.
8. **Erst fertige Seiten zeigen:** Neue Vertiefungen erst mit nutzbarem Inhalt
   eintragen. Schreibaufträge aus Bereichsstarts ins interne Backlog verschieben;
   unfertige Anleitungen nicht durch die Umgruppierung als fertig markieren.

Navigation und spätere Inhaltsüberarbeitung bleiben getrennt reviewbar. Dieser
Auftrag ändert weder API/DTOs noch Autorisierung. Die kanonische Doku-`AGENTS.md`
wird verdichtet; die Backend- und Sicherheitsregeln im Root bleiben bestehen.

## Reihenfolge und Prüfung

- **Jetzt:** Kritisch revidierter Strukturvorschlag, Aufgabenmatrix und dokumentierte Befunde.
- **Danach:** Nutzbaren ersten Stand umsetzen: Überblick, Bereichsstarts und
  vorhandene Anleitungen einordnen, beschriftete Querverweise setzen. Geplante
  Seiten erst nach Ausarbeitung sichtbar machen; alte Anker erhalten.
- **Für diesen ersten Stand:** Ausgearbeitete Bestandsanleitungen wiederverwenden.
  Eine Seite, die überwiegend aus Schreibaufträgen besteht, erhält erst nach
  Ausarbeitung einen neuen sichtbaren Eintrag. Falls eine vorhandene Anleitung
  nur teilweise fertig ist, werden nutzbare Aufgaben und offene Abdeckung im
  internen Arbeitsplan getrennt erfasst. Eine Lücke wird durch die neue Navigation
  weder als erledigt markiert noch mit einer weiteren leeren Seite verdeckt.
- **Anschließend:** Offene Kernanleitungen zu Zutritt, Buchungsverwaltung und Betrieb
  anhand echter Abläufe vervollständigen; optionale Anbindungen danach.

Mit neuen Lesern aus Nutzung und Verwaltung prüfen, ob folgende Suchaufgaben ohne
Erklärung des Autors gelingen. Ersten gewählten Bereich, Umwege und unklare Titel
notieren. Kein fester Klickwert ist ein Qualitätsbeweis.

| Suchaufgabe                                                | Erwarteter Weg                                                                                 |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| „Ich möchte einen Raum ohne Lesegerät buchbar machen.“     | Überblick → Administration → Ressourcen/Buchbarkeit; Querverweis vom Koordinationsstart.       |
| „Ich habe meine Karte verloren.“                           | Benutzer → Meine Zutrittsmedien/Hilfe; Verwaltung → Zugangs-Tags/Sperrung.                     |
| „Ich möchte einen Agenten verbinden.“                      | Benutzer → Eigene MCP-Verbindungen; bei fehlender Freigabe Administration/MCP.                 |
| „Ich möchte eine Buchung genehmigen.“                      | Koordination → Buchungen verwalten.                                                            |
| „Ich möchte Mitarbeiter aus einem Verzeichnis übernehmen.“ | Administration → LDAP-Verzeichnis anbinden; bis dahin Integrationseinstieg mit LDAP-Abschnitt. |
| „Ich möchte ein MQTT-Ereignis empfangen.“                  | Entwickeln → MQTT-Ereignisse beziehen.                                                         |
| „Ich baue einen neuen Server auf.“                         | Installieren → Raspberry-Pi-Installation.                                                      |
| „Die Anlage meldet keine Werte.“                           | Administration → Übersicht und Systemstatus → Geräte/Automationen je Quelle.                   |

Zusätzlich technisch prüfen: bestehende URLs/Anker; Direktaufruf und Zurück-
Navigation; Reihenfolge und aktive Seite; keine leeren Gruppen oder doppelten
Starts; Tastatur und mobile Sidebar; Diagramme in Hell/Dunkel; keine Planungsdateien
im Produkt-Suchindex.

Offen sind die Strukturabstimmung, die Website-Prüfung und Tests mit Lesern.
Codelektüre für das Modell ersetzt keine neue Hardware-, Protokoll- oder
Zustellabnahme. Frühere offene Prüfungen bleiben bestehen.

## Prüfstand dieses Vorschlags nach Revision

- Alle 54 aktuellen Seiten und beide historischen Einstiege bleiben im Inventar erfasst.
  Ergänzend sind 14 geplante Zuschnitte mit Inhalt, Quelle und Grenze benannt.
  Diese Anzahl ist eine Arbeitsannahme und kein Vollständigkeitsmaß.
- Die relativen Dateilinks und die Formatierung der geänderten Markdown-Dateien
  wurden geprüft; es wurden keine Produkt-URLs oder API-Verträge geändert.
- Beide Diagramme wurden mit Mermaid 11.12.0 gerendert und als SVG zum Entwurf
  abgelegt. Die separate Vorschau wurde bei 1200 und 390 Pixel Breite geprüft.
  Die Diagramme sind mobil innerhalb ihres Bereichs verschiebbar. Dies ist keine
  Prüfung der noch ausstehenden Mermaid-Integration in den Produkt-Consumern.
- Die frühere unabhängige Prüfung auf offene Umsetzungsfragen war keine Prüfung
  der Aufgabenabdeckung. Die kritische Revision benennt ihre Lücken und gleicht
  ausgewählte Produktbereiche im Code ab. Daraus folgt keine Funktionsabnahme.
- Website, Nutzer-Suchtests, die Live-Umsetzung und die praktische Abnahme der
  zusätzlich erfassten Aufgaben stehen weiterhin aus.
