# **PDC-Online Infos**

1. [Ternären Operator](#1-ternären-operator) <br>
    1.1 [Ternären Operator Beispiel](#ternären-operator-beispiel) <br>
    1.2 [Ternären Operator Erklärung](#ternären-operator-erklärung) <br>
2. [Unsterschied Task und Value Task](#2-unsterschied-task-und-value-task) <br>
    2.1 [Unsterschied Task und Value Task Beispiel](#unsterschied-task-und-value-task-beispiel) <br>
    2.2 [Unsterschied Task und Value Task Erklärung](#unsterschied-task-und-value-task-erklärung) <br>
3. [Was ist Blazor](#3-was-ist-blazor) <br>
    3.1 [Blazor Erklärung](#blazor-erklärung) <br>
    3.2 [Blazor Beispiel](#beispiel-einfacher-zähler-in-blazor) <br>
4. [LocalStorage Blazor](#localstorage-beispiel) <br>
    4.1 [LocalStorage Blazor Beispiel](#localstorage-beispiel) <br>
    4.2 [LocalStorage Blazor Erklärung](#ternären-operator-erklärung) <br>
5. [Blazor Statistik](#5-blazor-statistik) <br>
    5.1 [Blazor Stastik Beisiel](#blazor-stastik-beisiel) <br>
    5.2 [Blazor Statisk Erklärung](#blazor-statisk-erklärung) <br>

## 1. Ternären Operator

### Ternären Operator Beispiel:

```csharp
int num1 = 10;
int num2 = 5;

int max = (num1 > num2) ? num1 : num2;
```

###  Ternären Operator Erklärung:

Der Ternäre Operator, auch als bedingter Operator bezeichnet, ist in C# eine kompakte Möglichkeit, eine bedingte Anweisung auszudrücken. Sein Format lautet:

```csharp
bedingung ? ausdruck_wenn_wahr : ausdruck_wenn_falsch;
```
Im obigen Beispiel haben wir zwei Variablen num1 und num2, die mit den Werten 10 und 5 initialisiert sind. Der Ternäre Operator wird verwendet, um den größeren Wert der beiden Zahlen zu finden. Die Bedingung (num1 > num2) wird überprüft: Wenn sie wahr ist, wird num1 zurückgegeben, andernfalls wird num2 zurückgegeben. Das Ergebnis dieser Bedingung wird der Variablen max zugewiesen.

In diesem Fall ist die Bedingung num1 > num2 wahr, da 10 größer ist als 5. Daher wird der Wert von num1 (also 10) der Variablen max zugewiesen. Nach der Ausführung enthält die Variable max den Wert 10.


## 2. Unsterschied Task und Value Task

### Unsterschied Task und Value Task Beispiel:

```csharp
using System;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        // Beispiel mit Task
        Console.WriteLine("Task Beispiel:");
        Task<int> task = CalculateAsync(5);
        Console.WriteLine("Vor await: Task läuft im Hintergrund.");
        int result = await task;
        Console.WriteLine($"Ergebnis von CalculateAsync: {result}");
        Console.WriteLine();

        // Beispiel mit ValueTask
        Console.WriteLine("ValueTask Beispiel:");
        ValueTask<int> valueTask = CalculateValueAsync(7);
        Console.WriteLine("Vor await: ValueTask läuft im Hintergrund.");
        int valueResult = await valueTask;
        Console.WriteLine($"Ergebnis von CalculateValueAsync: {valueResult}");
    }

    static async Task<int> CalculateAsync(int value)
    {
        Console.WriteLine("CalculateAsync gestartet.");
        await Task.Delay(1000); // Simuliert eine asynchrone Berechnung
        Console.WriteLine("CalculateAsync beendet.");
        return value * 2;
    }

    static async ValueTask<int> CalculateValueAsync(int value)
    {
        Console.WriteLine("CalculateValueAsync gestartet.");
        await Task.Delay(1000); // Simuliert eine asynchrone Berechnung
        Console.WriteLine("CalculateValueAsync beendet.");
        return value * 3;
    }
}
```
### Unsterschied Task und Value Task Erklärung:

In diesem Beispiel gibt es zwei Methoden, CalculateAsync und CalculateValueAsync, die beide eine asynchrone Berechnung simulieren. Die CalculateAsync-Methode gibt eine Task<int> zurück, während die CalculateValueAsync-Methode eine ValueTask<int> zurückgibt.

Der Hauptunterschied zwischen Task und ValueTask liegt darin, wie sie mit den Ressourcen umgehen. Task ist ein allgemeines Konstrukt, das im Arbeitsspeicher Objekte erstellt und verwaltet, während ValueTask dazu optimiert ist, weniger Ressourcen zu verbrauchen, indem es so oft wie möglich den Speicherplatz wiederverwendet.

In diesem Beispiel wird die CalculateAsync-Methode eine Task<int> zurückgeben, während die CalculateValueAsync-Methode eine ValueTask<int> zurückgibt. Beide Methoden haben ähnliche asynchrone Verhaltensweisen, aber ValueTask wird bevorzugt, wenn die Methode in der Regel synchron beendet wird oder bereits abgeschlossen ist, um unnötige Speicherzuweisungen zu vermeiden.

## 3 Was ist Blazor

### Blazor Erklärung

Blazor ist ein Open-Source-Framework von Microsoft, das die Entwicklung von interaktiven Webanwendungen mithilfe von C# ermöglicht. Es gibt zwei Hauptvarianten:

1. Clientseitiges Blazor (WebAssembly): C#-Code wird in WebAssembly übersetzt, um Webanwendungen im Browser auszuführen.

2. Serverseitiges Blazor: Hier läuft die Anwendungslogik auf dem Server, während die Benutzeroberfläche im Browser gerendert wird.

### Beispiel: Einfacher Zähler in Blazor

```csharp
@page "/counter"

<h3>Counter</h3>

<p>Current count: @count</p>
<button class="btn btn-primary" @onclick="IncrementCounter">Increment</button>

@code {
    private int count = 0;

    private void IncrementCounter()
    {
        count++;
    }
}
````

Dieses Beispiel zeigt eine Blazor-Komponente, die einen Zähler darstellt. Der Zählerwert wird angezeigt, und ein Klick auf den "Increment"-Button erhöht den Wert. Blazor ermöglicht die Verwendung von C# für die Entwicklung von Webanwendungen, sei es clientseitig oder serverseitig.


## 4. LocalStorage 

### LocalStorage Beispiel:

LocalStorageService in Blazor, um auf den LocalStorage zuzugreifen. Beachte, dass du einen eigenen LocalStorageService erstellen müsstest, um auf den LocalStorage zuzugreifen. Hier ist eine einfache Umsetzung:

```csharp
using System.Threading.Tasks;
using Microsoft.AspNetCore.Components;
using Microsoft.JSInterop;

namespace BlazorLocalStorageExample.Services
{
    public interface ILocalStorageService
    {
        Task<string> GetItemAsync(string key);
        Task SetItemAsync(string key, string value);
    }

    public class LocalStorageService : ILocalStorageService
    {
        private readonly IJSRuntime _jsRuntime;

        public LocalStorageService(IJSRuntime jsRuntime)
        {
            _jsRuntime = jsRuntime;
        }

        public async Task<string> GetItemAsync(string key)
        {
            return await _jsRuntime.InvokeAsync<string>("localStorage.getItem", key);
        }

        public async Task SetItemAsync(string key, string value)
        {
            await _jsRuntime.InvokeVoidAsync("localStorage.setItem", key, value);
        }
    }
}
```

Verwende nun diesen LocalStorageService in deinen Blazor-Komponenten:

```csharp
@page "/localstorage-example"
@inject ILocalStorageService LocalStorageService

<h3>LocalStorage Beispiel in Blazor</h3>

<button @onclick="SaveToLocalStorage">In LocalStorage speichern</button>
<button @onclick="LoadFromLocalStorage">Aus LocalStorage laden</button>

@if (!string.IsNullOrEmpty(savedValue))
{
    <p>Wert aus LocalStorage: @savedValue</p>
}

@code {
    private string savedValue = "";

    private async Task SaveToLocalStorage()
    {
        await LocalStorageService.SetItemAsync("myKey", "Hallo von Blazor!");
        savedValue = "Gespeichert!";
    }

    private async Task LoadFromLocalStorage()
    {
        savedValue = await LocalStorageService.GetItemAsync("myKey");
    }
}
```

### LocalStorage Erklärung: 


Hier wird ein Interface namens ILocalStorageService definiert, das zwei Methoden deklariert: GetItemAsync und SetItemAsync.
Dieses Interface dient als Vertrag für die Methoden, die der LocalStorageService implementieren wird.
LocalStorageService Klasse:

Hier wird die Klasse LocalStorageService definiert, die das ILocalStorageService-Interface implementiert.
In ihrem Konstruktor erhält sie eine Instanz von IJSRuntime, was die Blazor-spezifische Schnittstelle für die Ausführung von JavaScript-Code ist.
Die GetItemAsync-Methode ruft mithilfe von IJSRuntime die JavaScript-Methode localStorage.getItem auf, um einen Wert aus dem LocalStorage abzurufen.
Die SetItemAsync-Methode verwendet ebenfalls IJSRuntime, um die JavaScript-Methode localStorage.setItem aufzurufen und einen Wert im LocalStorage zu speichern.
Blazor-Komponente (localstorage-example.razor):

Die Blazor-Komponente wird über die @page-Direktive auf /localstorage-example geroutet.
Das ILocalStorageService wird über das @inject-Directive in die Komponente injiziert, um auf den LocalStorage zuzugreifen.
Die Komponente enthält zwei Buttons, die jeweils die Methoden SaveToLocalStorage und LoadFromLocalStorage aufrufen.
SaveToLocalStorage: Ruft die SetItemAsync-Methode des LocalStorageService auf, um einen Wert im LocalStorage zu speichern.
LoadFromLocalStorage: Ruft die GetItemAsync-Methode des LocalStorageService auf, um einen Wert aus dem LocalStorage abzurufen und in der savedValue-Variable zu speichern.
Der Wert von savedValue wird in der Ansicht angezeigt, wenn er nicht leer ist.
In diesem Beispiel wurde ein Service erstellt, um den Zugriff auf den LocalStorage in Blazor zu abstrahieren. Die Blazor-Komponente selbst interagiert nur mit dem Service und ist somit unabhängig von den Details der JavaScript-Interoperabilität. Dies fördert eine saubere Trennung der Verantwortlichkeiten und verbessert die Wartbarkeit des Codes.

## 5. Blazor Statistik 

### Blazor Stastik Beisiel

```csharp

<div class="col-12 col-xxl-12">
    <!-- Title and Dropdown -->
    <RadzenText TextStyle="TextStyle.H6" Class="rz-color-primary">
        <RadzenIcon Icon="show_chart" /> @CustomText.NewCars
    </RadzenText>
    <RadzenDropDown @bind-Value="selectedCategory" Data="@CarCategories" 
    Change="@(() => ChangeCategory(selectedCategory))" TextProperty="Name" ValueProperty="Name" />

    <!-- Chart -->
    <RadzenChart @ref="chart">
        @if (CarStatistic.Count == 0)
        {
            InitCarStatistic(selectedCategory);
        }
        @if (CarStatistic.Count > 0)
        {
            @foreach (var car in CarStatistic)
            {
                <!-- Column Series for Cars -->
                <RadzenColumnSeries Data=@car.Value 
                Title="@car.Key" CategoryProperty="Car" ValueProperty="Leads">
                    <RadzenSeriesDataLabels Visible="@showDataLabels" />
                </RadzenColumnSeries>
                
                <!-- Column Options -->
                <RadzenColumnOptions Width="20" />

                <!-- Category Axis -->
                <RadzenCategoryAxis Padding="0" StrokeWidth="2">
                    <RadzenGridLines Visible="true" />
                </RadzenCategoryAxis>

                <!-- Value Axis -->
                <RadzenValueAxis Min="0">
                    <RadzenGridLines Visible="true" />
                    <RadzenAxisTitle Text=@CustomText.Leads />
                </RadzenValueAxis>
            }
        }
    </RadzenChart>
</div>
```

### Blazor Statisk Erklärung

In diesem Beispiel wurde die Methode InitCarStatistic hinzugefügt, um die Initialisierung der Statistikdaten zu übernehmen. Diese Methode wird aufgerufen, wenn noch keine Statistikdaten für die ausgewählte Kategorie vorhanden sind.

Die Methode InitCarStatistic nutzt die übergebene Kategorie, um die entsprechenden Daten auszuwählen und die Statistikdaten für die Anzeige vorzubereiten. Dies geschieht anstelle des direkt im HTML-Code eingefügten Logikblocks. Dadurch bleibt der HTML-Code übersichtlicher und die Logik ist in einer separaten Methode organisiert.

Bitte beachte, dass die Methodenimplementierung und die Datenstrukturen (wie MvCategory, MvCar, InterestCategorie, etc.) in deinem C#-Code bereitgestellt werden müssen. Diese werde ich nicht zeigen weil ich nicht Firmengeheimnisse preisgeben will.

