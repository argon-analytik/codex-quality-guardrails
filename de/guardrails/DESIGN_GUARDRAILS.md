# DESIGN GUARDRAILS

## Zweck
Dieses Produkt soll visuell ruhig, konsistent, lesbar und strukturell bewusst gestaltet wirken.
UI-Arbeit ist keine Dekoration, sondern Informationsarchitektur, Hierarchie, Abstände, Typografie, Interaktionsklarheit und visuelle Konsistenz.

Das Ziel ist kein Redesign um des Redesigns willen.
Das Ziel ist, das bestehende Produkt gezielt zu polieren, zu vereinfachen, auszurichten und zu normalisieren, damit es absichtlich und produktionsreif wirkt.

## Grundprinzipien
- Klarheit vor Dichte
- Konsistenz vor Vielfalt
- Vereinfachung vor zusätzlicher UI
- Gemeinsame Komponenten und Design-Tokens vor Einzellösungen
- Klare Hierarchie vor grossen Schriften
- Ruhige Abstände vor gequetschten Layouts
- Offensichtliche Interaktion vor erklärendem Ballast

## Was geprüft und verbessert werden soll
Prüfe im Browser alle relevanten Views, Dialoge, Sidebars, Split-Panes, Detailansichten, Formulare, Tabellen, Karten, Portale und Zustände.

Finde und behebe insbesondere:
- überladene Formulare
- inkonsistente Abstände
- schlecht ausgerichtete Elemente
- überlappende UI
- typografisch unausgewogene Texte
- Texte, die zu gross, zu klein oder schlecht proportioniert sind
- inkonsistente Padding-, Radius-, Schatten- und Fokus-Stile
- defekte Selected-, Outline- oder Border-Darstellungen
- Container oder innere Boxen, die andere Elemente berühren statt Luft zu haben
- schlechtes Scrollverhalten
- Split-Pane-Layouts, bei denen Bereiche nicht unabhängig scrollen
- Mischmasch bei Komponenten
- Mischmasch bei Fonts
- visuelles Rauschen durch zu viele Rahmen, Boxen und Verschachtelungen
- unnötige Textlabels bei offensichtlichen Aktionen
- schlechte Nutzung des horizontalen Platzes
- schwaches responsives Verhalten

## Layout und Abstände
Normalisiere das Layout mit einem kohärenten Abstandssystem.
Verwende konsistente Gaps, Padding, Margins und vertikalen Rhythmus.
Vermeide gequetschte Controls und ebenso unnötig grosse Leerräume.
Karten, Panels und Gruppen müssen innen sauberes Padding haben und nach aussen klar getrennt sein.
Dekorative innere Rahmen oder gerundete Container dürfen nie optisch mit benachbarten Elementen kollidieren.

## Typografie
Definiere und verwende eine klare Typografie-Hierarchie über die ganze App.
Nutze eine begrenzte, konsistente Skala für:
- Seitentitel
- Bereichstitel
- Untertitel
- Labels
- Fliesstext
- Hilfstexte
- Metadaten

Vermeide zufällige Grössensprünge, übergrosse Titel, winzige Nebentexte oder inkonsistente Zeilenhöhen.
Die Typografie soll ruhig, lesbar und ausgewogen wirken.

Mische Fonts nicht beliebig.
Verwende produktweit konsistent den vorgesehenen Font-Stack.

## Buttons und Aktionen
Reduziere visuelle Unruhe in Action-Bereichen.
Wo Aktionen aus dem Kontext klar sind und Platz knapp ist, bevorzuge Icon-only-Buttons mit sauberem Tooltip und aria-label.
Stapele Standardaktionen nicht vertikal, nur weil Textlabels zu breit sind.
Nutze kompakte, konsistente Action-Gruppen mit stabiler Grösse und Ausrichtung.

Entferne Textlabels nicht, wenn die Aktion dadurch unklar würde.
Nicht dogmatisch, sondern mit Urteil.

## Komponenten und Zustände
Vereinheitliche die Komponentenverwendung.
Erzeuge nicht mehrere fast gleiche Karten-, Button-, Input- oder Badge-Stile ohne echten semantischen Grund.
Normalisiere Hover-, Focus-, Active-, Selected-, Disabled-, Loading-, Empty- und Error-States.
Selected-Outlines und Focus-Ringe müssen sauber und konsistent gerendert werden, ohne kaputte Ecken, ungleichmässige Dicke oder Clipping.

## Formulare
Längere Formulare müssen für bessere Erfassbarkeit umstrukturiert werden.
Gruppiere zusammengehörige Felder klar.
Reduziere Dichte.
Verbessere visuelle Hierarchie.
Nutze Progressive Disclosure, wo sinnvoll.
Keine langen, komprimierten Wände aus Controls.

## Scroll- und Pane-Verhalten
Unabhängige Scrollbereiche müssen unabhängig funktionieren, wenn das der beabsichtigten UX entspricht.
Vermeide Scroll-Traps, gekoppelte Scroll-Bugs, abgeschnittene Sticky-Bereiche und Layouts, bei denen ein Pane die Nutzbarkeit eines anderen blockiert.

## Visueller Charakter
Die UI soll modern, ruhig, präzise und funktional wirken.
Nicht flashy.
Nicht überladen.
Nicht verspielt.
Nicht visuell laut.

## Sprach- und Typografie-Regeln für sichtbaren Text
Für sichtbaren Text gilt:
- richte dich nach der passenden Copy-Guardrail-Datei für Sprache und Zielmarkt
- in `/de/guardrails/` verwende `DESIGN_COPY_GUARDRAILS_SWITZERLAND.md` für die Schweiz oder `DESIGN_COPY_GUARDRAILS_GERMANY.md` für Deutschland
- für Österreich oder andere deutschsprachige Zielmärkte passe die nähere Variante bewusst an
- für andere Sprachen oder Märkte gilt dieselbe Regel: typografische Normen nicht blind übernehmen, sondern gezielt anpassen
- technische Strings, Code und menschlich sichtbare Sprache klar trennen

## Technische Disziplin
Kaschiere Probleme nicht mit ad-hoc CSS, wenn die Ursache in einer gemeinsamen Komponente, einem Token oder einer Layout-Regel liegt.
Bevorzuge saubere Korrekturen an der Quelle.
Fasse wiederholte Einzellösungen in gemeinsame Primitive, Tokens oder Shared Components zusammen, wo sinnvoll.

Führe keine neue Designsprache ein, wenn das nicht explizit verlangt wurde.
Arbeite innerhalb der bestehenden Produktsprache und verbessere sie.

## Accessibility und Robustheit
Erhalte lesbaren Kontrast, sinnvolle Hit Targets, Tastaturbedienbarkeit und sichtbare Fokuszustände.
Visuelle Verbesserungen dürfen keine Funktionalität beschädigen.

## Definition of Done
Ein UI/UX-Polishing-Pass ist erst fertig, wenn:
- keine offensichtlichen Überlappungen mehr existieren
- Abstände und Typografie seitenübergreifend kohärent wirken
- Komponenten verwandt statt improvisiert aussehen
- Selected- und Fokuszustände sauber gerendert sind
- Formulare lesbarer und weniger gequetscht sind
- Action-Bereiche den Platz effizient nutzen
- Scrollverhalten korrekt ist
- sichtbarer Text die passende Copy-Guardrail für Sprache und Zielmarkt einhält
- das Resultat ruhiger, sauberer und bewusster wirkt, ohne Funktionalität zu verlieren

## Pflichtausgabe nach jedem Polishing-Pass
Gib am Ende aus:
1. kurze Audit-Zusammenfassung der wichtigsten Probleme
2. was konkret geändert wurde
3. welche Shared Components, Tokens oder Stile normalisiert wurden
4. welche Restprobleme oder Blocker noch bestehen

Wichtig:
Nicht nur Probleme beschreiben, sondern tatsächlich beheben.
