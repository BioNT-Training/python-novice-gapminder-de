---
title: Listen
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erklären Sie, warum Programme Wertesammlungen benötigen.
- Programme schreiben, die flache Listen erstellen, indizieren, zerschneiden und durch
  Zuweisungen und Methodenaufrufe modifizieren.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich mehrere Werte speichern?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Eine Liste speichert viele Werte in einer einzigen Struktur.

- Berechnungen mit hundert Variablen, die `pressure_001`, `pressure_002`, usw. heißen,
  wären mindestens so langsam wie die manuelle Berechnung.
- Verwenden Sie eine *Liste*, um viele Werte zusammen zu speichern.
  - Enthält Werte innerhalb eckiger Klammern `[...]`.
  - Werte sind durch Kommata `,` getrennt.
- Verwenden Sie `len`, um herauszufinden, wie viele Werte in einer Liste sind.

```python
pressures = [0.273, 0.275, 0.277, 0.275, 0.276]
print('pressures:', pressures)
print('length:', len(pressures))
```

```output
pressures: [0.273, 0.275, 0.277, 0.275, 0.276]
length: 5
```

## Verwenden Sie den Index eines Elements, um es aus einer Liste zu holen.

- Genau wie Zeichenketten.

```python
print('zeroth item of pressures:', pressures[0])
print('fourth item of pressures:', pressures[4])
```

```output
zeroth item of pressures: 0.273
fourth item of pressures: 0.276
```

## Die Werte von Listen können durch Zuweisungen ersetzt werden.

- Verwenden Sie einen Indexausdruck auf der linken Seite der Zuweisung, um einen Wert zu
  ersetzen.

```python
pressures[0] = 0.265
print('pressures is now:', pressures)
```

```output
pressures is now: [0.265, 0.275, 0.277, 0.275, 0.276]
```

## Das Anhängen von Elementen an eine Liste verlängert diese.

- Verwenden Sie `list_name.append`, um Elemente am Ende einer Liste hinzuzufügen.

```python
primes = [2, 3, 5]
print('primes is initially:', primes)
primes.append(7)
print('primes has become:', primes)
```

```output
primes is initially: [2, 3, 5]
primes has become: [2, 3, 5, 7]
```

- `append` ist eine *Methode* von Listen.
  - Wie eine Funktion, aber an ein bestimmtes Objekt gebunden.
- Verwenden Sie `object_name.method_name`, um Methoden aufzurufen.
  - ähnelt absichtlich der Art und Weise, wie wir in einer Bibliothek auf Dinge
    verweisen.
- Wir werden im weiteren Verlauf weitere Methoden für Listen kennenlernen.
  - Verwenden Sie `help(list)` für eine Vorschau.
- `extend` ist ähnlich wie `append`, erlaubt es aber, zwei Listen zu kombinieren. Zum
  Beispiel:

```python
teen_primes = [11, 13, 17, 19]
middle_aged_primes = [37, 41, 43, 47]
print('primes is currently:', primes)
primes.extend(teen_primes)
print('primes has now become:', primes)
primes.append(middle_aged_primes)
print('primes has finally become:', primes)
```

```output
primes is currently: [2, 3, 5, 7]
primes has now become: [2, 3, 5, 7, 11, 13, 17, 19]
primes has finally become: [2, 3, 5, 7, 11, 13, 17, 19, [37, 41, 43, 47]]
```

Beachten Sie, dass `extend` zwar die "flache" Struktur der Liste beibehält, aber das
Anhängen einer Liste an eine Liste bedeutet, dass das letzte Element in `primes` selbst
eine Liste und keine Ganzzahl ist. Listen können Werte beliebigen Typs enthalten; daher
sind auch Listen von Listen möglich.

## Verwenden Sie `del`, um Elemente aus einer Liste vollständig zu entfernen.

- Wir verwenden `del list_name[index]`, um ein Element aus einer Liste zu entfernen (im
  Beispiel ist 9 keine Primzahl) und sie damit zu kürzen.
- `del` ist keine Funktion oder Methode, sondern eine Anweisung in der Sprache.

```python
primes = [2, 3, 5, 7, 9]
print('primes before removing last item:', primes)
del primes[4]
print('primes after removing last item:', primes)
```

```output
primes before removing last item: [2, 3, 5, 7, 9]
primes after removing last item: [2, 3, 5, 7]
```

## Die leere Liste enthält keine Werte.

- Verwenden Sie `[]` allein, um eine Liste darzustellen, die keine Werte enthält.
  - "Die Null der Listen."
- Hilfreich als Ausgangspunkt für die Sammlung von Werten (die wir in der [nächsten
  Folge](12-for-loops.md) sehen werden).

