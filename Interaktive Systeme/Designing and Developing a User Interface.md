## Modulübersicht

In diesem Modul geht es darum, wie Benutzeroberflächen mit WPF aufgebaut und gestaltet werden.

Die vier Themenbereiche sind:

1. Defining Page Layout – Seitenlayout definieren
    
2. Using Content Controls – Content Controls verwenden
    
3. Using Items Controls – Items Controls verwenden
    
4. Sharing Logical Resources in a Window – Ressourcen innerhalb eines Fensters gemeinsam verwenden
    

---

# Lesson 1 – Defining Page Layout

## WPF Page Layout Model

WPF verwendet verschiedene Layout-Container, sogenannte Panels, um Steuerelemente innerhalb einer Benutzeroberfläche anzuordnen.

Die wichtigsten Layout-Klassen sind:

|Klasse|Aufgabe|
|---|---|
|`Canvas`|Elemente frei über Koordinaten positionieren|
|`DockPanel`|Elemente an einer Seite des Containers anordnen|
|`Grid`|Elemente in Zeilen und Spalten anordnen|
|`StackPanel`|Elemente untereinander oder nebeneinander anordnen|
|`VirtualizingStackPanel`|Elemente wie ein StackPanel anordnen und nicht benötigte Elemente bei großen Listen nicht vollständig darstellen|
|`WrapPanel`|Elemente automatisch in die nächste Zeile oder Spalte umbrechen|

### Panel

`Panel` ist die Basisklasse für verschiedene Layout-Container.

Wichtige Eigenschaften:

- `Background`: Legt die Hintergrundfarbe fest.
    
- `Children`: Enthält die untergeordneten Elemente.
    
- `ZIndex`: Bestimmt, welches Element bei Überlappungen im Vordergrund liegt.
    

### Canvas

- Elemente werden mithilfe von Koordinaten positioniert.
    
- Die Position wird beispielsweise mit `Canvas.Left` und `Canvas.Top` festgelegt.
    
- Gut geeignet für eine freie Positionierung.
    

### DockPanel

- Elemente werden an einer Seite des Containers angeordnet.
    
- Mögliche Seiten: oben, unten, links und rechts.
    
- Verwendet die Eigenschaft `DockPanel.Dock`.
    

### Grid

- Teilt die Oberfläche in Zeilen und Spalten.
    
- Elemente können in bestimmten Zellen platziert werden.
    
- Gut geeignet für strukturierte Benutzeroberflächen.
    

### StackPanel

- Ordnet Elemente hintereinander an.
    
- `Orientation="Vertical"`: untereinander.
    
- `Orientation="Horizontal"`: nebeneinander.
    

### WrapPanel

- Ordnet Elemente nebeneinander oder untereinander an.
    
- Wenn nicht mehr genügend Platz vorhanden ist, werden die Elemente automatisch umgebrochen.
    

### VirtualizingStackPanel

- Funktioniert ähnlich wie ein StackPanel.
    
- Besonders bei großen Listen hilfreich.
    
- Nicht benötigte Elemente müssen nicht alle gleichzeitig dargestellt werden.
    

---

# Lesson 2 – Using Content Controls

## Understanding Content Controls

Ein Content Control kann grundsätzlich **ein einzelnes Inhaltselement** enthalten.

Es besitzt die Eigenschaft:

- `Content`: Bestimmt den Inhalt des Steuerelements.
    

Der Inhalt kann unterschiedliche Typen haben:

- Text
    
- Datum und Uhrzeit (`DateTime`)
    
- Ein anderes UI-Element (`UIElement`)
    
- Mehrere Objekte können beispielsweise über ein gemeinsames Element wie ein Panel dargestellt werden.
    

### Beispiele für Content Controls

