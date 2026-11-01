# Systemfunktionen überarbeiten und Dokumentation anlegen

Dieser Prozess gilt für bestehende Mardu-Funktionen und neue Produktanleitungen.
Die [Doku-Regeln](AGENTS.md) definieren die Qualitätsmaßstäbe. Architektur-,
Sicherheits- und Testregeln des jeweiligen Software-Repositories gelten zusätzlich.
Die Schritte werden nach Umfang der Änderung angewendet; eine Textkorrektur
braucht keine neue Projektplanung oder vollständige Hardwareabnahme.

## Gemeinsamer Ausgangspunkt: ein prüfbarer Änderungsbrief

Halte diese Angaben im vorhandenen Arbeitsplan oder in einer Planungsdatei fest,
bevor du Inhalt oder Verhalten änderst. Verwende für kleine Änderungen einen
Absatz, für größere Aufgaben diese Vorlage:

```text
Aufgabe und Anlass:
Leser / Nutzer und vorhandenes Vorwissen:
Gewünschtes, beobachtbares Ergebnis:
Betroffene Funktionen, Seiten und Consumer:
Vorhandene Quellen, Komponenten und Verträge:
Was bleibt erhalten; welche Änderung ist nötig:
Kanonische Anleitung und Navigationsbereich:
Nötige Prüfungen / geeigneter Testzugang:
Offene Fragen oder noch nicht belegtes Verhalten:
```

Prüfe die Funktionen selbst: Eine Route kann weiterleiten, ein Formular kann nur
ein Platzhalter sein und eine erfolgreich gespeicherte Einstellung muss keine
physische Wirkung haben. Ein vollständiger Seitenbaum ist noch keine vollständige
Abdeckung der Aufgaben.

## A. Bestehende Funktionen oder Bereiche überarbeiten

### 1. Bestand und Aufgaben abgleichen

- Lies die vorhandenen Anleitungen, Navigation und offenen Prüfpunkte.
- Ordne die Aufgaben den tatsächlichen UI-Aktionen, APIs, Berechtigungen und
  Zuständen zu. Prüfe die betroffenen Services, DTOs und Validierungen.
- Unterscheide passende Inhalte, überladene Sammelseiten, fehlende Anleitungen,
  veraltete Aussagen und noch nicht verfügbare Funktionen.
- Nutze vorhandene Komponenten, Modelle und Hilfsmittel. Eine Überarbeitung der
  Dokumentation rechtfertigt für sich keine neue Softwarearchitektur.

Ergebnis ist eine kurze Zuordnung **Aufgabe → vorhandene Funktion → Anleitung →
Lücke / Beleg**. Benenne Unsicherheit; fülle sie nicht mit einer vermuteten Funktion.

### 2. Die kleinste passende Änderung wählen

| Befund                                                       | Vorgehen                                                                                                                                                                     |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Eine gute Anleitung ist schwer auffindbar.                   | Titel, Gruppen oder Querverweise verbessern; Inhalt weiterverwenden.                                                                                                         |
| Dieselbe Erklärung steht mehrfach.                           | Eine kanonische Quelle wählen und die übrigen Stellen verlinken.                                                                                                             |
| Eine Seite deckt mehrere unabhängige Aufgaben ab.            | Nur die nötige Aufgabe ausgliedern. Bestehende URLs und benutzte Anker als Einstieg erhalten.                                                                                |
| Eine Aussage stimmt nicht mehr mit dem Produkt überein.      | Verhalten belegen und die Anleitung korrigieren. Eine nötige Produktkorrektur gesondert benennen.                                                                            |
| Eine Funktion muss laut Auftrag geändert werden.             | Bestehende Verträge und Auswirkungen prüfen, minimalen Patch mit passenden Verhaltenstests umsetzen und die betroffene Dokumentation im selben Änderungspaket aktualisieren. |
| Eine gewünschte Funktion oder ihre praktische Abnahme fehlt. | Als offene Aufgabe außerhalb der Produktquelle festhalten. Keine Anleitung für ein angenommenes Verhalten veröffentlichen.                                                   |

Trenne eine reine Umstrukturierung von einer Verhaltensänderung so, dass beide
reviewbar bleiben. Entferne keine Autorisierungs-, Validierungs- oder
Nebenläufigkeitsprüfung, nur weil sie den Ablauf länger macht.

### 3. Erst verdichten, dann ausarbeiten

Erhalte gültige Aussagen, Rechte, Voraussetzungen und Folgen. Entferne zuerst
Wiederholungen und Details ohne Nutzen für die Aufgabe. Ordne danach Ziel,
Voraussetzungen, Schritte, Ergebnis und Fehlerhilfe. Verfeinere zum Schluss Titel,
Sprache, Links und Darstellung.

