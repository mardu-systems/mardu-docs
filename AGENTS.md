# Mardu-Dokumentation: Regeln für Agenten

Diese Datei legt die Dokumentationsregeln für `mardu-systems/mardu-docs` fest.
Consumer-Repositories verlinken hierher, statt die Regeln zu kopieren. Sie gelten
auch für begleitende Dokumentation bei Änderungen an Software, APIs und Betrieb.
Die Architektur-, Sicherheits- und Entwicklungsregeln des jeweiligen Projekts
gelten zusätzlich. Wende Regeln nur an, wenn sie für die betroffene Dokumentation
relevant sind.

## Ablage und vorhandene Struktur

- Produktdokumentation und ihre Bilder werden in diesem Repository gepflegt.
  Website und Software konsumieren dieselben Inhalte über Git-Submodule.
- Veröffentlichte Seiten liegen unter `docs/`. Agentenanweisungen wie diese Datei
  bleiben außerhalb dieses Ordners, damit sie nicht als Produktseite erscheinen.
- Prüfe vor einer Änderung die vorhandenen Seiten, `meta.json`, Komponenten und
  die Dokumentationskonfiguration des betroffenen Consumers. Verwende vorhandene
  Mittel, bevor du neue Abstraktionen, Werkzeuge oder Abhängigkeiten einführst.
- Erhalte bestehende URLs und die Navigation nach Zielgruppen. Lege keine leeren
  Ordner für Dokumentationstypen an und strukturiere nicht ohne Auftrag alles um.
- Beginne relative MDX-Seitenverweise mit `./` oder `../`, damit die vorhandene
  Fumadocs-Linkauflösung sie in Seitenadressen umwandelt; prüfe auch Abschnittsanker.
- Jede veröffentlichte MDX-Seite erhält `title` und `description` im Frontmatter.
  Kein zusätzliches H1 im Inhalt; der Consumer zeigt den Seitentitel bereits an.
  Trage neue Seiten in die passende `meta.json` ein.

## Zielgruppe und Wissensstand

