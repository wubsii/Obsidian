## Modulübersicht

In diesem Modul geht es darum, wie Daten zwischen C#-Objekten und WPF-Steuerelementen ausgetauscht werden.

Die vier Themenbereiche sind:

1. Overview of Data Binding – Grundlagen der Datenbindung
    
2. Creating a Data Binding – Datenbindung erstellen
    
3. Implementing Property Change Notification – Änderungen an Eigenschaften melden
    
4. Converting Data – Daten konvertieren
    

---

# Lesson 1 – Overview of Data Binding

## The WPF Data-Binding Model

Data Binding (Datenbindung) ermöglicht den Datenaustausch zwischen einer Datenquelle und einem UI-Element.

Beispiele für mögliche Datenquellen:

- Dynamische Objekte
    
- UI-Elemente
    
- XML-Daten
    
- ADO.NET-Datenquellen
    
- Verwaltete Objekte (Managed Objects)
    

Die Datenquelle stellt Werte bereit, die an Eigenschaften eines UI-Elements gebunden werden können.

## Binding Sources and Binding Targets

Eine Datenbindung besteht aus mehreren Komponenten:

|Komponente|Bedeutung|
|---|---|
|Binding Target Object|Das UI-Element, das den Wert erhält|
|Binding Target Dependency Property|Die Eigenschaft des UI-Elements, an die gebunden wird|
|Binding Source|Das Objekt, aus dem die Daten stammen|
|Path|Gibt an, welche Eigenschaft der Datenquelle verwendet wird|

**Beispiel:**

Ein Button soll eine Farbe aus einem C#-Objekt übernehmen.

- Binding Target Object: `Button`
    
- Binding Target Dependency Property: `Background`
    
- Binding Source: C#-Objekt
    
- Path: Eigenschaft mit dem Farbwert
    

## Data-Binding Modes

WPF unterstützt vier Data-Binding-Modi:

|Modus|Beschreibung|
|---|---|
|`OneWay`|Daten fließen von der Quelle zum Ziel.|
|`TwoWay`|Daten fließen in beide Richtungen.|
|`OneWayToSource`|Daten fließen vom Ziel zurück zur Quelle.|
|`OneTime`|Der Wert wird einmalig von der Quelle zum Ziel übertragen.|

### Merkhilfe

- **OneWay:** Quelle → Ziel
    
- **TwoWay:** Quelle ↔ Ziel
    
- **OneWayToSource:** Ziel → Quelle
    
- **OneTime:** Einmalige Übertragung von Quelle zu Ziel
    

---

# Lesson 2 – Creating a Data Binding

## Binding to a Class Property

Eine Eigenschaft eines UI-Elements kann an eine Eigenschaft einer C#-Klasse gebunden werden.

Dafür sind zwei Dinge notwendig:

1. Eine Resource definieren, die die Binding-Source-Klasse bereitstellt.
    
2. Mit `Path` angeben, welche Eigenschaft der Klasse verwendet werden soll.
    

Beispiel für eine Binding-Angabe:

```
Text="{Binding Path=Name, Source={StaticResource person}}"
```

- `Binding`: Erstellt die Datenbindung.
    
- `Path=Name`: Gibt die Eigenschaft `Name` an.
    
- `Source`: Gibt die Datenquelle an.
    

## Binding Multiple Controls to a Class

Mehrere Steuerelemente können an Eigenschaften derselben Klasse gebunden werden.

Dafür kann die Eigenschaft `DataContext` eines übergeordneten Elements gesetzt werden.

Die untergeordneten Controls übernehmen den DataContext automatisch.

Beispiel:

```
<StackPanel DataContext="{StaticResource person}">
    <TextBox Text="{Binding Name}"/>
    <TextBox Text="{Binding Age}"/>
</StackPanel>
```

Die einzelnen Controls greifen über `Path` auf unterschiedliche Eigenschaften desselben Objekts zu.

**Wichtig:** Wenn der `DataContext` bereits gesetzt ist, muss die `Source` nicht bei jedem Binding erneut angegeben werden.

## Binding to a Full Object

Es ist auch möglich, ein ganzes Objekt statt einer einzelnen Eigenschaft zu binden.