Ein Akkordeon ersetzt keine Gliederung. Notwendige Schritte und Warnungen bleiben
sichtbar. Ein Diagramm erklärt Zusammenhänge; ein Screenshot zeigt eine konkrete
Oberfläche. Aktualisiere Bilder nur, wenn die Änderung sie betrifft.

### 4. Auswirkungen prüfen

Bei einer Verhaltensänderung prüfe betroffene Clients, Datenmodelle, API-Verträge,
Konfiguration, Übersetzungen und vorhandene Anleitungen. Nutze die im Projekt
vorgesehenen Tests und Dokumentationswege. Bei einer Änderung des Seitenzuschnitts
prüfe eingehende Links und Anker sowie beide Consumer.

## B. Eine neue Dokumentation anlegen

### 1. Eine eigene Leserfrage begründen

Prüfe zuerst, ob eine vorhandene Anleitung die Frage durch eine Ergänzung
beantworten kann. Eine neue Seite braucht ein eigenes Ergebnis oder einen eigenen
Nachschlagezweck. Ein neuer Menüpunkt, DTO oder Dienst braucht nicht automatisch
eine neue Produktseite.

Wähle den Hauptzweck: Zusammenhänge erklären, einen Lernweg führen, eine Aufgabe
lösen oder Fakten nachschlagen. Entscheide den Heimatbereich nach der Leserfrage,
nicht allein nach dem Speicherort im Code. Andere Bereiche dürfen dieselbe
Anleitung im passenden Zusammenhang verlinken.

### 2. Außerhalb der Produktquelle entwerfen

Lege einen Entwurf unter `drafts/` an oder ergänze den vorhandenen Plan unter
`planning/`. Die veröffentlichte Quelle ist `docs/`; dort erscheinen Pläne und
Schreibaufträge nicht als neue Seiten.

Eine kurze Anleitungsgrundlage:

```mdx
---
title: Konkrete Aufgabe erledigen
description: Das Ergebnis und den Umfang dieser Anleitung beschreiben.
---

Erkläre das Ziel und die Voraussetzung, die für diese Aufgabe entscheidend ist.

## Voraussetzungen

Benötigte Rechte, geeignete Umgebung und notwendige Ausgangsdaten.

## Aufgabe durchführen

1. Die erste konkrete Aktion mit der vorhandenen UI-Bezeichnung.
2. Die nächste Aktion und die wichtige Bedingung oder Folge.

Beschreibe das sichtbare Ergebnis und wie es überprüft wird.

## Wenn etwas nicht klappt

Nenne die relevanten Symptome, Ursachen und nächsten Schritte.
```

Diese Grundlage ist keine Pflichtliste. Eine Erklärung braucht beispielsweise
keinen künstlichen Abschnitt „Voraussetzungen“. Technische Verträge bleiben in
OpenAPI-/XML-Referenzen; die Anleitung erläutert ihre Verwendung und Auswirkungen.

### 3. Inhalt belegen und Bilder vorbereiten

Gleiche jede beschriebene Aktion mit dem vorhandenen Produkt ab. Nutze fiktive,
reproduzierbare Daten. Trenne Codeprüfung, Browserprüfung und reale Hardware- oder
Anbieterprüfung. Dokumentiere bei offenen Prüfungen den konkreten Umfang.

Bilder liegen beim späteren Seiteninhalt unter `bilder/`. Mermaid-Quellen können
als `.mmd` neben einem daraus erzeugten SVG liegen. Die Darstellung muss im
Consumer funktionieren; eine neue Diagrammabhängigkeit ist nicht automatisch
nötig. SVG-Exporte erhalten neben der `viewBox` eine passende Breite und Höhe,
damit Browser und Bildbetrachter dieselben Abmessungen verwenden. Prüfe den
Kontrast in beiden Themes. Wichtige Aussagen stehen auch im Text, informative
Bilder erhalten Alttext.

### 4. Erst nutzbare Inhalte in die Navigation aufnehmen

Übernimm die ausgearbeitete Seite nach `docs/<bereich>/<seite>.mdx`. Verwende
`title` und `description` im Frontmatter, kein zusätzliches H1 und relative
MDX-Seitenlinks mit `./` oder `../`.

Die Navigation wird mit den vorhandenen Fumadocs-Mitteln gepflegt:

- `meta.json` ist eine ausdrückliche Liste nutzbarer Inhalte. Verwende keine
  pauschale `...`-Erweiterung in Bereichen mit noch unfertigen Seiten.
- `---Gruppenname---` erzeugt eine Zwischenüberschrift. Sie braucht sichtbare
  Inhalte; ein Titel allein ist keine Gruppe.
