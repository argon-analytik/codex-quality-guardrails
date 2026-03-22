# TESTING GUARDRAILS

## Zweck
Dieses Projekt soll nicht nur gut aussehen, sicher wirken oder sauber strukturiert sein, sondern auch unter realen Bedingungen korrekt funktionieren.
Testing dient dazu, kritisches Verhalten zu verifizieren, Regressionen früh zu erkennen und Änderungen mit nachvollziehbarer Sicherheit freizugeben.

Das Ziel ist nicht, möglichst viele Tests zu produzieren.
Das Ziel ist, die richtigen Dinge risikobasiert zu prüfen und kritische Logik, Zustandswechsel, Berechtigungen, Fehlerpfade und Integrationen verlässlich abzusichern.

## Grundprinzipien
- Verifikation vor Bauchgefühl
- Kritische Pfade vor Test-Quantität
- Verhalten vor Implementation
- Risiko vor Dogma
- Reproduzierbarkeit vor informellem Klicken
- Regression-Schutz vor Einmal-Validierung
- Klare Testgrenzen vor unsauberem Mischmasch
- Pragmatismus vor Test-Bürokratie

## Grundregel
Nicht jede Änderung braucht dieselbe Testtiefe.
Der Testumfang muss zur Kritikalität, Komplexität, Änderungsgefahr und potenziellen Schadenshöhe passen.

Mehr Absicherung ist nötig bei:
- Auth-, Session- und Berechtigungslogik
- Multi-Tenant-Trennung
- Rechnungen, Zahlungen, PDF-Generierung, Exporten
- Imports, Datenmigrationen und Datenkonvertierung
- Hintergrundjobs, Queues, Scheduler, Webhooks
- Integrationen mit Drittanbietern
- Statusautomaten und Workflow-Übergängen
- kritischen Formularen mit Validierung
- zerstörerischen Aktionen
- Security-relevanten Änderungen
- komplexem Refactoring

Weniger Absicherung ist akzeptabel bei:
- rein visuellen Detailkorrekturen ohne Verhaltensänderung
- kleinen Text- oder Copy-Anpassungen
- lokalen Hilfsfunktionen ohne Betriebsrelevanz
- Prototypen ohne Produktionsanspruch

## Was verifiziert werden soll
Prüfe insbesondere:
- erwartetes Verhalten bei gültigen Eingaben
- Fehlerverhalten bei ungültigen Eingaben
- Randfälle und Grenzwerte
- Zustandsübergänge
- Berechtigungsgrenzen
- leere Zustände und Nullfälle
- Ausfälle von Integrationen
- Retry-, Timeout- und Idempotenz-Verhalten
- Import-/Export-Konsistenz
- Persistenz und Datenintegrität
- Regressionsrisiken nach Refactoring
- Multi-User- oder Multi-Tenant-Isolation
- Verhalten bei partiellen Fehlern
- manuelle Nutzerflüsse mit hoher Kritikalität

## Was vermieden werden soll
- keine Testmenge als Selbstzweck
- keine fragilen Tests, die nur intern verdrahtete Details abprüfen
- keine Snapshot-Flut ohne echten Erkenntniswert
- keine E2E-Tests für jede Kleinigkeit
- keine Unit-Tests für trivialen Boilerplate-Code
- keine stillen Lücken bei kritischer Businesslogik
- keine rein manuellen Freigaben für riskante Änderungen, wenn Automatisierung möglich wäre
- keine Scheinsicherheit durch oberflächliche Happy-Path-Checks

## Testarten und Einsatz
Nutze je nach Risiko und Struktur die passende Ebene.

### Unit-Tests
Für reine Logik, Berechnungen, Parser, Mapper, Validierung, Statusübergänge, Hilfsfunktionen und deterministische Regeln.
Unit-Tests sollen schnell, klar und fokussiert sein.

### Integrationstests
Für das Zusammenspiel mehrerer Schichten oder Komponenten, zum Beispiel:
- Route + Validierung + Businesslogik + Datenzugriff
- Service + Drittintegration
- Formular + API + Persistenz
- Job + Queue + Statusänderung

