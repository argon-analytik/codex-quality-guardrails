<div align="center">

# codex-quality-guardrails

**Pragmatische Guardrails und Review-Prompts für bessere Apps mit Codex**

Ein offenes Set aus Guardrails, Spawn-Review-Prompts und Umsetzungs-Prompts für Design, Security, Refactoring, Dokumentation, Testing, Operations/Release und Accessibility.

</div>

---

## Worum es hier geht

Dieses Repository bündelt wiederverwendbare Guardrails für KI-gestützte Softwareentwicklung mit **Codex Desktop App** und ähnlichen Coding-Agents.

Die Grundidee ist einfach:

- **`.md`-Dateien** definieren die dauerhaften Qualitätsregeln eines Bereichs
- **`01_...SPAWN_REVIEW_PROMPT.txt`** startet zuerst einen reinen Review mit Subagents
- **`02_...REVIEW_PROMPT.txt`** setzt danach die Arbeit um und berücksichtigt die Findings aus dem Spawn-Review

So entsteht ein sauberer zweistufiger Ablauf:

1. **zuerst analysieren**
2. **danach gezielt umsetzen**

Das verhindert blinde Aktionitis, unnötige Umbauten und generisches KI-Geschwafel.

---

## Warum dieses Repository existiert

Viele KI-generierte Projekte scheitern nicht an der ersten lauffähigen Version, sondern an der Qualität danach.

Typische Probleme sind:

- visuell überladene oder inkonsistente UIs
- fragiler, schwer wartbarer Code
- fehlende oder unverhältnismässige Security
- unklare oder veraltete Dokumentation
- fehlende Verifikation kritischer Logik
- schwache Betriebsfähigkeit vor produktiven Releases
- Accessibility, die nur optisch simuliert statt wirklich umgesetzt wird

Dieses Repository soll daraus **eine systematische Arbeitsweise** machen.

---

## Enthaltene Bereiche

| Bereich | Zweck | Standard oder optional? | Wann besonders sinnvoll |
|---|---|---:|---|
| **Design** | visuelle Ruhe, Konsistenz, Lesbarkeit, UI/UX-Polishing | Standard | sobald UI vorhanden ist |
| **Copy** | sichtbare Sprache, Umlaute, Schweizer Typografie, UI-Texte | Standard-Zusatz | zusammen mit Design |
| **Refactoring** | Struktur, Benennung, Wartbarkeit, Entkopplung | Standard | fast immer |
| **Security** | risikobasierte Sicherheitsprüfung und Härtung | Standard | fast immer |
| **Documentation** | Setup, Architektur, Betrieb, Übergabe, Annahmen | Standard | fast immer |
| **Testing** | Verifikation, Regression-Schutz, kritische Flows | Empfohlen | bei realer App-Logik praktisch immer |
| **Operations / Release** | Deploy, Migrationen, Beobachtbarkeit, Rollback, Runbooks | Optional | bei produktiven oder release-relevanten Systemen |
| **Accessibility** | Tastatur, Fokus, Semantik, Lesbarkeit, echte Zugänglichkeit | Optional, aber empfohlen | bei öffentlichen, kundenorientierten oder formularlastigen UIs |

---

## Was Standard sein sollte

Für die meisten ernsthaften Projekte ist dieser Kern sinnvoll:

- `DESIGN_GUARDRAILS.md`
- `COPY_GUARDRAILS.md`
- `REFACTORING_GUARDRAILS.md`
- `SECURITY_GUARDRAILS.md`
- `DOCUMENTATION_GUARDRAILS.md`
- `TESTING_GUARDRAILS.md`

Diese sechs Ebenen decken bereits die wichtigsten Qualitätsachsen ab:

- Wie es wirkt
- Wie es gebaut ist
- Wie sicher es ist
- Wie gut es verstanden und betrieben werden kann
- Wie gut kritisches Verhalten verifiziert ist

---

## Was optional ist

### Operations / Release