- Relative Einträge wie `../koordination/ressourcen` können eine bestehende
  Anleitung einem anderen Navigationsbereich zuordnen, ohne ihre URL zu ändern.
- Ein Profilzweig kann mit `pagesIndex` auf eine vorhandene Übersichtsseite
  verweisen. Es wird keine zusätzliche leere Indexseite benötigt.
- Ein Link zu einem anderen Bereich benennt das Ziel, zum Beispiel
  `Wartung → Administration`. Beim Öffnen kann der aktive Doku-Bereich wechseln.
- Prüfe im Software-Consumer zusätzlich `lib/docs-roles.tsx`: Eigentümer der URL,
  Bereichsstart und ausdrücklich erlaubte Querverweise müssen zum Metadatenbaum
  passen. Eine versteckte alte Seite darf weiterhin ihren Bereich erkennen.

Die Metadaten steuern die sichtbare Navigation. Im Software-Consumer verwenden
Suche und LLM-Index dieselbe Veröffentlichungsliste. Ein Entfernen aus der
Navigation löscht keine bestehende Seitenadresse und macht sie nicht vertraulich.
Vertrauliche Informationen gehören auch nicht auf eine versteckte Produktseite.

## Gemeinsamer Abschluss für beide Wege

| Prüfung     | Nachweis                                                                                                                                                     |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Inhalt      | Ziel, Begriffe, UI-Bezeichnungen, Rechte und Folgen stimmen mit den geprüften Quellen überein.                                                               |
| Verweise    | Relative Links, Zielabschnitte, bestehende Anker und Bilddateien funktionieren.                                                                              |
| Navigation  | Die Seite steht im richtigen Bereich, Starts sind erreichbar und leere Gruppen oder Platzhalter werden nicht angeboten.                                      |
| Darstellung | Geänderte Produktseiten im Consumer rendern; je nach Änderung mobile Navigation, Tastatur, Theme und Bilder prüfen.                                          |
| Verhalten   | Für Softwareänderungen die passenden bestehenden Tests ausführen; beschriebene Abläufe soweit erforderlich praktisch prüfen.                                 |
| Consumer    | Software und Website berücksichtigen; nicht ausgeführte Consumer ausdrücklich nennen. Bei einem Release müssen Inhalts- und Submodule-Stände zusammenpassen. |

Im Software-Repository existieren unter anderem die Navigationstests
`tests/lib/docs-roles.test.ts`, `type-check`, `lint` und `build`. Verwende die zum
Änderungsumfang passenden Prüfungen. Der MDX-Inhalt im Submodule muss zusätzlich
mit den vorhandenen Formatwerkzeugen berücksichtigt werden. Erfinde keine
Prüfskripte oder CI-Gates und behaupte keine Abnahme aufgrund eines einzelnen
Checks.

Wenn der Consumer eine Markdown-Ansicht oder Agentenausgabe anbietet, prüfe sie
bei Änderungen an Bildern, Komponenten oder API-Referenzen mit. Bilder brauchen
auflösbare URLs und Alttexte; Tab-Bezeichnungen, Warnungen und notwendige Schritte
müssen erhalten bleiben. Eine API-Ausgabe muss den beschriebenen Operationsvertrag
einschließlich seiner referenzierten Schemas enthalten. Eine erfolgreiche
HTML-Darstellung allein belegt diese Ausgabe nicht.

Eine Anleitung wird nach diesen drei getrennten Zuständen beurteilt:

1. **Entwurf:** Frage und Zuschnitt sind festgehalten; Inhalt oder Belege fehlen.
2. **Zur Prüfung:** Inhalt ist nutzbar, die erforderlichen Dokument- und
   Verhaltensprüfungen sind aufgezeichnet; offene Punkte sind konkret benannt.
3. **Abgenommen:** Die für den Umfang erforderliche Prüfung ist abgeschlossen.
   Erst jetzt wird ein entsprechender Arbeitsauftrag als erledigt markiert.

Diese Zustände sind Arbeitskonventionen, keine neue Produktfunktion und kein
Auftrag für eine zusätzliche Statusverwaltung. Eine gute, geprüfte Teilanleitung
kann veröffentlicht werden, wenn ihr Umfang klar ist; sie darf dabei keine
vollständige Abdeckung des gesamten Funktionsbereichs behaupten.

Berichte abschließend geänderte Inhalte und Softwaredateien, wiederverwendete
Mittel, angepasste API-Dokumentation soweit betroffen, ausgeführte Prüfungen und
offene Grenzen. Commits, Pushes und Veröffentlichungen erfolgen im Umfang des
Nutzerauftrags; eine Inhaltsänderung erteilt keinen Veröffentlichungsauftrag.
