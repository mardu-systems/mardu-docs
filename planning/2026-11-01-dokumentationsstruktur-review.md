# Kritische Prüfung des Strukturplans

Stand: 1. November 2026. Geprüft wurde der erste
[Strukturvorschlag](./2026-11-01-dokumentationsstruktur.md) gegen die vorhandenen
Anleitungen, die Dashboard-Navigation, ausgewählte Seitenimplementierungen und
Verträge. Das ist eine Prüfung der Informationsarchitektur anhand des Codes,
keine erneute praktische Abnahme aller Funktionen.

## Urteil

Der erste Vorschlag war als Bestandsordnung brauchbar, als Planung der gesamten
Dokumentation noch unvollständig. Die wichtigsten Schwächen sind die fehlende
Aufgabenabdeckung und die unklare Grenze zwischen Administration und Koordination.
Die vollständige Auflistung von 54 Seiten belegt keine vollständige Dokumentation.

## Befunde und Korrekturen

| Gewicht | Befund am ersten Plan                                                                  | Beleg und Auswirkung                                                                                                                                                                                                                                      | Korrektur im Plan                                                                                                                                                                                          |
| ------- | -------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hoch    | Vorhandene Seiten bestimmten den Umfang.                                               | Rollenpflege, Gruppenpflege und delegierte Zuständigkeiten wurden in „Benutzer und Rollen“ beziehungsweise „Zutritt“ versteckt. Die Benutzeranleitung nennt ihre fehlende vollständige Abdeckung ausdrücklich.                                            | Aufgabenabdeckung separat ausweisen; Rollen/Gruppen und Verwaltungszuständigkeiten als geplante Anleitungen aufnehmen.                                                                                     |
| Hoch    | Ressourcenverwaltung war ausschließlich unter Koordination auffindbar.                 | Die vorhandene Ressourcenseite enthält Einrichtung, Zugriffsregel, Leser/Aktor, Buchbarkeit, Wartung und Stilllegung. „Ressourcen und Buchungsregeln“ nur per allgemeinem Verweis anzubieten, unterschätzt die Administration.                            | Ressourcen-Einrichtung bekommt Administration als Heimat. Bestehende URL bleibt. Koordination erhält einen eigenen Aufgabenweg für Verfügbarkeit/Wartung und Verweise auf dieselbe Konfigurationsquelle.   |
| Hoch    | Die Abgrenzung „Administration richtet ein, Koordination organisiert“ war zu pauschal. | Gruppenregeln liegen in der Benutzergruppenverwaltung; ressourcenbezogene Technik und Buchbarkeit stehen im selben Ressourcendialog. Eine formale Systemrolle „Koordination“ folgt daraus nicht.                                                          | Aufgabenmatrix statt behaupteter Rollengrenze: Konfiguration, konkrete Entscheidung und persönliche Nutzung trennen; Rechte jeweils an der Aufgabe nennen.                                                 |
| Hoch    | Integrationen wurden zum zu kleinen Sammelthema.                                       | `integrations-nav.config.ts` enthält MQTT-Broker und Benutzerverwaltung. Das ist nicht durch „MQTT-Ereignisse beziehen“ für Entwickler abgedeckt. LDAP und OIDC führen zu eigenständigen Einstellungen; IP500 besitzt einen eigenen Konfigurationsablauf. | Integrationseinstieg behalten, eigene geplante Aufgaben zu LDAP, OIDC, MQTT-Verwaltung und IP500 ausweisen. Datenrichtung und Abhängigkeiten erklären.                                                     |
| Hoch    | Kompetenzen und Lernwege fehlten als Einrichtungsaufgaben.                             | `components/competencies/workspace.tsx` unterscheidet Bibliothek, Lernwege, Prüfungen und Einstellungen. `LearningPathsController` trennt Definition und persönliche Einschreibung. Eine Badge-Definition deckt das nicht ab.                             | Definitionen/Lernwege nach Administration, Bewertung und persönliche Vergaben/Einschreibungen nach Koordination, eigener Stand nach Benutzer. Externe Anbieter und Anerkennungsregeln gesondert planen.    |
| Hoch    | Betrieb konnte verfügbare Funktionen suggerieren, die nicht belegt sind.               | `admin/server/database-backup/page.tsx` zeigt nur „Backup-Funktionen werden vorbereitet“. Auch vorhandene Routen können reine Weiterleitungen sein.                                                                                                       | Kein GUI-Backup-Ablauf im Zielbaum. Externes Betriebsverfahren für Sicherung/Wiederherstellung erst nach Quellen- und Praxisklärung planen. Route, Implementierung und praktische Abnahme unterscheiden.   |
| Mittel  | Der Überblick sollte sofort zwei weitere Erklärseiten bekommen.                        | Startentwurf, „Ressourcen und Funktionen“ und „Systembestandteile“ würden weitgehend denselben Einstieg verteilen. Der Nutzen zusätzlicher Seiten ist nicht belegt.                                                                                       | Erste Fassung auf Mardu verstehen, Personen/Rollen/Freigaben und Begriffe beschränken. Vertiefungen erst bei konkreter Inhaltslast ergänzen. Neuerungen nur mit belegtem Release-Inhalt sichtbar machen.   |
| Mittel  | Die Benutzer-Sidebar blieb lang und gewichtete Spezialaufgaben zu stark.               | Profil-, Sicherheits-, Anzeige- und MCP-Seiten lagen als zahlreiche Einzelpunkte neben häufigen Nutzungsaufgaben.                                                                                                                                         | Eigene Nutzung und Kartenhilfe sichtbar; vorhandenes Profil als aufklappbaren Einstellungsbereich verwenden. Keine Kopie der Profileinhalte im Überblick.                                                  |
| Mittel  | Ein Heimatbereich wurde als Hindernis für andere Einstiege behandelt.                  | Das alte Ressourcenbeispiel zwang Administratoren zum Bereichswechsel, ohne eine konkrete Aufgabe zu benennen. Der URL-basierte Bereichsfilter kann einen Kontext nicht automatisch erhalten.                                                             | Eine kanonische Anleitung behalten; konkrete, beschriftete Querverweise an passenden Starts und Aufgaben. Bei Wechsel Zielbereich benennen; kein stillschweigendes Versprechen, der Fokus bleibe erhalten. |
| Mittel  | Prüfungen wurden zu nah an eine Strukturabnahme gerückt.                               | Dateilinks, vollständiges Inventar und eine Prüfung auf offene Umsetzungsfragen belegen weder Auffindbarkeit noch Aufgabenabdeckung.                                                                                                                      | Prüfstand nach Dokument-, Produktabdeckungs- und Nutzungsprüfung trennen. Keine allgemeine Qualitätsfreigabe aus dem früheren Builder Check ableiten.                                                      |