|Control|Beschreibung|
|---|---|
|`Button`|Schaltfläche|
|`CheckBox`|Kontrollkästchen|
|`GroupItem`|Gruppiert ein Element|
|`Label`|Beschriftung|
|`RadioButton`|Auswahl einer Option|
|`RepeatButton`|Wiederholt eine Aktion, solange die Schaltfläche gedrückt wird|
|`ToggleButton`|Schaltfläche mit zwei Zuständen|
|`ToolTip`|Zeigt zusätzliche Informationen an|

## Headered Content Controls

Headered Content Controls sind eine spezielle Form von Content Controls.

Sie besitzen zwei wichtige Eigenschaften:

- `Content`: Der eigentliche Inhalt.
    
- `Header`: Die Überschrift oder Beschriftung.
    

### Beispiele

|Control|Beschreibung|
|---|---|
|`Expander`|Ein- und ausklappbarer Bereich|
|`GroupBox`|Gruppiert Elemente mit einer Überschrift|
|`TabItem`|Einzelner Reiter innerhalb eines TabControls|

---

# Lesson 3 – Using Items Controls

## Understanding Items Controls

Items Controls können **mehrere Objekte** enthalten.

Sie besitzen zwei wichtige Eigenschaften:

- `Items`: Enthält die einzelnen Elemente direkt.
    
- `ItemsSource`: Gibt eine Datenquelle an, aus der die Elemente geladen werden.
    

Die enthaltenen Elemente können unterschiedliche Typen haben.

### Beispiele für Items Controls

|Control|Beschreibung|
|---|---|
|`ComboBox`|Dropdown-Liste|
|`ListBox`|Liste mit auswählbaren Elementen|
|`Menu`|Menü|
|`StatusBar`|Statusleiste|
|`TabControl`|Steuerelement mit mehreren Tabs|
|`ToolBar`|Werkzeugleiste|
|`TreeView`|Hierarchische Baumansicht|

## Handling Item Selection

Bei Items Controls kann auf die Auswahl eines Elements reagiert werden.

Dafür wird ein Event Handler verwendet.

### 1. Event Handler in XAML zuweisen

```
<ListBox SelectionChanged="ListBox1_SelectionChanged">
    ...
</ListBox>
```

### 2. Event Handler in C# definieren

```
public void ListBox1_SelectionChanged(
    object sender,
    SelectionChangedEventArgs e)
{
    // Wird ausgeführt, wenn sich die Auswahl ändert
}
```

**Wichtig:** `SelectionChanged` wird ausgelöst, wenn sich die Auswahl innerhalb der Liste verändert.

---

# Lesson 4 – Sharing Logical Resources in a Window

## Understanding Resources

Resources ermöglichen es, häufig verwendete Objekte und Werte wiederzuverwenden.

Beispiele:

- Brushes (Hintergrund- und Schriftfarben)
    
- Styles
    
- Control Templates
    

Dadurch müssen häufig verwendete Eigenschaften nicht immer wieder neu definiert werden.

## Defining Resources

Resources können auf verschiedenen Ebenen definiert werden:

1. **Application Scope:** Ressourcen für die gesamte Anwendung.
    
2. **Window oder Page Scope:** Ressourcen für ein bestimmtes Fenster oder eine Seite.
    
3. **Element-Level Scope:** Ressourcen für ein bestimmtes Element und dessen untergeordnete Elemente.
    

### Beispiel: Ressourcen in XAML definieren

```
<Window.Resources>
    <SolidColorBrush x:Key="blueBrush" Color="Blue"/>
    <SolidColorBrush x:Key="whiteBrush" Color="White"/>

    <sys:Double x:Key="myValue">100</sys:Double>
</Window.Resources>
```

- `x:Key`: Eindeutiger Schlüssel, über den die Ressource angesprochen wird.
    
- `SolidColorBrush`: Definiert einen Pinsel mit einer bestimmten Farbe.
    
- `Color`: Legt die Farbe fest.
    

## Referencing Resources in XAML

Es gibt zwei Möglichkeiten, auf Ressourcen in XAML zuzugreifen.

### StaticResource

```
<Button
    Background="{StaticResource blueBrush}"
    Foreground="{StaticResource whiteBrush}">
    Text
</Button>
```

