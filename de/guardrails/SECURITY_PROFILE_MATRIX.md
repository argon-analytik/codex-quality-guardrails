# SECURITY PROFILE MATRIX

## Zweck
Diese Matrix dient dazu, vor einer Security-Umsetzung oder einem Review die Sicherheitsstufe einer App pragmatisch einzuschätzen.

## Vorgehen
Bewerte die App entlang dieser Achsen:

### 1. Datenkritikalität
- niedrig: kaum sensible Daten, keine Personendaten oder nur wenig kritische Inhalte
- mittel: normale Kunden-, Kontakt-, Betriebs- oder Geschäftsdaten
- hoch: besonders schützenswerte Personendaten, Finanzdaten, HR-Daten, Gesundheitsdaten, Vertragsdaten, Zugangsdaten

### 2. Exponierung
- niedrig: nur lokal oder intern, stark eingeschränkter Zugriff
- mittel: Login-geschützte Web-App oder API
- hoch: öffentlich erreichbare Internet-App, offene Integrationen, Webhooks, mobile Clients, viele externe Einstiegspunkte

### 3. Berechtigungskomplexität
- niedrig: kein Login oder nur sehr einfache Rollenlogik
- mittel: Benutzer, Admin, einfache Teams oder normale CRUD-Rechte
- hoch: Multi-Tenant, Support-Rollen, Service-Accounts, Delegation, Freigaben, Mandanten- und Objektgrenzen

### 4. Seiteneffekte und Missbrauchspotenzial
- niedrig: Lesesystem ohne kritische Aktionen
- mittel: normale Schreibfunktionen, Uploads, E-Mails, PDFs, Exporte
- hoch: Rechnungen, Zahlungen, Automationen, Massenänderungen, Integrationen, Agenten, Tools mit Schreibrechten

### 5. Schaden bei Vorfall
- niedrig: begrenzter operativer Schaden
- mittel: reale Geschäftsunterbrechung, Datenverlust oder Reputationsschaden
- hoch: grosse rechtliche, finanzielle oder operative Auswirkungen

## Einordnung

### S1
Wenn fast alles niedrig ist und kein klar hoher Risikofaktor vorhanden ist.

### S2
Sobald mehrere Achsen mittel sind oder eine einzelne Achse klar produktiv relevant wird.
Das ist der typische Standard für die meisten echten Business-Apps.

### S3
Sobald mindestens eine Achse hochkritisch ist und die App zugleich produktiv, internetexponiert, rollenkomplex oder stark integrationslastig ist.
Auch Multi-Tenant-Produkte mit sensiblen Daten oder agentische Systeme mit Toolzugriff fallen meist hier hinein.

## Entscheidungsregeln
- Im Zweifel eher S2 als S1.
- S3 nicht inflationär verwenden, aber ernst nehmen.
- Tiefe Risikoklasse rechtfertigt keine schlampige Umsetzung.
- Hohe Risikoklasse rechtfertigt zusätzliche Komplexität nur dort, wo sie reale Risiken reduziert.

## Mindestmassnahmen pro Stufe

### S1
- sichere Inputs und Outputs
- keine offensichtlichen Injection- oder XSS-Fehler
- aktuelle Dependencies
- keine Secrets im Code oder Frontend
- saubere Fehlerbehandlung
- sichere Konfiguration

### S2
- alles aus S1
- saubere Authentisierung und serverseitige Autorisierung
- Rate Limits wo sinnvoll
- Upload-, Export- und Integrationspfade prüfen
- Tenant- und Rollenlogik testen, falls vorhanden
- Dependency- und Supply-Chain-Hygiene
- wichtige Aktionen nachvollziehbar machen

### S3
- alles aus S1 und S2
- formalisierter Threat-Model-Review
- härtere Rollen- und Tenant-Trennung
- Missbrauchsszenarien explizit testen
- stärkere Secret- und Session-Härtung
- bessere Audit-Logs und Alarmierung
- Security-Gates vor Release

## Pflichtfrage vor zusätzlicher Härtung
Reduziert diese Massnahme ein realistisches Risiko dieser App spürbar?
Wenn nein, nicht blind einbauen.