## Geprüfte Produktquellen

Pfade beziehen sich auf den Software-Consumer beziehungsweise das übergeordnete
API-Repository, nicht auf neue Dateien im Docs-Repository:

- `web/components/layout/sidebar/dashboard-navigation.ts`: aktive Arbeitsbereiche,
  Systemverwaltung und ausdrücklich geplante Menüpunkte.
- `web/components/layout/settings/server-nav.config.ts` und
  `integrations-nav.config.ts`: Anmelderichtlinien, Zertifikate, Monitoring,
  Fehlerberichte, Tag-Einstellungen, Audit, MQTT und weitere Anbindungen.
- `web/app/[project]/dashboard/permission/roles/page.tsx` und
  `user-management/settings/page.tsx`: Rollen- und Gruppenpflege.
- `web/app/[project]/dashboard/access-management/scopes/page-client.tsx`:
  Verwaltungszuordnungen, Diagnose und Widerruf.
- `web/app/[project]/dashboard/admin/bookings/policies/page.tsx` und
  `admin/integrations/{ldap,oidc}/page.tsx`: Weiterleitungen statt weiterer Funktionen.
- `web/app/[project]/dashboard/admin/server/database-backup/page.tsx`:
  Platzhalter statt verfügbarer Backup-Bedienung.
- `web/components/competencies/workspace.tsx` sowie
  `api/Service/Competencies/Boundary/HttpControllers/LearningPathsController.cs`
  und `AssessmentRunsController.cs`: Definition, Lernwege und Bewertungen.
- [Ressourcenanleitung](../docs/koordination/ressourcen.mdx),
  [Zutrittsentwurf](../docs/administration/zutritt-verwalten.mdx),
  [Integrationsentwurf](../docs/administration/integrationen.mdx) und
  [Prüfgrenzen der Benutzerverwaltung](../docs/administration/benutzer-rollen.mdx#prüfstand-und-grenzen):
  tatsächlicher Dokumentationsumfang und überladene Sammelseiten.

## Was bestehen bleibt

Die sechs vom Nutzer gewünschten Bereiche bleiben erhalten. Gute Anleitungen,
URLs und verwendete Anker werden weiterverwendet. Ressourcen und Personen bleiben
der gemeinsame Einstieg. Geplante Seiten und interne Schreibaufträge erscheinen
erst nach Ausarbeitung in der Produktnavigation. APIs, Rechte und Produktverhalten
werden durch diese Planrevision nicht geändert.

## Verbleibende Grenzen

Die neue Aufgabenmatrix ist anhand des Codes begründet, aber noch nicht mit
Lesern getestet. Neue Seitenzuschnitte sind Arbeitsannahmen, keine verbindliche
Anzahl und keine Funktionsfreigaben. Website-Navigation, praktische Abnahme der
zusätzlich untersuchten Funktionen und reale Wiederherstellung bleiben offen.
