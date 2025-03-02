---
title: Konditionale
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Korrektes Schreiben von Programmen, die if- und else-Anweisungen und einfache
  boolesche Ausdrücke (ohne logische Operatoren) verwenden.
- Verfolgen Sie die Ausführung von nicht verschachtelten Konditionalen und Konditionalen
  in Schleifen.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie können Programme verschiedene Dinge für verschiedene Daten tun?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Benutze `if` Anweisungen, um zu kontrollieren, ob ein Codeblock ausgeführt wird oder nicht.

- Eine `if`-Anweisung (richtiger: eine *bedingte* Anweisung) steuert, ob ein Codeblock
  ausgeführt wird oder nicht.
- Die Struktur ähnelt der einer `for`-Anweisung:
  - Die erste Zeile beginnt mit `if` und endet mit einem Doppelpunkt
  - Körper, der eine oder mehrere Anweisungen enthält, wird eingerückt (normalerweise um
    4 Leerzeichen)

```python
mass = 3.54
if mass > 3.0:
    print(mass, 'is large')

mass = 2.07
if mass > 3.0:
    print (mass, 'is large')
```

```output
3.54 is large
```

## Konditionale Bedingungen werden oft innerhalb von Schleifen verwendet.

- Es macht wenig Sinn, eine Bedingung zu verwenden, wenn wir den Wert kennen (wie oben).
- Nützlich, wenn wir eine Sammlung zu verarbeiten haben.

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
```

```output
3.54 is large
9.22 is large
```

## Verwenden Sie `else`, um einen Codeblock auszuführen, wenn eine `if` Bedingung *nicht* wahr ist.

- `else` kann nach einem `if` verwendet werden.
- Ermöglicht die Angabe einer Alternative, die ausgeführt werden soll, wenn der `if`
  *Zweig* nicht genommen wird.

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
```

```output
3.54 is large
2.07 is small
9.22 is large
1.86 is small
1.71 is small
```

## Verwenden Sie `elif`, um zusätzliche Tests zu spezifizieren.

- Vielleicht möchten Sie mehrere Alternativen anbieten, jede mit ihrem eigenen Test.
- Verwenden Sie `elif` (kurz für "else if") und eine Bedingung, um diese anzugeben.
- Immer verbunden mit einem `if`.
- Muss vor `else` stehen (das ist der "catch all").

```python
masses = [3.54, 2.07, 9.22, 1.86, 1.71]
for m in masses:
    if m > 9.0:
        print(m, 'is HUGE')
    elif m > 3.0:
        print(m, 'is large')
    else:
        print(m, 'is small')
```

```output
3.54 is large
2.07 is small
9.22 is HUGE
1.86 is small
1.71 is small
```

## Bedingungen werden einmal getestet, in der Reihenfolge.

- Python durchläuft die Zweige der Bedingung der Reihe nach und testet sie.
- Die Reihenfolge ist also wichtig.

```python
grade = 85
if grade >= 90:
    print('grade is A')
elif grade >= 80:
    print('grade is B')
elif grade >= 70:
    print('grade is C')
```

```output
grade is B
```

- Geht *nicht* automatisch zurück und wertet neu aus, wenn sich Werte ändern.

```python
velocity = 10.0
if velocity > 20.0:
    print('moving too fast')
else:
    print('adjusting velocity')
    velocity = 50.0
```

```output
adjusting velocity
```

- Verwenden Sie oft Konditionale in einer Schleife, um die Werte von Variablen zu
  "entwickeln".

```python
velocity = 10.0
for i in range(5): # execute the loop 5 times
    print(i, ':', velocity)
    if velocity > 20.0:
        print('moving too fast')
        velocity = velocity - 5.0
    else:
        print('moving too slow')
        velocity = velocity + 10.0
print('final velocity:', velocity)
```

```output
0 : 10.0
moving too slow
1 : 20.0
moving too slow
2 : 30.0
moving too fast
3 : 25.0
moving too fast
4 : 20.0
moving too slow
final velocity: 30.0
```

## Erstellen Sie eine Tabelle mit den Werten von Variablen, um die Ausführung eines Programms zu verfolgen.

<table>
  <tr>   <td><strong>i</strong></td>   <td>0</td>   <td>.</td>   <td>1</td>   <td>.</td>   <td>2</td>   <td>.</td>   <td>3</td>   <td>.</td>   <td>4</td>   <td>.</td>
  </tr>
  <tr>   <td><strong>velocity</strong></td>   <td>10.0</td>   <td>20.0</td>   <td>.</td>   <td>30.0</td>   <td>.</td>   <td>25.0</td>   <td>.</td>   <td>20.0</td>   <td>.</td>   <td>30.0</td>
  </tr>
</table>

- Das Programm muss eine `print`-Anweisung *außerhalb* des Schleifenkörpers haben, um
  den Endwert von `velocity` anzuzeigen, da sein Wert durch die letzte Iteration der
  Schleife aktualisiert wird.

::::::::::::::::::::::::::::::::::::::::: callout

## Zusammengesetzte Beziehungen mit `and`, `or` und Klammern

Oft will man, dass eine Kombination von Dingen wahr ist. Sie können Beziehungen
innerhalb einer Bedingung mit `and` und `or` kombinieren. Um das obige Beispiel
fortzusetzen, nehmen wir an, Sie haben