Orientierung: [Google Technical Writing: Audience](https://developers.google.com/tech-writing/one/audience).

- Bestimme vor dem Schreiben die Zielgruppe, ihr Vorwissen und das gewünschte
  Ergebnis. Eine Rollenbezeichnung allein beschreibt den Wissensstand nicht.
- Nutze die vorhandenen Bereiche: Überblick, Benutzer, Koordination,
  Administration, Installieren und Entwickeln.
- Erkläre Wissen, das die Leser für ihre Aufgabe brauchen, aber noch nicht
  vorausgesetzt werden kann. Erläutere unbekannte Abkürzungen beim ersten Gebrauch.
- Bedienungsanleitungen beschreiben Aufgaben und Auswirkungen. Interne Klassen,
  DTOs oder Implementierungsdetails gehören nur hinein, wenn sie bei der Aufgabe
  helfen; ansonsten verlinke Entwicklerdokumentation.
- Vermeide vorausgesetztes Teamwissen, Redewendungen und kulturelle Vergleiche.
  Schreibe so, dass auch neue Mitarbeitende und Übersetzungen den Text verstehen.

## Dokumentationstyp nach Diátaxis

Grundlage: [Diátaxis](https://diataxis.fr) und
[die vier Dokumentationstypen](https://diataxis.fr/start-here/).
Wähle für jede Seite einen Hauptzweck:

| Typ                 | Bedürfnis der Leser                | Aufbau                                                                      | Mardu-Beispiel                              |
| ------------------- | ---------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------- |
| Einstieg / Tutorial | Durch eigenes Tun etwas lernen     | Geführter, überprüfbarer Lernweg mit Beispieldaten und erkennbarem Ergebnis | Dein erstes Badge anlegen                   |
| Anleitung / How-to  | Eine bekannte Aufgabe erledigen    | Benötigte Rechte, Schritte und Ergebnis; relevante Varianten und Fehler     | Eine Badge-Vergabe widerrufen               |
| Referenz            | Fakten nachschlagen                | Felder, Typen, Werte, Grenzen und Verhalten nach fester Struktur            | Badge-Felder und Statuswerte                |
| Erklärung           | Zusammenhänge und Gründe verstehen | Begriffe, Beziehungen, Auswirkungen und begründete Entscheidungen           | Fähigkeiten, Badges, Versionen und Vergaben |

- Vermische nicht umfangreiche Erklärungen, vollständige Referenzen und
  Arbeitsschritte auf einer Seite. Verlinke ergänzende Inhalte am passenden Punkt.
- Ein Tutorial vermittelt einen Lernweg; eine Anleitung löst eine konkrete
  Aufgabe. Zwinge erfahrene Leser nicht durch einen Einführungskurs.
- Eine Referenz enthält überprüfbare Fakten. Eine Erklärung macht Beziehungen
  verständlich und kennzeichnet Annahmen oder Abwägungen.
- Halte gemeinsam benötigte Begriffe an einer Stelle und verlinke dorthin,
  statt Definitionen über mehrere Seiten zu duplizieren.
- Vermeide pauschale „Weiter“-Abschnitte und wiederholte Linklisten. Setze Verweise
  bei der passenden Aufgabe. Wiederhole ein Ziel nur, wenn ein anderer Ablauf oder
  eine notwendige Voraussetzung dies begründet; Warnungen gehören vor die jeweilige Aktion.

## Aufgaben, Ergebnisse und Sprache

- Beginne mit dem Zweck: Was ermöglicht die Funktion, wofür wird sie verwendet
  und welche anderen Begriffe muss man dafür kennen?
- Für Anleitungen gilt, soweit relevant: Ziel → benötigte Rechte und
  Voraussetzungen → nummerierte Schritte → erwartetes Ergebnis → Probleme und
  Abhilfe. Nenne Umgebungs- oder Versionsbedingungen vor dem betroffenen Schritt.
- Verwende exakte UI-Bezeichnungen und beschreibe jeweils eine konkrete Aktion.
  Schreibe etwa „Wähle **Neue Version speichern**“, nicht „klicke rechts unten“.
- Beschreibe auch die Auswirkung: Was wird gespeichert, veröffentlicht, entfernt
  oder freigegeben? Welche vorhandenen Daten oder Vergaben bleiben erhalten?
- Benenne Konsequenzen einer schwer rückgängig zu machenden Aktion vor ihrer
  Ausführung. Platziere Hinweise dort, wo sie für eine Entscheidung nötig sind.
- Schreibe aktiv, sachlich und direkt. Vermeide Werbung, Floskeln, unbelegte
  Versprechen und bedeutungsarme Zusätze wie „einfach“, „optimal“ oder „sicher“.
- Verwende Domänenbegriffe durchgehend gleich. Unterscheide zum Beispiel
  Badge-Definition, Inhaltsversion und Vergabe sowie Rolle und Benutzergruppe.
- Verwende Tabellen für vergleichbare Felder oder Zustände, Listen für Schritte
  oder Aufzählungen und Absätze für Erklärungen. Vermeide unnötige Verschachtelung.
- Vorhandene Übersetzungen müssen in Bedeutung, Beispielen und Verhalten
  übereinstimmen. Neue Sprachen oder Übersetzungswerkzeuge benötigen einen Auftrag.

## Verhalten belegen

- Lies die betroffenen Implementierungen, DTOs, Validatoren und Berechtigungen,
  bevor du Systemverhalten beschreibst. Die UI allein belegt keine Backend-Wirkung.
- Prüfe Abläufe durch Ausführen, soweit ein geeigneter Testzugang vorhanden ist.
  Kennzeichne Grenzen der Prüfung; behaupte keinen Test, der nicht stattgefunden hat.
- Unterscheide verfügbare Funktionen, Einschränkungen und geplante Funktionen.
  Beschreibe Pläne nie als bereits nutzbares Verhalten.
- Erfinde keine Felder, Prüfungen, Statuscodes, Zeitangaben oder Automatismen.
  Dokumentiere Abweichungen zwischen UI und API als Einschränkung.
- Nutze reproduzierbare, fiktive Beispiele. Beispiele dürfen keine echten
  Zugangsdaten, persönlichen Daten oder internen Produktionsinformationen enthalten.

## Screenshots, Bilder und Barrierefreiheit

Orientierung: [Google: Diagrams, figures, and other images](https://developers.google.com/style/images).

- Verwende Bilder, wenn sie einen wichtigen Zustand oder schwer auffindbare
  Bedienelemente verständlich machen. Nicht jeder Schritt benötigt einen Screenshot.
- Erfasse Screenshots der vorhandenen Oberfläche. Verwende keine nachgezeichneten
  oder generierten UI-Bilder als Beleg für das Produktverhalten.
- Zeige den relevanten Ausschnitt lesbar und mit genügend Orientierung.
  Halte Sprache, Theme, Plattform und Beispieldaten innerhalb einer Anleitung gleich.
- Nutze fiktive Daten. Falls echte Daten unvermeidbar im Ausgangsbild sind,
  entferne sie vollständig; Weichzeichnen reicht nicht zur Anonymisierung.
- Speichere Bilder nach dem vorhandenen Muster im zugehörigen `bilder/`-Ordner.
  Nutze beschreibende Dateinamen und relative Verweise.
- Beschreibe wichtige Schritte auch als Text. Code und Terminalausgaben bleiben
  kopierbarer Text. Keine wesentlichen Informationen ausschließlich im Bild.
- Jedes informative Bild erhält einen kurzen Alternativtext, der seinen Zweck
  vermittelt. Komplexe Diagramme brauchen zusätzlich eine Erklärung im Fließtext.
- Erläuterungen stehen neben dem Bild, nicht als lange Texte im Screenshot.
  Verwende vorhandene Bildkomponenten und responsive Darstellung.
- Prüfe das gerenderte Bild auf Lesbarkeit und aktualisiere es bei Änderungen
  des dargestellten Ablaufs. Kennzeichne Darstellungen mit Testdaten oder Fixtures.

## API- und technische Referenzen

- Verwende vorhandene OpenAPI-/Swagger- und XML-Dokumentationswege als Quelle
  für API-Verträge. Pflege generierte Dateien nicht von Hand.
- Dokumentiere bei API-Änderungen Methode und Pfad, Authentifizierung und benötigte
  Rechte, Request und Response, Pflichtfelder, optionale Felder, Null-/Leer-Semantik,
  Defaults, Validierung, Einheiten, Statuscodes und relevante Fehlerfälle.
- Erläutere die Bedeutung von Statuswerten, Versionierung, Seitennavigation und
  Parallelitätskontrolle, soweit die API diese Konzepte verwendet.
- Ergänze gültige Request-/Response-Beispiele und relevante Fehlerbeispiele.
  Prüfe Beispiele gegen den beschriebenen Vertrag; generierte Schemas ersetzen
  keine Erklärung von Auswirkungen oder Zusammenhängen.
- Verlinke technische Details aus Produktanleitungen, statt denselben Vertrag
  mehrfach zu pflegen. Interne Architekturentscheidungen bleiben in den dafür
  vorgesehenen Dokumenten des Software-Repositories.

## Docs as Code und Pflege

Grundlage: [Write the Docs: Docs as Code](https://www.writethedocs.org/guide/docs-as-code/).

- Behandle Dokumentation wie Code: Markdown/MDX in Git, nachvollziehbare Änderungen,
  Review und automatisierte Prüfungen mit den vorhandenen Werkzeugen.
- Aktualisiere betroffene Anleitungen, Referenzen und Screenshots zusammen mit
  der jeweiligen Verhaltensänderung. Prüfe dabei auch verlinkte Seiten.
- Bei mehreren Repositories gehören die Inhaltsänderung ins Docs-Repository und
  der passende Submodule-Verweis in den Consumer. Referenzen dürfen keine Inhalte
  erwarten, die am gepinnten Docs-Stand fehlen. Release-Stände müssen zusammenpassen.
- Führe Commits, Pushes, Submodule-Bumps oder Veröffentlichungen nur im Umfang
  des Nutzerauftrags aus. Eine Dokumentationsänderung ist kein Veröffentlichungsauftrag.
- Prüfe vorhandene Versionsstrukturen, bevor du Release-Seiten änderst.
  Veraltete Anleitungen erhalten einen Versionshinweis oder eine Aktualisierung;
  entferne historische Informationen nicht ohne Prüfung ihrer Verwendung.
- Erfinde keine Prüfskripte oder CI-Gates. Verwende vorhandene Format-, Link-,
  Beispiel- und Build-Prüfungen; melde fehlende Prüfungen als Grenze.

## Abschlussprüfung

1. Zielgruppe und Dokumentationstyp sind klar; Titel und Navigation helfen beim Finden.
2. Begriffe, UI-Bezeichnungen, Rechte, Voraussetzungen und Auswirkungen stimmen
   mit dem geprüften Systemverhalten überein.
3. Beispiele sind gültig und ohne echte Zugangsdaten oder persönliche Daten.
4. Interne Links, Anker, Bildverweise und `meta.json`-Einträge sind geprüft.
5. Betroffene Seiten sind, soweit möglich, im Consumer gerendert geprüft;
   neue Bilder sind lesbar und haben passenden Alternativtext.
6. Passende vorhandene Checks sind ausgeführt. Bei reinen Agentenanweisungen
   genügen Format- und Linkprüfungen; dafür sind keine Anwendungstests erforderlich.
7. Berichte kurz geänderte Dateien, ausgeführte Prüfungen und offene Einschränkungen.

Die verlinkten Quellen erläutern die Methoden; die hier formulierten Regeln
konkretisieren ihre Anwendung für Mardu.
