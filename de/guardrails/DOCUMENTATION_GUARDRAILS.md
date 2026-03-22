# DOCUMENTATION GUARDRAILS

## Zweck
Dieses Projekt soll nicht nur funktionieren, sondern auch nachvollziehbar, übergebbar, wartbar und betreibbar sein.
Dokumentation ist kein nachträglicher Dekor und kein Selbstzweck. Sie dient dazu, Entscheidungen, Struktur, Betrieb, Grenzen, Risiken und Nutzung so festzuhalten, dass ein anderer Mensch das System verstehen und sicher weiterführen kann.

Das Ziel ist nicht, möglichst viel Text zu produzieren.
Das Ziel ist, genau die Informationen sauber zu dokumentieren, die für Verständnis, Betrieb, Änderungen, Fehlersuche und Übergabe relevant sind.

## Grundprinzipien
- Klarheit vor Vollständigkeitsillusion
- Relevanz vor Textmenge
- Konkretheit vor Marketing-Sprache
- Struktur vor Fliesstext-Müllhalde
- Aktuelle Dokumentation vor schöner, veralteter Dokumentation
- Entscheidungen und Grenzen explizit machen
- Dokumentation entlang echter Nutzungsszenarien schreiben
- Pragmatismus vor Dokumentations-Bürokratie

## Grundregel
Nicht alles braucht gleich viel Dokumentation.
Der Umfang der Dokumentation soll zum Risiko, zur Komplexität, zur Betriebsrelevanz und zur Übergabewahrscheinlichkeit passen.

Mehr Dokumentation ist nötig bei:
- produktiven Systemen
- Multi-User- oder Multi-Tenant-Lösungen
- sicherheitsrelevanten Funktionen
- Integrationen mit Drittanbietern
- komplexen Deployments
- Rollen- und Rechtesystemen
- asynchronen Prozessen, Jobs, Queues, Webhooks, Automationen
- Import/Export, Abrechnung, PDF, Archivierung, Backups
- allem, was bei Ausfall, Fehlbedienung oder Missverständnis teuer wird

Weniger Dokumentation ist akzeptabel bei:
- kleinen Wegwerf-Prototypen
- lokalen Einweg-Skripten
- isolierten Hilfsfunktionen ohne Betriebsrelevanz
- rein visuellen Kleinanpassungen ohne Verhaltensänderung

## Was dokumentiert werden soll
Dokumentiere insbesondere:
- Zweck und Scope des Systems oder Moduls
- Architektur und Hauptbausteine
- Verantwortlichkeiten und Grenzen
- Datenfluss und zentrale Zustände
- wichtige Annahmen
- Konfiguration und Voraussetzungen
- Setup, Build, Run, Deploy
- Umgebungsvariablen und deren Bedeutung
- Integrationen und Abhängigkeiten
- Auth-, Rollen- und Sicherheitsannahmen
- relevante Fehlerfälle, Limits und bekannte Restriktionen
- Betriebswissen, Runbooks und Wiederherstellung
- API-Verhalten, Events, Jobs, Scheduler, Webhooks
- Datenmodelle, Statusmodelle oder relevante Zustandsübergänge
- Migrations- oder Breaking-Change-Hinweise
- offene Risiken, technische Schulden und bewusste Kompromisse

## Was vermieden werden soll
- keine generischen KI-Textwüsten ohne Informationswert
- keine Dokumentation, die nur den Code paraphrasiert
- keine offensichtlichen Dinge breit erklären, wenn sie aus dem Code direkt klar sind
- keine veralteten Copy-Paste-Blöcke
- keine Aussagen wie «einfach», «robust», «sicher», «skalierbar» ohne konkrete Einordnung
- keine Marketing-Texte in technischen Dokumenten
- keine Scheingenauigkeit
- keine Dokumentation, die so abstrakt ist, dass sie operativ nutzlos wird

## Zielgruppen
Schreibe Dokumentation so, dass klar ist, für wen sie gedacht ist.
Typische Zielgruppen:
- Entwickler
- Betreiber / Admins
- zukünftiges Ich
- Kunden oder interne Fachseite
- Integratoren
- Onboarding von Mitwirkenden

Mische diese Zielgruppen nicht unnötig in einem unklaren Dokument.
Wenn nötig, trenne:
- technische Referenz
- Betriebsdokumentation
- Endnutzer-Dokumentation
- Architektur-Entscheidungen
- Übergabe- oder Setup-Anleitungen

## Dokumentationsarten
Nutze je nach Bedarf die passende Form.

### README
Für Einstieg, Zweck, Setup, Start, Grundstruktur, wichtigste Befehle und Links zu tieferer Dokumentation.

### Architektur-Dokumentation
Für Systemgrenzen, Hauptkomponenten, Datenflüsse, Integrationen, Sicherheitsannahmen und zentrale Entscheidungen.

### Runbook / Operations-Dokumentation
Für Deployment, Konfiguration, Monitoring, Logs, Backups, Restore, Rollback, Troubleshooting, bekannte Failure Modes und Notfallabläufe.

### API- oder Schnittstellen-Dokumentation
Für Endpunkte, Eingaben, Ausgaben, Fehlerfälle, Events, Webhooks, Auth-Anforderungen, Idempotenz und Seiteneffekte.

### ADRs oder Entscheidungsnotizen
Für wichtige Architektur- oder Technologieentscheide:
- welche Entscheidung
- warum
- welche Alternativen verworfen wurden
- welche Konsequenzen das hat

### Änderungsdokumentation
Für Breaking Changes, Migrationen, neue Konfigurationen, veränderte Sicherheitsannahmen oder neue Betriebsanforderungen.

