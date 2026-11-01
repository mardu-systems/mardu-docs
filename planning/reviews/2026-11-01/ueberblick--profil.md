# P10 – Eigenes Profil

## Änderungsbrief

Seite: `docs/ueberblick/profil.mdx`. Leserfrage: Wie ändere ich eigene Kontodaten
und das Profilbild, wie speichere ich Änderungen und wo finde ich weitere
Kontoeinstellungen? Vorausgesetzt werden ein angemeldetes Konto und die nötigen
Profilrechte. Ergebnis: Die Person findet die aktuelle Oberfläche, speichert den
gewünschten Bereich und erkennt Fehler sowie getrennte Speicheraktionen.
Kanonischer Heimatbereich bleibt **Benutzer**, die historische URL unter
`ueberblick/` bleibt erhalten. Umfang: Nur die Profilseite und dieser Bericht;
keine Software-, Navigations- oder API-Änderung.

## Entscheidung und Änderungen

**Verbessert; statisch geprüft, praktische Prüfung offen.**

- Einstieg von „Mein Profil → Profil“ auf „Mein Profil → Kontoeinstellungen“
  korrigiert; mobile Bereichsliste auf die Benutzeransicht eingegrenzt.
- Kontaktinformationen und persönliche Karten mit ihren tatsächlichen
  Speicheraktionen beschrieben; Erfolgsmeldung, Werteprüfung und Fehlerhilfe ergänzt.
- Feldübersicht präzisiert, Kontozeitzone von Browser-Anzeigezeitzone abgegrenzt.
  Das bisherige pauschale Versprechen über Benachrichtigungen entfällt: Ruhezeiten
  verwenden eine gesonderte Zeitzone.
- E-Mail-Aktion neben der Adresse ergänzt und auf den bestehenden
  Bestätigungsablauf verwiesen.
- „Pflichtangaben“ unter Profilergänzung korrigiert: freiwillige Angaben,
  Ausfüllstand, getrennte Bildspeicherung, „Später“ und erneutes Laden beschrieben.
- Unbelegtes Versprechen, optionale Angaben per Oberfläche löschen zu können,
  entfernt; Produktfehler siehe unten.
- Gute Bildanleitung, Rechte, Tastaturhinweis, Warnung vor ungespeicherten
  Änderungen und sämtliche bisherigen Abschnittsüberschriften/Anker und
  Spezialseitenverweise erhalten. Vorhandene Bilder bleiben Beispiele aus der
  bestehenden Dokumentation, keine neue Browserabnahme.

## Quellen und fachlicher Abgleich

Pfade relativ zum Software-Repository:

- `web/components/layout/common/account-menu-items.tsx`, `getAccountMenuItems`:
  aktueller Menüeintrag und kontextbezogener Profileinstieg;
  `web/locales/de/navigation.json`, `nav.accountMenu.settings`:
  „Kontoeinstellungen“.
- `web/lib/profile-navigation.ts`, `profilePathForContext` und
  `profileReturnPath`; `web/components/profile/profile-settings-layout.tsx`:
  gemeinsame Profilseiten, mobile Benutzerübersicht, „Profildaten“, Zurück-Link,
  Lade- und Wiederholungszustände. `web/components/layout/settings/profile-nav.config.ts`:
  verfügbare Profilbereiche.
- `web/app/[project]/portal/profile/page.tsx` und `details/page.tsx`:
  Wiederverwendung derselben Profilseite.
- `web/app/[project]/dashboard/user-management/profile/profile/page.tsx`:
  Profilbild, Kontaktinformationen und persönliche Angaben;
  `profile-form.tsx`: Namens-/Telefonfelder, separate E-Mail-Aktion,
  „Benutzer aktualisieren“, Fehlerbehandlung;
  `account/account-form.tsx`: getrennte Kartenformulare, Namenslänge, Datumsauswahl,
  Sprachpräferenz, Zeitzone und Einzel-Speicheraktionen.
- `web/locales/de/settings.json`, `settings.profile`, `settings.account`;
  `web/locales/de/users.json`, `user.settings.updateUser`;
  `web/locales/de/account.json`, `profileComplete` und `profileBanner`:
  UI-Bezeichnungen, freiwillige Ergänzungen, „Profil speichern“, „Später“,
  Lade-/Speicherfehler.
- `web/components/profile/profile-avatar-editor.tsx`:
  eigene API-Speicherung von Bildänderung und -entfernung;
  `avatar-editor.tsx`: Auswahl, Richtungsschaltflächen, Zoom, Zurücksetzen,
  Upload-/Löschfehler;
  `web/lib/images/image-upload.ts`, `IMAGE_UPLOAD_RULES.avatar`:
  JPEG/PNG/WebP, 2 × 1024 × 1024 Bytes.
- `web/app/[project]/dashboard/user-management/profile/complete/complete-page-client.tsx`:
  freiwilliges Formular, Entwurfsfortschritt, gespeicherter Erfolgszustand,
  getrennte Bildspeicherung, „Später“, Laden wiederholen und Fehler erhalten;
  `web/lib/users/profile-completeness.ts`, `getProfileCompleteness`:
  sechs geprüfte Ergänzungen einschließlich Bild; kein Nachweis von Pflichtfeldern.
