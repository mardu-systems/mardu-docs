# P39 – HTTP-API nutzen

## Änderungsbrief und Entscheidung

Leserfrage: Wie verbindet eine Person mit HTTP-/JSON-Vorwissen ihre Anwendung mit
einem eingerichteten Mardu-Server, erhält einen passenden Zugang und prüft einen
lesenden sowie einen versionierten schreibenden Aufruf? Heimatbereich:
Entwickeln; kanonische Vertragsdetails bleiben in der generierten API-Referenz.
Die vorhandene versteckte TODO-Seite wird zu einer Anleitung für Profil-Lesen
und Ressourcenentwürfe. Bestehende URL und drei Abschnittsanker bleiben erhalten.
Keine Schnittstellenvergleichs- oder Einstiegsdoppelung. Entscheidung:
**belegbare Teildokumentation / offene Prüfung** (Inhalt verbessert, statischer
Vertragsabgleich; keine Laufzeitabnahme).

## Befunde und Umsetzung

- API-Server von Dashboard-Projektpfad getrennt; lokaler Compose-Standard und
  entfernte HTTPS-Adresse beschrieben.
- Aktuelle Capability-Discovery, `identifier`/`password`, 200/202-MFA-Fortsetzung,
  Passkey-Ceremony und OIDC-Broker mit S256-PKCE statt generischer OAuth- oder
  veralteter Loginrequests. Keine API-Schlüssel oder Client-Credentials erfunden.
- Bearer-Aufruf `GET /profile`, Rechte, eigene Identität, Refresh-`userId`,
  Sekunden-Laufzeiten, Rotation, Serialisierung und Widerruf erklärt.
- Reproduzierbare Requestformen für Ressourcenliste und Entwurf-Anlegen,
  Detail-Lesen, Ändern aus dem letzten Stand. Fiktiver Name/Typ ohne Gerätebindung;
  erzeugte ID wird vom Leser übernommen. PUT-Ersetzungssemantik, Null-/Leerwerte,
  Validierung und Version/409 explizit.
- Fehlerformate nicht pauschal vereinheitlicht: Middleware liefert bei beendeter
  Sitzung `error`/`message`, Validierung hat verschiedene `errors`-Formen.
- Endpunktspezifische Raten statt allgemeinem API-Limit; asynchrone Schaltung
  und physische Bestätigung getrennt, Vertragsdetails verlinkt.
- Kein guter Fachinhalt aus dem bisherigen Entwurf entfernt: Er bestand aus
  Schreibaufträgen. Keine Software-/DTO- oder generierten Vertragsänderungen.

## Quellen

- `api/Service/Admin/Settings/Boundary/HttpControllers/InfoController.cs`:
  `GetAuthCapabilities`, `CreateProviderHint`, `AuthCapabilitiesResponse` –
  Discovery-Pfad, Kennungen und Laufzeitstatus.
- `api/Framework/Infrastructure/Identity/Tokens/Boundary/TokensController.cs`:
  Authenticate, Challenge, Refresh, Revoke – Pfade, Rechte, Status, Bodies.
- `api/Framework/Core/Identity/Request/{AuthenticateRequest,CompleteAuthenticationChallengeRequest,RefreshTokenRequest,RevokeTokenRequest}.cs`,
  `api/Framework/Core/Identity/Dto/{TokenResponse,AuthenticationChallengeDto}.cs`,
  `api/Framework/Core/Identity/AuthenticationChallengeMethod.cs`: konkrete Felder,
  Serialisierung und Validierung.
- `api/Framework/Infrastructure/Identity/Tokens/Services/TokenService.cs`:
  `AuthenticateAsync`, `RefreshTokenAsync`, `RevokeTokenAsync`,
  `EnsureUserCanIssueTokensAsync`, `EnsureAuthenticationAssuranceAsync`,
  `GenerateTokensAndUpdateUser` – Konto/MFA, Rotation und Lebensdauern.
- `api/Framework/Infrastructure/Identity/Tokens/Challenges/AuthenticationChallengeStore.cs`:
  Challenge-Laufzeit und Einmaligkeit.
- `api/Framework/Infrastructure/Identity/Users/Boundary/ProfileController.cs`:
  `GetProfile`, `GetAuthorization`; `UserDto.cs`: Profil-ID und Rückgabemodell.
- `api/Framework/Infrastructure/Auth/Boundary/{OidcBrokerController,OidcBrokerDtos}.cs`,
  `api/Framework/Infrastructure/Auth/Application/OidcBrokerService.cs`:
  Start-/Exchange-Vertrag, freigegebene Rücksprünge, Projekt und PKCE.