```python
mass     = [ 3.54,  2.07,  9.22,  1.86,  1.71]
velocity = [10.00, 20.00, 30.00, 25.00, 20.00]

i = 0
for i in range(5):
    if mass[i] > 5 and velocity[i] > 20:
        print("Fast heavy object.  Duck!")
    elif mass[i] > 2 and mass[i] <= 5 and velocity[i] <= 20:
        print("Normal traffic")
    elif mass[i] <= 2 and velocity[i] <= 20:
        print("Slow light object.  Ignore it")
    else:
        print("Whoa!  Something is up with the data.  Check it")
```

Genau wie in der Arithmetik können und sollten Sie Klammern verwenden, wenn es eine
mögliche Mehrdeutigkeit gibt. Eine gute allgemeine Regel ist es, *immer* Klammern zu
verwenden, wenn man `and` und `or` in derselben Bedingung mischt. Das heißt, anstelle
von:

```python
if mass[i] <= 2 or mass[i] >= 5 and velocity[i] > 20:
```

schreibe eine von diesen:

```python
if (mass[i] <= 2 or mass[i] >= 5) and velocity[i] > 20:
if mass[i] <= 2 or (mass[i] >= 5 and velocity[i] > 20):
```

so ist es für den Leser (und für Python) völlig klar, was Sie wirklich meinen.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Tracing Execution

Was gibt dieses Programm aus?

```python
pressure = 71.9
if pressure > 50.0:
    pressure = 25.0
elif pressure <= 50.0:
    pressure = 0.0
print(pressure)
```

::::::::::::::: solution

## Lösung

```output
25.0
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Trimmen von Werten

Füllen Sie die Lücken aus, so dass dieses Programm eine neue Liste erstellt, die Nullen
enthält, wenn die Werte der ursprünglichen Liste negativ waren, und Einsen, wenn die
Werte der ursprünglichen Liste positiv waren.

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = ____
for value in original:
    if ____:
        result.append(0)
    else:
        ____
print(result)
```

```output
[0, 1, 1, 1, 0, 1]
```

::::::::::::::: solution

## Lösung

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = []
for value in original:
    if value < 0.0:
        result.append(0)
    else:
        result.append(1)
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Verarbeitung kleiner Dateien

Ändern Sie dieses Programm so, dass es nur Dateien mit weniger als 50 Datensätzen
verarbeitet.

```python
import glob
import pandas as pd
for filename in glob.glob('data/*.csv'):
    contents = pd.read_csv(filename)
    ____:
        print(filename, len(contents))
```

::::::::::::::: solution

## Lösung

```python
import glob
import pandas as pd
for filename in glob.glob('data/*.csv'):
    contents = pd.read_csv(filename)
    if len(contents) < 50:
        print(filename, len(contents))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Initialisierung

Ändern Sie dieses Programm so, dass es den größten und den kleinsten Wert in der Liste
findet, unabhängig davon, wie groß der ursprüngliche Wertebereich ist.

```python
values = [...some test data...]
smallest, largest = None, None
for v in values:
    if ____:
        smallest, largest = v, v
    ____:
        smallest = min(____, v)
        largest = max(____, v)
print(smallest, largest)
```

Was sind die Vor- und Nachteile dieser Methode, um den Bereich der Daten zu bestimmen?

::::::::::::::: solution

## Lösung

```python
values = [-2,1,65,78,-54,-24,100]
smallest, largest = None, None
for v in values:
    if smallest is None and largest is None:
        smallest, largest = v, v
    else:
        smallest = min(smallest, v)
        largest = max(largest, v)
print(smallest, largest)
```

Wenn Sie `== None` anstelle von `is None` geschrieben haben, funktioniert das auch, aber
Python-Programmierer schreiben immer `is None` wegen der besonderen Art und Weise, wie
`None` in dieser Sprache funktioniert.

Man kann argumentieren, dass ein Vorteil dieser Methode darin besteht, den Code lesbarer
zu machen. Ein Nachteil ist jedoch, dass dieser Code nicht effizient ist, da es
innerhalb jeder Iteration der Schleifenanweisung `for` zwei weitere Schleifen gibt, die
jeweils über zwei Zahlen laufen (die Funktionen `min` und `max`). Es wäre effizienter,
jede Zahl nur einmal zu durchlaufen:

```python
values = [-2,1,65,78,-54,-24,100]
smallest, largest = None, None
for v in values:
    if smallest is None or v < smallest:
        smallest = v
    if largest is None or v > largest:
        largest = v
print(smallest, largest)
```

Jetzt haben wir eine Schleife, aber vier Vergleichstests. Es gibt zwei Möglichkeiten,
die Schleife weiter zu verbessern: Entweder werden in jeder Iteration weniger Vergleiche
durchgeführt, oder es werden zwei Schleifen verwendet, die jeweils nur einen
Vergleichstest enthalten. Die einfachste Lösung ist oft die beste:

```python
values = [-2,1,65,78,-54,-24,100]
smallest = min(values)
largest = max(values)
print(smallest, largest)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Verwenden Sie `if`-Anweisungen, um zu kontrollieren, ob ein Codeblock ausgeführt wird
  oder nicht.
- Konditionale Bedingungen werden oft innerhalb von Schleifen verwendet.
- Verwenden Sie `else`, um einen Codeblock auszuführen, wenn eine `if` Bedingung *nicht*
  wahr ist.
- Verwenden Sie `elif`, um zusätzliche Tests zu spezifizieren.
- Die Bedingungen werden einmal in der Reihenfolge getestet.
- Erstellen Sie eine Tabelle mit den Werten der Variablen, um die Ausführung eines
  Programms zu verfolgen.

::::::::::::::::::::::::::::::::::::::::::::::::::



