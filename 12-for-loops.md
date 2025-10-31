---
title: For-Schleifen
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erläutern Sie, wozu for-Schleifen normalerweise verwendet werden.
- Verfolgen Sie die Ausführung einer einfachen (nicht verschachtelten) Schleife und
  geben Sie die Werte der Variablen in jeder Iteration korrekt an.
- Schreiben Sie for-Schleifen, die das Accumulator-Muster verwenden, um Werte zu
  aggregieren.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich ein Programm dazu bringen, viele Dinge zu tun?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Eine *for-Schleife* führt Befehle für jeden Wert in einer Sammlung einmal aus.

- Die Berechnung der Werte in einer Liste ist genauso mühsam wie die Arbeit mit
  `pressure_001`, `pressure_002`, etc.
- Eine *for-Schleife* weist Python an, einige Anweisungen für jeden Wert in einer Liste,
  einer Zeichenkette oder einer anderen Sammlung einmal auszuführen.
- "führe für jedes Ding in dieser Gruppe diese Operationen aus"

```python
for number in [2, 3, 5]:
    print(number)
```

- Diese `for` Schleife ist äquivalent zu:

```python
print(2)
print(3)
print(5)
```

- Und die Ausgabe der `for` Schleife ist:

```output
2
3
5
```

## Eine `for`-Schleife besteht aus einer Auflistung, einer Schleifenvariablen und einem Körper.

```python
for number in [2, 3, 5]:
    print(number)
```

- Die Schleife wird auf der Sammlung `[2, 3, 5]` ausgeführt.
- Der Körper, `print(number)`, gibt an, was für jeden Wert in der Sammlung zu tun ist.
- Die Schleifenvariable, `number`, ändert sich bei jeder *Iteration* der Schleife.
  - Das "aktuelle Ding".

## Die erste Zeile der `for`-Schleife muss mit einem Doppelpunkt enden, und der Körper muss eingerückt sein.

- Der Doppelpunkt am Ende der ersten Zeile signalisiert den Beginn eines *Blocks* von
  Anweisungen.
- Python verwendet Einrückungen anstelle von `{}` oder `begin`/`end`, um
  *Schachtelungen* anzuzeigen.
  - Jede konsistente Einrückung ist erlaubt, aber fast jeder verwendet vier Leerzeichen.

```python
for number in [2, 3, 5]:
print(number)
```

```error
IndentationError: expected an indented block
```

- Die Einrückung ist in Python immer sinnvoll.

```python
firstName = "Jon"
  lastName = "Smith"
```

```error
  File "<ipython-input-7-f65f2962bf9c>", line 2
    lastName = "Smith"
    ^
IndentationError: unexpected indent
```

- Dieser Fehler kann behoben werden, indem die zusätzlichen Leerzeichen am Anfang der
  zweiten Zeile entfernt werden.

## Schleifenvariablen können beliebig benannt werden.

- Wie alle Variablen sind auch die Schleifenvariablen:
  - Wird bei Bedarf erstellt.
  - Bedeutungslos: ihre Namen können alles Mögliche sein.

```python
for kitten in [2, 3, 5]:
    print(kitten)
```

## Der Körper einer Schleife kann viele Anweisungen enthalten.

- Aber keine Schleife sollte mehr als ein paar Zeilen lang sein.
- Für Menschen ist es schwer, sich größere Codeabschnitte zu merken.

```python
primes = [2, 3, 5]
for p in primes:
    squared = p ** 2
    cubed = p ** 3
    print(p, squared, cubed)
```

```output
2 4 8
3 9 27
5 25 125
```

## Verwenden Sie `range`, um über eine Folge von Zahlen zu iterieren.

