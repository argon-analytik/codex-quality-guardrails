# OPERATIONS / RELEASE GUARDRAILS

## Zweck
Dieses Projekt soll nicht nur lokal funktionieren, sondern auch kontrolliert ausrollbar, beobachtbar, betreibbar und wiederherstellbar sein.
Operations und Release-Qualität stellen sicher, dass Änderungen nicht blind in produktive Systeme kippen und dass Ausfälle, Fehlkonfigurationen und Datenprobleme operativ beherrschbar bleiben.

Das Ziel ist nicht, unnötige Enterprise-Prozesse aufzubauen.
Das Ziel ist, Betriebsrisiken proportional zur tatsächlichen Kritikalität zu reduzieren.

## Grundprinzipien
- Betriebsfähigkeit vor lokaler Bequemlichkeit
- Beobachtbarkeit vor blindem Vertrauen
- Reproduzierbarkeit vor Klick-Deploys
- sichere Änderungen vor hektischem Rollout
- Rollback-Fähigkeit vor Hoffnung
- klare Verantwortung vor impliziter Betriebslogik
- verhältnismässige Prozesse vor Overengineering
- pragmatische Absicherung vor Release-Theater

## Grundregel
Nicht jede App braucht dieselbe Betriebs- und Release-Disziplin.
Der Umfang muss zu Nutzerzahl, Datenkritikalität, Integrationen, Änderungsfrequenz und Ausfallkosten passen.

Mehr Operations-Disziplin ist nötig bei:
- produktiven Kunden- oder Multi-User-Systemen
- Integrationen mit Drittanbietern
- Jobs, Queues, Webhooks oder Automationen
- Datenbankmigrationen
- Billing, PDF, Exporte, Archivierung
- Multi-Tenant-Betrieb
- sensiblen oder auditrelevanten Daten
- hohem Release-Tempo
- geringer Fehlertoleranz

Weniger Aufwand ist akzeptabel bei:
- lokalen Tools ohne Fremdnutzer
- Prototypen ohne Produktionsanspruch
- isolierten Hilfsskripten ohne Betriebsrelevanz

## Was abgedeckt werden soll
Prüfe insbesondere:
- Build- und Deploy-Nachvollziehbarkeit
- Konfigurations- und ENV-Hygiene
- Secret-Handling
- Migrationen und deren Risiken
- Rollback- oder Recovery-Möglichkeiten
- Logging, Monitoring und Healthchecks
- Fehlererkennung bei Jobs, Webhooks und Integrationen
- Backups und Restore-Pfade
- Post-Deploy-Verifikation
- Release-Kommunikation und Breaking-Change-Hinweise
- Beobachtbarkeit stiller Teil-Ausfälle
- sichere Behandlung partieller Fehler

## Was vermieden werden soll
- keine unnötige Prozess-Schwere für kleine Lösungen
- keine manuelle Magie ohne Dokumentation
- keine stillen produktiven Änderungen ohne minimale Verifikation
- keine Migrationen ohne Rücksicht auf Datenintegrität
- keine Releases ohne Beobachtbarkeit
- keine Rollbacks, die nur theoretisch existieren
- keine verstreute Konfiguration ohne klare Quelle
- kein Secret-Leak in Repos, Logs oder Beispielwerten

## Konfiguration und Secrets
Konfiguration muss explizit, nachvollziehbar und trennbar von Code sein.
Dokumentiere:
- welche ENV-Variablen oder Settings existieren
- welche Pflicht vs. optional sind
- welche sicherheitsrelevant sind
- welche Defaults gelten
- welche Auswirkungen Fehlkonfiguration hat

Secrets dürfen nicht im Code, Frontend, Beispiel-Configs oder Logs landen.

## Build und Deploy
Build und Deploy sollen reproduzierbar und kontrollierbar sein.
Achte auf:
- nachvollziehbare Start- und Build-Befehle
- definierte Deploy-Schritte
- idempotente oder kontrollierte Deploy-Mechanik
- saubere Behandlung von Assets, Migrationsschritten und Hintergrundprozessen
- klare Unterschiede zwischen lokal, staging und produktiv

