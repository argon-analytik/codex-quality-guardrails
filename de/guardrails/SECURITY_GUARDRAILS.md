# SECURITY GUARDRAILS

## Zweck
Diese Regeln sollen verhindern, dass Sicherheit entweder zu schwach oder unnötig übertrieben umgesetzt wird.
Nicht jede App braucht dieselbe Härte. Aber jede App braucht eine saubere, bewusste, risikobasierte Sicherheitsprüfung.

Das Ziel ist nicht maximale Komplexität.
Das Ziel ist eine pragmatische, saubere, zur App passende Sicherheitsarchitektur.

## Grundsatz
Sicherheit ist kein pauschales Feature-Add-on.
Sicherheit ist eine Kombination aus:
- korrekter Bedrohungseinschätzung
- sauberer Architektur
- sicheren Defaults
- robuster Implementierung
- guten Betriebs- und Update-Prozessen

Behandle Sicherheit immer risikobasiert.
Vermeide zwei Extreme:
- zu schwache Umsetzung, weil klassische oder moderne Angriffsflächen übersehen werden
- unnötige Überhärtung, die Produkt, UX und Wartbarkeit verschlechtert, obwohl das reale Risiko niedrig ist

## Sicherheitsvorgehen vor jeder Umsetzung oder Review
Vor Änderungen zuerst das Sicherheitsprofil der App bestimmen:
1. Welche Daten werden verarbeitet?
2. Welche Schäden wären bei Leak, Manipulation oder Missbrauch realistisch?
3. Ist die App öffentlich im Internet erreichbar oder nur intern?
4. Gibt es Benutzerkonten, Rollen, Mandanten oder Admin-Funktionen?
5. Gibt es Zahlungs-, Dokument-, Upload-, PDF-, E-Mail-, Import-, Export- oder Integrationsfunktionen?
6. Gibt es privilegierte Automationen, Agenten oder Tools mit Seiteneffekten?
7. Welche Compliance-, Vertrags- oder Reputationsfolgen hätte ein Vorfall?

Erst danach Sicherheitsmassnahmen auswählen.
Nicht blind Enterprise-Komplexität einbauen.
Aber auch nicht trivialisieren.

## Sicherheitsstufen

### Stufe S1: Geringes Risiko
Beispiele:
- einfache interne Tools ohne sensible Daten
- kleine Microsites ohne Login
- einfache Dashboards mit geringer Kritikalität

Erwartung:
- saubere Input-Validierung
- sichere Defaults
- keine offensichtlichen Injection-, XSS-, CSRF- oder Auth-Fehler
- keine Secrets im Code
- aktuelle Dependencies
- Logging ohne Leaks
- sichere Konfiguration

### Stufe S2: Normales Produktivrisiko
Beispiele:
- normale Web-Apps mit Login
- CRUD-Systeme mit Kundendaten
- Mandantenfähige Business-Apps
- Portale mit Uploads, PDFs, E-Mails, Rollen oder APIs

Erwartung:
- alles aus S1
- saubere Authentisierung und Autorisierung
- serverseitige Rechteprüfung
- Schutz gegen IDOR/BOLA
- CSRF-Schutz, Session-Härtung, Rate Limits
- sichere Dateibehandlung
- Auditierbarkeit wichtiger Aktionen
- Dependency- und Supply-Chain-Hygiene
- Mindest-Threat-Model pro Feature

### Stufe S3: Hohes Risiko
Beispiele:
- Finanz-, Gesundheits- oder HR-nahe Systeme
- Apps mit besonders sensiblen Personendaten
- Admin-Plattformen mit hoher Reichweite
- Systeme mit vielen Integrationen oder weitreichenden Automationen
- agentische Systeme mit externen Tools oder Schreibrechten

Erwartung:
- alles aus S1 und S2
- formalisierter Threat-Model-Review
- strengere Session-, Secret- und Key-Verwaltung
- härtere Trennung von Rollen, Tenants und Vertrauensgrenzen
- minimierte Berechtigungen
- Missbrauchsszenarien und Abuse Cases explizit prüfen
- Härtung von Infrastruktur und Deployments
- bessere Audit-Logs, Alarmierung und Incident-Fähigkeit
- Security-Gates vor Release

## Immer prüfen, unabhängig von der Stufe
Diese Punkte sind immer Pflicht, auch bei kleineren Apps:

