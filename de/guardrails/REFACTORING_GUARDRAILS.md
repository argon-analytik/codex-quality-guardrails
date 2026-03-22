# REFACTORING GUARDRAILS

## Zweck
Dieses Projekt soll technisch klar, wartbar, robust und nachvollziehbar bleiben.
Refactoring ist keine kosmetische Aktivität, sondern dient dazu, Komplexität zu senken, Risiken zu reduzieren, Wiederverwendbarkeit zu erhöhen und Änderungen sicherer zu machen.

Das Ziel ist nicht, Code grundlos umzuschreiben.
Das Ziel ist, Struktur, Verantwortlichkeiten, Benennung, Datenflüsse, Zuständigkeiten und Fehlermodi so zu verbessern, dass das System einfacher verstanden, getestet, erweitert und betrieben werden kann.

## Grundprinzipien
- Einfachheit vor Cleverness
- Lesbarkeit vor Kürze
- Klare Zuständigkeiten vor implizitem Mischmasch
- Explizite Datenflüsse vor versteckten Seiteneffekten
- Kleine, gut benannte Bausteine vor grossen Mehrzweckblöcken
- Gemeinsame Primitive vor Copy-Paste
- Stabile Schnittstellen vor chaotischer Durchreichlogik
- Pragmatismus vor Dogma

## Was Refactoring leisten soll
Refactoring soll insbesondere:
- unnötige Komplexität reduzieren
- Verantwortlichkeiten sauber trennen
- wiederholten Code konsolidieren
- implizite Logik explizit machen
- riskante Sonderfälle besser abfangen
- Namensgebung präzisieren
- Module, Dateien und Komponenten klarer zuschneiden
- Testbarkeit verbessern
- technische Schulden gezielt abbauen
- künftige Änderungen billiger und sicherer machen

## Was vermieden werden soll
- kein grossflächiges Umschreiben ohne klaren Nutzen
- keine abstrakten Architekturspielereien ohne konkreten Bedarf
- keine zusätzlichen Schichten nur um «sauber» zu wirken
- keine neue Komplexität im Namen von Wiederverwendbarkeit
- keine Premature Abstraction
- keine Refactors, die Verhalten unbeabsichtigt ändern
- keine stillen API-Brüche ohne explizite Anpassung
- keine neuen Patterns nur weil sie modisch wirken

## Typische Probleme, die gesucht und behoben werden sollen
Prüfe gezielt auf:
- zu grosse Dateien oder Funktionen
- unklare oder gemischte Verantwortlichkeiten
- doppelte oder fast doppelte Logik
- Copy-Paste mit leichter Variation
- kryptische oder irreführende Namen
- logische Ketten mit zu vielen verschachtelten Bedingungen
- implizite Zustände
- zu viele boolesche Flags als versteckter Zustandsautomat
- unklare Seiteneffekte
- zu breite Komponenten oder Services
- UI-Komponenten mit zu viel Geschäftslogik
- Backend-Routen mit Validierung, Businesslogik und Persistence in einem Block
- fehlende Grenzziehung zwischen Domäne, Transport, Darstellung und Storage
- zu enge Kopplung
- unnötige globale Abhängigkeiten
- magische Strings, Zahlen und Einzelfall-Konstanten
- schwer testbare Funktionen
- unklare Fehlerbehandlung
- tote Pfade, Altlasten und ungenutzte Hilfsfunktionen
- Datenmodelle, die nicht zur eigentlichen Domäne passen

## Struktur und Modularität
Strukturiere Code entlang echter Verantwortlichkeiten, nicht entlang Zufall oder Wachstumsgeschichte.
Eine Datei, Komponente oder Klasse soll eine klar erkennbare Hauptaufgabe haben.
Wenn ein Modul gleichzeitig orchestriert, validiert, transformiert, rendert und speichert, ist die Struktur wahrscheinlich falsch.

Bevorzuge:
- kleine, fokussierte Module
- klare Grenzen zwischen Schichten
- konsistente Ordner- und Dateistrukturen
- stabile öffentliche Schnittstellen
- interne Hilfsfunktionen nur dort, wo sie semantisch hingehören

## Benennung
Benennung ist Teil der Architektur.
Namen müssen Absicht, Rolle und Ebene klar machen.
Vermeide:
- generische Namen wie data, util, helper, manager, thing, handleStuff
- Namen, die Implementation statt Bedeutung beschreiben
- Abkürzungen, die nur lokal verständlich sind

Bevorzuge Namen, die:
- fachlich präzise sind
- Verantwortung klar abgrenzen
- Ein- und Ausgaben verständlich machen
- Seiteneffekte sichtbar machen, wenn vorhanden

## Funktionen und Methoden
Funktionen sollen klar, lesbar und fokussiert sein.
Wenn eine Funktion mehrere mentale Ebenen mischt, ist sie zu breit.
Wenn eine Funktion nicht sinnvoll benannt werden kann, ist sie meist zu diffus.

Achte auf:
- überschaubare Länge
- klare Ein- und Ausgaben
- möglichst wenige versteckte Seiteneffekte
- frühzeitige Validierung
- verständliche Fehlerpfade
- Reduktion verschachtelter Logik
- Extraktion echter Teilaufgaben, nicht künstlicher Minifunktionen