- `api/Framework/Infrastructure/Identity/Passkeys/Boundary/PasskeyController.cs`:
  AuthenticationOptions/Verify, Tokenausgabe nach WebAuthn.
- `api/Service/ManagedResources/Boundary/HttpControllers/ManagedResourcesController.cs`:
  List/Get/Create/Update – Rechte, Location und Erfolg-/Fehlerstatus.
- `api/Service/ManagedResources/Boundary/Dto/ManagedResourceDtos.cs`,
  `api/Service/ManagedResources/Entity/ManagedResource.cs`,
  `api/Service/ManagedResources/Application/Services/ManagedResourceService.cs`:
  Draft/Other, Datenlimits, Normalisierung, Ersetzungssemantik, Version/409.
- `api/Service/ManagedResources/Gateway/ManagedResourceSpecifications.cs`,
  `api/Framework/Core/Common/Models/{BaseFilter,PaginationFilter,PaginationResponse}.cs`:
  Filter, Seitenparameter und Antwort.
- `api/Framework/Infrastructure/Exception/CustomExceptionHandler.cs`,
  `api/Framework/Infrastructure/Validation/FluentValidationActionFilter.cs`,
  `api/Framework/Infrastructure/Auth/{CurrentUserMiddleware,JwtExtensions}.cs`:
  reale Problem-/Validierungs-/Sitzungsfehler.
- `api/Framework/Infrastructure/RateLimiting/RateLimitingExtensions.cs`:
  benannte Policies, Schlüssel, Limits und optionaler Retry-After.
- `api/Service/ManagedResources/Boundary/HttpControllers/ResourceSwitchController.cs`,
  `api/Service/ManagedResources/Boundary/Dto/ResourceControlDtos.cs`: 202,
  Objektberechtigung, Idempotency-Key, unabhängige Soll-/Istzustände.
- `api/Service/Observability/Boundary/HttpControllers/PersonalDashboardsController.cs`:
  anderer Parallelitätsvertrag ETag/If-Match.
- `docker-compose.yml`: Port/API-Adresse. `web/lib/{source,openapi}.ts` und
  `web/contracts/backend-swagger-docs.json`: generierte Referenzquelle und Pfade.

## Checks und Praxisgrenzen

- `bunx --no-install prettier --ignore-path /dev/null --write` nur für die zwei
  zugewiesenen Dateien; anschließender `--check` erfolgreich.
- Produktseite mit installiertem `@mdx-js/mdx` kompiliert: erfolgreich.
- Alle 18 Seitenlinks auf vorhandene Dateien oder durch
  `createOpenAPI(...).staticSource({baseDir: 'entwickeln/API', groupBy: 'tag'})`
  erzeugte virtuelle Referenzseiten abgeglichen: keine fehlenden Ziele.
- Sieben Bash-Codeblöcke jeweils mit `bash -n` und `zsh -n` geprüft;
  JSON-Requestblock erfolgreich geparst. Kein HTTP-Request dabei ausgeführt.
- `git -C web/content/docs diff --check -- docs/entwickeln/http-api.mdx
planning/reviews/2026-11-01/entwickeln--http-api.md`: erfolgreich.

Nicht durchgeführt: echte Anmeldung,
MFA, OIDC-Provider/Passkey-Browser, HTTP-Lese-/Schreibaufrufe, Rendering in beiden
Consumern und Hardwareausführung. Die Shell-Beispiele sind gegen Request-/DTO-
Verträge und Syntax geprüft; sie sind kein Nachweis einer echten Sitzung oder
erfolgreich angelegten Testressource.

## Koordination und Publikationsvorschlag

- Status **zur Prüfung**. Die Anleitung ist als begrenzter Einstieg verwendbar,
  Veröffentlichung erst nach zentralem Render-/Linkcheck und einem geeigneten
  authentifizierten Testlauf entscheiden. Aktuelle Navigation blendet die Seite
  aus; Navigation/Bereichsfilter sind bewusst nicht geändert.
- Vorhandene Anker: `authentifizierung-und-rechte`,
  `beispielaufrufe-und-verträge`, `fehler-und-betrieb`. Die Überschriften bleiben.
- Virtuelle `.mdx`-Referenzlinks liegen nicht im Docs-Dateibaum, sondern werden
  durch Fumadocs aus dem Backend-Vertrag erzeugt; zentralen Linkcheck entsprechend
  ausführen. Einstieg `api-integration.mdx` gehört einem anderen Seitenagenten.
- Keine zusätzlich benötigte Produktseite, kein Screenshot-/Assetbedarf.

Geänderte Dateien: `docs/entwickeln/http-api.mdx` und dieser Bericht.
