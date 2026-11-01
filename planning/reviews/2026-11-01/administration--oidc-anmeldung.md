# N09 — Anmeldung über OpenID Connect einrichten

## Änderungsbrief und Entscheidung

- Leserfrage: Wie richtet eine Person mit Zugang zur Anbieterregistrierung die angebotene externe Anmeldung ein, prüft Identitätszuordnung und schaltet sie mit einem funktionierenden Rückweg frei?
- Eigenständiger Bedarf: `docs/administration/integrationen.mdx#anmeldung-über-openid-connect` bietet eine zutreffende Übersicht, aber keine ausführbare Einrichtung einschließlich der unterschiedlichen Callback-Adressen, Registrierung, Mapping- und MFA-Folgen. Kanonische Aufgabenanleitung unter Administration; Übersicht bleibt bestehen.
- Vorgehen: Frontend, Übersetzungen und Broker-/Settings-Code lesen, Schritte und Folgen abgleichen, ausschließlich eigene MDX und diesen Bericht schreiben, dateibezogene Format-/MDX-/Verweisprüfung. Keine Software-, Navigations- oder Vertragsänderungen.
- Entscheidung: **belegbare Teildokumentation / offene Prüfung**, Status **zur Prüfung**. Codelektüre ist keine praktische Anbieter- oder Consumer-Abnahme.

## Quellen und fachliche Abdeckung

Pfade relativ zum Software-Repository:

