
## Inhaltsverzeichnis
1. [[#1. Strategy Pattern|Strategy Pattern]] 
2. [[#2. Decorator Pattern|Decorator Pattern]]
3. [[#3. Observer Pattern|Observer Pattern]]
4. [[#4. Singleton Pattern|Singleton Pattern]]
5. [[#5. Factory Method Pattern|Factory Method Pattern]]
6. [[#6. Command Pattern|Command Pattern]]
7. [[#7. Adapter Pattern|Adapter Pattern]]
8. [[#8. Facade Pattern|Facade Pattern]]
9. [[#9. Template Method Pattern|Template Method Pattern]]
10. [[#10. Iterator Pattern|Iterator Pattern]]

---

# 1. Strategy Pattern

**Zweck:** Verschiedene Algorithmen oder Verhaltensweisen austauschbar machen.

**Typische Methoden:** `ausfuehren()`, `setStrategie()`

## Beispiel 1: Zahlungsmethoden

```java
interface Zahlungsstrategie {
    void bezahlen(double betrag);
}

class Barzahlung implements Zahlungsstrategie {
    public void bezahlen(double betrag) {
        System.out.println("Bar bezahlt: " + betrag + " Euro");
    }
}

class Kartenzahlung implements Zahlungsstrategie {
    public void bezahlen(double betrag) {
        System.out.println("Mit Karte bezahlt: " + betrag + " Euro");
    }
}

class Kasse {
    private Zahlungsstrategie strategie;

    public Kasse(Zahlungsstrategie strategie) {
        this.strategie = strategie;
    }

    public void setStrategie(Zahlungsstrategie strategie) {
        this.strategie = strategie;
    }

    public void bezahlen(double betrag) {
        strategie.bezahlen(betrag);
    }
}

class Main {
    public static void main(String[] args) {
        Kasse kasse = new Kasse(new Barzahlung());
        kasse.bezahlen(20);

        kasse.setStrategie(new Kartenzahlung());
        kasse.bezahlen(30);
    }
}
```

## Beispiel 2: Rabattberechnung

```java
interface Rabattstrategie {
    double berechnePreis(double preis);
}

class KeinRabatt implements Rabattstrategie {
    public double berechnePreis(double preis) {
        return preis;
    }
}

class ZehnProzentRabatt implements Rabattstrategie {
    public double berechnePreis(double preis) {
        return preis * 0.9;
    }
}

class Shop {
    public void preisAnzeigen(
            double preis, Rabattstrategie strategie) {
        System.out.println(strategie.berechnePreis(preis));
    }
}

class Main {
    public static void main(String[] args) {
        Shop shop = new Shop();

        shop.preisAnzeigen(100, new KeinRabatt());
        shop.preisAnzeigen(100, new ZehnProzentRabatt());
    }
}
```

**Merke:** Strategy tauscht ein Verhalten aus.

---

# 2. Decorator Pattern

**Zweck:** Ein Objekt um zusätzliche Funktionen erweitern, ohne die ursprüngliche Klasse zu verändern.

**Typische Methoden:** `kosten()`, `beschreibung()`

## Beispiel 1: Kaffee mit Zusätzen

```java
interface Getraenk {
    double kosten();
    String beschreibung();
}

class Kaffee implements Getraenk {
    public double kosten() {
        return 2.0;
    }

    public String beschreibung() {
        return "Kaffee";
    }
}

class MilchDecorator implements Getraenk {
    private Getraenk getraenk;

    public MilchDecorator(Getraenk getraenk) {
        this.getraenk = getraenk;
    }

    public double kosten() {
        return getraenk.kosten() + 0.5;
    }

    public String beschreibung() {
        return getraenk.beschreibung() + " mit Milch";
    }
}

class SirupDecorator implements Getraenk {
    private Getraenk getraenk;

    public SirupDecorator(Getraenk getraenk) {
        this.getraenk = getraenk;
    }

    public double kosten() {
        return getraenk.kosten() + 0.7;
    }

    public String beschreibung() {
        return getraenk.beschreibung() + " mit Sirup";
    }
}

class Main {
    public static void main(String[] args) {
        Getraenk kaffee = new Kaffee();
        kaffee = new MilchDecorator(kaffee);
        kaffee = new SirupDecorator(kaffee);

        System.out.println(kaffee.beschreibung());
        System.out.println(kaffee.kosten() + " Euro");
    }
}
```

## Beispiel 2: Benachrichtigungen erweitern

```java
interface Benachrichtigung {
    void senden();
}

class EinfacheNachricht implements Benachrichtigung {
    public void senden() {
        System.out.println("Nachricht gesendet");
    }
}

class EmailDecorator implements Benachrichtigung {
    private Benachrichtigung nachricht;

    public EmailDecorator(Benachrichtigung nachricht) {
        this.nachricht = nachricht;
    }

    public void senden() {
        nachricht.senden();
        System.out.println("Zusätzlich per E-Mail gesendet");
    }
}

class SMSDecorator implements Benachrichtigung {
    private Benachrichtigung nachricht;

    public SMSDecorator(Benachrichtigung nachricht) {
        this.nachricht = nachricht;
    }

    public void senden() {
        nachricht.senden();
        System.out.println("Zusätzlich per SMS gesendet");
    }
}

class Main {
    public static void main(String[] args) {
        Benachrichtigung nachricht =
                new SMSDecorator(
                    new EmailDecorator(new EinfacheNachricht()));

        nachricht.senden();
    }
}
```

**Merke:** Decorator ergänzt Funktionen. Mehrere Decorators können kombiniert werden.

---

# 3. Observer Pattern

**Zweck:** Mehrere Objekte automatisch über Änderungen informieren.

**Typische Methoden:** `registrieren()`, `abmelden()`, `benachrichtigen()`, `aktualisieren()`

## Beispiel 1: Nachrichten abonnieren

```java
import java.util.ArrayList;
import java.util.List;

interface Beobachter {
    void aktualisieren(String nachricht);
}

class Abonnent implements Beobachter {
    private String name;

    public Abonnent(String name) {
        this.name = name;
    }

    public void aktualisieren(String nachricht) {
        System.out.println(name + " erhielt: " + nachricht);
    }
}

class Nachrichtendienst {
    private List<Beobachter> beobachter = new ArrayList<>();

    public void registrieren(Beobachter b) {
        beobachter.add(b);
    }

    public void abmelden(Beobachter b) {
        beobachter.remove(b);
    }

    public void benachrichtigen(String nachricht) {
        for (Beobachter b : beobachter) {
            b.aktualisieren(nachricht);
        }
    }
}

class Main {
    public static void main(String[] args) {
        Nachrichtendienst dienst = new Nachrichtendienst();

        dienst.registrieren(new Abonnent("Anna"));
        dienst.registrieren(new Abonnent("Max"));

        dienst.benachrichtigen("Neuer Beitrag!");
    }
}
```

## Beispiel 2: Temperatur überwachen

```java
import java.util.ArrayList;
import java.util.List;

interface TemperaturBeobachter {
    void aktualisieren(double temperatur);
}

class Anzeige implements TemperaturBeobachter {
    public void aktualisieren(double temperatur) {
        System.out.println("Temperatur: " + temperatur + " Grad");
    }
}

class Thermometer {
    private List<TemperaturBeobachter> beobachter =
            new ArrayList<>();

    public void registrieren(TemperaturBeobachter b) {
        beobachter.add(b);
    }

    public void temperaturSetzen(double temperatur) {
        for (TemperaturBeobachter b : beobachter) {
            b.aktualisieren(temperatur);
        }
    }
}

class Main {
    public static void main(String[] args) {
        Thermometer thermometer = new Thermometer();
        thermometer.registrieren(new Anzeige());

        thermometer.temperaturSetzen(22.5);
    }
}
```

**Merke:** Ein Objekt benachrichtigt alle angemeldeten Beobachter.

---

# 4. Singleton Pattern

**Zweck:** Sicherstellen, dass es nur eine Instanz einer Klasse gibt.

**Typische Bestandteile:** `private` Konstruktor, `getInstance()`

## Beispiel 1: Konfiguration

```java
class Konfiguration {
    private static Konfiguration instanz;

    private Konfiguration() {
    }

    public static Konfiguration getInstance() {
        if (instanz == null) {
            instanz = new Konfiguration();
        }
        return instanz;
    }

    public void anzeigen() {
        System.out.println("Zentrale Konfiguration");
    }
}

class Main {
    public static void main(String[] args) {
        Konfiguration k1 = Konfiguration.getInstance();
        Konfiguration k2 = Konfiguration.getInstance();

        k1.anzeigen();
        System.out.println(k1 == k2); // true
    }
}
```

## Beispiel 2: Spielstand verwalten

```java
class Spielstand {
    private static final Spielstand instanz =
            new Spielstand();

    private int punkte;

    private Spielstand() {
    }

    public static Spielstand getInstance() {
        return instanz;
    }

    public void punkteHinzufuegen(int anzahl) {
        punkte += anzahl;
    }

    public int getPunkte() {
        return punkte;
    }
}

class Main {
    public static void main(String[] args) {
        Spielstand s1 = Spielstand.getInstance();
        Spielstand s2 = Spielstand.getInstance();

        s1.punkteHinzufuegen(10);

        System.out.println(s2.getPunkte()); // 10
    }
}
```

**Merke:** Privater Konstruktor und zentraler Zugriff auf dieselbe Instanz.

---

# 5. Factory Method Pattern

**Zweck:** Die Erzeugung konkreter Objekte über eine Methode organisieren.

**Typische Methode:** `erzeugeProdukt()`

## Beispiel 1: Fahrzeuge erzeugen

```java
interface Fahrzeug {
    void fahren();
}

class Auto implements Fahrzeug {
    public void fahren() {
        System.out.println("Auto fährt");
    }
}

class Fahrrad implements Fahrzeug {
    public void fahren() {
        System.out.println("Fahrrad fährt");
    }
}

abstract class FahrzeugFactory {
    public abstract Fahrzeug erzeugeFahrzeug();
}

class AutoFactory extends FahrzeugFactory {
    public Fahrzeug erzeugeFahrzeug() {
        return new Auto();
    }
}

class FahrradFactory extends FahrzeugFactory {
    public Fahrzeug erzeugeFahrzeug() {
        return new Fahrrad();
    }
}

class Main {
    public static void main(String[] args) {
        FahrzeugFactory factory = new AutoFactory();
        Fahrzeug fahrzeug = factory.erzeugeFahrzeug();

        fahrzeug.fahren();
    }
}
```

## Beispiel 2: Dokumente erzeugen

```java
interface Dokument {
    void oeffnen();
}

class PDF implements Dokument {
    public void oeffnen() {
        System.out.println("PDF wird geöffnet");
    }
}

class Textdatei implements Dokument {
    public void oeffnen() {
        System.out.println("Textdatei wird geöffnet");
    }
}

abstract class DokumentFactory {
    public abstract Dokument erzeugeDokument();
}

class PDFFactory extends DokumentFactory {
    public Dokument erzeugeDokument() {
        return new PDF();
    }
}

class TextFactory extends DokumentFactory {
    public Dokument erzeugeDokument() {
        return new Textdatei();
    }
}

class Main {
    public static void main(String[] args) {
        DokumentFactory factory = new PDFFactory();
        Dokument dokument = factory.erzeugeDokument();

        dokument.oeffnen();
    }
}
```

**Merke:** Die Factory Method erzeugt ein Produkt, ohne dass der aufrufende Code die konkrete Klasse kennen muss.

---

# 6. Command Pattern

**Zweck:** Eine Aktion als eigenes Objekt kapseln.

**Typische Methoden:** `ausfuehren()`, optional `undo()`

## Beispiel 1: Lichtsteuerung

```java
interface Kommando {
    void ausfuehren();
    void undo();
}

class Licht {
    public void einschalten() {
        System.out.println("Licht an");
    }

    public void ausschalten() {
        System.out.println("Licht aus");
    }
}

class EinschaltenKommando implements Kommando {
    private Licht licht;

    public EinschaltenKommando(Licht licht) {
        this.licht = licht;
    }

    public void ausfuehren() {
        licht.einschalten();
    }

    public void undo() {
        licht.ausschalten();
    }
}

class Main {
    public static void main(String[] args) {
        Licht licht = new Licht();
        Kommando kommando = new EinschaltenKommando(licht);

        kommando.ausfuehren();
        kommando.undo();
    }
}
```

## Beispiel 2: Fernseher bedienen

```java
interface TVKommando {
    void ausfuehren();
}

class Fernseher {
    public void einschalten() {
        System.out.println("Fernseher eingeschaltet");
    }

    public void lauter() {
        System.out.println("Lautstärke erhöht");
    }
}

class EinschaltenKommando implements TVKommando {
    private Fernseher tv;

    public EinschaltenKommando(Fernseher tv) {
        this.tv = tv;
    }

    public void ausfuehren() {
        tv.einschalten();
    }
}

class LauterKommando implements TVKommando {
    private Fernseher tv;

    public LauterKommando(Fernseher tv) {
        this.tv = tv;
    }

    public void ausfuehren() {
        tv.lauter();
    }
}

class Main {
    public static void main(String[] args) {
        Fernseher tv = new Fernseher();

        TVKommando kommando = new EinschaltenKommando(tv);
        kommando.ausfuehren();

        kommando = new LauterKommando(tv);
        kommando.ausfuehren();
    }
}
```

**Merke:** Der Befehl wird als Objekt übergeben und ausgeführt. `undo()` ist optional.

---

# 7. Adapter Pattern

**Zweck:** Zwei inkompatible Schnittstellen miteinander verbinden.

**Typische Bestandteile:** Zielinterface, vorhandene Klasse, Adapter-Methode.

## Beispiel 1: Altes Zahlungssystem

```java
interface Zahlung {
    void bezahlen(double betrag);
}

class AltesZahlungssystem {
    public void zahleBetrag(double betrag) {
        System.out.println("Altes System: " + betrag + " Euro");
    }
}

class ZahlungsAdapter implements Zahlung {
    private AltesZahlungssystem system;

    public ZahlungsAdapter(AltesZahlungssystem system) {
        this.system = system;
    }

    public void bezahlen(double betrag) {
        system.zahleBetrag(betrag);
    }
}

class Main {
    public static void main(String[] args) {
        Zahlung zahlung =
                new ZahlungsAdapter(new AltesZahlungssystem());

        zahlung.bezahlen(50);
    }
}
```

## Beispiel 2: Medienplayer

```java
interface AudioPlayer {
    void abspielen(String datei);
}

class AlterPlayer {
    public void spieleDatei(String datei) {
        System.out.println("Spiele Datei: " + datei);
    }
}

class PlayerAdapter implements AudioPlayer {
    private AlterPlayer player;

    public PlayerAdapter(AlterPlayer player) {
        this.player = player;
    }

    public void abspielen(String datei) {
        player.spieleDatei(datei);
    }
}

class Main {
    public static void main(String[] args) {
        AudioPlayer player = new PlayerAdapter(new AlterPlayer());
        player.abspielen("musik.mp3");
    }
}
```

**Merke:** Der Adapter implementiert die erwartete Schnittstelle und übersetzt den Aufruf für die vorhandene Klasse.

---

# 8. Facade Pattern

**Zweck:** Ein komplexes System über eine einfache Schnittstelle bedienen.

**Typische Methoden:** `starten()`, `beenden()` oder eine Methode, die mehrere Schritte bündelt.

## Beispiel 1: Heimkino

```java
class Fernseher {
    public void einschalten() {
        System.out.println("Fernseher an");
    }
}

class Soundsystem {
    public void einschalten() {
        System.out.println("Soundsystem an");
    }
}

class Streaminggeraet {
    public void starten() {
        System.out.println("Streaming gestartet");
    }
}

class HeimkinoFacade {
    private Fernseher tv = new Fernseher();
    private Soundsystem sound = new Soundsystem();
    private Streaminggeraet streaming = new Streaminggeraet();

    public void filmStarten() {
        tv.einschalten();
        sound.einschalten();
        streaming.starten();
    }
}

class Main {
    public static void main(String[] args) {
        HeimkinoFacade kino = new HeimkinoFacade();
        kino.filmStarten();
    }
}
```

## Beispiel 2: Computer starten

```java
class Prozessor {
    public void starten() {
        System.out.println("Prozessor gestartet");
    }
}

class Speicher {
    public void laden() {
        System.out.println("Speicher geladen");
    }
}

class Betriebssystem {
    public void starten() {
        System.out.println("Betriebssystem gestartet");
    }
}

class ComputerFacade {
    private Prozessor cpu = new Prozessor();
    private Speicher speicher = new Speicher();
    private Betriebssystem os = new Betriebssystem();

    public void computerStarten() {
        cpu.starten();
        speicher.laden();
        os.starten();
    }
}

class Main {
    public static void main(String[] args) {
        ComputerFacade computer = new ComputerFacade();
        computer.computerStarten();
    }
}
```

**Merke:** Eine Facade bündelt mehrere interne Aufrufe hinter einer einfachen Methode.

---

# 9. Template Method Pattern

**Zweck:** Einen festen Ablauf definieren und einzelne Schritte von Unterklassen anpassen lassen.

**Typische Methoden:** eine Ablaufmethode wie `zubereiten()` und überschreibbare Methoden wie `zutatenVorbereiten()`.

## Beispiel 1: Getränke zubereiten

```java
abstract class Getraenk {
    public final void zubereiten() {
        wasserErhitzen();
        zutatenVorbereiten();
        aufgiessen();
    }

    private void wasserErhitzen() {
        System.out.println("Wasser erhitzen");
    }

    protected abstract void zutatenVorbereiten();

    private void aufgiessen() {
        System.out.println("Aufgießen");
    }
}

class Tee extends Getraenk {
    protected void zutatenVorbereiten() {
        System.out.println("Teebeutel vorbereiten");
    }
}

class Kaffee extends Getraenk {
    protected void zutatenVorbereiten() {
        System.out.println("Kaffeepulver vorbereiten");
    }
}

class Main {
    public static void main(String[] args) {
        Getraenk tee = new Tee();
        tee.zubereiten();

        Getraenk kaffee = new Kaffee();
        kaffee.zubereiten();
    }
}
```

## Beispiel 2: Berichte erstellen

```java
abstract class Bericht {
    public final void erstellen() {
        datenLaden();
        datenVerarbeiten();
        berichtAusgeben();
    }

    private void datenLaden() {
        System.out.println("Daten werden geladen");
    }

    protected abstract void datenVerarbeiten();

    private void berichtAusgeben() {
        System.out.println("Bericht wird ausgegeben");
    }
}

class Verkaufsbericht extends Bericht {
    protected void datenVerarbeiten() {
        System.out.println("Verkaufsdaten werden berechnet");
    }
}

class Personalbericht extends Bericht {
    protected void datenVerarbeiten() {
        System.out.println("Personaldaten werden ausgewertet");
    }
}

class Main {
    public static void main(String[] args) {
        new Verkaufsbericht().erstellen();
        new Personalbericht().erstellen();
    }
}
```

**Merke:** Die Basisklasse bestimmt die Reihenfolge. Unterklassen passen einzelne Schritte an.

---

# 10. Iterator Pattern

**Zweck:** Elemente einer Sammlung nacheinander durchlaufen, ohne ihre interne Struktur kennen zu müssen.

**Typische Methoden:** `hasNext()`, `next()`, optional `remove()`.

## Beispiel 1: Namen durchlaufen

```java
import java.util.Arrays;
import java.util.Iterator;
import java.util.List;

class Main {
    public static void main(String[] args) {
        List<String> namen = Arrays.asList("Anna", "Max", "Lisa");

        Iterator<String> iterator = namen.iterator();

        while (iterator.hasNext()) {
            String name = iterator.next();
            System.out.println(name);
        }
    }
}
```

## Beispiel 2: Eigene Sammlung mit Iterator

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

class Einkaufstasche implements Iterable<String> {
    private List<String> artikel = new ArrayList<>();

    public void artikelHinzufuegen(String name) {
        artikel.add(name);
    }

    @Override
    public Iterator<String> iterator() {
        return artikel.iterator();
    }
}

class Main {
    public static void main(String[] args) {
        Einkaufstasche tasche = new Einkaufstasche();

        tasche.artikelHinzufuegen("Milch");
        tasche.artikelHinzufuegen("Brot");
        tasche.artikelHinzufuegen("Apfel");

        for (String artikel : tasche) {
            System.out.println(artikel);
        }
    }
}
```

**Merke:** `hasNext()` prüft, ob ein weiteres Element vorhanden ist. `next()` liefert das nächste Element.

---

# Abschließende Merkliste

| Pattern | Woran erkenne ich es? |
|---|---|
| Strategy | Verhalten austauschen |
| Decorator | Funktionen ergänzen und kombinieren |
| Observer | Änderungen an Beobachter melden |
| Singleton | Nur eine Instanz |
| Factory Method | Objekte über eine Erzeugungsmethode erstellen |
| Command | Aktion als Objekt kapseln |
| Adapter | Inkompatible Schnittstellen verbinden |
| Facade | Komplexe Abläufe vereinfachen |
| Template Method | Fester Ablauf mit anpassbaren Schritten |
| Iterator | Sammlung Element für Element durchlaufen |

**Prüfungstipp:** Achte zuerst darauf, welches Problem gelöst werden soll. Methodennamen können unterschiedlich sein; entscheidend ist die Struktur und Aufgabe des Patterns.
