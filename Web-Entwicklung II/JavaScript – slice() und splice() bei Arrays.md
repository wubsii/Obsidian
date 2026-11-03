
## 1. `slice()` – Elemente kopieren

Mit `slice()` kann man einen bestimmten Teil eines Arrays **herauskopieren**, ohne das ursprüngliche Array zu verändern.

### Syntax

```
array.slice(start, end);
```

- `start`: Index, ab dem kopiert wird (inklusive).
    
- `end`: Index, bis zu dem kopiert wird (exklusive – dieses Element wird nicht mehr kopiert).
    
- `end` ist optional. Wird es weggelassen, werden alle Elemente bis zum Ende kopiert.
    

### Beispiel

```
let fruechte = ["Apfel", "Banane", "Kiwi", "Birne"];

let auswahl = fruechte.slice(1, 3);

console.log(auswahl);
// ["Banane", "Kiwi"]

console.log(fruechte);
// ["Apfel", "Banane", "Kiwi", "Birne"]
```

**Erklärung:**

- Index `1` ist `"Banane"`.
    
- Index `3` ist `"Birne"`, wird aber nicht mehr kopiert.
    
- Das Ergebnis enthält deshalb `"Banane"` und `"Kiwi"`.
    
- Das ursprüngliche Array bleibt unverändert.
    

### Weitere Beispiele

```
let zahlen = [10, 20, 30, 40, 50];

zahlen.slice(2);
// [30, 40, 50]

zahlen.slice(0, 2);
// [10, 20]

zahlen.slice(-2);
// [40, 50]
```

Negative Indizes zählen vom Ende des Arrays.

---

## 2. `splice()` – Elemente verändern

Mit `splice()` kann man Elemente aus einem Array **entfernen, ersetzen oder neue Elemente einfügen**.

Im Gegensatz zu `slice()` wird dabei das ursprüngliche Array verändert.

### Syntax

```
array.splice(start, anzahl, element1, element2, ...);
```

- `start`: Index, an dem die Veränderung beginnt.
    
- `anzahl`: Anzahl der Elemente, die entfernt werden sollen.
    
- `element1, element2, ...`: Optionale neue Elemente, die eingefügt werden.
    

### Beispiel 1: Elemente entfernen

```
let fruechte = ["Apfel", "Banane", "Kiwi", "Birne"];

fruechte.splice(1, 2);

console.log(fruechte);
// ["Apfel", "Birne"]
```

**Erklärung:**

- Startindex ist `1` → `"Banane"`.
    
- Es werden `2` Elemente entfernt → `"Banane"` und `"Kiwi"`.
    
- Das ursprüngliche Array wird verändert.
    

### Beispiel 2: Elemente ersetzen

```
let fruechte = ["Apfel", "Banane", "Kiwi"];

fruechte.splice(1, 1, "Orange");

console.log(fruechte);
// ["Apfel", "Orange", "Kiwi"]
```

**Erklärung:**

- Startindex ist `1` → `"Banane"`.
    
- Es wird `1` Element entfernt.
    
- `"Orange"` wird an dieser Stelle eingefügt.
    

### Beispiel 3: Elemente einfügen

```
let fruechte = ["Apfel", "Kiwi"];

fruechte.splice(1, 0, "Banane");

console.log(fruechte);
// ["Apfel", "Banane", "Kiwi"]
```

**Erklärung:**

- Startindex ist `1`.
    
- Es werden `0` Elemente entfernt.
    
- `"Banane"` wird an Index `1` eingefügt.
    
- Die vorhandenen Elemente bleiben erhalten und werden nach hinten verschoben.
    

### Beispiel 4: Elemente am Ende einfügen

```
let zahlen = [10, 20, 30];

zahlen.splice(3, 0, 40, 50);

console.log(zahlen);
// [10, 20, 30, 40, 50]
```

---

## 3. Der wichtigste Unterschied

|Eigenschaft|`slice()`|`splice()`|
|---|---|---|
|Zweck|Elemente kopieren|Elemente entfernen, ersetzen oder einfügen|
|Verändert das Originalarray?|Nein|Ja|
|Rückgabewert|Neues Array mit den ausgewählten Elementen|Array mit den entfernten Elementen|
|Zweiter Parameter|Endindex (exklusive)|Anzahl der zu entfernenden Elemente|

### Merksatz

- `**slice()**` **= ausschneiden und kopieren** – das Original bleibt unverändert.
    
- `**splice()**` **= im Originalarray etwas verändern** – Elemente entfernen, ersetzen oder einfügen.
    

---

## 4. `slice()` und `splice()` im direkten Vergleich

```
let zahlen1 = [10, 20, 30, 40];
let ergebnis1 = zahlen1.slice(1, 3);

console.log(ergebnis1);
// [20, 30]

console.log(zahlen1);
// [10, 20, 30, 40]
```

Hier kopiert `slice()` die Elemente mit den Indizes `1` und `2`. Das Originalarray bleibt gleich.

```
let zahlen2 = [10, 20, 30, 40];
let ergebnis2 = zahlen2.splice(1, 2);

console.log(ergebnis2);
// [20, 30]

console.log(zahlen2);
// [10, 40]
```

Hier entfernt `splice()` zwei Elemente ab Index `1`. Das Ergebnis enthält die entfernten Elemente, während sie im Originalarray nicht mehr vorhanden sind.

---

## 5. Typische Fehler in einer Prüfung

**Fehler 1: Den Endindex bei** `**slice()**` **mitzählen**

```
let zahlen = [10, 20, 30, 40];

console.log(zahlen.slice(1, 3));
// [20, 30]
```

Index `3` wird nicht mitgenommen.

**Fehler 2: Die Parameter bei** `**splice()**` **verwechseln**

```
let zahlen = [10, 20, 30, 40];

zahlen.splice(1, 2);
```

Es werden zwei Elemente ab Index `1` entfernt. Die `2` ist hier **kein Endindex**, sondern die Anzahl der zu entfernenden Elemente.

**Fehler 3: Vergessen, dass** `**splice()**` **das Original verändert**

```
let zahlen = [10, 20, 30];

zahlen.splice(1, 1);

console.log(zahlen);
// [10, 30]
```

Die `20` wurde dauerhaft aus dem Array entfernt.

---

## 6. Mini-Übung

Was wird jeweils ausgegeben?

```
let tiere = ["Hund", "Katze", "Maus", "Pferd"];

console.log(tiere.slice(1, 3));

tiere.splice(1, 2);

console.log(tiere);
```

**Lösung:**

```
// Ausgabe von slice():
["Katze", "Maus"]

// Ausgabe von tiere nach splice():
["Hund", "Pferd"]
```

`slice()` kopiert die Elemente, während `splice()` sie aus dem ursprünglichen Array entfernt.