- `web/components/layout/settings/server-nav.config.ts:123–138`: aktueller Einstieg `/dashboard/admin/server/oidc`, Kategorie Identität und `Integrations.View`. `web/app/[project]/dashboard/admin/integrations/oidc/page.tsx`: Alias leitet dorthin weiter.
- `web/app/[project]/dashboard/admin/server/oidc/page.tsx`: Status, Anbieterentwurf, gemeinsame Speicherung, Risikobestätigung und Entfernung zunächst aus dem Entwurf.
- `web/app/[project]/dashboard/admin/server/oidc/oidc-provider-editor.tsx`: Schritte Verbindung/Sicherheit/Identität/Zugriff/Prüfen; Editor für Claims, Rollen/Gruppen, verwaltete Rollen, MFA, optionaler API-Bearer-Zugang; isoliertes Anmeldefenster und Ergebnisanzeige.
- `web/locales/de/settings.json:320–635`, `settings.oidc`: genaue Feld-, Schritt- und Aktionsnamen. `settings.authPolicy.fields`: Selbstregistrierung, SSO-Freigabe und bestätigtes Konto.
- `web/app/[project]/dashboard/admin/server/oidc/oidc-settings.utils.ts:140–180`: neuer Provider deaktiviert, Redirect-URI leer, Standardclaims, Scopes und Subject-only. `oidc-settings.presentation.ts`: bestehende ID nicht editierbar; Testbezug zum Entwurf und Ablaufprüfung.
- `web/app/[project]/dashboard/admin/server/oidc/use-oidc-settings-controller.ts:131–142,540–693`: Frontend verwendet Integrations.View/Update, Rollenliste Roles.View; ETag/If-Match, aktuelle Testnachweise, Risikomengen; Test-Rückleitung ist aktuelle absolute Einstellungsadresse; Popup/Polling. Keine erfundene manuelle Kontoverknüpfung.
- `api/Framework/Infrastructure/Auth/Boundary/OidcIntegrationController.cs`: Settings.View für Lesen/Vorlagen; Settings.Update für Änderungen, Validierung, Verbindungstest, Mapping und Testlogin/Ergebnis; test-login/callback baut URL aus Request-Schema/Host/PathBase mit `/api/v1/settings/oidc/test-login/callback`; ENV-Sperren und HotReload.
- `api/Framework/Core/Auth/OidcSettings.cs`: tatsächlich vorhandene Felder und Werte; HTTPS-Redirect ohne Query/Fragment/Userinfo, Pflichtscope openid, reservierte Parameter, Clientauth, Subject-only, kein Algorithmus none. Keine erfundenen OAuth-Endpointfelder oder Anbieterkompatibilität.
- `api/Framework/Infrastructure/Auth/Application/OidcRuntimeSchemeManager.cs:163–192`: Discovery-Fallback, Codeflow, PKCE, CallbackPath aus konfigurierter Redirect-URI; kein UserInfo-Abruf, unveränderte Claimnamen; Entfernen deaktivierter Laufzeitschemes in ApplyAsync.
- `api/Framework/Infrastructure/Auth/Application/OidcBrokerEvents.cs:11–32`: exakte konfigurierte Redirect-URI bei Autorisierung und Codeaustausch. `web/app/api/internal/auth/oidc/start/route.ts:29–57`: getrennte Dashboard-Rückleitung `/api/internal/auth/oidc/callback` und Projektbindung.
- `api/Framework/Core/Auth/AuthBrokerSettings.cs`: explizite HTTPS-Returnurl-Allowlist und ProjectId; leere Allowlist erlaubt keine Broker-Rückleitung. `OidcTestLoginService.StartAsync`: Einstellungs-Returnurl muss dort separat erlaubt sein.
- `api/Framework/Infrastructure/Auth/Application/OidcProviderProbe.cs`: Discovery-, Issuer-, Endpunkt-, TLS-, JWKS- und Algorithmusdiagnose; kein tatsächlicher Client-Tokenaustausch im Verbindungstest.
- `api/Framework/Infrastructure/Auth/Application/OidcDiagnosticsService.cs` und `OidcIntegrationService.cs:53–101,127–166`: Testnachweis an Benutzer/Entwurf/ETag gebunden; Aktivierung und verbindungskritische Änderungen verlangen erfolgreichen Test; atomare Liste, exakte Risikobestätigung und Rücknahme bei Laufzeitfehler.
- `api/Framework/Infrastructure/Auth/Application/OidcTestLoginService.cs:44–163,194–230`: isolierter Browser-Codeflow mit eigener Callback-Adresse, PKCE, drei Clientauth-Varianten; lokale Benutzer bleiben unverändert. `OidcPrincipalMappingService.cs`: Claim-/Mappingvorschau ohne Benutzeränderung.
- `api/Framework/Infrastructure/Auth/Application/OidcBrokerService.cs`, besonders `ResolveLocalUserAsync`, `ApplyRoleMappingsAsync`, `EnsureProspectiveAdminMfaAsync`, `HasAcceptedMfa`: tatsächliches Issuer+Subject-Linking, neue Links hinter AutoProvisioning und globaler Registrierung, Email-link nur bei gewähltem Modus und email_verified; E-Mail-Vertrauen bei Neuanlage separat; SSO-Freigabe; vorhandene lokale Rolle Admin verlangt exakte AMR/ACR-Allowlist; verwaltete Rollen werden bei entfallendem Mapping entfernt, andere behalten.
- `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs:719–763`: OIDC-MFA auch bei kontobezogener Pflicht und bei Erneuerung; kein lokaler 2FA-Ersatz. Abschalten wird nicht als ausdrücklicher globaler Sitzungswiderruf beschrieben.
- Vorhandene Seiten `administration/server-einstellungen.mdx`, `benutzer-rollen.mdx`, `sicherheit-betrieb.mdx`, `ueberblick/profil-nachweisquellen.mdx`: gemeinsame Registrierung, Zertifikate, lokale Rollen, Sitzungswiderruf und Abgrenzung persönlicher Nachweisquellen werden verlinkt statt neu dokumentiert.

## Grenzen und Befunde für den Koordinator

