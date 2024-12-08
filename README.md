
# **README: Funktionale Programmierkonzepte**

Dieses Dokument erklärt die wichtigsten Konzepte der funktionalen Programmierung. Ziel ist es, die Theorie verständlich zu machen und zu zeigen, wie du diese Konzepte in der Praxis anwendest.

---

## **1. Reine Funktionen (Pure Functions)**

### **Definition**
Eine reine Funktion ist eine Funktion, die:
1. **Deterministisch ist**: Gleiche Eingaben führen immer zu denselben Ausgaben.
2. **Keine Seiteneffekte hat**: Sie ändert keine globalen Variablen, greift nicht auf externe Datenquellen zu und beeinflusst nichts ausserhalb ihres Scopes.

### **Vorteile**
- **Einfach zu testen**: Du kannst Eingaben und Ausgaben isoliert überprüfen.  
- **Vorhersehbares Verhalten**: Keine versteckten Abhängigkeiten, da alles nur von den Parametern abhängt.  
- **Einfache Fehlersuche**: Da die Funktion keine Seiteneffekte hat, kannst du Fehler schnell finden.

### **Beispiel**
```csharp
// Pure Function
int Add(int a, int b) => a + b;

// Eingabe: a = 2, b = 3
// Ausgabe: 5
```

**Nicht reine Funktion (Impure Function):**
```csharp
int AddAndChangeGlobal(int a, int b)
{
    globalVar = a + b; // Ändert eine globale Variable (Seiteneffekt)
    return globalVar;
}
```

Diese Funktion ist nicht rein, da sie eine globale Variable beeinflusst. Änderungen an `globalVar` können zu schwer auffindbaren Fehlern führen.

---

## **2. Immutabilität**

### **Definition**
Immutabilität bedeutet, dass Daten nach ihrer Erstellung **nicht verändert werden**. Jede "Änderung" erzeugt eine neue Kopie der Daten.

### **Vorteile**
- **Datenintegrität**: Daten bleiben unverändert, was unabsichtliche Änderungen verhindert.  
- **Parallele Programmierung**: Unveränderliche Daten können sicher von mehreren Threads verwendet werden.  
- **Vorhersehbares Verhalten**: Du weisst, dass Daten sich nicht verändern.

### **Beispiel**
```csharp
// Mutable List (Problematisch)
var list = new List<int> { 1, 2, 3 };
list[0] = 42; // Ändert das Original

// Immutable Example
var list = new List<int> { 1, 2, 3 };
var newList = list.Select(x => x * 2).ToList(); // Neue Kopie erstellen
```

---

## **3. Funktionsverkettung (Function Chaining)**

### **Definition**
Bei der Funktionsverkettung wird die Ausgabe einer Funktion direkt als Eingabe der nächsten Funktion verwendet.

### **Vorteile**
- **Lesbarer Code**: Transformationen sind in einer einzigen Kette sichtbar.  
- **Keine unnötigen Variablen**: Alles passiert inline.

### **Beispiel**
```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };

var result = numbers
    .Where(n => n > 2)   // Filtere Zahlen > 2
    .Select(n => n * 2)  // Verdopple jede Zahl
    .OrderBy(n => n)     // Sortiere
    .ToList();           // Ergebnis: [6, 8, 10]

Console.WriteLine(string.Join(", ", result));
```

---

## **4. Currying**

### **Definition**
Currying wandelt eine Funktion mit mehreren Parametern in eine Serie von Funktionen um, die jeweils **einen Parameter** akzeptieren.

### **Vorteile**
- **Wiederverwendbarkeit**: Du kannst "Teile" der Funktion fixieren, um neue Funktionen zu erstellen.  
- **Lesbarkeit**: Komplexe Funktionen werden in kleinere, verständlichere Teile zerlegt.

### **Beispiel**
```csharp
// Currying-Funktion
Func<int, Func<int, int>> Add = x => y => x + y;

var add5 = Add(5);  // Erstellt eine Funktion, die 5 zu allem hinzufügt
Console.WriteLine(add5(3)); // Ausgabe: 8
```

---

## **5. Funktionen höherer Ordnung (Higher-Order Functions)**

### **Definition**
Eine Funktion ist "höherer Ordnung", wenn sie:
1. **Andere Funktionen als Parameter akzeptiert**, oder  
2. **Eine Funktion zurückgibt.**

### **Vorteile**
- **Flexibilität**: Funktionen können kombiniert und wiederverwendet werden.  
- **Weniger Code**: Du kannst generische Logik für viele Anwendungsfälle schreiben.

### **Beispiel**
```csharp
// Höhere Ordnung: Nimmt eine Funktion und ein Array
Func<int, int> square = x => x * x;

Func<int[], int[]> applyFunc = arr => arr.Select(square).ToArray();

var result = applyFunc(new[] { 1, 2, 3 }); // Ergebnis: [1, 4, 9]
```

---

## **6. Pattern Matching**

### **Definition**
Pattern Matching vergleicht Daten mit bestimmten Mustern und führt basierend darauf Operationen aus.

### **Vorteile**
- **Klarheit**: Komplexe Bedingungen werden einfacher zu lesen.  
- **Weniger Code**: Spart lange `if`- oder `switch`-Statements.

### **Beispiel**
```csharp
string CheckNumber(int number) => number switch
{
    < 0 => "Negativ",
    0 => "Null",
    > 0 => "Positiv"
};

Console.WriteLine(CheckNumber(-3)); // Ausgabe: Negativ
Console.WriteLine(CheckNumber(0));  // Ausgabe: Null
```

---

## **Zusammenfassung**

Diese Konzepte sind nicht nur theoretisch nützlich, sondern helfen dir dabei, **robusteren, wartbaren und testbaren Code** zu schreiben. Wenn du reine Funktionen, Immutabilität und Funktionsverkettung anwendest, kannst du Fehlerquellen minimieren und deinen Code einfacher verstehen.
