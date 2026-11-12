---
tags:
  - webentwicklung2
  - javascript
  - json
  - fh-campus02
---

# Webentwicklung 2 – JSON

## 1. Was ist JSON?

**JSON** steht für **JavaScript Object Notation**.

- JSON ist ein leichtgewichtiges Datenformat zum Datenaustausch.
- Es basiert auf einer an JavaScript angelehnten Syntax mit Schlüssel-Wert-Paaren.
- Es wird häufig zum Datenaustausch zwischen Client und Server in Webanwendungen verwendet.
- APIs liefern Daten, beispielsweise Benutzerprofile oder Produktdetails, oft im JSON-Format zurück.

## 2. Warum verwendet man JSON?

- **Lesbarkeit:** Für Menschen und Maschinen gut lesbar.
- **Einfachheit:** Einfache Struktur, die leicht geparst werden kann.
- **Selbstbeschreibend:** Schlüssel beschreiben, wofür Werte stehen.
- **Plattformunabhängig:** Kann in vielen Programmiersprachen verwendet werden, z. B. JavaScript, Python, Java und C#.
- **Leichtgewichtig:** Im Vergleich zu XML weniger umfangreich verpackt und dadurch oft schneller zu übertragen und zu verarbeiten.

## 3. Aufbau und Syntaxregeln

Ein JSON-Objekt steht in geschweiften Klammern `{ }`. Es enthält Schlüssel-Wert-Paare.

```json
{
    "name": "Max",
    "alter": 30
}
```

Wichtige Regeln:

1. Schlüssel müssen in **doppelten Anführungszeichen** stehen.
2. Strings stehen in doppelten Anführungszeichen.
3. Zahlen stehen ohne Anführungszeichen.
4. Boolean-Werte sind `true` oder `false`.
5. Ein leerer bzw. fehlender Wert kann als `null` angegeben werden.
6. Arrays stehen in eckigen Klammern `[ ]`.
7. Objekte stehen in geschweiften Klammern `{ }`.
8. Kommas trennen Schlüssel-Wert-Paare und Array-Elemente.
9. Nach dem letzten Element steht kein zusätzliches Komma.

### JSON-Datentypen

| Datentyp | Beispiel |
|---|---|
| String | `"Max Mustermann"` |
| Number | `30`, `4.65`, `-12.13` |
| Boolean | `true`, `false` |
| Null | `null` |
| Array | `["Anna", "Ben", "Clara"]` |
| Objekt | `{ "name": "Max" }` |

## 4. Objekte und Arrays

### Objekt

Ein Objekt enthält Schlüssel-Wert-Paare:

```json
{
    "name": "Marlene Musterfrau",
    "alter": 30
}
```

### Array

Ein Array enthält eine Liste von Werten:

```json
{
    "studenten": ["Anna", "Ben", "Clara"]
}
```

### Verschachtelte Objekte und Arrays

JSON kann Objekte und Arrays miteinander kombinieren:

```json
{
    "isActiveWorker": true,
    "minHeight": 1.6,
    "employees": [
        {
            "firstName": "John",
            "lastName": "Doe"
        },
        {
            "firstName": "Anna",
            "lastName": "Smith"
        },
        {
            "firstName": "Peter",
            "lastName": "Jones"
        }
    ]
}
```

Hier enthält das Objekt `employees` ein Array mit drei Einträgen. Jeder Eintrag ist ein eigenes Objekt mit Vor- und Nachnamen.

## 5. JSON bei APIs

RESTful APIs verwenden JSON häufig als Standardformat, um Daten zu senden und zu empfangen.

Beispiel einer möglichen API-Antwort:

```json
{
    "userId": 1,
    "id": 102,
    "title": "Einführung in JSON",
    "completed": true
}
```

Das könnte beispielsweise eine Antwort einer To-Do-App-API sein.

## 6. JSON in JavaScript verwenden

JSON ist ein Textformat. JavaScript kann JSON-Text in ein JavaScript-Objekt umwandeln und umgekehrt.

