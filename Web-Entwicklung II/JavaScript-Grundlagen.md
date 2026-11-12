---
tags:
  - webentwicklung2
  - javascript
  - fh-campus02
---

# Webentwicklung 2 – JavaScript-Grundlagen

## 1. HTML, CSS und JavaScript

| Technologie | Aufgabe |
|---|---|
| **HTML** | Struktur und Inhalt einer Website |
| **CSS** | Design, Layout und Darstellung |
| **JavaScript (JS)** | Verhalten und Logik; reagiert auf Benutzeraktionen und verändert Inhalte |

### HTML-Grundlagen

- HTML = **HyperText Markup Language**
- Standard-Auszeichnungssprache zur Erstellung von Webseiten.
- HTML besteht aus Elementen mit Start-Tag, Inhalt und End-Tag.
- Es gibt auch leere Elemente ohne End-Tag.
- Der Browser liest HTML und zeigt den Inhalt entsprechend an.

Wichtige Elemente:

| Element | Bedeutung |
|---|---|
| `<!DOCTYPE html>` | Kennzeichnet ein HTML5-Dokument |
| `<html>` | Wurzelelement |
| `<head>` | Metainformationen |
| `<title>` | Titel im Browser-Tab |
| `<body>` | Sichtbarer Inhalt |
| `<h1>` | Große Überschrift |
| `<p>` | Absatz |
| `<header>`, `<nav>`, `<section>`, `<footer>` | Semantische Bereiche |

### CSS-Grundlagen

- CSS = **Cascading Style Sheets**
- CSS legt fest, wie HTML-Elemente dargestellt werden.
- Externe Stylesheets ermöglichen es, das Aussehen mehrerer Seiten zentral zu steuern.
- `Cascading`: Eigenschaften können vom Parent-Element auf Child-Elemente vererbt werden.
- CSS trennt Gestaltung vom Inhalt. Das W3C entwickelte CSS, nachdem Formatierungsangaben direkt im HTML die Pflege größerer Websites erschwert hatten.

Eine CSS-Regel besteht aus Selektor und Deklarationsblock:

```css
p {
    color: red;
    text-align: center;
}
```

- `p`: Selektor
- `color` und `text-align`: Properties/Eigenschaften
- `red` und `center`: Values/Werte
- Deklarationen werden mit Semikolons getrennt und stehen in geschweiften Klammern.

Drei Arten, CSS einzubinden:

1. **Inline** – direkt am HTML-Element über `style`.
2. **Internal** – im `<style>`-Bereich des HTML-Dokuments.
3. **External** – in einer eigenen CSS-Datei.

Laut Unterrichtsfolie gilt als Faustregel: Je näher die Formatierung am Element steht, desto höher ihre Priorität.

## 2. JavaScript – Zweck und Geschichte

- JavaScript erweitert Webseiten um dynamische Inhalte und Interaktionen.
- Es kann auf Klicks, Eingaben und andere Benutzeraktionen reagieren.
- Es kann im Browser (clientseitig) und auf dem Server (serverseitig) eingesetzt werden.

### Geschichte

- **1995:** Von Netscape entwickelt; Brendan Eich entwickelte die Sprache zunächst unter dem Namen „LiveScript“.
- Sie wurde in Netscape Navigator 2.0 integriert.
- Ziel war es, Webseiten dynamischer zu machen.
- Der Name wurde aus Marketinggründen in „JavaScript“ geändert. Java und JavaScript sind trotzdem unterschiedliche Programmiersprachen.
- **1997:** Standardisierung durch ECMA als ECMAScript (ECMA-262). Das unterstützt die Kompatibilität zwischen Browsern.

### Frontend, Backend und Fullstack

- **Frontend:** Teil, den Benutzer sehen und mit dem sie interagieren (HTML, CSS, JavaScript).
- **Backend:** Läuft auf dem Server und kümmert sich um Logik, Daten und API-Integration (z. B. Server, Datenbanken, PHP, Java oder JavaScript).
- **Fullstack:** Entwicklung sowohl des Frontends als auch des Backends.

### Java und JavaScript

| JavaScript | Java |
|---|---|
| Dynamisch und schwach typisiert | Statisch typisiert |
| Im Kurs als interpretierte Sprache beschrieben; moderne Engines nutzen JIT | Im Kurs als kompilierte, objektorientierte Sprache beschrieben |
| Häufig für Webentwicklung und DOM-Manipulation | Allgemeine objektorientierte Programmiersprache |

