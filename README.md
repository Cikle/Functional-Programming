# Functional-Programming

1. Pure Functions (Reine Funktionen)
Was genau sind pure Funktionen?

Stell dir eine Funktion wie eine mathematische Gleichung vor:

    Sie nimmt Eingaben (Parameter).
    Sie führt eine Berechnung durch.
    Sie gibt ein Ergebnis zurück, ohne andere Teile des Programms zu verändern.

Eine pure Funktion bedeutet:

    Deterministisch: Gleiche Eingabe → Immer gleiche Ausgabe.
    Beispiel: Die Funktion Add(2, 3) gibt immer 5 zurück, unabhängig von äusseren Umständen.
    Keine Seiteneffekte: Eine Funktion darf keine globalen Variablen ändern, keine Daten schreiben oder lesen (z. B. aus einer Datei), und auch keine UI verändern.

Warum sind pure Funktionen wichtig?

    Einfaches Testen: Du kannst vorhersagen, was eine Funktion tut, weil sie immer gleich arbeitet.
    → Beispiel: Wenn ein Bug auftritt, kannst du sofort die Funktion isolieren und testen.
    Vermeidung von Bugs: Es gibt keine "versteckten" Änderungen an globalen Variablen oder Daten.
    Einfaches Debugging: Da die Funktion nur von ihrer Eingabe abhängt, ist der Fehler leichter zu finden.

Beispiele:

Pure Funktion:

int Add(int a, int b) => a + b; 

// Eingabe: a = 2, b = 3 → Ausgabe: 5

Warum ist sie rein?

    Die Ausgabe (a + b) hängt nur von den Eingaben ab.
    Es gibt keine globalen Variablen, die verändert werden.

Unreine Funktion (impure):

int AddAndChangeGlobal(int a, int b)
{
    globalVar = a + b; // Ändert eine globale Variable (Seiteneffekt)
    return globalVar;
}

Warum ist sie nicht rein?

    Sie ändert eine globale Variable globalVar.
    Das Ergebnis hängt nicht nur von a und b ab, sondern auch von globalVar.

2. Immutabilität
Was ist das genau?

Immutabilität bedeutet, dass Daten unveränderlich sind. Wenn du Daten ändern möchtest, erstellst du eine neue Kopie der Daten anstelle der Änderung der Originaldaten.
Warum ist Immutabilität wichtig?

    Datenintegrität: Keine unabsichtlichen Änderungen.
    Beispiel: Stell dir vor, du arbeitest mit einer Liste. Wenn jemand die Liste "still und heimlich" ändert, kann es schwer sein, Bugs zu finden.
    Einfaches Debugging: Wenn Daten unveränderlich sind, weisst du, dass sie sich nach ihrer Erstellung nicht verändern.
    Parallele Programmierung: Mehrere Threads können sicher mit denselben Daten arbeiten.

Beispiele:

Mutierbare Daten (Problem):

var list = new List<int> { 1, 2, 3 };
list[0] = 42; // Ändert das Original

Wenn mehrere Funktionen dieselbe Liste benutzen, könnte dies zu unerwarteten Problemen führen.

Immutable Beispiel:

var list = new List<int> { 1, 2, 3 };
var newList = list.Select(x => x * 2).ToList(); // Erstelle eine neue Liste

Console.WriteLine(string.Join(", ", list));    // Original: 1, 2, 3
Console.WriteLine(string.Join(", ", newList)); // Neu: 2, 4, 6

3. Function Chaining (Funktionsverkettung)
Was ist das?

Bei Function Chaining verkettest du mehrere Funktionen, indem du die Ausgabe einer Funktion direkt als Eingabe für die nächste Funktion nutzt.
Warum ist das wichtig?

    Lesbarer Code: Anstatt viele Zwischenschritte zu speichern, kannst du die Transformation direkt nachvollziehen.
    Weniger Fehleranfällig: Du veränderst keine globalen Variablen, da alles in einer Kette passiert.

Beispiel:

Du möchtest:

    Zahlen filtern (> 2).
    Jede Zahl verdoppeln.
    Die Zahlen sortieren.

Mit Funktionsverkettung sieht das so aus:

var numbers = new List<int> { 1, 2, 3, 4, 5 };

var result = numbers
    .Where(n => n > 2)   // Filtere Zahlen > 2
    .Select(n => n * 2)  // Verdopple jede Zahl
    .OrderBy(n => n)     // Sortiere
    .ToList();           // Ergebnis: [6, 8, 10]

Console.WriteLine(string.Join(", ", result));

4. Currying
Was ist Currying?

Currying wandelt eine Funktion, die mehrere Parameter hat, in eine Reihe von Funktionen um, die jeweils nur einen Parameter akzeptieren.
Warum ist das wichtig?

    Wiederverwendbarkeit: Du kannst eine Funktion mit einem festen Parameter "vorbereiten".
    Beispiel: Eine Steuerberechnung (TaxCalculator) für eine feste Steuer (19%).

Beispiel:

// Currying-Funktion
Func<int, Func<int, int>> Add = x => y => x + y;

var add5 = Add(5);  // Erstellt eine neue Funktion, die 5 zu allem hinzufügt
Console.WriteLine(add5(3)); // 8
Console.WriteLine(add5(10)); // 15

5. Higher-Order Functions
Was ist das?

Eine Funktion ist "höherer Ordnung", wenn sie:

    Andere Funktionen als Parameter nimmt, oder
    Eine Funktion zurückgibt.

Warum ist das wichtig?

    Du kannst flexibel Funktionen kombinieren und Code wiederverwenden.
    Sie ermöglichen komplexe Logik mit wenig Code.

Beispiel:

Func<int, int> square = x => x * x;

Func<int[], int[]> applyFunc = arr => arr.Select(square).ToArray();

var result = applyFunc(new[] { 1, 2, 3 }); // Ergebnis: [1, 4, 9]

Hier wird applyFunc verwendet, um beliebige Funktionen wie square auf ein Array anzuwenden.
6. Pattern Matching
Was ist das?

Pattern Matching erlaubt dir, Daten oder Zustände direkt zu vergleichen und basierend darauf Aktionen auszuführen.
Warum ist das wichtig?

    Weniger Code: Du brauchst keine langen if- oder switch-Statements.
    Klarheit: Dein Code ist strukturierter und einfacher zu lesen.

Beispiel:

string CheckNumber(int number) => number switch
{
    < 0 => "Negativ",
    0 => "Null",
    > 0 => "Positiv"
};

Console.WriteLine(CheckNumber(-3)); // Negativ
Console.WriteLine(CheckNumber(0));  // Null