Dieser Bereich ist nicht für jeden kleinen Prototyp nötig.

Er wird wichtig, sobald mindestens eines davon zutrifft:

- produktive Nutzung
- echte Deployments
- Migrationsrisiken
- Jobs, Queues, Webhooks oder Integrationen
- Daten, die im Fehlerfall teuer oder kritisch werden
- Bedarf an Rollback, Healthchecks, Backups oder Runbooks

Wenn dein Projekt nur lokal, klein oder wegwerfartig ist, kannst du diesen Bereich oft weglassen.

### Accessibility

Accessibility ist **empfohlen**, aber sie sollte bewusst eingesetzt werden.

Warum optional?

Weil Accessibility-Verbesserungen oft nicht nur Farben oder Labels betreffen, sondern:

- semantische Struktur
- Fokusmanagement
- Tastaturnavigation
- Fehlermeldungen
- Dialogverhalten
- Formularstruktur
- teilweise auch Komponenten- und Layoutentscheidungen

Das kann zu **echten strukturellen Designanpassungen** führen. Genau deshalb ist Accessibility für öffentliche, kundenorientierte oder formularlastige Produkte sehr wertvoll, sollte aber nicht blind als rein kosmetischer Pass behandelt werden.

Pragmatische Regel:

- **öffentliche oder kundenorientierte UIs:** klar empfohlen
- **interne Tools:** oft sinnvoll, aber bewusst scopen
- **frühe Prototypen:** optional

---

## Grundprinzip des Workflows

Dieses Repository ist auf einen Review-first-Workflow ausgelegt.

### Phase 1: Spawn-Review
Verwende zuerst den passenden `01_...SPAWN_REVIEW_PROMPT.txt`.

Ziel:
- Subagents parallel prüfen lassen
- nur analysieren
- keine Änderungen
- Findings priorisieren
- Überschneidungen zusammenführen

### Phase 2: Umsetzungs-Pass
Verwende danach den passenden `02_...REVIEW_PROMPT.txt` zusammen mit der zugehörigen `.md`-Datei.

Ziel:
- Spawn-Findings validieren
- bestätigte Punkte umsetzen
- zusätzliche Probleme erkennen
- am Ende klar ausweisen, was bestätigt, umgesetzt, verworfen oder vertagt wurde

---

## Verwendung mit Codex Desktop App

## 1. Dateien ins Projekt legen

Lege die Guardrails in dein Repository, zum Beispiel so:

```text
/guardrails
  DESIGN_GUARDRAILS.md
  COPY_GUARDRAILS.md
  REFACTORING_GUARDRAILS.md
  SECURITY_GUARDRAILS.md
  SECURITY_PROFILE_MATRIX.md
  DOCUMENTATION_GUARDRAILS.md
  TESTING_GUARDRAILS.md
  OPERATIONS_RELEASE_GUARDRAILS.md
  ACCESSIBILITY_GUARDRAILS.md

/prompts
  01_DESIGN_SPAWN_REVIEW_PROMPT.txt
  02_DESIGN_REVIEW_PROMPT.txt
  01_REFACTORING_SPAWN_REVIEW_PROMPT.txt
  02_REFACTORING_REVIEW_PROMPT.txt
  01_SECURITY_SPAWN_REVIEW_PROMPT.txt
  02_SECURITY_REVIEW_PROMPT.txt
  01_DOCUMENTATION_SPAWN_REVIEW_PROMPT.txt
  02_DOCUMENTATION_REVIEW_PROMPT.txt
  01_TESTING_SPAWN_REVIEW_PROMPT.txt
  02_TESTING_REVIEW_PROMPT.txt
  01_OPERATIONS_RELEASE_SPAWN_REVIEW_PROMPT.txt
  02_OPERATIONS_RELEASE_REVIEW_PROMPT.txt
  01_ACCESSIBILITY_SPAWN_REVIEW_PROMPT.txt
  02_ACCESSIBILITY_REVIEW_PROMPT.txt
```