Der ähnliche Name bedeutet nicht, dass Java und JavaScript eng miteinander verwandt sind.

## 3. Interpretierte und kompilierte Sprachen

### Interpretierte Sprache

Der Quellcode wird zur Laufzeit durch einen Interpreter ausgeführt.

**Vorteile**
- Keine separate Kompilierung vor jeder Ausführung notwendig.
- Plattformunabhängigkeit.
- Änderungen lassen sich schnell testen.

**Nachteile**
- Ausführung kann langsamer sein, da während der Laufzeit interpretiert wird.
- Interpreter benötigt zusätzliche Ressourcen.

Beispiele aus den Folien: Python, JavaScript, PHP.

### Kompilierte Sprache

Der Quellcode wird vor der Ausführung durch einen Compiler in Maschinensprache übersetzt.

**Vorteile**
- Schnelle Ausführung, da der Code bereits übersetzt ist.
- Die ausführbare Datei benötigt zur Ausführung keinen Interpreter.

**Nachteile**
- Vor der Ausführung muss kompiliert werden.
- Ausführbare Dateien müssen gegebenenfalls für verschiedene Plattformen separat erstellt werden.

Beispiele aus den Folien: C und C++.

### JavaScript und JIT-Compilation

JavaScript wird nicht einfach nur Zeile für Zeile ausgeführt. Moderne JavaScript-Engines optimieren häufig ausgeführten Code zur Laufzeit:

1. Code wird zunächst ausgeführt.
2. Die Engine erkennt häufig verwendete Codeabschnitte.
3. Diese werden durch **Just-in-Time-Compilation (JIT)** in optimierten Maschinencode übersetzt.
4. Bereits kompilierter Code kann zwischengespeichert und später schneller ausgeführt werden.

Engines aus den Folien:
- Chrome: V8
- Firefox: SpiderMonkey
- Safari: JavaScriptCore
- Node.js verwendet V8 für serverseitiges JavaScript.

**Merke:** JavaScript verbindet die Flexibilität der Laufzeitausführung mit Performance-Optimierungen durch JIT.

## 4. JavaScript ausführen und einbinden

Möglichkeiten zur Ausführung:
- Entwicklerkonsole im Browser (F12)
- Texteditor oder IDE und Browser
- Visual Studio Code mit Node.js
- IntelliJ

In Visual Studio Code:
- Ausführen: `Ctrl + F5`
- Formatieren: `Shift + Alt + F`
- Mehrzeilig kommentieren: `Shift + Alt + A`

Externes JavaScript wird mit `script` eingebunden:

```html
<script src="myScript.js"></script>
```

- Das Script kann im `head` oder `body` stehen.
- Üblich ist die Einbindung am Ende des `body`.
- Ohne `defer` wird das Script beim Laden an dieser Stelle ausgeführt.
- `defer` verschiebt die Ausführung, bis das HTML geparst wurde (bei externen Scripts).

## 5. Typisierung und Variablen

JavaScript ist **dynamisch und schwach typisiert**:
- Variablen benötigen keine explizite Typdeklaration.
- Der Typ ergibt sich aus dem zugewiesenen Wert.
- Die Typprüfung findet zur Laufzeit statt.
- JavaScript kann Werte implizit umwandeln.

Den Typ kann man mit `typeof` abfragen:

```javascript
let alter = 21;
console.log(typeof alter); // "number"
```

### `var`, `let` und `const`

| Schlüsselwort | Bedeutung |
|---|---|
| `var` | Ältere Deklarationsart; Function Scope; erneute Deklaration möglich |
| `let` | Moderne Deklaration; Block Scope; erneute Deklaration im selben Scope nicht möglich |
| `const` | Block Scope; muss bei der Deklaration initialisiert werden; Neuzuweisung nicht möglich |

In neuem Code normalerweise `let` und `const` verwenden. `var` ist vor allem für älteren Code relevant.

```javascript
let alter = 21;
alter = 22; // erlaubt

const name = "Anna";
// name = "Mia"; // Fehler: const kann nicht neu zugewiesen werden
```

### Scope: `let` und `var`

- `let` besitzt **Block Scope**: Die Variable ist auf den Block `{ ... }` beschränkt.
- `var` besitzt **Function Scope**: Ein Block wie `if` oder `for` begrenzt die Variable nicht.
- `var` erlaubt eine erneute Deklaration; `let` nicht im selben Scope.

### Datentypen

Primitive Datentypen:

| Typ | Bedeutung | Beispiel |
|---|---|---|
| `Number` | Ganze und Kommazahlen | `1044`, `10.44` |
| `String` | Text | `"Hallo"` |
| `Boolean` | Wahrheitswert | `true`, `false` |
| `Undefined` | Deklarierte Variable ohne zugewiesenen Wert | `let x;` |
| `Null` | Bewusst kein Wert | `let x = null;` |

Weitere Datentypen:
- **Array:** Liste von Werten, z. B. `[1, 2, 3]`
- **Object:** Zusammengehörige Daten als Schlüssel-Wert-Paare, z. B. `{ name: "Hansi" }`

### `null` vs. `undefined`

```javascript
let meineVar = null;
console.log(meineVar); // null

let deineVar;
console.log(deineVar); // undefined

let person = { name: "Max" };
console.log(person.age); // undefined: Eigenschaft existiert nicht

let person2 = { name: "Max", age: null };
console.log(person2.age); // null: Eigenschaft existiert, hat aber keinen Wert
```

- `undefined`: Es wurde kein Wert zugewiesen oder eine Eigenschaft existiert nicht.
- `null`: Es wurde bewusst „kein Wert“ angegeben.

## 6. Variablen deklarieren und ausgeben

```javascript
let hundName = "Bello";
let hundAlter = 5;

let vorname = "Miriam",
    autoName = "Porsche",
    preis = 200000;

console.log(hundName);
```

- Mehrere Variablen können mit Kommas getrennt deklariert werden.
- Anweisungen enden üblicherweise mit einem Semikolon.
- Eine deklarierte, aber nicht initialisierte `let`-Variable hat den Wert `undefined`.

## 7. Funktionen

Funktionen bündeln wiederverwendbaren Code.

```javascript
function addiere(a, b) {
    return a + b;
}

let ergebnis = addiere(2, 3);
console.log(ergebnis); // 5
```

- `function`: definiert eine Funktion.
- `addiere`: Funktionsname.
- `a` und `b`: Parameter.
- `return`: gibt einen Wert zurück.
- Aufruf über den Funktionsnamen und runde Klammern.

## 8. Vergleichsoperatoren

Wichtig ist der Unterschied zwischen Zuweisung und Vergleich:

| Operator | Bedeutung |
|---|---|
| `=` | Zuweisung |
| `==` | Vergleich mit möglicher Typumwandlung |
| `===` | Strikter Vergleich: Wert und Datentyp müssen übereinstimmen |
| `!=` | Ungleich, mit möglicher Typumwandlung |
| `!==` | Strikt ungleich |

```javascript
let x = 5;       // Zuweisung

console.log(5 == "5");  // true: Typumwandlung
console.log(5 === "5"); // false: number ist nicht string
console.log(0 == false);  // true
console.log(0 === false); // false
```

**Empfehlung:** In der Regel `===` und `!==` verwenden, damit keine unerwartete Typumwandlung stattfindet.

## 9. Browser-Interaktionen

Diese Funktionen sind im Browser verfügbar:

```javascript
alert("Hallo!"); // Meldung anzeigen

let name = prompt("Wie heißt du?"); // Texteingabe

let bestaetigt = confirm("Sind die Angaben richtig?"); // OK/Abbrechen
```

- `alert()`: zeigt eine Meldung.
- `prompt()`: fragt einen Wert als Text ab.
- `confirm()`: liefert `true` oder `false`.

### Achtung: `prompt()` liefert einen String

```javascript
let zahl1 = prompt("Erste Zahl:");
let zahl2 = prompt("Zweite Zahl:");

console.log(zahl1 + zahl2); // z. B. "23" statt 5
```

Eingaben müssen bei Bedarf in Zahlen umgewandelt werden:

```javascript
let zahl1 = Number(prompt("Erste Zahl:"));
let zahl2 = parseInt(prompt("Zweite Zahl:"));

console.log(zahl1 + zahl2);
```

### `parseInt()` und `Number()`

| Eingabe | `parseInt()` | `Number()` |
|---|---:|---:|
| `"123"` | `123` | `123` |
| `"123.45"` | `123` | `123.45` |
| `"123abc"` | `123` | `NaN` |
| `"abc123"` | `NaN` | `NaN` |
| `" 123 "` | `123` | `123` |

`parseInt("101", 2)` interpretiert die Eingabe als Binärzahl und liefert `5`.

## 10. Arrays

Ein Array speichert mehrere Werte in einer geordneten Liste.