### 1. Eingaben und Ausgaben
- keine ungeprüften Eingaben in SQL, NoSQL, Shell, Templates, Markdown-Renderer, PDF-Renderer oder Dateipfade einspeisen
- parametrisierte Queries statt String-Zusammenbau
- serverseitige Validierung, nicht nur Frontend-Validierung
- Output-Kontext korrekt behandeln: HTML, URL, JS, CSS, Markdown, Template, CLI
- XSS, Injection, Path Traversal, Command Injection und SSRF mitdenken

### 2. Authentisierung und Sessions
- keine selbstgebastelte Kryptografie oder Sessionlogik
- etablierte Libraries und Flows nutzen
- Session- und Token-Lebensdauer bewusst wählen
- sichere Cookie-Flags setzen, wo Cookies verwendet werden
- kein Vertrauen in clientseitige Rollen oder versteckte UI-Zustände
- Logout, Session-Invalidierung und Passwort-Reset sauber prüfen

### 3. Autorisierung
- Rechte immer serverseitig prüfen
- nie nur UI verstecken
- Objektzugriffe auf fremde Datensätze prüfen
- Mandanten- und Rollenlogik explizit testen
- Admin-Funktionen separat härten

### 4. Secrets und Konfiguration
- keine Secrets in Repo, Frontend-Bundle, Logs oder Screenshots
- Secrets nur über sichere Secret-Mechanismen oder Environment-Management
- dev/test/prod sauber trennen
- Debug-Modi, offene Admin-Endpunkte, Demo-Credentials und Verbose-Errors vor Release entfernen

### 5. Dependencies und Supply Chain
- Frameworks, Plugins, SDKs, Zusatzmodule und Build-Tools auf veraltete oder verwundbare Versionen prüfen
- unnötige Abhängigkeiten entfernen
- Lockfiles und reproduzierbare Builds bevorzugen
- Herkunft und Vertrauenswürdigkeit neuer Pakete prüfen
- transitive Risiken nicht ignorieren

### 6. Logging und Fehlerbehandlung
- keine Passwörter, Tokens, Session-IDs, API-Keys, personenbezogene Inhalte oder interne Secrets loggen
- Fehlermeldungen für Nutzer reduziert, für interne Diagnose aber trotzdem nutzbar halten
- Stacktraces und interne Details nicht an Endnutzer leaken

### 7. Transport und Datenhaltung
- TLS erzwingen, wo relevant
- sensible Daten nur speichern, wenn wirklich nötig
- Aufbewahrung minimieren
- Export, Backup, Cache und temporäre Dateien mitprüfen
- sensible Daten im Browser, in Local Storage, im Dateisystem oder in mobilen Caches bewusst beurteilen

## Klassische Schwachstellen gezielt abklopfen
Prüfe explizit:
- SQL Injection
- NoSQL Injection
- Command Injection
- XSS
- CSRF
- SSRF
- Path Traversal
- unsichere Deserialisierung
- offene Redirects
- IDOR / BOLA
- fehlerhafte Zugriffskontrolle
- Security Misconfiguration
- ungenügende Rate Limits
- File Upload Missbrauch
- Directory Listing oder frei zugängliche Artefakte
- zu breite CORS-Regeln
- fehlende Sicherheitsheader, wo sinnvoll
- unsichere Passwort-Reset- oder Invite-Flows
- Session Fixation oder schwache Token-Verwaltung

## Moderne und häufig übersehene Risiken
Prüfe auch:
- veraltete Framework-, Plugin- oder SDK-Versionen
- schwache Supply-Chain-Hygiene
- gefährliche Standardkonfigurationen
- Leaks über Telemetrie, Error-Tracking, Analytics oder Third-Party-Skripte
- unsichere Webhooks, Callback-Endpoints oder Integrationen
- fehlende Tenant-Isolation
- Bypass durch Queue-Worker, Cronjobs, Background-Tasks oder interne APIs
- PDF-, Export-, Import- oder Office-Datei-Pipelines
- Markdown-, Rich-Text- oder Template-Rendering
- signierte URLs, Presigned Uploads, Attachment-Zugriffe und Download-Berechtigungen
- Schattenkopien sensibler Daten in Cache, Queue, Search-Index oder Logs