Du kannst die Dateien auch im Root ablegen. Wichtig ist nur, dass Codex sie klar lesen kann und die Pfade konsistent bleiben.

## 2. Passenden Bereich wählen

Nicht jeden Prompt auf jede Änderung loslassen.

Wähle nur die Bereiche, die wirklich relevant sind.

Beispiele:

| Änderung | Sinnvolle Bereiche |
|---|---|
| UI überarbeiten | Design, Copy, evtl. Accessibility |
| API umbauen | Refactoring, Security, Testing, Documentation |
| Auth oder Rollen ändern | Security, Testing, Documentation, evtl. Operations |
| PDF-/Export-Flow ergänzen | Design, Security, Testing, Documentation |
| Produktiver Release mit Migrationen | Security, Testing, Operations/Release, Documentation |

## 3. Zuerst `01_...` laufen lassen

Starte zuerst den Spawn-Review.

Beispielgedanke:
- zuerst Design-Spawn-Review
- danach Design-Umsetzung
- erst dann nächster Bereich

Das ist meist besser, als sofort fünf Umsetzungs-Prompts hintereinander zu schicken.

## 4. Danach `02_...` zusammen mit den `.md`-Guardrails

Der `02_...`-Prompt ist für die eigentliche Umsetzung gedacht.

Er soll:
- die Spawn-Findings berücksichtigen
- sie aber **nicht blind übernehmen**
- alles gegen den aktuellen Stand validieren
- zusätzliche Probleme ebenfalls beheben
- am Ende die Änderungen sauber zusammenfassen

---

## Empfohlene Reihenfolgen

### Für UI-lastige Apps

1. Design  
2. Refactoring  
3. Security  
4. Testing  
5. Documentation  
6. Accessibility  
7. Operations / Release

### Für Backend-, API- oder Integrationsarbeit

1. Refactoring  
2. Security  
3. Testing  
4. Documentation  
5. Operations / Release  
6. Design nur dort, wo UI betroffen ist

### Für produktive Releases

1. Security  
2. Testing  
3. Documentation  
4. Operations / Release  
5. Accessibility nur falls UI betroffen und relevant  
6. Design nur falls sichtbare Änderung enthalten ist

---

## Repository-Struktur

```text
codex-quality-guardrails/
├─ README.md
├─ DESIGN_GUARDRAILS.md
├─ COPY_GUARDRAILS.md
├─ REFACTORING_GUARDRAILS.md
├─ SECURITY_GUARDRAILS.md
├─ SECURITY_PROFILE_MATRIX.md
├─ DOCUMENTATION_GUARDRAILS.md
├─ TESTING_GUARDRAILS.md
├─ OPERATIONS_RELEASE_GUARDRAILS.md
├─ ACCESSIBILITY_GUARDRAILS.md
├─ 01_DESIGN_SPAWN_REVIEW_PROMPT.txt
├─ 02_DESIGN_REVIEW_PROMPT.txt
├─ 01_REFACTORING_SPAWN_REVIEW_PROMPT.txt
├─ 02_REFACTORING_REVIEW_PROMPT.txt
├─ 01_SECURITY_SPAWN_REVIEW_PROMPT.txt
├─ 02_SECURITY_REVIEW_PROMPT.txt
├─ 01_DOCUMENTATION_SPAWN_REVIEW_PROMPT.txt
├─ 02_DOCUMENTATION_REVIEW_PROMPT.txt
├─ 01_TESTING_SPAWN_REVIEW_PROMPT.txt
├─ 02_TESTING_REVIEW_PROMPT.txt
├─ 01_OPERATIONS_RELEASE_SPAWN_REVIEW_PROMPT.txt
├─ 02_OPERATIONS_RELEASE_REVIEW_PROMPT.txt
├─ 01_ACCESSIBILITY_SPAWN_REVIEW_PROMPT.txt
└─ 02_ACCESSIBILITY_REVIEW_PROMPT.txt
```