```javascript
let arr = [1, 2, 3];

arr.push(4, 5); // Elemente hinten hinzufügen
arr[0] = 7;     // Element am Index 0 ändern

console.log(arr.pop());   // letztes Element entfernen und zurückgeben
console.log(arr.shift()); // erstes Element entfernen und zurückgeben

console.log(arr);
```

Array-Indizes beginnen bei `0`.

### Wichtige Array-Methoden

| Methode | Aufgabe | Ändert Original? | Rückgabe |
|---|---|---|---|
| `slice(start, ende)` | Kopiert einen Ausschnitt; Ende exklusiv | Nein | Neues Array |
| `splice(start, anzahl, ...neueElemente)` | Entfernt, fügt ein oder ersetzt Elemente | Ja | Array der entfernten Elemente |
| `push(element)` | Hängt hinten an | Ja | Neue Länge |
| `pop()` | Entfernt letztes Element | Ja | Entferntes Element |
| `shift()` | Entfernt erstes Element | Ja | Entferntes Element |
| `unshift(element)` | Fügt vorne ein | Ja | Neue Länge |

### `splice()` – Original wird verändert

```javascript
let a = [10, 20, 30, 40];

a.splice(1, 2);     // Entfernt 20 und 30: [10, 40]
a.splice(1, 0, 50); // Fügt 50 bei Index 1 ein: [10, 50, 40]
a.splice(1, 1, 99); // Ersetzt 50 durch 99: [10, 99, 40]
```

Syntax:

```javascript
array.splice(startIndex, anzahlZuEntfernenderElemente, neueElemente);
```

### `slice()` – Original bleibt unverändert

```javascript
let a = [10, 20, 30, 40];

let b = a.slice(1, 3); // [20, 30]
let kopie = a.slice(); // vollständige Kopie
```

Das Ende ist exklusiv: `slice(1, 3)` nimmt Index 1 und 2, aber nicht Index 3.

## 11. Übungsaufgaben aus den Unterlagen

### Übung 00 – Website mit HTML und CSS

Erstellen Sie eine Website mit:
- Navigation mit Links zu Abschnitten
- Home-Bereich mit Titel und Beschreibung
- „Über uns“-Abschnitt
- großem Bild
- Kontaktbereich im Footer
- semantischen Tags wie `header`, `nav`, `section`, `footer`
- zwei externen CSS-Dateien

### Übung 01A – Alter berechnen

- Name mit `prompt()` abfragen.
- Geburtsjahr abfragen.
- Mit `confirm()` bestätigen lassen, ob Name und Alter richtig eingegeben wurden.
- Alter in einer eigenen Funktion berechnen.
- Prüfen, ob die Person mindestens 18 Jahre alt ist.
- Personalisierte Meldung mit `alert()` ausgeben.

### Übung 01B – Rechenprogramm

- Externe Datei `rechenProgramm.js` einbinden.
- Programm über einen Button starten.
- Zwei Zahlen und eine Rechenoperation (`+`, `-`, `*`, `/`) abfragen.
- Für jede Operation eine eigene Funktion mit zwei Parametern erstellen.
- Passende Funktion aufrufen.
- Rechnung und Ergebnis mit `alert()` und `console.log()` ausgeben.
- Bei Eingaben aus `prompt()` an die Umwandlung mit `Number()` oder `parseInt()` denken.

### Übung 02 – Aufgabenverwaltung mit Array

- Leeres Array für Aufgaben erstellen.
- Aufgabe über `prompt()` hinzufügen.
- Alle Aufgaben über `alert()` anzeigen.
- Aufgabe anhand ihrer Position entfernen.
- Buttons zum Hinzufügen, Anzeigen und Entfernen verwenden.
- Erfolgsmeldung ausgeben.
- `splice()` und `slice()` ausprobieren.

## 12. Merksätze

- HTML = Struktur, CSS = Design, JavaScript = Verhalten/Logik.
- Java und JavaScript sind unterschiedliche Sprachen.
- JavaScript ist dynamisch und schwach typisiert.
- `let` ist block-scoped, `var` function-scoped.
- `const` verhindert eine Neuzuweisung.
- `null` bedeutet bewusst kein Wert; `undefined` bedeutet nicht zugewiesen/nicht vorhanden.
- `==` kann Typen umwandeln; `===` vergleicht auch den Typ.
- `prompt()` liefert einen String.
- `slice()` verändert das Original nicht; `splice()` verändert es.
