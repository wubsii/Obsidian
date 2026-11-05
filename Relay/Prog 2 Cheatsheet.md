Here’s the full study summary as a reusable Markdown document:

# **Lernzettel Programmieren 2 (Java)**

## **Vererbung**

Vererbung bedeutet:  
Eine Klasse übernimmt Eigenschaften und Methoden einer anderen Klasse.

```java
class Animal {
    public void eat() {
        System.out.println("isst");
    }
}

class Dog extends Animal {
}
```

`Dog` erbt von `Animal`.

---

## **Wichtige Begriffe**

|**Begriff**|**Bedeutung**|
|---|---|
|Basisklasse|Oberklasse / Superklasse|
|abgeleitete Klasse|Unterklasse / Subklasse|
|extends|Schlüsselwort für Vererbung|
|IS-A Beziehung|Ein Beagle IST EIN Hund|

---

## **Keine Mehrfachvererbung in Java**

Java erlaubt nur:

```java
class Dog extends Animal
```

NICHT:

```java
class Dog extends Animal, Pet
```

Aber:  
Eine Klasse kann mehrere Interfaces implementieren.

---

# **final**

## **final bei Variablen**

Wert darf nicht mehr geändert werden.

```java
final int age = 5;
```

---

## **final bei Methoden**

Methode darf nicht überschrieben werden.

```java
public final void print() {
}
```

---

## **final bei Klassen**

Von der Klasse darf nicht geerbt werden.

```java
public final class Dog {
}
```

---

# **Konstruktor + super()**

In einer Subklasse wird automatisch zuerst der Konstruktor der Oberklasse aufgerufen.

```java
super();
```

Wenn die Oberklasse keinen Default-Konstruktor hat, muss explizit ein passender `super(...)` Aufruf gemacht werden.

---

# **Polymorphismus**

„Vielgestaltigkeit“

Arten:

- impliziter Polymorphismus
- überladener Polymorphismus
- parametrisierter Polymorphismus
- Subtyp-Polymorphismus

---

## **Impliziter Polymorphismus**

Automatische Typumwandlung.

```java
3 + 2.0
```

oder Upcasting:

```java
Object o = new String("abc");
```

---

## **Überladener Polymorphismus**

Method Overloading:

```java
doSomething(int x)
doSomething(int x, int y)
```

---

## **Parametrisierter Polymorphismus**

Generics.

```java
ArrayList<String>
ArrayList<Integer>
```

---

## **Subtyp-Polymorphismus**

```java
Animal a = new Dog();
```

Variable ist `Animal`,  
Objekt ist `Dog`.

Aufgerufen wird immer die speziellste überschriebene Methode des echten Objekts.

---

# **Upcasting**

```java
Dog d = new Beagle();
```

Spezielle Klasse → allgemeinere Klasse.

Automatisch erlaubt.

---

# **Downcasting**

```java
Beagle b = (Beagle)d;
```

Allgemeiner Typ → spezieller Typ.

Nur explizit möglich.

Gefährlich:  
Kann Runtime Error verursachen (`ClassCastException`).

---

# **Klasse Object**

Alle Klassen erben indirekt von `Object`.

Wichtige Methoden:

```java
toString()
equals()
hashCode()
```

---

# **Abstrakte Klassen**

```java
abstract class Animal
```

Von abstrakten Klassen können KEINE Objekte erzeugt werden.

  

NICHT erlaubt:

```java
Animal a = new Animal();
```

Aber:

```java
Animal a = new Dog();
```

funktioniert.

---

# **Abstrakte Methoden**

```java
public abstract void makeNoise();
```

- keine Implementierung
- kein Methodenrumpf
- MUSS in Subklassen überschrieben werden

---

# **Interfaces**

Ein Interface beschreibt nur Funktionalität.

```java
interface Flyable {
    void fly();
}
```

Eigenschaften:

- Methoden automatisch `public abstract`
- Attribute automatisch `public static final`

---

## **implements**

```java
class Bird implements Flyable
```

Eine Klasse kann:

- nur 1 Klasse erben
- aber mehrere Interfaces implementieren

---

# **Unterschied abstrakte Klasse vs Interface**

|**Abstrakte Klasse**|**Interface**|
|---|---|
|kann Attribute besitzen|nur Konstanten|
|kann Methoden mit Code haben|nur abstrakte Methoden|
|Vererbung mit extends|Implementierung mit implements|
|nur einfache Vererbung|mehrere Interfaces möglich|

---

# **instanceof**

Prüft Typ eines Objekts.

```java
if(obj instanceof Dog)
```

---

# **getClass()**

Prüft exakte Klasse.

```java
obj.getClass().equals(Dog.class)
```

---

# **Comparable**

Definiert natürliche Sortierung.

```java
class Person implements Comparable<Person>
```

Methode:

```java
compareTo(Person o)
```

---

## **compareTo Rückgabewerte**

|**Wert**|**Bedeutung**|
|---|---|
|< 0|this vorher|
|> 0|this nachher|
|0|gleich|

---

## **Sortieren**

```java
Collections.sort(list);
```

oder

```java
Arrays.sort(array);
```

---

# **Comparator**

Für alternative Sortierungen.

```java
class NameComparator implements Comparator<Person>
```

Methode:

```java
compare(o1, o2)
```

---

# **Wann Comparable vs Comparator?**

## **Comparable**

- natürliche Standardsortierung
- direkt in Klasse definiert

## **Comparator**

- mehrere Sortierungen möglich
- externe Vergleichsklasse

---

# **Testen**

Warum testen?

- Fehler früh finden
- automatische Überprüfung
- wichtig bei großen Projekten

---

# **Wichtige Begriffe**

|**Begriff**|**Bedeutung**|
|---|---|
|Error|menschlicher Fehler|
|Defect|Fehler im Code|
|Failure|sichtbarer Fehler beim Ausführen|

---

# **Dynamisches Binden**

```java
Person p = new Student();
p.getInfo();
```

Es wird `Student.getInfo()` aufgerufen, nicht `Person.getInfo()`.

Das ist der Kern von Subtyp-Polymorphismus.

---

# **Typische Prüfungsfragen**

- Unterschied Interface vs abstrakte Klasse?
- Unterschied Comparable vs Comparator?
- Was ist Polymorphismus?
- Unterschied Upcasting / Downcasting?
- Warum ist Downcasting gefährlich?
- Was macht `final`?
- Was macht `instanceof`?
- Warum braucht Comparable `compareTo()`?
- Was bedeutet natürliche Ordnung?
- Warum gibt es keine Mehrfachvererbung in Java?

---

# **Besonders wichtige Themen**

1. Vererbung
2. Polymorphismus
3. abstract vs interface
4. Comparable vs Comparator
5. Casting
6. Collections.sort vs Arrays.sort