---

## Design-Prinzip dieser Sammlung

Diese Sammlung folgt ein paar bewussten Regeln:

### 1. Nicht alles ist immer nötig
Die Guardrails sollen helfen, **gezielt** bessere Entscheidungen zu treffen, nicht jede App künstlich aufblasen.

### 2. Review vor Umsetzung
Erst prüfen, dann schneiden. Das gilt für Design genauso wie für Security oder Refactoring.

### 3. Risiko vor Dogma
Nicht jede App braucht Enterprise-Security, vollständige E2E-Abdeckung oder schwere Betriebsprozesse.

### 4. Keine KI-Texttapete
Dokumentation, Tests, Security-Härtung und Accessibility sollen konkret, nachvollziehbar und umsetzbar bleiben.

### 5. Codex braucht klare Zuständigkeiten
Die Guardrails definieren, **was** ein Bereich leisten soll. Die `01_`- und `02_`-Prompts definieren, **wie** der jeweilige Pass ablaufen soll.

---

## Für wen das gedacht ist

Diese Sammlung ist besonders nützlich für:

- Einzelentwickler und kleine Teams
- Leute, die mit Codex oder Claude produktiv bauen
- Apps mit wachsender Komplexität
- Produkte, bei denen «läuft irgendwie» nicht reicht
- Projekte, die sauberer werden sollen, ohne in Prozessbürokratie zu kippen

---

## Was diese Sammlung nicht ist

Dieses Repository ist:

- **kein Framework**
- **keine Design-Library**
- **keine Security-Zertifizierung**
- **kein Ersatz für menschliches Urteilsvermögen**
- **keine Aufforderung, immer alle Bereiche gleichzeitig auszuführen**

Es ist ein Set aus wiederverwendbaren **Arbeitsregeln und Review-Schablonen**.

---

## Empfehlungen für ein öffentliches Repo

Wenn du dieses Repository öffentlich machst, sind zusätzlich sinnvoll:

- `LICENSE`
- `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md` nur falls du aktiv Community-Beiträge erwartest
- `examples/` mit ein paar echten Prompt-Kombinationen
- `templates/` für projektbezogene Varianten
- `CHANGELOG.md`, falls sich die Guardrails aktiv weiterentwickeln

---

## Empfohlener Repository-Name

**Empfehlung:** `codex-quality-guardrails`

Warum dieser Name gut funktioniert:

- breit genug für Design, Security, Refactoring, Testing, Documentation, Operations und Accessibility
- klar verständlich
- direkt auf Codex bezogen
- nicht zu eng auf nur einen Bereich reduziert
- als öffentliches Repo gut lesbar

Weitere brauchbare Alternativen wären:

- `codex-review-guardrails`
- `codex-shipping-guardrails`
- `agent-quality-guardrails`

Wenn der Fokus bewusst nicht nur auf Codex liegen soll, wäre `agent-quality-guardrails` die neutralere Variante.

---

## Praktischer Start

Wenn du nicht weisst, womit du anfangen sollst, nimm diesen Minimal-Workflow:

1. Design  
2. Refactoring  
3. Security  
4. Testing  
5. Documentation  

Und ergänze danach je nach Projekt:

- Operations / Release für produktive Systeme
- Accessibility für öffentliche oder UI-kritische Produkte

---

## Lizenz und Nutzung

Du kannst diese Guardrails direkt in eigene Projekte kopieren, anpassen und kombinieren.
Für ein öffentliches Repository ist eine einfache, permissive Lizenz meist am praktikabelsten.

Typische Optionen:
- MIT
- Apache-2.0

---

## Hinweis

Die Guardrails sind absichtlich **pragmatisch** geschrieben.
Sie sollen reale Qualität erhöhen, nicht künstlich Komplexität erzeugen.

Wenn du sie nutzt, nutze sie nicht als Dogma, sondern als saubere Grundlage für bessere Urteile.