- Die Ressource wird beim Laden der Oberfläche aufgelöst.
    
- Eine spätere Änderung der Ressource wird normalerweise nicht automatisch übernommen.
    

### DynamicResource

```
<Button
    Background="{DynamicResource blueBrush}"
    Foreground="{DynamicResource whiteBrush}">
    Text
</Button>
```

- Die Ressource wird dynamisch aufgelöst.
    
- Änderungen an der Ressource können zur Laufzeit übernommen werden.
    

### Unterschied

|StaticResource|DynamicResource|
|---|---|
|Statische Ressourcenreferenz|Dynamische Ressourcenreferenz|
|Wird beim Laden aufgelöst|Kann zur Laufzeit neu aufgelöst werden|
|Für unveränderliche Ressourcen geeignet|Für Ressourcen geeignet, die sich zur Laufzeit ändern können|

## Referencing Resources Programmatically

Ressourcen können auch direkt im C#-Code verwendet werden.

### FindResource()

Sucht eine Ressource anhand ihres Schlüssels.

```
SolidColorBrush brush = (SolidColorBrush)
    this.FindResource("whiteBrush");
```

### TryFindResource()

Funktioniert ähnlich wie `FindResource()`, gibt aber `null` zurück, wenn die Ressource nicht gefunden wird, anstatt eine Ausnahme auszulösen.

### SetResourceReference()

Verknüpft eine Eigenschaft eines Steuerelements mit einer Ressource.

```
this.myButton.SetResourceReference(
    Button.BackgroundProperty,
    "whiteBrush");
```

### Resources-Eigenschaft

Auf Ressourcen des aktuellen Elements kann auch direkt über die `Resources`-Eigenschaft zugegriffen werden.

```
SolidColorBrush brush = (SolidColorBrush)
    this.Resources["whiteBrush"];
```

---

# Prüfungswissen – Das solltest du können

## Layouts

- Unterschied zwischen `Canvas`, `DockPanel`, `Grid`, `StackPanel` und `WrapPanel` erklären.
    
- Wissen, dass `Panel` die Basisklasse der Layout-Container ist.
    
- Wissen, dass `Grid` mit Zeilen und Spalten arbeitet.
    

## Content Controls

- Wissen, dass Content Controls grundsätzlich ein einzelnes Inhaltselement enthalten.
    
- Die Eigenschaften `Content` und `Header` unterscheiden können.
    
- Beispiele für Content Controls und Headered Content Controls nennen können.
    

## Items Controls

- Wissen, dass Items Controls mehrere Elemente enthalten.
    
- Unterschied zwischen `Items` und `ItemsSource` kennen.
    
- Beispiele für Items Controls nennen können.
    
- Wissen, wofür `SelectionChanged` verwendet wird.
    

## Resources

- Erklären können, warum Ressourcen verwendet werden.
    
- Die drei Ebenen der Ressourcendefinition kennen.
    
- `StaticResource` und `DynamicResource` unterscheiden können.
    
- `FindResource()`, `TryFindResource()` und `SetResourceReference()` kennen.
    

---

# Merksätze

- **Canvas:** Elemente frei positionieren.
    
- **DockPanel:** Elemente an Seiten anordnen.
    
- **Grid:** Zeilen und Spalten.
    
- **StackPanel:** Elemente hintereinander anordnen.
    
- **WrapPanel:** Elemente automatisch umbrechen.
    
- **ContentControl:** Grundsätzlich ein Inhaltselement.
    
- **HeaderedContentControl:** Inhalt plus Überschrift.
    
- **ItemsControl:** Mehrere Elemente.
    
- **ItemsSource:** Datenquelle für die Elemente.
    
- **SelectionChanged:** Reagiert auf eine veränderte Auswahl.
    
- **Resources:** Wiederverwendbare Objekte und Werte.
    
- **StaticResource:** Statische Ressourcenreferenz.
    
- **DynamicResource:** Dynamische Ressourcenreferenz.