Dafür wird die `Path`-Eigenschaft weggelassen.

Beispiel:

```
<TextBlock Text="{Binding}"/>
```

Diese Schreibweise wird als _Empty Binding Syntax_ bezeichnet.

Die Binding-Quelle wird dabei beispielsweise vom übergeordneten Element übernommen.

## Binding to User Interface Controls

Eine Datenbindung kann auch zwischen zwei UI-Elementen hergestellt werden.

Dafür wird die Eigenschaft `ElementName` verwendet.

Beispiel:

```
<Slider x:Name="mySlider"
        Minimum="0"
        Maximum="100"/>

<TextBlock Text="{Binding ElementName=mySlider, Path=Value}"/>
```

Der TextBlock zeigt dadurch den aktuellen Wert des Sliders an.

- `ElementName`: Gibt das UI-Element an, das als Datenquelle dient.
    
- `Path`: Gibt die Eigenschaft dieses Elements an.
    

---

# Lesson 3 – Implementing Property Change Notification

## Understanding Property Change Notifications

Property Change Notification bedeutet, dass eine Klasse Änderungen an ihren Eigenschaften melden kann.

Dadurch kann WPF erkennen, wenn sich ein Wert in der Datenquelle verändert hat, und den gebundenen Zielwert aktualisieren.

Bei einer TwoWay-Bindung können Änderungen außerdem vom Ziel zurück zur Quelle übertragen werden.

Der Zeitpunkt der Aktualisierung wird unter anderem über `UpdateSourceTrigger` bestimmt.

## Propagating Property Change Notifications to a Binding Target

Damit Änderungen an Eigenschaften einer C#-Klasse erkannt werden, kann das Interface `INotifyPropertyChanged` verwendet werden.

### Umsetzung von INotifyPropertyChanged

Dafür sind drei Schritte notwendig:

1. Das Event `PropertyChanged` deklarieren.
    
2. Eine Methode `OnPropertyChanged` erstellen.
    
3. Bei einer Änderung einer Eigenschaft `OnPropertyChanged` aufrufen.
    

Beispiel:

```
using System.ComponentModel;

public class Person : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    private string name;

    public string Name
    {
        get { return name; }
        set
        {
            name = value;
            OnPropertyChanged(nameof(Name));
        }
    }

    protected void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(
            this,
            new PropertyChangedEventArgs(propertyName)
        );
    }
}
```

**Wichtig:**

- `INotifyPropertyChanged` ermöglicht die Benachrichtigung über Eigenschaftsänderungen.
    
- `PropertyChanged` ist das Event, das ausgelöst wird.
    
- `OnPropertyChanged()` informiert WPF darüber, welche Eigenschaft geändert wurde.
    

## Propagating Value Changes to a Binding Source

Mit `UpdateSourceTrigger` wird festgelegt, wann Änderungen vom Binding Target zurück zur Binding Source übertragen werden.

WPF unterstützt folgende Werte:

|Wert|Beschreibung|
|---|---|
|`Default`|Verwendet das Standardverhalten der gebundenen Eigenschaft.|
|`Explicit`|Die Aktualisierung muss ausdrücklich ausgelöst werden.|
|`LostFocus`|Aktualisierung, wenn das Element den Fokus verliert.|
|`PropertyChanged`|Aktualisierung bei jeder Änderung der Eigenschaft.|

Beispiel:

```
<TextBox Text="{Binding Name, UpdateSourceTrigger=PropertyChanged}"/>
```

Hier wird die Datenquelle bei jeder Änderung des Textes aktualisiert.

---

# Lesson 4 – Converting Data

## Default Data Conversions

Bei einer Datenbindung müssen der Datentyp der Binding Source und der Datentyp der Binding Target Property miteinander kompatibel sein.

WPF versucht, automatisch eine passende Typkonvertierung durchzuführen.

Beispiel:

- Binding Source: `ColorName` vom Typ `String`
    
- Binding Target: `Background` vom Typ `Brush`
    

WPF kann bestimmte Standardkonvertierungen durchführen.

**Wichtig:**

- Ist eine Standardkonvertierung möglich, wird sie automatisch verwendet.
    
- Ist keine passende Konvertierung möglich, entsteht ein Fehler.
    

