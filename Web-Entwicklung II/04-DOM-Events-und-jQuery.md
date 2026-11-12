---
tags:
  - webentwicklung2
  - javascript
  - dom
  - events
  - fh-campus02
---

# Webentwicklung 2 – DOM-Events, jQuery und Event Propagation

## 1. DOM-Events

DOM-Events treten auf, wenn Benutzer mit einer Website interagieren oder Ereignisse im Browser stattfinden.

Beispiele: Mausklick, Tastatureingabe oder Scrollen.

### Event-Kategorien

| Kategorie | Wann tritt das Event auf? |
|---|---|
| Maus-Events | Benutzer verwendet die Maus |
| Tastatur-Events | Benutzer gibt etwas über die Tastatur ein |
| Formular-Events | Benutzer interagiert mit Formularen |
| Fenster-Events | Aktionen im Browserfenster |
| Clipboard-Events | Text wird kopiert, ausgeschnitten oder eingefügt |
| Drag-and-Drop-Events | Etwas wird per Drag-and-Drop verschoben |
| Touch-Events | Interaktion über Touchscreens |
| Multimedia-Events | Audio- und Videoereignisse |

### Übung 04 – Neue Events recherchieren

1. Neue Events aus den Kategorien Maus, Tastatur und Fenster recherchieren.
2. Für je ein neues Event eine Einsatzmöglichkeit überlegen.
3. Die Events im eigenen Programm einsetzen.

## 2. DOM vs. jQuery

### Was ist jQuery?

jQuery ist eine JavaScript-Bibliothek, die eine kompaktere Syntax für die Arbeit mit DOM-Elementen anbietet.

Vorteile aus den Unterlagen:
- Einfachere und kürzere Syntax.
- Früher weniger Probleme mit Browser-Kompatibilität.
- Zusätzliche Funktionen, z. B. AJAX, Animationen und Effekte.

Nachteile:
- Muss als zusätzliche Bibliothek eingebunden werden.
- In modernen Browsern sind viele benötigte Funktionen bereits nativ vorhanden.
- Kann durch die zusätzliche Bibliothek etwas langsamer sein.

### jQuery-Beispiele und DOM-Entsprechungen

Elemente auswählen:

```javascript
// jQuery
$("div");

// DOM
document.querySelectorAll("div");
```

HTML ändern:

```javascript
// jQuery
$("#element").html("Neuer Text");

// DOM
document.getElementById("element").innerHTML = "Neuer Text";
```

Event hinzufügen:

```javascript
// jQuery
$("#button").click(function () {
    alert("Geklickt!");
});

// DOM
document.getElementById("button").addEventListener("click", function () {
    alert("Geklickt!");
});
```

CSS ändern:

```javascript
// jQuery
$("#element").css("color", "red");

// DOM
document.getElementById("element").style.color = "red";
```

### Vergleich

| Kriterium | DOM | jQuery |
|---|---|---|
| Verwendung | Direkt mit JavaScript | Über Bibliothek und `$()` |
| Syntax | Teilweise länger | Kürzer |
| Browser-Kompatibilität | Früher teilweise problematisch | Behandelte ältere Unterschiede |
| Zusatzfunktionen | Grundlegende DOM-Manipulation und Events | z. B. Animationen, AJAX, Effekte |
| Performance | Nativ, keine zusätzliche Bibliothek | Zusätzlicher Bibliotheksaufwand |
| Heute | Moderner Standard | Weniger verbreitet als früher |

**Merke:** In modernen Browsern reicht das native DOM für viele Aufgaben aus.

## 3. Dynamische DOM-Manipulation

Bei dynamischer Manipulation werden HTML-Elemente mit JavaScript erzeugt, verändert oder entfernt, statt sie direkt in HTML einzutragen.

### Übung 5 – Dynamische Manipulation

Erweitern Sie eine Seite ausschließlich mit DOM/JavaScript:

1. Neue `<section>` mit `<h2>` und `<p>` erstellen.
2. Eine `<ul>` mit drei dynamisch erzeugten `<li>`-Elementen erstellen.
3. Button hinzufügen, der bei jedem Klick ein neues Listenelement einfügt.
4. Ein Bild dynamisch mit JavaScript hinzufügen.
5. Den Text eines vorhandenen Elements ändern.
6. Bonus: Button erstellen, der das erste Listenelement entfernt. Wenn keine Elemente mehr vorhanden sind, Meldung ausgeben.
7. Bonus: CSS-Klassen oder Inline-Stile über JavaScript hinzufügen.

Beispiel für das Erzeugen und Einfügen eines Elements:

```javascript
const liste = document.getElementById("todoList");

const eintrag = document.createElement("li");
eintrag.textContent = "Neue Aufgabe";

liste.appendChild(eintrag);
```

Beispiel für das Entfernen des ersten Elements:

```javascript
if (liste.firstElementChild) {
    liste.firstElementChild.remove();
} else {
    console.log("Keine Listenelemente mehr vorhanden!");
}
```

## 4. Event Propagation: Capturing, Target und Bubbling

Ein DOM-Event durchläuft mehrere Phasen:

1. **Capturing Phase:** Das Event bewegt sich von der Wurzel des Dokuments durch die DOM-Hierarchie nach unten.
2. **Target Phase:** Das Event erreicht das eigentliche Ziel-Element.
3. **Bubbling Phase:** Das Event bewegt sich vom Ziel-Element wieder nach oben durch die DOM-Hierarchie.

Vereinfachtes Beispiel:

```text
document
└── div
    └── span
        └── button  ← Klickziel
```

## 5. Event Capturing

Beim **Capturing** bewegt sich das Event vom Ursprung (z. B. `document`) hinunter zum Ziel-Element.

Reihenfolge beim Beispiel:

```text
document → div → span → button
```

- Event-Handling wird auf dem Weg von den Eltern-Elementen zum Ziel ausgeführt.
- Capturing wird auch „Trickling“ genannt.
- In der Praxis wird Capturing laut Unterlagen eher selten verwendet.
- Es kann sinnvoll sein, ein Event bereits auf einer höheren Ebene abzufangen.

Capturing kann beim Registrieren eines Listeners mit der dritten Option aktiviert werden:

```javascript
element.addEventListener("click", handler, true);
```

## 6. Event Bubbling

Beim **Bubbling** wird das Event zuerst am Ziel-Element ausgelöst und wandert danach zu den Eltern-Elementen hinauf.

Reihenfolge beim Beispiel:

```text
button → span → div → document
```

Vorteile:
- Ein Listener auf einem übergeordneten Element kann Events mehrerer untergeordneter Elemente behandeln.
- Besonders nützlich für **Event Delegation**.
- Hilfreich bei dynamisch hinzugefügten Elementen.

Bubbling ist bei vielen Events das Standardverhalten.

## 7. `event.stopPropagation()`

Mit `event.stopPropagation()` wird verhindert, dass ein Event weiter durch die DOM-Hierarchie propagiert.

```javascript
button.addEventListener("click", function (event) {
    event.stopPropagation();
});
```

- Wirkt abhängig davon, in welcher Phase und auf welchem Element es aufgerufen wird.
- Kann sowohl beim Bubbling als auch beim Capturing die Weitergabe stoppen.

## 8. Bubbling vs. Capturing

| Capturing | Bubbling |
|---|---|
| Von außen nach innen | Von innen nach außen |
| Wurzel → Ziel | Ziel → Wurzel |
| Wird seltener verwendet | Häufiger verwendet |
| Kann beim Registrieren mit `true` aktiviert werden | Standard bei vielen Events |

**Stop Propagation:** Verhindert, dass das Event weitergegeben wird.

## 9. Event Delegation

**Event Delegation** bedeutet, dass ein Event-Listener auf einem übergeordneten Element sitzt und Events von untergeordneten Elementen verarbeitet.

Beispiel: Eine To-Do-Liste enthält viele `<li>`-Elemente. Statt jedem `<li>` einen eigenen Listener zu geben, wird ein Listener auf dem übergeordneten `<ul>` registriert.

```html
<ul id="todoList">
    <li>Aufgabe 1</li>
    <li>Aufgabe 2</li>
</ul>

<script>
    const todoList = document.getElementById("todoList");

    todoList.addEventListener("click", function (event) {
        if (event.target.tagName === "LI") {
            console.log("Du hast auf: " + event.target.textContent + " geklickt");
        }
    });
</script>
```

### Ablauf

1. Benutzer klickt auf ein `<li>`.
2. Das Event wird am `<li>` ausgelöst.
3. Durch Bubbling wandert es zum übergeordneten `<ul>`.
4. Der Listener auf dem `<ul>` wird ausgeführt.
5. `event.target` zeigt, welches Element ursprünglich angeklickt wurde.
6. Über `event.target` kann das konkrete Listenelement angesprochen werden.

### Vorteile

- Weniger Event-Listener notwendig.
- Neue, dynamisch hinzugefügte Elemente funktionieren ebenfalls.
- Event-Behandlung wird zentralisiert.
- Besonders praktisch bei großen Listen oder vielen untergeordneten Elementen.

### Übung 6 – Event Delegation und Bubbling

1. Die Liste aus Übung 5 erweitern.
2. Event-Handler auf einem übergeordneten Element, z. B. dem `<ul>`, registrieren.
3. Klicks auf `<li>`-Elemente über Event Delegation abfangen.
4. Mit `event.target` feststellen, welches `<li>` angeklickt wurde.
5. Das angeklickte Element zuerst in der Konsole ausgeben und danach löschen.
6. Ein eigenes Szenario entwickeln, bei dem Bubbling gestoppt wird.
7. Ein eigenes Szenario entwickeln, bei dem Capturing gestoppt wird.
8. Vorgehensweise demonstrieren und erklären.

## 10. Merksätze

- Events entstehen durch Benutzerinteraktionen oder Browserereignisse.
- Capturing: von der Wurzel zum Ziel.
- Target: das Event erreicht das Ziel-Element.
- Bubbling: vom Ziel zurück zur Wurzel.
- `event.stopPropagation()` stoppt die Weitergabe.
- Event Delegation nutzt Bubbling und einen Listener auf einem übergeordneten Element.
- `event.target` bezeichnet das Element, auf dem das Event ursprünglich ausgelöst wurde.
