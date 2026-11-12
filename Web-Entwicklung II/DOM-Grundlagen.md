---
tags:
  - webentwicklung2
  - javascript
  - dom
  - fh-campus02
---

# Webentwicklung 2 – DOM-Grundlagen

## 1. Was ist das DOM?

**DOM** steht für **Document Object Model**.

- Das DOM ist eine Schnittstelle, mit der JavaScript die HTML-Struktur einer Webseite ansprechen und verändern kann.
- HTML-Elemente werden als Baumstruktur aus Knoten (Nodes) dargestellt.
- Das DOM ist wie ein Bauplan: Es beschreibt, wie die Elemente miteinander verbunden sind.
- JavaScript kann Inhalte verändern, ohne die gesamte Seite neu laden zu müssen.

### Wozu braucht man das DOM?

Mit dem DOM kann man:
- einzelne HTML-Elemente auswählen und deren Werte auslesen,
- vorhandene Elemente verändern,
- neue Elemente an beliebigen Stellen einfügen,
- auf Benutzeraktionen reagieren.

Zwei wichtige Browser-Objekte:

| Objekt | Bedeutung |
|---|---|
| `document` | Zugriff auf das HTML-Dokument und seine Elemente |
| `window` | Zugriff auf das Browserfenster und die Browserumgebung |

## 2. XML und Baumstruktur

XML = **Extensible Markup Language**. Es wird verwendet, wenn Informationen strukturiert verarbeitet, ausgetauscht oder gespeichert werden müssen.

### Wann ist XML wohlgeformt?

- Es gibt genau ein Wurzelelement.
- Alle Elemente besitzen Start- und End-Tags.
- XML ist case-sensitive.
- Elemente sind korrekt und paarig verschachtelt.
- Ein Element darf nicht mehrere gleichnamige Attribute besitzen.
- Attributwerte stehen in Anführungszeichen.

XML und HTML können als Baumstruktur dargestellt werden. Ein Baum besteht aus Knoten (Nodes), zum Beispiel Element-, Attribut- und Textknoten. In den Unterlagen werden insgesamt sieben Node-Typen erwähnt.

### Beispiel einer HTML-Baumstruktur

HTML:

```html
<html>
    <head>
        <title>Seitentitel</title>
    </head>
    <body>
        <h1>Überschrift</h1>
        <a href="https://example.com">Text</a>
    </body>
</html>
```

Vereinfachtes Modell:

```text
document
└── html
    ├── head
    │   └── title
    │       └── Text: Seitentitel
    └── body
        ├── h1
        │   └── Text: Überschrift
        └── a
            ├── Attribut: href
            └── Text: Text
```

## 3. DOM-Selektoren

Selektoren sind Methoden, mit denen gezielt HTML-Elemente ausgewählt werden. Erst nach der Auswahl kann man das Element verändern.

### `getElementById()`

Wählt ein einzelnes Element über seine eindeutige ID aus.

```javascript
let element = document.getElementById("meineId");
```

- IDs sollen innerhalb einer Seite eindeutig sein.
- Gibt ein einzelnes Element zurück.

### `getElementsByClassName()`

Wählt alle Elemente mit einer bestimmten Klasse aus.

```javascript
let elemente = document.getElementsByClassName("meineKlasse");
```

- Gibt eine `HTMLCollection` zurück.
- Mehrere Elemente können dieselbe Klasse besitzen.

### `getElementsByTagName()`

Wählt alle Elemente eines bestimmten HTML-Tags aus.

```javascript
let divs = document.getElementsByTagName("div");
```

- Gibt eine `HTMLCollection` zurück.

### `querySelector()`

Wählt das erste Element aus, das einem CSS-Selektor entspricht.

```javascript
let element = document.querySelector(".meineKlasse");
let titel = document.querySelector("#titel");
let absatz = document.querySelector("p");
```

- Unterstützt IDs, Klassen, Tags und komplexere CSS-Selektoren.
- Gibt nur das erste passende Element zurück.

### `querySelectorAll()`

Wählt alle Elemente aus, die einem CSS-Selektor entsprechen.

```javascript
let elemente = document.querySelectorAll("div.meineKlasse");
```

- Gibt eine `NodeList` zurück.

### Vergleich