## Implementing a Custom Value Converter

Wenn WPF eine benötigte Konvertierung nicht automatisch durchführen kann, kann ein eigener Value Converter erstellt werden.

Dafür wird das Interface `IValueConverter` verwendet.

### Schritte

1. Eine Klasse erstellen, die `IValueConverter` implementiert.
    
2. Die Klasse mit dem Attribut `ValueConversion` versehen.
    
3. Die Methoden `Convert()` und `ConvertBack()` implementieren.
    

### Die beiden Methoden

|Methode|Aufgabe|
|---|---|
|`Convert()`|Konvertiert den Wert von der Datenquelle zum Ziel.|
|`ConvertBack()`|Konvertiert den Wert vom Ziel zurück zur Datenquelle.|

### Beispiel für einen Converter

```
using System;
using System.Globalization;
using System.Windows.Data;
using System.Windows.Media;

[ValueConversion(typeof(string), typeof(Brush))]
public class ColorBrushConverter : IValueConverter
{
    public object Convert(
        object value,
        Type targetType,
        object parameter,
        CultureInfo culture)
    {
        string colorName = value as string;

        return new SolidColorBrush(
            (Color)ColorConverter.ConvertFromString(colorName)
        );
    }

    public object ConvertBack(
        object value,
        Type targetType,
        object parameter,
        CultureInfo culture)
    {
        return value.ToString();
    }
}
```

Der Converter wandelt einen Farbnamen als `String` in einen `Brush` um.

Beispiel:

- Source: `"Red"` (`String`)
    
- Target: `SolidColorBrush` (`Brush`)
    

---

# Prüfungswissen – Das solltest du können

## Data Binding

- Erklären können, was Data Binding bedeutet.
    
- Binding Source und Binding Target unterscheiden.
    
- Die vier Binding Modes erklären können.
    
- Die Bestandteile eines Bindings kennen: Target, Dependency Property, Source und Path.
    

## Creating a Data Binding

- Eine Klasse als Binding Source verwenden können.
    
- Wissen, wofür `DataContext` verwendet wird.
    
- Mehrere Controls an dieselbe Klasse binden können.
    
- Wissen, was ein Empty Binding ist.
    
- `ElementName` für Bindings zwischen UI-Elementen kennen.
    

## Property Change Notification

- Erklären können, warum Property Change Notification benötigt wird.
    
- Die Aufgabe von `INotifyPropertyChanged` kennen.
    
- Das Event `PropertyChanged` und die Methode `OnPropertyChanged()` erklären können.
    
- Die vier `UpdateSourceTrigger`-Werte unterscheiden können.
    

## Converting Data

- Wissen, dass WPF automatische Typkonvertierungen durchführen kann.
    
- Erklären können, wann ein eigener Value Converter notwendig ist.
    
- Die Aufgaben von `Convert()` und `ConvertBack()` unterscheiden können.
    
- Wissen, wofür `IValueConverter` verwendet wird.
    

---

# Merksätze

- **Binding Source:** Woher kommen die Daten?
    
- **Binding Target:** Wohin werden die Daten übertragen?
    
- **Path:** Welche Eigenschaft wird verwendet?
    
- **OneWay:** Quelle → Ziel.
    
- **TwoWay:** Quelle ↔ Ziel.
    
- **OneWayToSource:** Ziel → Quelle.
    
- **OneTime:** Einmalige Übertragung.
    
- **DataContext:** Gemeinsame Datenquelle für untergeordnete Elemente.
    
- **ElementName:** Bindung an ein anderes UI-Element.
    
- **INotifyPropertyChanged:** Meldet Änderungen an Eigenschaften.
    
- **UpdateSourceTrigger:** Bestimmt, wann Änderungen zur Quelle übertragen werden.
    
- **IValueConverter:** Ermöglicht eigene Typkonvertierungen.
    
- **Convert():** Quelle → Ziel.
    
- **ConvertBack():** Ziel → Quelle.


```
public delegate void MethodenName();
```

Methoden in Variablen:
übergeben, wie etwas passiert, kann man einer Methode übergeben, wenn man eine Variable (delegate) erstellt.

callbackmethode:
