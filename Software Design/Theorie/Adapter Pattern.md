**Kategorie:** Strukturmuster (Structural Pattern)

## Was ist das Adapter Pattern?

Das Adapter Pattern ermöglicht es, zwei Schnittstellen zusammenarbeiten zu lassen, die eigentlich nicht zueinander passen.

Der Adapter übersetzt zwischen der Schnittstelle, die der Client erwartet, und der Schnittstelle, die ein bestehendes Objekt anbietet.

## Welches Problem löst es?

Ein Programm erwartet eine bestimmte Methode. Eine vorhandene Klasse bietet dieselbe Funktionalität an, verwendet dafür aber eine andere Schnittstelle.

Die vorhandene Klasse soll nicht verändert werden.

Der Adapter übernimmt die Übersetzung.

## Aufbau

- **Target:** Die Schnittstelle, die der Client erwartet.
- **Adaptee:** Die vorhandene Klasse mit der unpassenden Schnittstelle.
- **Adapter:** Übersetzt die Aufrufe zwischen Target und Adaptee.
- **Client:** Verwendet die erwartete Schnittstelle.

## Beispiel in Java

Ein Programm erwartet ein europäisches Ladegerät mit einer Methode `laden()`.

Ein vorhandenes Gerät bietet aber nur `usbLaden()` an.

```java
interface Ladegeraet {
    void laden();
}

class USBGeraet {
    public void usbLaden() {
        System.out.println("USB-Gerät wird geladen");
    }
}

class LadeAdapter implements Ladegeraet {
    private USBGeraet usbGeraet;

    public LadeAdapter(USBGeraet usbGeraet) {
        this.usbGeraet = usbGeraet;
    }

    public void laden() {
        usbGeraet.usbLaden();
    }
}
```

Verwendung:

```java
USBGeraet geraet = new USBGeraet();

Ladegeraet adapter = new LadeAdapter(geraet);
adapter.laden();
```

Der Client verwendet `laden()`, während der Adapter intern `usbLaden()` aufruft.

## Vorteile

- Bestehender Code kann weiterverwendet werden.
- Unpassende Schnittstellen werden kompatibel gemacht.
- Die vorhandene Klasse muss nicht verändert werden.
- Fremde Bibliotheken lassen sich leichter integrieren.

## Nachteile

- Zusätzliche Klassen entstehen.
- Bei vielen Adaptern kann die Struktur umfangreicher werden.
- Ein Adapter kann keine grundsätzlich fehlende Funktionalität automatisch ersetzen.

## Eselsbrücke

**Adapter = Übersetzer.**

Ein Reiseadapter passt den Stecker an eine andere Steckdose an. Das Gerät bleibt gleich, aber die Verbindung wird passend gemacht.

## Theoriefragen und Antworten

**Frage 1: Was ist das Ziel des Adapter Patterns?**

Antwort: Zwei inkompatible Schnittstellen miteinander kompatibel zu machen.

**Frage 2: Was ist der Adaptee?**

Antwort: Die vorhandene Klasse, deren Schnittstelle nicht zur erwarteten Schnittstelle passt.

**Frage 3: Was ist das Target?**

Antwort: Die Schnittstelle, die der Client verwenden möchte.

**Frage 4: Welche Aufgabe hat der Adapter?**

Antwort: Er übersetzt die Aufrufe des Clients in Aufrufe, die der Adaptee versteht.

**Frage 5: Muss die bestehende Klasse verändert werden?**

Antwort: Nein. Der Adapter kann die Schnittstelle anpassen, ohne die vorhandene Klasse direkt zu ändern.

**Frage 6: Was ist der Unterschied zwischen Adapter und Decorator?**

Antwort: Adapter macht eine Schnittstelle kompatibel. Decorator erweitert ein Objekt um zusätzliche Funktionalität.

**Frage 7: Was ist ein typisches Anwendungsbeispiel?**

Antwort: Eine alte Bibliothek besitzt eine andere Schnittstelle als die neue Anwendung erwartet. Ein Adapter verbindet beide.

**Merksatz:** Adapter übersetzt eine Schnittstelle in eine andere.