- Die eingebaute Funktion
  [`range`](https://docs.python.org/3/library/stdtypes.html#range) erzeugt eine Folge
  von Zahlen.
  - *Keine* Liste: Die Zahlen werden bei Bedarf erzeugt, um die Schleifenbildung über
    große Bereiche effizienter zu machen.
- `range(N)` ist die Zahlen 0..N-1
  - Genau die zulässigen Indizes einer Liste oder Zeichenkette der Länge N

```python
print('a range is not a list: range(0, 3)')
for number in range(0, 3):
    print(number)
```

```output
a range is not a list: range(0, 3)
0
1
2
```

## Das Accumulator-Muster macht aus vielen Werten einen einzigen.

- Ein häufiges Muster in Programmen ist to:
  1. Initialisiere eine *Accumulator*-Variable auf Null, die leere Zeichenkette oder die
     leere Liste.
  2. Aktualisiere die Variable mit Werten aus einer Sammlung.

```python
# Sum the first 10 integers.
total = 0
for number in range(10):
   total = total + (number + 1)
print(total)
```

```output
55
```

- Lies `total = total + (number + 1)` als:
  - Addiere 1 zum aktuellen Wert der Schleifenvariablen `number`.
  - Addiere das zum aktuellen Wert der Akkumulatorvariablen `total`.
  - Weisen Sie dies `total` zu und ersetzen Sie damit den aktuellen Wert.
- Wir müssen `number + 1` hinzufügen, weil `range` 0..9 erzeugt, nicht 1..10.

::::::::::::::::::::::::::::::::::::::: challenge

## Klassifizierung von Fehlern

Ist ein Einrückungsfehler ein Syntaxfehler oder ein Laufzeitfehler?

::::::::::::::: solution

## Lösung

Ein IndentationError ist ein Syntaxfehler. Programme mit Syntaxfehlern können nicht
gestartet werden. Ein Programm mit einem Laufzeitfehler wird zwar gestartet, aber unter
bestimmten Bedingungen wird ein Fehler ausgelöst.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Verfolgung der Ausführung

Erstelle eine Tabelle mit den Zeilennummern, die bei der Ausführung dieses Programms
ausgeführt werden, und den Werten der Variablen nach der Ausführung jeder Zeile.

```python
total = 0
for char in "tin":
    total = total + 1
```

::::::::::::::: solution

## Lösung

| Line no | Variables            |
| ------- | -------------------- |
| 1       | total = 0            |
| 2       | total = 0 char = 't' |
| 3       | total = 1 char = 't' |
| 2       | total = 1 char = 'i' |
| 3       | total = 2 char = 'i' |
| 2       | total = 2 char = 'n' |
| 3       | total = 3 char = 'n' |

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Umkehrung einer Zeichenkette

Füllen Sie die Leerzeichen im folgenden Programm so aus, dass es "nit" (das Gegenteil
der ursprünglichen Zeichenkette "tin") ausgibt.

```python
original = "tin"
result = ____
for char in original:
    result = ____
print(result)
```

::::::::::::::: solution

## Lösung

```python
original = "tin"
result = ""
for char in original:
    result = char + result
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Übung Akkumulieren

Füllen Sie die Lücken in jedem der folgenden Programme aus, um das angegebene Ergebnis
zu erhalten.

```python
# Total length of the strings in the list: ["red", "green", "blue"] => 12
total = 0
for word in ["red", "green", "blue"]:
    ____ = ____ + len(word)
print(total)
```

::::::::::::::: solution

## Lösung

```python
total = 0
for word in ["red", "green", "blue"]:
    total = total + len(word)
print(total)
```

:::::::::::::::::::::::::

```python
# List of word lengths: ["red", "green", "blue"] => [3, 5, 4]
lengths = ____
for word in ["red", "green", "blue"]:
    lengths.____(____)
print(lengths)
```

::::::::::::::: solution

## Lösung

```python
lengths = []
for word in ["red", "green", "blue"]:
    lengths.append(len(word))
print(lengths)
```

:::::::::::::::::::::::::

```python
# Concatenate all words: ["red", "green", "blue"] => "redgreenblue"
words = ["red", "green", "blue"]
result = ____
for ____ in ____:
    ____
print(result)
```

::::::::::::::: solution

## Lösung

```python
words = ["red", "green", "blue"]
result = ""
for word in words:
    result = result + word
print(result)
```

:::::::::::::::::::::::::

**Erstellen eines Akronyms:** Ausgehend von der Liste `["red", "green", "blue"]`,
erstellen Sie das Akronym `"RGB"` mit Hilfe einer for-Schleife.

**Hinweis:** Möglicherweise müssen Sie eine String-Methode verwenden, um das Akronym
richtig zu formatieren.

::::::::::::::: solution

## Lösung

```python
acronym = ""
for word in ["red", "green", "blue"]:
    acronym = acronym + word[0].upper()
print(acronym)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Kumulative Summe

Ordnen Sie die folgenden Codezeilen neu an und rücken Sie sie richtig ein, so dass sie
eine Liste mit der kumulierten Summe der Daten ausgeben. Das Ergebnis sollte `[1, 3, 5,
10]` sein.

```python
cumulative.append(total)
for number in data:
cumulative = []
total = total + number
total = 0
print(cumulative)
data = [1,2,2,5]
```

::::::::::::::: solution

## Lösung

```python
total = 0
data = [1,2,2,5]
cumulative = []
for number in data:
    total = total + number
    cumulative.append(total)
print(cumulative)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Identifizierung von Variablennamensfehlern

1. Lesen Sie den folgenden Code und versuchen Sie, die Fehler zu identifizieren, ohne
   ihn auszuführen.
2. Führen Sie den Code aus und lesen Sie die Fehlermeldung. Was für ein Typ von
   `NameError` ist dies Ihrer Meinung nach? Ist es eine Zeichenkette ohne
   Anführungszeichen, eine falsch geschriebene Variable oder eine Variable, die
   definiert werden sollte, aber nicht definiert wurde?
3. Beheben Sie den Fehler.
4. Wiederholen Sie die Schritte 2 und 3, bis Sie alle Fehler behoben haben.

```python
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (Number % 3) == 0:
        message = message + a
    else:
        message = message + "b"
print(message)
```

::::::::::::::: solution

## Lösung

- Bei Python-Variablennamen wird zwischen Groß- und Kleinschreibung unterschieden:
  `number` und `Number` beziehen sich auf unterschiedliche Variablen.
- Die Variable `message` muss mit einem leeren String initialisiert werden.
- Wir wollen die Zeichenkette `"a"` zu `message` hinzufügen, nicht die undefinierte
  Variable `a`.

```python
message = ""
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (number % 3) == 0:
        message = message + "a"
    else:
        message = message + "b"
print(message)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Identifizierung von Elementfehlern

1. Lesen Sie den folgenden Code und versuchen Sie, die Fehler zu identifizieren, ohne
   ihn auszuführen.
2. Führen Sie den Code aus, und lesen Sie die Fehlermeldung. Um welche Art von Fehler
   handelt es sich?
3. Beheben Sie den Fehler.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[4])
```

::::::::::::::: solution

## Lösung

Diese Liste hat 4 Elemente und der Index für den Zugriff auf das letzte Element in der
Liste ist `3`.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[3])
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Eine *for-Schleife* führt Befehle einmal für jeden Wert in einer Sammlung aus.
- Eine *for-Schleife*besteht aus einer Sammlung, einer Schleifenvariablen und einem
  Körper.
- Die erste Zeile der *for-Schleife* muss mit einem Doppelpunkt enden, und der Körper
  muss eingerückt sein.
- Die Einrückung ist in Python immer sinnvoll.
- Schleifenvariablen können beliebig benannt werden (es wird jedoch dringend empfohlen,
  einen aussagekräftigen Namen für die Schleifenvariable zu verwenden).
- Der Körper einer Schleife kann viele Anweisungen enthalten.
- Benutze `range`, um über eine Folge von Zahlen zu iterieren.
- Das Accumulator-Muster macht aus vielen Werten einen einzigen.

::::::::::::::::::::::::::::::::::::::::::::::::::