## Listen können Werte unterschiedlichen Typs enthalten.

- Eine einzelne Liste kann Zahlen, Zeichenketten und alles andere enthalten.

```python
goals = [1, 'Create lists.', 2, 'Extract items from lists.', 3, 'Modify lists.']
```

## Zeichenketten können wie Listen indiziert werden.

- Abrufen einzelner Zeichen aus einer Zeichenkette unter Verwendung von Indizes in
  eckigen Klammern.

```python
element = 'carbon'
print('zeroth character:', element[0])
print('third character:', element[3])
```

```output
zeroth character: c
third character: b
```

## Zeichenketten sind unveränderlich.

- Die Zeichen in einer Zeichenkette können nicht geändert werden, nachdem sie erstellt
  wurde.
  - *Immutable (unveränderlich)*: kann nach der Erstellung nicht mehr geändert werden.
  - Im Gegensatz dazu sind Listen *veränderlich*: Sie können an Ort und Stelle geändert
    werden.
- Python betrachtet die Zeichenkette als einen einzelnen Wert mit Teilen, nicht als eine
  Sammlung von Werten.

```python
element[0] = 'C'
```

```error
TypeError: 'str' object does not support item assignment
```

- Listen und Zeichenketten sind beides *Sammlungen*.

## Eine Indizierung über das Ende der Auflistung hinaus ist ein Fehler.

- Python meldet einen `IndexError`, wenn wir versuchen, auf einen Wert zuzugreifen, der
  nicht existiert.
  - Dies ist eine Art von [Laufzeitfehler](04-built-in.md).
  - Kann beim Parsen des Codes nicht erkannt werden, da der Index möglicherweise anhand
    von Daten berechnet wird.

```python
print('99th element of element is:', element[99])
```

```output
IndexError: string index out of range
```

::::::::::::::::::::::::::::::::::::::: challenge

## Füllen Sie die Lücken aus

Füllen Sie die Leerzeichen aus, so dass das folgende Programm die gezeigte Ausgabe
erzeugt.

```python
values = ____
values.____(1)
values.____(3)
values.____(5)
print('first time:', values)
values = values[____]
print('second time:', values)
```

```output
first time: [1, 3, 5]
second time: [3, 5]
```

::::::::::::::: solution

## Lösung

```python
values = []
values.append(1)
values.append(3)
values.append(5)
print('first time:', values)
values = values[1:]
print('second time:', values)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Wie groß ist ein Slice?

Wenn `start` und `stop` beide nicht-negative ganze Zahlen sind, wie lang ist die Liste
`values[start:stop]`?

::::::::::::::: solution

## Lösung

Die Liste `values[start:stop]` hat bis zu `stop - start` Elemente. Zum Beispiel hat
`values[1:4]` die 3 Elemente `values[1]`, `values[2]`, und `values[3]`. Warum "bis zu"?
Wie wir in [Folge 2](02-variables.md) gesehen haben, erhalten wir immer noch eine Liste
zurück, wenn `stop` größer ist als die Gesamtlänge der Liste `values`, aber sie wird
kürzer sein als erwartet.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Von Zeichenketten zu Listen und zurück

Angesichts dieser:

```python
print('string to list:', list('tin'))
print('list to string:', ''.join(['g', 'o', 'l', 'd']))
```

```output
string to list: ['t', 'i', 'n']
list to string: gold
```

1. Was bewirkt `list('some string')`?
2. Was erzeugt `'-'.join(['x', 'y', 'z'])`?

::::::::::::::: solution

## Lösung

1. [`list('some string')`](https://docs.python.org/3/library/stdtypes.html#list) wandelt
   eine Zeichenkette in eine Liste um, die alle ihre Zeichen enthält.
2. [`join`](https://docs.python.org/3/library/stdtypes.html#str.join) gibt eine
   Zeichenkette zurück, die die *Verkettung* jedes Zeichenkettenelements in der Liste
   ist und fügt das Trennzeichen zwischen jedem Element in der Liste hinzu. Das Ergebnis
   ist `x-y-z`. Das Trennzeichen zwischen den Elementen ist die Zeichenkette, die diese
   Methode liefert.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Arbeiten mit dem Ende

Was gibt das folgende Programm aus?

```python
element = 'helium'
print(element[-1])
```

1. Wie interpretiert Python einen negativen Index?
2. Wenn eine Liste oder Zeichenkette N Elemente hat, welches ist der negativste Index,
   der sicher verwendet werden kann, und welche Stelle repräsentiert dieser Index?
3. Wenn `values` eine Liste ist, was macht dann `del values[-1]`?
4. Wie kann man alle Elemente außer dem letzten anzeigen, ohne `values` zu ändern?
   (Tipp: Sie müssen Slicing und negative Indizierung kombinieren.)

::::::::::::::: solution

## Lösung

Das Programm gibt `m` aus.

1. Python interpretiert einen negativen Index so, als würde man vom Ende her beginnen
   (im Gegensatz zum Anfang). Das letzte Element ist `-1`.
2. Der letzte Index, der bei einer Liste mit N Elementen sicher verwendet werden kann,
   ist das Element `-N`, das das erste Element darstellt.
3. `del values[-1]` entfernt das letzte Element aus der Liste.
4. `values[:-1]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Schrittweise durch eine Liste

