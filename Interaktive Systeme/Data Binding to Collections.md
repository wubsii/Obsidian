## Modulübersicht

In diesem Modul geht es darum, wie Sammlungen von Objekten an WPF-Steuerelemente gebunden und dargestellt werden.

Die vier Themenbereiche sind:

1. Binding to Collections of Objects – Sammlungen von Objekten binden
    
2. Using Collection Views – Collection Views verwenden
    
3. Creating Master-Detail User Interfaces – Master-Detail-Oberflächen erstellen
    
4. Using Data Templates – Data Templates verwenden
    

---

# Lesson 1 – Binding to Collections of Objects

## Overview of Binding to Collections

WPF ermöglicht es, eine Sammlung von Objekten an ein Items Control zu binden.

Beispiel:

Eine `ListBox` kann an eine Sammlung von Personen oder an ein Datenbank-Ergebnis gebunden werden.

Dabei gibt es zwei wichtige Bestandteile:

- **Binding Target:** Das Items Control, beispielsweise eine `ListBox`.
    
- **Binding Source:** Die Sammlung von Objekten.
    

Die Sammlung wird über die Eigenschaft `ItemsSource` an das Steuerelement gebunden.

### Beispiel

```
<ListBox ItemsSource="{Binding Source={StaticResource list}}"/>
```

Hier wird die Sammlung mit dem Schlüssel `list` als Datenquelle verwendet.

## Understanding Observable Collections

Eine normale Sammlung erkennt nicht automatisch, wenn Elemente hinzugefügt oder entfernt werden.

Eine Observable Collection kann solche Änderungen melden.

Dafür implementiert sie das Interface:

`INotifyCollectionChanged`

Wenn sich die Sammlung verändert, wird das Event `CollectionChanged` ausgelöst.

Beispiel:

- Eine neue Person wird hinzugefügt.
    
- Ein Element wird entfernt.
    
- Die Sammlung verändert sich.
    
- Das gebundene UI-Element kann auf diese Änderung reagieren.
    

**Wichtig:** `ObservableCollection<T>` sorgt dafür, dass Änderungen an der Sammlung an gebundene Steuerelemente weitergegeben werden.

## Defining an Observable Collection Class

Eine eigene Observable Collection wird erstellt, indem eine Klasse von `ObservableCollection<T>` erbt.

### Beispiel

```
using System.Collections.ObjectModel;

public class NameList : ObservableCollection<Person>
{
    // Hier können zusätzliche Methoden definiert werden.
}

public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

Die Klasse `NameList` enthält mehrere Objekte vom Typ `Person`.

### Observable Collection in XAML verwenden

Zuerst wird die Collection als Resource definiert:

```
<Window
    xmlns:c="clr-namespace:MySample">

    <Window.Resources>
        <c:NameList x:Key="list"/>
    </Window.Resources>

    <ListBox ItemsSource="{Binding Source={StaticResource list}}"/>

</Window>
```

- `xmlns:c`: Verweist auf den Namespace der eigenen Klasse.
    
- `NameList`: Die Observable Collection.
    
- `x:Key`: Der Schlüssel der Resource.
    
- `ItemsSource`: Verbindet die ListBox mit der Sammlung.
    

---

# Lesson 2 – Using Collection Views

## Understanding Collection Views

Eine Collection View ermöglicht es, die Darstellung einer Sammlung zu verändern, ohne die ursprüngliche Sammlung selbst zu verändern.

Mit einer Collection View können Daten:

- Sortiert werden (Sort).
    
- Gefiltert werden (Filter).
    
- Gruppiert werden (Group).
    

Die ursprüngliche Sammlung bleibt dabei bestehen.

## Creating and Using a Collection View

Eine Collection View kann über `CollectionViewSource` erstellt werden.

Dafür sind zwei Schritte notwendig:

1. Eine `CollectionViewSource` als Resource definieren.
    
2. Ein UI-Control an diese Resource binden.
    

### Beispiel

```
<Window.Resources>

    <CollectionViewSource
        Source="{Binding Source={x:Static Application.Current},
        Path=AuctionItems}"
        x:Key="listView"/>

</Window.Resources>

<ListBox
    ItemsSource="{Binding Source={StaticResource listView}}"/>
```

- `CollectionViewSource`: Erstellt eine Collection View.
    
- `Source`: Gibt die ursprüngliche Sammlung an.
    
- `x:Key`: Schlüssel der Resource.
    
- `ItemsSource`: Bindet die ListBox an die Collection View.
    

## Sorting Data by Using a Collection View

Mit `SortDescriptions` können Elemente einer Collection View sortiert werden.

Dafür wird ein `SortDescription`-Objekt erstellt und zur Sammlung `SortDescriptions` hinzugefügt.

### Beispiel

```
view.SortDescriptions.Add(
    new SortDescription(
        "CategoryName",
        ListSortDirection.Ascending
    )
);

