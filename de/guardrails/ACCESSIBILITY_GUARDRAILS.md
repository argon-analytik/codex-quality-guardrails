# ACCESSIBILITY GUARDRAILS

## Zweck
Dieses Produkt soll nicht nur visuell sauber wirken, sondern für reale Menschen robust bedienbar und verständlich sein.
Accessibility stellt sicher, dass Oberflächen auch mit Tastatur, Screenreader, Zoom, reduzierter Motorik, eingeschränktem Sehvermögen oder veränderter Darstellung sinnvoll nutzbar bleiben.

Das Ziel ist nicht, formale Compliance nur abzuhaken.
Das Ziel ist, reale Bedienbarkeit, Verständlichkeit und technische Zugänglichkeit systematisch zu verbessern.

## Grundprinzipien
- Benutzbarkeit vor Optik-Tricks
- Semantik vor Div-Mischmasch
- Tastatur vor Maus-Annahme
- Klarheit vor rein visueller Codierung
- robuste Interaktion vor dekorativer Animation
- korrekte Zustände vor visueller Illusion
- echte Lesbarkeit vor ästhetischer Härte
- Pragmatismus vor ARIA-Theater

## Grundregel
Accessibility ist nicht nur für öffentliche Grossprojekte relevant.
Auch interne oder kleine Apps profitieren stark von korrekter Tastaturbedienung, klaren Fehlermeldungen, Fokusführung und lesbarer Struktur.

Mehr Sorgfalt ist nötig bei:
- kundenorientierten oder öffentlichen Oberflächen
- Formular-lastigen UIs
- datenreichen Dashboards und Tabellen
- komplexen Dialogen, Drawern, Menüs und Multi-Step-Flows
- Admin- oder Betriebsoberflächen mit hoher Arbeitsdichte
- Apps mit häufiger Tastaturnutzung
- regulatorisch oder vertraglich sensiblen Projekten

## Was geprüft und verbessert werden soll
Prüfe insbesondere:
- Tastaturnavigation
- sichtbare Fokuszustände
- semantische Struktur
- Formularlabels und Fehlermeldungen
- Kontrast und Lesbarkeit
- Bedienelementgrössen und Klickflächen
- sinnvolle Reihenfolge von Fokus und Interaktion
- Dialog- und Menüverhalten
- Screenreader-relevante Zustände
- Zoom- und Responsive-Verhalten
- Bedeutungen, die nicht nur über Farbe vermittelt werden
- Statusmeldungen bei asynchronen Vorgängen

## Was vermieden werden soll
- keine Maus-only-Interaktion
- keine unsichtbaren oder kaum sichtbaren Fokuszustände
- keine ARIA-Attribute als Alibi ohne korrekte Semantik
- keine Interaktion, die nur aus Farbe oder Position verständlich ist
- keine Fehlermeldungen ohne Kontext oder Zuordnung
- keine modalen Dialoge ohne Fokus-Management
- keine winzigen Hit Targets
- keine übertriebene Motion ohne Rücksicht auf reduzierte Bewegung

## Struktur und Semantik
Bevorzuge echte semantische Elemente, wo sie passen:
- button statt klickbares div
- label statt blosser Placeholder
- heading-Struktur statt optischer Überschriften ohne Struktur
- Listen, Tabellen und Landmarken dort, wo sie fachlich sinnvoll sind

Semantik ist Teil der Bedienbarkeit, nicht bloss HTML-Ästhetik.

## Tastatur und Fokus
Alle wesentlichen Interaktionen müssen per Tastatur erreichbar und sinnvoll nutzbar sein.
Achte auf:
- logische Fokus-Reihenfolge
- sichtbaren Fokus
- keine Fokus-Fallen
- korrekte Fokus-Rückgabe nach Dialogen oder Menüs
- Enter-, Escape- und Tab-Verhalten bei üblichen Controls
- keine versteckten, aber fokussierbaren Elemente
- keine wichtigen Aktionen, die nur per Hover sichtbar oder erreichbar sind

## Formulare und Fehlerzustände
Formulare müssen verständlich und fehlertolerant sein.
Achte auf:
- klare Labels
- unterstützende Hilfstexte dort, wo nötig
- verständliche Fehlertexte
- Fehler direkt am relevanten Feld oder Bereich
- sinnvolle Zustände bei Loading, Success und Failure
- Pflichtfelder nicht nur farblich markieren
- keine alleinige Nutzung von Placeholdern als Label-Ersatz

## Kontrast, Lesbarkeit und Skalierung
Die UI muss unter realen Bedingungen lesbar bleiben.
Prüfe:
- ausreichenden Kontrast
- ausreichend grosse und ruhige Typografie
- Skalierung bei Browser-Zoom
- keine abgeschnittenen Texte oder Controls bei Zoom
- brauchbare Layouts auch bei vergrösserter Darstellung
- keine zu kleinen klickbaren Flächen

## Dynamische UI und Statuskommunikation
Bei asynchronen oder dynamischen UIs muss klar bleiben, was passiert.
Achte auf:
- verständliche Ladezustände
- Statusmeldungen bei Erfolg oder Fehler
- sinnvolle Live-Regionen, wenn notwendig
- keine stillen Änderungen ohne Rückmeldung
- zugängliche Dialoge, Menüs, Tabs, Accordions und Drawers

## Tabellen, Filter und datenreiche UIs
Bei komplexen Datenansichten prüfe:
- sinnvolle Tabellenstruktur
- lesbare Spalten und Header
- Fokus- und Tastaturverhalten
- zugängliche Filter und Sortierung
- verständliche leere Zustände
- keine reine Farbcodierung für kritische Unterschiede

## Motion und Präferenzen
Animationen dürfen Nutzung nicht erschweren.
Beachte:
- reduzierte Bewegung respektieren, wo sinnvoll
- keine wichtige Information nur über Animation transportieren
- keine übermässigen Bewegungen, die Orientierung oder Lesbarkeit stören

## Qualität von KI-erzeugter Accessibility
KI neigt dazu, Accessibility oberflächlich zu «simulieren».
Prüfe kritisch:
- ob die Semantik wirklich stimmt
- ob ARIA korrekt und nötig ist
- ob Fokusmanagement real funktioniert
- ob Fehlermeldungen verständlich und zuordenbar sind
- ob zugängliche Interaktion tatsächlich getestet oder verifiziert wurde

## Definition of Done
Ein Accessibility-Pass ist erst gut, wenn:
- zentrale Interaktionen per Tastatur nutzbar sind
- Fokus sichtbar und sinnvoll geführt ist
- Semantik und Struktur nachvollziehbar sind
- Formulare verständlich und fehlertoleranter sind
- Kontrast und Lesbarkeit brauchbar sind
- dynamische Zustände verständlich kommuniziert werden
- Barrieren reduziert wurden, ohne die UI unnötig zu verkomplizieren

## Pflichtausgabe nach jedem Accessibility-Pass
Gib am Ende aus:
1. welche Accessibility-Probleme geprüft wurden
2. was direkt verbessert wurde
3. welche Bereiche manuell verifiziert werden sollten
4. welche Barrieren oder Rest-Risiken bleiben
5. welche Accessibility-Themen bewusst vertagt wurden

Wichtig:
Accessibility ist kein rein visuelles Feintuning.
Sie ist Teil von Qualität, Robustheit und echter Nutzbarkeit.