| Methode | Auswahl | Rückgabe |
|---|---|---|
| `getElementById()` | Eine ID | Einzelnes Element |
| `getElementsByClassName()` | Alle Elemente einer Klasse | `HTMLCollection` |
| `getElementsByTagName()` | Alle Elemente eines Tags | `HTMLCollection` |
| `querySelector()` | Erster Treffer eines CSS-Selektors | Einzelnes Element |
| `querySelectorAll()` | Alle Treffer eines CSS-Selektors | `NodeList` |

**Merke:** Für den Zugriff auf genau ein Element mit bekannter ID eignet sich `getElementById()`.

## 4. Einstiegspunkt und Manipulation

### `document`

`document` ist das globale Objekt, das das gesamte HTML-Dokument repräsentiert. Es ist der Einstiegspunkt, um Elemente im DOM zu finden.

### Ein ausgewähltes `element`

Nachdem ein Element gefunden wurde, kann es verändert werden.

Drei häufige Möglichkeiten:

```javascript
element.innerHTML = "<strong>Neuer Inhalt</strong>";
element.style.color = "red";
element.addEventListener("click", function () {
    console.log("Geklickt!");
});
```

- `innerHTML`: liest oder schreibt den HTML-Inhalt eines Elements.
- `style`: liest oder schreibt Inline-CSS-Eigenschaften.
- `addEventListener()`: registriert einen Event-Listener.

## 5. `onclick` im HTML vs. `addEventListener()` in JavaScript

### `onclick`-Attribut

```html
<button onclick="alert('Button geklickt!')">
    Klick mich!
</button>
```

- JavaScript steht direkt im HTML.
- Schnell und einfach für kleine Beispiele.
- HTML und JavaScript werden vermischt.
- Wartung und Erweiterung werden bei größeren Projekten schwieriger.

### `addEventListener()`

```html
<button id="button1">Klick mich!</button>

<script>
    const button = document.getElementById("button1");

    button.addEventListener("click", function () {
        alert("Button geklickt!");
    });
</script>
```

- Der Event-Handler wird in JavaScript registriert.
- HTML und JavaScript bleiben getrennt.
- Mehrere Listener können für dasselbe Event hinzugefügt werden.
- Listener können mit `removeEventListener()` entfernt werden.
- Flexibler und besser wartbar.

| Kriterium | `onclick` im HTML | `addEventListener()` |
|---|---|---|
| Verwendung | Direkt im HTML-Attribut | In JavaScript |
| Trennung | HTML und JS vermischt | Sauber getrennt |
| Mehrere Listener | Nur ein Handler über das Attribut | Mehrere Listener möglich |
| Entfernen | Nicht auf dieselbe Weise entfernbar | Mit `removeEventListener()` |
| Flexibilität | Weniger flexibel | Flexibler |

**Empfehlung aus den Unterlagen:** Event-Handler mit `addEventListener()` hinzufügen.

## 6. Übung aus den Unterlagen

### Übung 03A – DOM

- Starterpaket aus Moodle herunterladen.
- Aufgaben schrittweise lösen.
- JavaScript kann in den `script`-Tags derselben HTML-Datei stehen; ein eigenes JS-File ist optional.
- Ziel: mit der Funktionsweise des DOM vertraut werden.

### Übung 03B – Events

Alle Event-Handler mit `addEventListener()` hinzufügen.

1. Rechteck erstellen, dessen Farbe sich bei `mouseover` ändert und beim Entfernen der Maus wieder zurückgesetzt wird.
2. Button erstellen: Klick zeigt eine Nachricht; Doppelklick ändert die Nachricht.
3. Textfeld erstellen: Bei Eingabe von `A` oder `a` die Nachricht „Sie haben A getippt!“ anzeigen.
4. Zusatz: Bei Rechtsklick das Standard-Kontextmenü verhindern und stattdessen „Rechtsklick wurde erkannt!“ anzeigen.

## 7. Merksätze

- DOM = Document Object Model.
- Das DOM bildet HTML als Baumstruktur aus Nodes ab.
- `document` ist der Einstiegspunkt in das HTML-Dokument.
- Selektieren ist noch nicht dasselbe wie Manipulieren.
- `querySelector()` liefert den ersten Treffer, `querySelectorAll()` alle Treffer.
- `innerHTML` verändert Inhalt, `style` verändert Inline-CSS.
- `addEventListener()` trennt HTML und JavaScript und ist flexibler als Inline-`onclick`.