### `JSON.parse()` – JSON-Text in JS-Objekt umwandeln

```javascript
const jsonString = '{"name": "Max", "age": 30}';

const user = JSON.parse(jsonString);

console.log(user.name); // Max
```

- `JSON.parse()` nimmt einen JSON-String entgegen.
- Rückgabe ist ein JavaScript-Wert bzw. Objekt.
- Danach kann man auf Eigenschaften zugreifen, z. B. `user.name`.

### `JSON.stringify()` – JS-Objekt in JSON-Text umwandeln

```javascript
const user = {
    name: "Max",
    age: 30
};

const jsonString = JSON.stringify(user);

console.log(jsonString);
// {"name":"Max","age":30}
```

- `JSON.stringify()` wandelt einen JavaScript-Wert in einen JSON-String um.
- Praktisch, wenn Daten als JSON übertragen oder ausgegeben werden sollen.

### Unterschied

| Methode | Richtung |
|---|---|
| `JSON.parse()` | JSON-String → JavaScript-Objekt |
| `JSON.stringify()` | JavaScript-Objekt → JSON-String |

**Merke:** JSON ähnelt der JavaScript-Objekt-Syntax, ist aber strenger. Beispielsweise müssen JSON-Schlüssel und Strings doppelte Anführungszeichen verwenden.

## 7. Übungsaufgaben aus den Unterlagen

### Übung 01A – Text in JSON abbilden

Gegeben ist eine Person mit folgenden Informationen:

- Name: Anna
- Alter: 35
- Sprachen: Deutsch und Englisch
- Adresse: Hauptstraße 114, 8401 Kalsdorf bei Graz
- Fahrzeuge:
  - BMW – Motorrad
  - Tesla – Auto
  - KTM – Fahrrad
- Beste Freunde: Max, Nadine und Tanja

Eine mögliche JSON-Struktur:

```json
{
    "name": "Anna",
    "alter": 35,
    "sprachen": ["German", "English"],
    "adresse": {
        "strasse": "Hauptstraße 114",
        "stadt": "Kalsdorf bei Graz",
        "plz": 8401
    },
    "vehicles": [
        {
            "type": "Motorrad",
            "marke": "BMW"
        },
        {
            "type": "Auto",
            "marke": "Tesla"
        },
        {
            "type": "Fahrrad",
            "marke": "KTM"
        }
    ],
    "bestFriends": ["Max", "Nadine", "Tanja"]
}
```

### Übung 01B – JSON parsen und ausgeben

1. Das JSON-Objekt mit `JSON.parse()` in ein JavaScript-Objekt umwandeln.
2. Alle Informationen auf einer HTML-Seite ausgeben:
   - einmal im JSON-Format,
   - einmal als normale HTML-Ausgabe.

Beispiel:

```javascript
let person = JSON.parse('{"name":"Anna","alter":35}');
console.log(person.name);
```

### Übung 02 – To-Do-Liste

Gegebenes JSON:

```json
{
    "todoList": [
        { "id": 1, "todo": "Milch kaufen" },
        { "id": 2, "todo": "Brot kaufen" },
        { "id": 3, "todo": "Für Prüfung lernen" }
    ]
}
```

Aufgaben:

1. JSON mit `JSON.parse()` in ein JS-Objekt namens `todoListe` umwandeln.
2. Nur das zweite Objekt (ID = 2) in der Konsole ausgeben.
3. Über einen Button eine neue Aufgabe hinzufügen.
4. Ein Element gezielt anhand seiner ID löschen.
5. Die Liste mit `JSON.stringify()` im JSON-Format in der Konsole ausgeben.

## 8. Merksätze

- JSON = JavaScript Object Notation.
- JSON ist ein Textformat für den Datenaustausch.
- Objekte verwenden `{ }`, Arrays verwenden `[ ]`.
- JSON-Schlüssel und Strings benötigen doppelte Anführungszeichen.
- `JSON.parse()` wandelt JSON-Text in einen JS-Wert um.
- `JSON.stringify()` wandelt einen JS-Wert in JSON-Text um.