### End-to-End-Tests
Für wenige, aber kritische Nutzerflüsse mit hohem Wert oder hohem Risiko.
Zum Beispiel:
- Login
- Berechtigungsrelevante Aktionen
- Rechnung erstellen und exportieren
- Multi-Step-Wizards
- kritische Admin-Aktionen
- Checkout- oder Freigabeprozesse

### Manuelle Verifikation
Sinnvoll bei:
- visuellen Änderungen
- Accessibility-Prüfung
- Browser-spezifischem Verhalten
- PDF- oder Druckdarstellung
- Integrationen, die schwer automatisierbar sind
- Post-Deploy-Checks

Manuelle Checks ersetzen keine automatisierbare Absicherung kritischer Logik.

## Fokus auf Verhalten
Tests sollen Verhalten absichern, nicht interne Implementation erraten.
Bevorzuge:
- Eingabe -> erwartete Ausgabe
- Aktion -> erwarteter Zustand
- Fehlerfall -> erwartete Behandlung
- Rolle X darf, Rolle Y darf nicht
- Event -> erwartete Folge
- Persistenz -> erwartete Datenform

Vermeide Tests, die bei harmlosem Refactoring grundlos brechen.

## Kritische Prüfbereiche
Achte besonders auf:
- Autorisierung und Ownership
- Multi-Tenant-Leaks
- Statuswechsel und Unveränderlichkeit
- Berechnungen und Rundungslogik
- Datums-, Zeit- und Zeitzonenlogik
- Retry- und Deduplizierungslogik
- Imports mit fehlerhaften Daten
- Exporte, PDFs, Mails, Webhooks
- Fehlerpfade und Fallbacks
- Race Conditions und doppelte Ausführung
- Idempotenz bei wiederholten Requests oder Jobs
- Filter, Suche, Pagination und Sortierung bei komplexen Datenansichten

## Testdaten und Isolation
Testdaten sollen kontrolliert, nachvollziehbar und möglichst stabil sein.
Vermeide:
- versteckte Abhängigkeiten zu produktionsnahen Systemen
- flüchtige externe Zustände ohne Stub oder Mock
- schwer reproduzierbare Randomness
- gemeinsam genutzte, unbereinigte Testzustände

## Refactoring und Tests
Grössere Refactors ohne Verifikation sind unvollständig.
Wenn Struktur geändert wird, prüfe aktiv:
- welche bestehende Logik regressionsgefährdet ist
- welche Tests angepasst werden müssen
- welche neuen Tests nötig werden
- ob vorher untestbare Logik testbar gemacht wurde

## Release-relevante Verifikation
Vor riskanten Releases oder produktiven Änderungen sollen gezielte Smoke-Checks existieren.
Diese sollen mindestens kritische Kernpfade, Berechtigungen, Jobs, Integrationen und sichtbare Hauptfunktionen abdecken.

## Qualität von KI-erzeugten Tests
KI-erzeugte Tests sind nicht automatisch sinnvoll.
Prüfe kritisch:
- ob der Test überhaupt das Richtige absichert
- ob der Test wirklich fehlschlagen würde, wenn der Fehler existiert
- ob der Test zu implementationsnah ist
- ob Randfälle sinnvoll gewählt sind
- ob der Test nicht bloss bestehendes Verhalten kopiert, ohne es fachlich zu prüfen

## Definition of Done
Ein Testing-Pass ist erst gut, wenn:
- kritische Risiken explizit identifiziert wurden
- passende Testebenen gewählt wurden
- relevante Fehlerpfade und Randfälle abgedeckt sind
- kritische Änderungen regressionssicherer sind als vorher
- Tests Verhalten statt Zufall absichern
- manuelle und automatisierte Checks sinnvoll getrennt sind
- unnötige Testbürokratie vermieden wurde

## Pflichtausgabe nach jedem Testing-Pass
Gib am Ende aus:
1. welche Risiken oder kritischen Flows geprüft wurden
2. welche Tests neu erstellt, angepasst oder bewusst nicht ergänzt wurden
3. welche Bereiche automatisiert vs. manuell verifiziert wurden
4. welche Lücken oder Rest-Risiken bleiben
5. welche Checks vor Release zusätzlich sinnvoll sind

Wichtig:
Nicht einfach «mehr Tests» produzieren.
Erst Risiko und Kritikalität verstehen, dann gezielt absichern.