## README-Regeln
Ein gutes README soll mindestens beantworten:
- Was ist das?
- Wofür ist es da?
- In welchem Kontext wird es eingesetzt?
- Wie startet man es lokal?
- Welche Voraussetzungen gibt es?
- Wo liegt die weiterführende Dokumentation?
- Welche Limits oder Besonderheiten muss man kennen?

Das README ist Einstiegspunkt, nicht komplette Enzyklopädie.

## Architektur-Dokumentation
Architektur-Dokumentation soll nicht aus leerem Buzzword-Nebel bestehen.
Sie soll konkret machen:
- Hauptbausteine und Zuständigkeiten
- Datenfluss
- zentrale Abhängigkeiten
- Auth- und Rollenmodell
- synchron vs. asynchron
- Zustandsübergänge
- wo Businesslogik liegt
- welche Teile kritisch sind
- welche Grenzen bewusst gezogen wurden

Wenn Diagramme helfen, nutze sie.
Diagramme ersetzen aber keinen präzisen Text.

## Dokumentation von Konfiguration
Konfiguration muss explizit und nachvollziehbar dokumentiert werden.
Beschreibe:
- welche Variablen oder Settings es gibt
- welche Werte erwartet werden
- welche Defaults gelten
- was optional vs. Pflicht ist
- welche Werte sicherheitsrelevant sind
- welche Auswirkungen Fehlkonfiguration hat

Keine rätselhaften ENV-Listen ohne Erklärung.

## Dokumentation von Sicherheit
Sicherheitsrelevante Aspekte sollen dokumentiert werden, aber ohne unnötige Angriffsanleitung.
Dokumentiere insbesondere:
- Auth- und Berechtigungsmodell
- Vertrauensgrenzen
- sicherheitsrelevante Annahmen
- Secret Handling
- relevante Datenklassifikation
- Rate Limits, Validierung, Upload-Regeln, Session- oder Token-Verhalten
- Backup-, Restore- und Audit-Verhalten
- bekannte Restrisiken oder bewusst nicht umgesetzte Massnahmen

Nicht dokumentieren:
- konkrete produktive Secrets
- unnötig exploitable Interna
- operative Details, die nur in geschütztem Kontext stehen sollten

## Dokumentation von Datenmodellen und Zuständen
Wenn Datenmodelle, Statusmodelle oder Workflow-Zustände wichtig sind, müssen sie klar dokumentiert sein.
Beschreibe:
- relevante Felder
- fachliche Bedeutung
- erlaubte Zustände
- Übergänge
- Invarianten
- was unveränderlich ist
- was auditierbar oder versioniert ist
- wie Fehler- und Sonderfälle behandelt werden

## Dokumentation von Betrieb und Fehlersuche
Betriebsrelevante Systeme brauchen dokumentierte Antworten auf:
- Wie wird gestartet?
- Wie wird deployed?
- Wie wird überwacht?
- Wo sind Logs?
- Welche typischen Fehler gibt es?
- Wie sieht ein sicherer Rollback aus?
- Wie funktioniert Backup und Restore?
- Was tun bei Ausfall einer Integration?
- Was tun bei Dateninkonsistenz?
- Welche Checks sind nach Änderungen nötig?

## Dokumentation bei Refactoring und Änderungen
Wenn Struktur, Verhalten, Schnittstellen oder Betriebsannahmen geändert werden, prüfe aktiv, ob Dokumentation angepasst werden muss.
Codeänderung ohne Doku-Prüfung gilt nicht als sauber abgeschlossen.

Achte besonders auf:
- geänderte Setups
- neue ENV-Variablen
- veränderte Rollen oder Berechtigungen
- neue APIs oder Payloads
- geänderte Datenmodelle
- neue Scheduler, Queues oder Background-Jobs
- neue Risiken, Limits oder Failure Modes

## Sprache und Stil
Dokumentation soll:
- sachlich
- präzise
- knapp, aber vollständig genug
- strukturiert
- überprüfbar
- technisch sauber

Vermeide:
- Füllsätze
- Wiederholungen
- unklare Pronomen
- Worthülsen
- nicht überprüfbare Behauptungen

## Qualität von KI-erzeugter Dokumentation
Jede KI-erzeugte Dokumentation muss auf Wahrheit und Passung geprüft werden.
Nicht erfinden:
- Dateien
- Prozesse
- Deployments
- Sicherheitsmechanismen
- Tests
- Integrationen
- Monitoring
- Limits
- Roadmap-Zusagen

Wenn etwas unklar oder nicht implementiert ist, schreibe das klar hin.

## Definition of Done
Dokumentation ist erst gut, wenn:
- klar ist, wozu das System oder Modul dient
- relevante Architektur, Konfiguration und Betriebslogik nachvollziehbar sind
- wichtige Entscheidungen und Grenzen explizit sind
- Setup und Betrieb ohne Rätsel möglich sind
- geänderte Annahmen und Risiken dokumentiert wurden
- der Text konkret statt generisch ist
- die Dokumentation zur tatsächlichen Implementierung passt
- unnötige Textmenge vermieden wurde

## Pflichtausgabe nach jedem Dokumentations-Pass
Gib am Ende aus:
1. welche Dokumente neu erstellt oder aktualisiert wurden
2. welche Themen abgedeckt wurden
3. welche bewussten Grenzen, Annahmen oder Risiken dokumentiert wurden
4. was bewusst noch nicht dokumentiert ist
5. wo die Dokumentation künftig gepflegt werden soll

Wichtig:
Nicht nur Dokumentation hinzufügen, sondern bestehende Dokumentation auch korrigieren, straffen oder löschen, wenn sie irreführend, veraltet oder redundant ist.