## Migrationen und Datenintegrität
Änderungen an Datenmodellen oder Persistenz sind betrieblich kritisch.
Prüfe:
- ob Migrationen sicher und nachvollziehbar sind
- ob Vor- und Rückwärtskompatibilität berücksichtigt wurde
- ob Rollback realistisch ist
- ob Backfill, Reindex oder Datenkonvertierung nötig wird
- ob Post-Migration-Checks definiert sind

## Logging, Monitoring und Healthchecks
Relevante Systeme brauchen sinnvolle Beobachtbarkeit.
Achte auf:
- strukturierte Logs mit genug Kontext
- keine sensitiven Daten in Logs
- Healthchecks für relevante Dienste
- Fehlererkennung bei stillen Teil-Ausfällen
- Sichtbarkeit für Job-Fehler, Retry-Loops, Queue-Stau oder Integrationsabbrüche
- sinnvolle Metriken oder andere Beobachtungssignale, wenn das Risiko es verlangt

## Backups, Restore und Recovery
Für datenrelevante Systeme muss klar sein:
- ob und wie gesichert wird
- welche Daten kritisch sind
- wie Restore funktioniert
- wie Integrität nach Restore geprüft wird
- welche Daten oder Zustände nicht sauber rückspielbar sind
- welche Recovery-Schritte bei Integrations- oder Job-Ausfällen nötig sind

## Release-Disziplin
Releases sollen nicht nur «deploybar», sondern kontrolliert freigebbar sein.
Achte auf:
- klare Release- oder Merge-relevante Checks
- Kennzeichnung von Breaking Changes
- Migrationshinweise
- Post-Deploy-Smoke-Checks
- Rückfallstrategie bei Problemen
- stufenweises Ausrollen, wenn Risiko und Kontext das rechtfertigen

## Runbooks und Betriebswissen
Operativ kritische Systeme brauchen dokumentierte Antworten auf:
- Wie wird deployt?
- Wie wird ein Fehler erkannt?
- Wie wird ein Job neu angestossen?
- Wie wird bei Integrationsfehlern reagiert?
- Wie wird Rollback oder Restore durchgeführt?
- Welche Checks sind nach Release nötig?
- Welche Failure Modes sind bekannt?

## Qualität von KI-erzeugten Operations-Änderungen
KI darf keine imaginären Betriebsmechanismen erfinden.
Nicht behaupten oder dokumentieren, wenn nicht vorhanden:
- Monitoring
- Alerts
- Rollbacks
- Backups
- Migrationssicherheit
- Blue/Green oder Canary-Strategien
- Retry- oder Recovery-Logik

Wenn etwas fehlt, muss es klar als Lücke bezeichnet werden.

## Definition of Done
Ein Operations-/Release-Pass ist erst gut, wenn:
- kritische Betriebsrisiken sichtbar sind
- Konfiguration und Secrets sauber behandelt werden
- Migrationen und Datenrisiken bewusst eingeordnet sind
- relevante Beobachtbarkeit vorhanden oder als Lücke benannt ist
- Post-Deploy- und Recovery-Checks klarer sind als vorher
- unnötige Prozesslast vermieden wurde
- reale Release-Risiken geringer oder klarer kontrolliert sind

## Pflichtausgabe nach jedem Operations-/Release-Pass
Gib am Ende aus:
1. welche Betriebs- oder Release-Risiken geprüft wurden
2. was direkt verbessert wurde
3. welche Deploy-, Migrations-, Observability- oder Recovery-Themen betroffen sind
4. welche Risiken bewusst bleiben
5. welche Checks oder Runbooks vor produktivem Release noch fehlen

Wichtig:
Nicht pauschal verkomplizieren.
Operative Disziplin soll reale Risiken senken, nicht nur professionell aussehen.