## Dateiuploads, Dokumente und Generierung
Sobald die App Uploads, PDFs, Exporte oder Dokumentgenerierung hat, zusätzlich prüfen:
- MIME-Type, Dateiendung und tatsächlichen Dateiinhalt validieren
- Dateigrösse und Limits erzwingen
- Dateinamen sanitizen
- keine direkte Ausführung oder öffentliche Ablegung ohne Zugriffskontrolle
- temporäre Dateien sauber löschen
- keine unkontrollierte Template-Injektion in PDF-, HTML- oder Dokumentgeneratoren
- Download-URLs und Attachment-Rechte serverseitig prüfen

## APIs und Integrationen
Bei APIs, Webhooks und Integrationen prüfen:
- Authentisierung und Autorisierung pro Endpoint
- Eingabevalidierung pro Endpoint, nicht nur global
- Rate Limits, Replay-Schutz oder Signaturprüfung, wo relevant
- Idempotenz bei kritischen Schreiboperationen
- robuste Fehlerbehandlung ohne Datenleck
- externe Antworten nie blind vertrauen
- Timeouts, Retries und Fallbacks sicher gestalten

## Multi-Tenant und Rollenmodelle
Bei mandantenfähigen Apps ist das Pflicht:
- jede Query, jeder Objektzugriff und jeder Export auf Tenant-Kontext prüfen
- keine tenant-fremden IDs akzeptieren
- Rechte nicht nur im Frontend modellieren
- Admin, Support, Service-Account und Benutzerrollen strikt unterscheiden
- Cross-Tenant-Leaks systematisch testen

## Infrastruktur und Betrieb
Prüfe auch die nicht sichtbaren Schichten:
- sichere Standardkonfigurationen für Reverse Proxy, App-Server, Datenbank und Storage
- keine unnötig offenen Ports, Buckets, Queues oder Admin-Panels
- Deployments reproduzierbar halten
- Secrets-Rotation zumindest für kritische Systeme ermöglichen
- Backups verschlüsselt und zugriffsgeschützt behandeln
- Monitoring und Alarmierung für sicherheitsrelevante Vorfälle vorsehen

## Agentische, KI- oder Tool-gestützte Systeme
Wenn die App Agenten, Tools, LLMs oder automatisierte Aktionen nutzt, zusätzlich prüfen:
- strikte Trennung zwischen Lesen, Entscheiden und Handeln
- Tools nur mit minimal nötigen Rechten freigeben
- keine impliziten Tool-Aufrufe ohne klare Policy
- Prompt-Injection, Context-Manipulation und Tool-Missbrauch mitdenken
- externe Inhalte nie automatisch als vertrauenswürdig behandeln
- Aktionen mit Seiteneffekt explizit absichern und protokollieren
- Secrets niemals ungefiltert in Prompts, Kontext oder Modellantworten geben
- unterschiedliche Vertrauensstufen für Benutzerinput, Retrieval-Inhalt, Systeminstruktionen und Tool-Output beachten

## Pragmatik-Regel
Nicht jede App braucht MFA, Hardware-Keys, Audit-Trails bis ins letzte Detail oder komplizierte Freigabeworkflows.
Aber jede produktive App braucht eine saubere Mindestprüfung.

Darum gilt:
- Basisschutz immer
- zusätzliche Härtung nach Risikoprofil
- Komplexität nur dort erhöhen, wo Schaden, Exposure oder Missbrauchspotenzial es rechtfertigen

## Release-Gate vor produktiver Freigabe
Vor Release mindestens prüfen:
1. Sicherheitsstufe bestimmt und begründet
2. wichtigste Trust Boundaries dokumentiert
3. klassische Schwachstellen abgeklopft
4. Autorisierung und Tenant-Grenzen getestet
5. Secrets, Logs und Fehlerausgaben geprüft
6. Dependencies und veraltete Komponenten geprüft
7. Upload-, Export-, PDF-, E-Mail- und Integrationspfade geprüft, falls vorhanden
8. Security-relevante Restprobleme dokumentiert

## Pflichtausgabe nach jedem Security-Review
Gib am Ende aus:
1. Sicherheitsstufe der App und kurze Begründung
2. wichtigste Risiken nach Eintrittswahrscheinlichkeit und Schaden
3. konkrete Funde
4. was direkt behoben wurde
5. was bewusst akzeptiert wird und warum
6. welche Punkte vor Release zwingend offen bleiben oder noch getestet werden müssen

## Wichtig
Nicht nur Checklisten abhaken.
Sicherheitsrelevante Zusammenhänge verstehen.
Nicht blind verkomplizieren.
Aber auch nicht verharmlosen.
Arbeite risikobasiert, sauber, nachvollziehbar und pragmatisch.
