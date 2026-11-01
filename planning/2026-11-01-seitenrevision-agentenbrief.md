# Auftrag für einen Seiten-Agenten

Projekt: `/Users/lucaschoeneberg/Documents/GitHub/mardu-rpi-api`.
Dokumentationsquelle: `web/content/docs/docs/`.
Ein Agent besitzt genau die ihm zugewiesene MDX-Seite und den zugehörigen Bericht
unter `web/content/docs/planning/reviews/2026-11-01/`.

## Verbindliche Grundlagen

Lies Root-AGENTS, `web/AGENTS.md` soweit Frontend relevant, und vollständig
`web/content/docs/AGENTS.md` sowie `ARBEITSWEISE.md`. Lies den passenden Teil von
`planning/offene-dokumentationsaufgaben.md` und benachbarte Anleitungen als Kontext.
Vorhandene gute Inhalte bleiben erhalten. Keine Änderungsquote.

## Durchführung für die zugewiesene Seite

1. Leserfrage, Vorwissen, Ergebnis und Heimatbereich bestimmen. Bestehenden
   Inhalt, Links, Bilder und verwendete Anker lesen.
2. Jede wesentliche fachliche Aussage mit vorhandener UI, Übersetzungen,
   Backend-/App-Code, Rechten oder Verträgen abgleichen. Erst nach dem Abgleich
   ergänzen oder korrigieren. Relevante Backend-/Frontend-Anweisungen beachten.
3. Kritik an Aufbau und Abdeckung: fehlende Schritte, falsche Automatismen,
   unklare Rechte, ungenannte Auswirkungen, veraltete UI-Namen, Doppelungen.
4. Erst distill, dann clarify/polish: Unnötiges entfernen, verständlich ordnen,
   präzise formulieren, passende vorhandene MDX-Komponenten verwenden. Keine
   Kernschritte oder Warnungen in Akkordeons verstecken. Keine neue Designsprache.
5. Ist die Seite gut, ändere sie nicht und belege diese Entscheidung im Bericht.
   Bei einer leeren Seite nur belegbaren Inhalt ausarbeiten; fehlende Praxisprüfung
   außerhalb der Produktquelle festhalten. Keine TODO-Schreibaufträge im neuen Text.
6. Erhalte URL und bestehende Anker; beim Umbenennen einer Überschrift vorhandene
   Anker explizit erhalten. Relative MDX-Verweise mit `./` oder `../` verwenden.
   Keine Links auf bloß vermutete neue Seiten. Zusätzlichen Seitenbedarf melden.
7. Prüfe deine Dateien mit vorhandenen Werkzeugen. Der Koordinator übernimmt
   gemeinsame Browser-/Build-/Navigationsprüfungen nach den Seitenänderungen.

## Zuständigkeitsgrenzen

- Keine anderen Produktseiten, `meta.json`, Bereichsfilter, gemeinsamem Backlog,
  Frameworkcode, Lockfiles oder Übersetzungsdateien ändern. Folgefehler an den
  Koordinator melden. Keine eigenen Subagenten starten.
- Keine Commits, Stashes, Resets, Worktrees, Pushes oder externen Schreibaktionen.
  Andere Agenten bearbeiten gleichzeitig ihre eigenen Dateien. Ihre Änderungen
  nicht zurücksetzen. Keine Server stoppen, Builds starten oder globale Caches ändern.
- Für Screenshots/zusätzliche Assets zunächst Bedarf melden. Keine alten Bilder
  als neue praktische Abnahme ausgeben. Softwarefunktionen nicht für die Anleitung
  umbauen. Bestätigte Produktfehler getrennt mit Codebeleg melden.
- Browser-/Hardware-/Provider-Prüfung nur behaupten, wenn selbst tatsächlich
  durchgeführt. Rechts-/Sicherheitsaussagen nicht aus Teamvermutungen ableiten.

## Erwarteter Bericht (kurz, aber überprüfbar)

- Seite, Leserfrage und Entscheidung: **unverändert gut**, **verbessert** oder
  **belegbare Teildokumentation / offene Prüfung**.
- Fachliche Befunde und vorgenommene Änderungen; wichtige unveränderte Inhalte.
- Konkrete Code-/UI-/Vertragsquellen mit Dateipfad und relevanten Stellen.
- Eigene ausgeführte Checks; benötigte Browser-/Hardware-/Provider-Prüfung.
- Verweise, Anker, Nachbarseiten oder neue Themen, die der Koordinator bearbeiten soll.
- Geänderte Dateien. Keine Abnahmebehauptung bei ausschließlich statischer Prüfung.

Antworte am Ende mit demselben Kurzbefund und dem Berichtspfad. Danach ist dein
Seitenauftrag beendet; weitere Seiten werden von hier separat zugeteilt.