view.SortDescriptions.Add(
    new SortDescription(
        "ProductName",
        ListSortDirection.Ascending
    )
);
```

Hier wird zuerst nach `CategoryName` und anschließend nach `ProductName` sortiert.

### Sortierrichtungen

|Wert|Bedeutung|
|---|---|
|`Ascending`|Aufsteigend|
|`Descending`|Absteigend|

## Filtering Data by Using a Collection View

Mit einem Filter können bestimmte Elemente ausgeblendet werden.

Dafür wird ein Handler für das `Filter`-Event implementiert.

Der Handler entscheidet, ob ein Element angezeigt werden soll.

### Beispiel

```
listView.Filter += new FilterEventHandler(ShowBargains);

private void ShowBargains(object s, FilterEventArgs e)
{
    Product p = e.Item as Product;

    if (p != null)
    {
        if (p.CurrentPrice >= 25)
            e.Accepted = false;
        else
            e.Accepted = true;
    }
}
```

### Erklärung

- `FilterEventHandler`: Verbindet den Filter mit einer Methode.
    
- `e.Item`: Das aktuell überprüfte Element.
    
- `e.Accepted = true`: Das Element wird angezeigt.
    
- `e.Accepted = false`: Das Element wird ausgeblendet.
    

Im Beispiel werden nur Produkte mit einem Preis unter 25 angezeigt.

## Grouping Data by Using a Collection View

Collection Views unterstützen auch die Gruppierung von Elementen.

Dabei werden Elemente anhand gemeinsamer Eigenschaften in Gruppen zusammengefasst.

Beispiel:

Produkte können nach ihrer Kategorie gruppiert werden.

Die Präsentation nennt das Gruppieren als Funktion der Collection View, enthält aber keine konkrete Codeimplementierung dazu.

---

# Lesson 3 – Creating Master-Detail User Interfaces

## Understanding Master-Detail User Interfaces

Eine Master-Detail-Oberfläche stellt eine Beziehung zwischen einer übergeordneten Auswahl und den dazugehörigen Detailinformationen dar.

Sie wird verwendet, um eine sogenannte One-to-Many-Beziehung darzustellen.

Beispiel:

- Master: Eine Liste mit Kunden.
    
- Detail: Die Bestellungen des ausgewählten Kunden.
    

### Eigenschaften von Master-Detail-Oberflächen

- Stellen eine One-to-Many-Beziehung dar.
    
- Sind eine Form der Filterung.
    
- Ermöglichen die Navigation durch mehrere Elemente.
    

Ein Beispiel für die Umsetzung in WPF ist die Verwendung eines `DataGrid`-Controls.

---

# Lesson 4 – Using Data Templates

## Understanding Data Templates

Ein Data Template legt fest, wie ein Datenobjekt in der Benutzeroberfläche dargestellt wird.

Ohne Data Template kann beispielsweise der Klassenname eines Objekts angezeigt werden.

Mit einem Data Template kann festgelegt werden, welche Eigenschaften sichtbar sein sollen und wie sie angeordnet werden.

Beispiel:

Statt `MySample.Person` werden die Eigenschaften einer Person angezeigt:

- Vorname
    
- Nachname
    
- Alter
    

## Defining and Using a Data Template

Ein Data Template wird mit dem Element `DataTemplate` definiert.

Anschließend wird es beispielsweise über `ItemTemplate` einem Items Control zugewiesen.

### Beispiel

```
<ListBox ItemsSource="{Binding Source={StaticResource list}}">

    <ListBox.ItemTemplate>

        <DataTemplate>
            <StackPanel>

                <TextBlock Text="{Binding Path=FirstName}"/>

                <TextBlock Text="{Binding Path=LastName}"/>

            </StackPanel>
        </DataTemplate>

    </ListBox.ItemTemplate>

</ListBox>
```

### Erklärung

- `DataTemplate`: Definiert die Darstellung eines Objekts.
    
- `ItemTemplate`: Legt fest, welches Template für jedes Listenelement verwendet wird.
    
- `StackPanel`: Ordnet die Elemente untereinander an.
    
- `TextBlock`: Zeigt die Eigenschaften des Objekts an.
    
- `Binding Path`: Greift auf die Eigenschaften des jeweiligen Objekts zu.
    

## Defining a Data Template as a Resource

Ein Data Template kann auch als Resource definiert werden.

Dadurch kann es mehrfach verwendet werden.

### Beispiel

```
<Window.Resources>

    <DataTemplate x:Key="myDataTemplate">

        <StackPanel>

            <TextBlock Text="{Binding Path=FirstName}"/>

            <TextBlock Text="{Binding Path=LastName}"/>

        </StackPanel>

    </DataTemplate>