1. **Clientauth-Test-/Produktivunterschied:** UI und DTO bieten None, ClientSecretPost und ClientSecretBasic. Der isolierte `OidcTestLoginService.ExchangeCodeAsync` behandelt diese explizit. Der reguläre Konfigurator `OidcRuntimeOptionsConfigurator.Configure` übernimmt dagegen ClientId/ClientSecret, verwendet `ClientAuthenticationMethod` nicht; `OidcBrokerEvents.OnAuthorizationCodeReceived` setzt nur RedirectUri. Daraus folgt keine belegte produktive Basic-Unterstützung. Separat prüfen/korrigieren; keine Softwareänderung in diesem Auftrag. Die Anleitung nennt die angebotenen Optionen, verlangt aber abschließende reguläre Anmeldung und behauptet keine Gleichwertigkeit oder Anbieterabnahme.
2. **Vorschau ist unvollständig:** `OidcPrincipalMappingService` kennt globale Selbstregistrierung/Freigabe, Kontosperren und MFA nicht. Er kann vorhandenes Emailkonto trotz AutoProvisioning=false als verknüpfbar anzeigen; produktiver Broker prüft AutoProvisioning und globale Registrierung vor der ersten Verknüpfung. „Erfolgreich“ beim Testlogin bedeutet Token-/Browserprüfung mit Vorschau, keine zugesagte reguläre Anmeldung. Im Produkttext ausdrücklich begrenzt.
3. **Provider-Identität:** Wirklicher Link ist Issuer+Subject, nicht Provider-ID oder E-Mail allein. Provider entfernen löscht keine externen Identitätsdatensätze und keine lokalen Rollen. Keine Behauptung automatischer Migration bei Issuerwechsel oder pauschaler Sitzungslöschung.
4. **Anbieterregistrierung und Proxy nötig:** Keine automatisch erzeugte Produktions-Redirect-URI; neuer Entwurf ist leer. Testcallback hängt von öffentlichem Backend-Schema/Host/PathBase ab. Beide Provider-Callback-Adressen und beide Dashboard-Returnurls samt Projekt müssen praktisch geprüft werden. Die Provider-Vorlagen sind keine Kompatibilitätszusage.

## Checks und offene Praxisprüfung

- `bun fmt --check` für die beiden eigenen Dateien ohne Meldung. Da Consumer-Ignore-Regeln die Produktquelle ausnehmen können, zusätzlich vorhandenes Prettier mit `--ignore-path /dev/null` verwendet; neue MDX-Tabelle damit formatiert und beide Dateien erneut explizit geprüft.
- Neue Produktseite mit dem vorhandenen `@mdx-js/mdx` ohne Frontmatter kompiliert: erfolgreich. Das belegt MDX-Syntax, keine Darstellung im Consumer.
- Lokaler Python-Check: Frontmatter mit title/description, kein zusätzliches H1, alle relativen Seitenlinks vorhanden und verwendete Zielanker in den vorhandenen Überschriften gefunden.
- `git -C web/content/docs diff --check -- <beide eigene Pfade>` ohne Meldung; neue Dateien zusätzlich direkt gelesen und explizit formatiert.
- Gemeinsame Builds, Serverstarts, Providerlogins und externe Mutationen sind gemäß Auftrag nicht durchgeführt.

Offen: Darstellung in Software- und Website-Consumer, Navigation und Suche durch Koordinator; Browserprüfung von Schritten, Sperren, Secret-/Risikodialogen, Popup und Ergebniszuordnung; reale Anbieterregistrierung/HTTPS-/Proxy-Rückleitung, Clientauth einschließlich Basic-Unterschied, reguläre Anmeldung mit neuen/bestehenden Konten, Freigabe, fehlender E-Mail-Bestätigung, verwalteter Rollenentzug, Admin-/kontobezogene MFA und Abschaltfolgen.

## Querverweise und Dateien

- Koordinator: neue Seite in Administration veröffentlichen; `integrationen.mdx#anmeldung-über-openid-connect`, `server-einstellungen.mdx` und `sicherheit-betrieb.mdx` passend darauf verweisen lassen. Vorhandenen OIDC-Anker der Übersicht erhalten.
- Keine Links auf gleichzeitig entstehende Nachbar-Neuseiten gesetzt. Die vorhandene Benutzer-/Rollenanleitung bleibt Ziel für lokale Rechte; eine spätere separate Rollen-/Gruppenanleitung kann der Koordinator berücksichtigen.
- Geändert: `web/content/docs/docs/administration/oidc-anmeldung.mdx`, dieser Bericht.
- Wiederverwendet: vorhandener Settings-/Provider-Dialog, deutsche UI-Texte, Markdown/MDX-Konventionen und bestehende Aufgabenlinks. API-/DTO-Dokumentation unverändert, da kein Vertrag geändert wurde.
