**Kategorie:** Strukturmuster (Structural Pattern)

## Was ist das Decorator Pattern?

Das Decorator Pattern erweitert ein Objekt dynamisch um zusätzliche Funktionalität, ohne die ursprüngliche Klasse verändern zu müssen.

Ein Decorator umhüllt ein anderes Objekt und besitzt denselben Supertyp wie das Objekt, das er erweitert.

## Welches Problem löst es?

In einem Kaffeehaus gibt es Kaffee mit verschiedenen Extras:

- Milch
- Sojamilch
- Sirup
- Milchschaum

Ohne Decorator müsste man viele Klassen für sämtliche Kombinationen erstellen, zum Beispiel `KaffeeMitMilch` oder `KaffeeMitMilchUndSirup`.

Mit Decorators lassen sich die Extras flexibel kombinieren.

## Aufbau

- **Component:** Gemeinsames Interface.
- **Concrete Component:** Das ursprüngliche Objekt.
- **Decorator:** Umhüllt ein Objekt desselben Supertyps.
- **Concrete Decorator:** Ergänzt eine bestimmte Funktionalität.

## Beispiel

```java
interface Getraenk {
    double kosten();
}

class Kaffee implements Getraenk {
    public double kosten() {
        return 3.00;
    }
}

class Milch implements Getraenk {
    private Getraenk getraenk;

    public Milch(Getraenk getraenk) {
        this.getraenk = getraenk;
    }

    public double kosten() {
        return getraenk.kosten() + 0.50;
    }
}

class Sirup implements Getraenk {
    private Getraenk getraenk;

    public Sirup(Getraenk getraenk) {
        this.getraenk = getraenk;
    }

    public double kosten() {
        return getraenk.kosten() + 0.70;
    }
}
```

Verwendung:

```java
Getraenk bestellung = new Kaffee();
bestellung = new Milch(bestellung);
bestellung = new Sirup(bestellung);

System.out.println(bestellung.kosten());
// 4.20
```

Der Kaffee kostet 3,00 €. Milch und Sirup werden jeweils hinzugefügt.

## Vorteile

- Objekte können dynamisch erweitert werden.
- Mehrere Erweiterungen lassen sich kombinieren.
- Die ursprüngliche Klasse muss nicht verändert werden.
- Häufig flexibler als viele Unterklassen.

## Nachteile

- Viele kleine Decorator-Objekte können entstehen.
- Verschachtelungen können unübersichtlich werden.

## Eselsbrücke

**Decorator = Dekorieren und Extras hinzufügen.**

Wie beim Kaffee: Der Kaffee bleibt derselbe, aber du kannst Milch, Sirup und andere Extras hinzufügen.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Decorator Patterns?**

Antwort: Es erweitert ein Objekt dynamisch um zusätzliche Funktionalität, ohne dessen ursprüngliche Klasse verändern zu müssen.

**Frage 2: Warum haben Decorator und Originalobjekt denselben Supertyp?**

Antwort: Dadurch kann ein Decorator überall verwendet werden, wo auch das ursprüngliche Objekt erwartet wird.

**Frage 3: Können mehrere Decorators kombiniert werden?**

Antwort: Ja. Decorators können ineinander verschachtelt werden.

**Frage 4: Warum ist Decorator eine Alternative zur Vererbung?**

Antwort: Zusätzliche Funktionalitäten können flexibel kombiniert werden, ohne für jede Kombination eine eigene Unterklasse erstellen zu müssen.

**Frage 5: Welches Designprinzip unterstützt Decorator?**

Antwort: Das Open-Closed-Prinzip. Bestehende Klassen können erweitert werden, ohne sie direkt verändern zu müssen.

**Frage 6: Was bedeutet Wrapper?**

Antwort: Ein Wrapper umhüllt ein anderes Objekt und stellt zusätzliche Funktionalität bereit.

**Merksatz:** Decorator erweitert ein Objekt dynamisch durch zusätzliche Funktionalität.