Was gibt das folgende Programm aus?

```python
element = 'fluorine'
print(element[::2])
print(element[::-1])
```

1. Wenn wir ein Slice als `low:high:stride` schreiben, was macht dann `stride`?
2. Welcher Ausdruck würde alle geradzahligen Elemente aus einer Sammlung auswählen?

::::::::::::::: solution

## Lösung

Das Programm druckt

```python
furn
eniroulf
```

1. `stride` ist die Schrittweite des Slice.
2. Das Slice `1::2` wählt alle geradzahligen Elemente einer Sammlung aus: es beginnt mit
   dem Element `1` (welches das zweite Element ist, da die Indizierung bei `0` beginnt),
   geht weiter bis zum Ende (da kein `end` angegeben ist) und verwendet eine
   Schrittweite von `2` (d.h. es wählt jedes zweite Element aus).

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Slice Bounds

Was gibt das folgende Programm aus?

```python
element = 'lithium'
print(element[0:20])
print(element[-1:3])
```

::::::::::::::: solution

## Lösung

```output
lithium

```

Die erste Anweisung gibt die gesamte Zeichenkette aus, da der Slice über die Gesamtlänge
der Zeichenkette hinausgeht. Die zweite Anweisung gibt eine leere Zeichenkette zurück,
da der Ausschnitt "außerhalb der Grenzen" der Zeichenkette liegt.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Sortieren und sortiert

Was geben diese beiden Programme aus? Erklären Sie in einfachen Worten den Unterschied
zwischen `sorted(letters)` und `letters.sort()`.

```python
# Program A
letters = list('gold')
result = sorted(letters)
print('letters is', letters, 'and result is', result)
```

```python
# Program B
letters = list('gold')
result = letters.sort()
print('letters is', letters, 'and result is', result)
```

::::::::::::::: solution

## Lösung

Programm A druckt

```output
letters is ['g', 'o', 'l', 'd'] and result is ['d', 'g', 'l', 'o']
```

Programm B druckt

```output
letters is ['d', 'g', 'l', 'o'] and result is None
```

`sorted(letters)` gibt eine sortierte Kopie der Liste `letters` zurück (die
ursprüngliche Liste `letters` bleibt unverändert), während `letters.sort()` die Liste
`letters` in-place sortiert und nichts zurückgibt.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Kopieren (oder nicht)

Was geben diese beiden Programme aus? Erklären Sie in einfachen Worten den Unterschied
zwischen `new = old` und `new = old[:]`.

```python
# Program A
old = list('gold')
new = old      # simple assignment
new[0] = 'D'
print('new is', new, 'and old is', old)
```

```python
# Program B
old = list('gold')
new = old[:]   # assigning a slice
new[0] = 'D'
print('new is', new, 'and old is', old)
```

::::::::::::::: solution

## Lösung

Programm A druckt

```output
new is ['D', 'o', 'l', 'd'] and old is ['D', 'o', 'l', 'd']
```

Programm B druckt

```output
new is ['D', 'o', 'l', 'd'] and old is ['g', 'o', 'l', 'd']
```

`new = old` macht `new` zu einem Verweis auf die Liste `old`; `new` und `old` zeigen auf
das gleiche Objekt.

`new = old[:]` erzeugt jedoch ein neues Listenobjekt `new`, das alle Elemente der Liste
`old` enthält; `new` und `old` sind unterschiedliche Objekte.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Eine Liste speichert viele Werte in einer einzigen Struktur.
- Verwenden Sie den Index eines Elements, um es aus einer Liste zu holen.
- Die Werte von Listen können durch Zuweisung ersetzt werden.
- Das Anhängen von Elementen an eine Liste verlängert diese.
- Verwenden Sie `del`, um Elemente aus einer Liste vollständig zu entfernen.
- Die leere Liste enthält keine Werte.
- Listen können Werte unterschiedlichen Typs enthalten.
- Zeichenketten können wie Listen indiziert werden.
- Zeichenketten sind unveränderlich.
- Die Indizierung über das Ende der Auflistung hinaus ist ein Fehler.

::::::::::::::::::::::::::::::::::::::::::::::::::