</Window.Resources>

<ListBox
    ItemsSource="{Binding Source={StaticResource list}}"
    ItemTemplate="{StaticResource myDataTemplate}"/>
```

### Wichtige Eigenschaften

- `x:Key`: Gibt dem Template einen eindeutigen Schlüssel.
    
- `DataType`: Kann verwendet werden, um ein Template einem bestimmten Datentyp zuzuordnen.
    
- `ItemTemplate`: Verwendet das Template für die Elemente eines Items Controls.
    
- `ContentTemplate`: Verwendet ein Template für den Inhalt eines Content Controls.
    

## Using Data Triggers in a Data Template

Mit einem Data Trigger kann die Darstellung eines Elements abhängig von einem Datenwert verändert werden.

Beispiel:

Ein Element soll blau dargestellt werden, wenn das Geschlecht den Wert `Male` hat.

### Schritte

1. Ein `DataTrigger`-Element definieren.
    
2. Die Eigenschaften `Binding` und `Value` setzen.
    
3. Mit `Setter` die gewünschte Eigenschaft verändern.
    

### Beispiel

```
<DataTemplate x:Key="myDataTemplate">

    <DataTemplate.Triggers>

        <DataTrigger
            Binding="{Binding Path=Gender}"
            Value="Male">

            <Setter
                TargetName="border"
                Property="Foreground"
                Value="Blue"/>

        </DataTrigger>

    </DataTemplate.Triggers>

</DataTemplate>
```

- `DataTrigger`: Prüft einen bestimmten Datenwert.
    
- `Binding`: Gibt an, welche Eigenschaft überprüft wird.
    
- `Value`: Der Wert, bei dem der Trigger ausgelöst wird.
    
- `Setter`: Legt fest, welche Eigenschaft verändert wird.
    
- `TargetName`: Gibt das Ziel-Element an.
    

---

# Prüfungswissen – Das solltest du können

## Collections

- Erklären können, wie eine Collection an eine ListBox gebunden wird.
    
- `ItemsSource` kennen.
    
- Den Unterschied zwischen einer normalen Collection und `ObservableCollection<T>` erklären.
    
- Wissen, wofür `INotifyCollectionChanged` verwendet wird.
    
- Eine eigene Klasse von `ObservableCollection<T>` ableiten können.
    

## Collection Views

- Erklären können, was eine Collection View macht.
    
- Die drei Funktionen Sortieren, Filtern und Gruppieren kennen.
    
- Wissen, wofür `CollectionViewSource` verwendet wird.
    
- `SortDescriptions` und `SortDescription` kennen.
    
- `Ascending` und `Descending` unterscheiden.
    
- Wissen, wie `FilterEventHandler` und `e.Accepted` funktionieren.
    

## Master-Detail

- Erklären können, was eine Master-Detail-Oberfläche ist.
    
- Wissen, was eine One-to-Many-Beziehung bedeutet.
    
- Ein Beispiel für eine Master-Detail-Oberfläche nennen können.
    

## Data Templates

- Erklären können, warum Data Templates verwendet werden.
    
- Wissen, wofür `DataTemplate` und `ItemTemplate` verwendet werden.
    
- Ein Data Template als Resource definieren und wiederverwenden können.
    
- `DataTrigger`, `Binding`, `Value` und `Setter` erklären können.
    

---

# Merksätze

- **ItemsSource:** Verbindet ein Items Control mit einer Sammlung.
    
- **ObservableCollection<T>:** Meldet Änderungen an der Sammlung.
    
- **INotifyCollectionChanged:** Ermöglicht Benachrichtigungen über Collection-Änderungen.
    
- **CollectionViewSource:** Erstellt eine Ansicht auf eine Sammlung.
    
- **SortDescriptions:** Legt die Sortierung fest.
    
- **Filter:** Entscheidet, welche Elemente angezeigt werden.
    
- **e.Accepted:** Bestimmt, ob ein Element den Filter passiert.
    
- **Grouping:** Fasst Elemente in Gruppen zusammen.
    
- **Master-Detail:** Zeigt zu einer Auswahl passende Detailinformationen.
    
- **DataTemplate:** Legt fest, wie ein Datenobjekt dargestellt wird.
    
- **ItemTemplate:** Verwendet ein Data Template für Listenelemente.
    
- **DataTrigger:** Verändert die Darstellung abhängig von einem Datenwert.
    
- **Setter:** Legt fest, welche Eigenschaft durch einen Trigger verändert wird.