## Komponenten und Frontend-Struktur
Im Frontend sollen Darstellung, Zustand, Datenladen und Seiteneffekte nicht unnötig vermischt werden.
UI-Komponenten sollen primär UI bleiben.
Komplexe Datenlogik, Mapping, Validierung oder Orchestrierung gehören in klar benannte Hilfsschichten, Hooks, Stores oder Services, je nach Architektur.

Achte auf:
- zu fette Page-Komponenten
- Props-Ketten ohne klare Grenze
- verstreute State-Logik
- duplizierte Mapping- oder Formatierungslogik
- schwer verständliche useEffect-Ketten
- uneinheitliche Form-Logik
- unklare Ownership von Daten und Zuständen

## Backend- und Service-Struktur
Routen, Controller oder Handler sollen nicht gleichzeitig alles machen.
Validierung, Auth, Businesslogik, Datenzugriff und externe Integrationen sollen nachvollziehbar getrennt sein.

Achte auf:
- fehlende Input-Validierung
- Businesslogik in Controllern
- Datenbanklogik an unpassenden Stellen
- unklare Transaktionsgrenzen
- fehlende Fehlerklassifikation
- verstreute Integrationslogik
- unklare Retry- oder Timeout-Strategien
- schwer nachvollziehbare Orchestrierung

## Datenmodelle und Typen
Typen, Interfaces, DTOs und Models sollen das reale System sauber abbilden.
Vermeide schwammige Universaltöpfe, überbreite Typen und Strukturen, die nur aus historischen Gründen existieren.

Achte auf:
- unpräzise Typen
- optionale Felder ohne fachlichen Grund
- widersprüchliche Datenformen
- Mapping-Chaos zwischen API, Domäne und UI
- fehlende Normalisierung
- magische unions oder any-artige Ausweichstrukturen

## Fehlerbehandlung
Fehlerbehandlung ist Teil der Architektur.
Fehler dürfen weder still geschluckt noch chaotisch nach oben gereicht werden.
Jeder wichtige Fehlerpfad soll bewusst behandelt werden.

Achte auf:
- leere catch-Blöcke
- unklare Fallbacks
- fehlende Kontextinformationen in Logs
- vermischte Nutzerfehler, Systemfehler und Integrationsfehler
- inkonsistente Fehlertypen
- fehlende Rückgabeverträge bei Fehlerfällen

## Konfiguration und Abhängigkeiten
Konfiguration soll explizit, zentral und nachvollziehbar sein.
Vermeide verstreute Environment-Zugriffe und hart codierte Sonderwerte.
Prüfe auch, ob Libraries, Plugins oder Hilfsbausteine noch sinnvoll sind oder ob sie unnötige Komplexität tragen.

## Performance und Ressourcen
Refactoring soll nicht nur «schöner», sondern auch vernünftiger werden.
Prüfe auf:
- unnötige Re-Renders
- unnötige Datenladungen
- redundante Berechnungen
- unnötig breite Payloads
- Blockierungen im UI
- ineffiziente Schleifen oder N+1-artige Muster
- unnötige Serialisierung oder Mapping-Ketten

Nicht auf Mikrooptimierung fokussieren, wenn die eigentliche Struktur das Hauptproblem ist.

## Tests und Verifikation
Wichtige Refactors müssen absicherbar sein.
Wenn Verhalten kritisch ist, ergänze oder korrigiere Tests.
Refactoring ohne Verifikation ist nur Hoffnung.

Achte auf:
- fragile Tests, die nur Implementation statt Verhalten prüfen
- fehlende Tests an kritischen Grenzen
- fehlende Regression-Absicherung bei extrahierter Logik
- untestbare Strukturen, die zuerst testbarer gemacht werden sollten

## Technische Disziplin
Refactoring soll an der Ursache ansetzen, nicht nur Symptome verschieben.
Bevorzuge gemeinsame Lösungen an der richtigen Stelle statt lokale Workarounds.
Wenn mehrere Stellen das gleiche Problem tragen, behebe die Quelle.

Dokumentiere wichtige strukturelle Entscheidungen kurz und klar, wenn sie nicht sofort offensichtlich sind.

## Definition of Done
Ein Refactoring-Pass ist erst fertig, wenn:
- Struktur und Zuständigkeiten klarer sind als vorher
- Komplexität spürbar reduziert wurde
- doppelte Logik konsolidiert wurde
- Benennung präziser ist
- Fehlerpfade nachvollziehbarer sind
- zentrale Datenflüsse verständlicher sind
- das Verhalten erhalten blieb oder bewusst verbessert wurde
- kritische Änderungen sinnvoll verifiziert wurden
- der Code nicht nur anders, sondern tatsächlich besser wartbar ist

## Pflichtausgabe nach jedem Refactoring-Pass
Gib am Ende aus:
1. kurze Analyse der Hauptprobleme
2. was strukturell geändert wurde
3. welche Dateien, Module oder Komponenten betroffen sind
4. welche Duplikate, Komplexitäten oder Kopplungen reduziert wurden
5. welche Risiken, offenen Punkte oder Folgearbeiten bleiben

Wichtig:
Nicht blind umstrukturieren.
Nur dort eingreifen, wo der Nutzen klar ist.
Erst verstehen, dann schneiden.