- `web/components/profile/profile-draft-provider.tsx`:
  Entwurfswarnung bei Links/Abmeldung, `beforeunload`, browserabhängiges
  Zurück/Vorwärts, flüchtige Entwürfe. `web/lib/stores/profile-store.ts`:
  Ladefehler, Verwerfen geladener Daten bei 401/403 und Kontextwechseln.
- `api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs`,
  `GetProfile`, `UpdateProfile`: Profil-Lese-/Änderungsrechte, eigenes Konto,
  Null-/Leer-Semantik, separater E-Mail-Ablauf.
- `api/Framework/Core/Identity/Request/UpdateUserRequest.cs`:
  Feldvalidierung und bestehende API-Dokumentation;
  `api/Framework/Infrastructure/Identity/Users/Services/UserService.CreateUpdate.cs`,
  `UpdateUser` und `EnsureExternallyManagedFieldsUnchanged`:
  Speicherverhalten, Telefonänderung ohne Bestätigung, externe Schreibsperre,
  E-Mail-Änderung nur im eigenen Ablauf.
- `api/Framework/Infrastructure/RequestPreferences/RequestTimeZoneService.cs`:
  Kontozeitzone für serverseitige Zeitumrechnung;
  `api/Service/Notifications/Application/Policy/NotificationPolicyEngine.cs`:
  gesonderte `QuietHoursTimeZoneId`.

## Produktbefund außerhalb der Anleitung

Optionale Felder lassen sich im Profilformular aktuell nicht zuverlässig löschen.
`ProfileForm` und `AccountForm` senden geleerte Telefonnummer, Anzeigename,
Sprachpräferenz und Kontozeitzone mit `toNullable(...)` als `null`.
`formatDateOfBirth(undefined)` liefert ebenfalls `null`. Der dokumentierte
Backendvertrag und `UserService.UpdateUser` behalten bei `null` den bisherigen
Wert; zum Löschen wäre eine leere Zeichenfolge nötig. Auch die Ergänzungsseite
wandelt leere Eingaben in `undefined` um. Die Erfolgsmeldung kann daher erscheinen,
obwohl der bisherige Wert erhalten bleibt. Beleg ist die Codekette; keine
praktische Browserreproduktion durchgeführt. Keine Softwarekorrektur im Seitenauftrag.

## Prüfungen und offene Punkte

- Bestehende Quellen, Nachbaranleitungen und alle drei vorhandenen Bilder gelesen
  beziehungsweise visuell betrachtet. Keine neue Screenshotaufnahme.
- Format-, Link-/Anker- und Diff-Prüfungen: siehe abschließenden Prüfvermerk unten.
- Keine Builds, globalen Tests, Serverstarts oder externen Aktionen ausgeführt.
- Koordinator: Profilseite im Software-Consumer und Website-Consumer rendern;
  Desktop und mobile Benutzeransicht prüfen, einschließlich E-Mail-Querverweis,
  Bildaktionen und Entwurfswarnung. Angemeldeter Ablauf mit geeigneten Testdaten
  bleibt offen.
- Koordinator: Screenshots bei einer neuen Browserrunde aktualisieren. Die mobile
  Bestandsaufnahme zeigt ältere Hauptnavigationsbezeichnungen; die Profilbereichsliste
  stimmt mit der geprüften Implementierung überein. Kontaktbild enthält ältere
  E-Mail-Hilfetexte. Keine Bilder als aktuelle praktische Abnahme ausgegeben.
- Koordinator: Löschfehler der optionalen Felder als Softwarefolgeaufgabe behandeln;
  nach Korrektur Löschanleitung wieder aufnehmen und praktisch prüfen.
- Nachbarseiten enthalten ebenfalls den alten Einstieg „Mein Profil → …“;
  deren Korrektur liegt bei den jeweiligen Seitenaufträgen. Historische Profil-URL
  und alle bisherigen Überschriften bleiben unverändert. Kein zusätzlicher
  Seitenbedarf festgestellt.

## Geänderte Dateien

- `web/content/docs/docs/ueberblick/profil.mdx`
- `web/content/docs/planning/reviews/2026-11-01/ueberblick--profil.md`

Bestehende Markdown-Mittel, Tabelle, Bilder und relative Spezialseitenverweise
wiederverwendet. API-/DTO-Dokumentation unverändert, da kein Vertrag geändert wurde.

## Abschließender Prüfvermerk

- `web/node_modules/.bin/prettier --check --ignore-path /dev/null` mit genau
  dieser MDX-Seite und diesem Bericht: erfolgreich. Die Ausnahme von
  `.prettierignore` ist nötig, weil der Software-Consumer das Docs-Submodule
  standardmäßig ausschließt.
- `@mdx-js/mdx` aus den vorhandenen Web-Dependencies: Seiteninhalt ohne
  Frontmatter erfolgreich kompiliert; keine neue Dependency.
- Lokale Dokumentprüfung mit vorhandenem `github-slugger`: alle 13 referenzierten
  Seiten-/Bilddateien vorhanden, der explizit verlinkte Zielanker existiert,
  alle MDX-Seitenlinks beginnen mit `./` oder `../`.
- Vergleich mit `HEAD`: alle 11 bisherigen Abschnittsüberschriften unverändert.
- `git -C web/content/docs diff --check -- docs/ueberblick/profil.mdx
planning/reviews/2026-11-01/ueberblick--profil.md`: erfolgreich.
- Kein gerenderter Consumer und kein angemeldeter Ablauf geprüft. Der Status
  bleibt **zur Prüfung**, nicht abgenommen.
