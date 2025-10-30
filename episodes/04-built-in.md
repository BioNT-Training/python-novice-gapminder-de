---
title: Eingebaute Funktionen und Hilfe
teaching: 15
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erläutern Sie den Zweck von Funktionen.
- Rufen Sie eingebaute Python-Funktionen korrekt auf.
- Richtiges Verschachteln von Aufrufen zu eingebauten Funktionen.
- Verwenden Sie die Hilfe, um die Dokumentation für eingebaute Funktionen anzuzeigen.
- Situationen, in denen SyntaxError und NameError auftreten, korrekt beschreiben.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich eingebaute Funktionen verwenden?
- Wie kann ich herausfinden, was sie tun?
- Welche Arten von Fehlern können in Programmen auftreten?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Verwenden Sie Kommentare, um die Dokumentation von Programmen zu ergänzen.

```python
# This sentence isn't executed by Python.
adjustment = 0.5   # Neither is this - anything after '#' is ignored.
```

## Eine Funktion kann null oder mehr Argumente annehmen.

- Wir haben schon einige Funktionen gesehen --- jetzt wollen wir sie uns genauer
  ansehen.
- Ein *Argument* ist ein Wert, der an eine Funktion übergeben wird.
- `len` nimmt genau einen.
- `int`, `str` und `float` erzeugen einen neuen Wert aus einem bestehenden.
- `print` nimmt null oder mehr.
- `print` ohne Argumente gibt eine leere Zeile aus.
  - Muss immer Klammern verwenden, auch wenn sie leer sind, damit Python weiß, dass eine
    Funktion aufgerufen wird.

```python
print('before')
print()
print('after')
```

```output
before

after
```

## Jede Funktion gibt etwas zurück.

- Jeder Funktionsaufruf erzeugt ein Ergebnis.
- Wenn die Funktion kein brauchbares Ergebnis zurückgeben kann, gibt sie normalerweise
  den speziellen Wert `None` zurück.`None` ist ein Python-Objekt, das immer dann
  einspringt, wenn es keinen Wert gibt.

```python
result = print('example')
print('result of print is', result)
```

```output
example
result of print is None
```

## Häufig genutzte eingebaute Funktionen sind `max`, `min` und `round`.

- Verwenden Sie `max`, um den größten Wert von einem oder mehreren Werten zu finden.
- Verwenden Sie `min`, um die kleinste Zahl zu finden.
- Beide funktionieren sowohl mit Zeichenketten als auch mit Zahlen.
  - "Größer" und "kleiner" verwenden (0-9, A-Z, a-z), um Buchstaben zu vergleichen.

```python
print(max(1, 2, 3))
print(min('a', 'A', '0'))
```

```output
3
0
```

## Funktionen können nur für bestimmte (Kombinationen von) Argumenten funktionieren.

- `max` und `min` müssen mit mindestens einem Argument versehen werden.
  - "Größte der leeren Menge" ist eine sinnlose Frage.
- Und ihnen müssen Dinge gegeben werden, die sinnvoll verglichen werden können.

```python
print(max(1, 'a'))
```

```error
TypeError                                 Traceback (most recent call last)
<ipython-input-52-3f049acf3762> in <module>
----> 1 print(max(1, 'a'))

TypeError: '>' not supported between instances of 'str' and 'int'
```

## Funktionen können Standardwerte für einige Argumente haben.

- `round` rundet eine Fließkommazahl ab.
- Rundet standardmäßig auf null Dezimalstellen.

```python
round(3.712)
```

```output
4
```

- Wir können die Anzahl der gewünschten Dezimalstellen angeben.

```python
round(3.712, 1)
```

```output
3.7
```

## Funktionen, die an Objekte angehängt sind, werden Methoden genannt

- Funktionen nehmen eine andere Form an, die in den Pandas-Episoden üblich sein wird.
- Methoden haben Klammern wie Funktionen, stehen aber hinter der Variablen.
- Einige Methoden werden für interne Python-Operationen verwendet und sind durch
  doppelte Unterstriche gekennzeichnet.

```python
my_string = 'Hello world!'  # Erstellung eines String-Objekts

print(len(my_string))       # Die Funktion len nimmt eine Zeichenkette als Argument und gibt die Länge der Zeichenkette zurück

print(my_string.swapcase()) # Aufruf der swapcase-Methode für das Objekt my_string

print(my_string.__len__())  # Aufruf der internen Methode __len__ für das Objekt my_string, verwendet von len(my_string)

```

```output
12
hELLO WORLD!
12
```

- Man kann sie sogar aneinandergereiht sehen. Sie arbeiten von links nach rechts.

```python
print(my_string.isupper())          # Nicht alle Buchstaben sind Großbuchstaben
print(my_string.upper())            # Dadurch werden alle Buchstaben großgeschrieben

print(my_string.upper().isupper())  # Jetzt sind alle Buchstaben groß geschrieben
```

```output
False
HELLO WORLD
True
```

## Verwenden Sie die eingebaute Funktion `help`, um Hilfe für eine Funktion zu erhalten.

- Jede eingebaute Funktion hat eine Online-Dokumentation.

```python
help(round)
```

```output
Help on built-in function round in module builtins:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.

    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
```

## Das Jupyter Notebook bietet zwei Möglichkeiten, Hilfe zu erhalten.

- Option 1: Platzieren Sie den Cursor in der Nähe der Stelle, an der die Funktion in
  einer Zelle aufgerufen wird (d.h. der Funktionsname oder ihre Parameter),
  - Halten Sie <kbd>Shift</kbd> gedrückt und drücken Sie <kbd>Tab</kbd>.
  - Führen Sie dies mehrmals durch, um die zurückgegebenen Informationen zu erweitern.
- Option 2: Geben Sie den Funktionsnamen in eine Zelle ein, hinter der ein Fragezeichen
  steht. Führen Sie dann die Zelle aus.

## Python meldet einen Syntaxfehler, wenn es den Quelltext eines Programms nicht verstehen kann.

- Versucht erst gar nicht, das Programm auszuführen, wenn es nicht geparst werden kann.

```python
# Forgot to close the quote marks around the string.
name = 'Feng
```

```error
  File "<ipython-input-56-f42768451d55>", line 2
    name = 'Feng
                ^
SyntaxError: EOL while scanning string literal
```

```python
# An extra '=' in the assignment.
age = = 52
```

```error
  File "<ipython-input-57-ccc3df3cf902>", line 2
    age = = 52
          ^
SyntaxError: invalid syntax
```

- Sehen Sie sich die Fehlermeldung genauer an:

```python
print("hello world"
```

```error
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
```

- Die Meldung weist auf ein Problem in der ersten Zeile der Eingabe ("Zeile 1") hin.
  - In diesem Fall sagt uns der Abschnitt "ipython-input" des Dateinamens, dass wir mit
    Eingaben in IPython arbeiten, dem Python-Interpreter, der vom Jupyter Notebook
    verwendet wird.
- Der Teil `-6-` des Dateinamens zeigt an, dass der Fehler in Zelle 6 unseres Notebooks
  aufgetreten ist.
- Es folgt die problematische Codezeile, die auf das Problem mit einem `^`-Zeiger
  hinweist.

## Python meldet einen Laufzeitfehler, wenn bei der Ausführung eines Programms etwas schief läuft. {#laufzeit-fehler}

```python
age = 53
remaining = 100 - aege # mis-spelled 'age'
```

```error
NameError                                 Traceback (most recent call last)
<ipython-input-59-1214fb6c55fc> in <module>
      1 age = 53
----> 2 remaining = 100 - aege # mis-spelled 'age'

NameError: name 'aege' is not defined
```

- Beheben Sie Syntaxfehler durch Lesen des Quellcodes und Laufzeitfehler durch Verfolgen
  der Ausführung.

::::::::::::::::::::::::::::::::::::::: challenge

## Was passiert, wenn

1. Erklären Sie in einfachen Worten die Reihenfolge der Operationen im folgenden
   Programm: wann erfolgt die Addition, wann die Subtraktion, wann wird jede Funktion
   aufgerufen, usw.
2. Was ist der Endwert von `radiance`?

```python
radiance = 1.0
radiance = max(2.1, 2.0 + min(radiance, 1.1 * radiance - 0.5))
```

::::::::::::::: solution

## Lösung

1. Reihenfolge der Operationen:
  1. `1.1 * radiance = 1.1`
  2. `1.1 - 0.5 = 0.6`
  3. `min(radiance, 0.6) = 0.6`
  4. `2.0 + 0.6 = 2.6`
  5. `max(2.1, 2.6) = 2.6`
2. Am Ende, `radiance = 2.6`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Erkenne den Unterschied

1. Sagen Sie voraus, was jede der `print`-Anweisungen im folgenden Programm ausgeben
   wird.
2. Läuft `max(len(rich), poor)` oder gibt es eine Fehlermeldung? Wenn es ausgeführt
   wird, ergibt das Ergebnis einen Sinn?

```python
easy_string = "abc"
print(max(easy_string))
rich = "gold"
poor = "tin"
print(max(rich, poor))
print(max(len(rich), len(poor)))
```

::::::::::::::: solution

## Lösung

```python
print(max(easy_string))
```

```output
c
```

```python
print(max(rich, poor))
```

```output
tin
```

```python
print(max(len(rich), len(poor)))
```

```output
4
```

`max(len(rich), poor)` wirft einen TypeError. Daraus wird `max(4, 'tin')`, und wie wir
bereits besprochen haben, können eine Zeichenkette und eine ganze Zahl nicht sinnvoll
verglichen werden.

```error 
TypeError                                 Traceback (most recent call last)
<ipython-input-65-bc82ad05177a> in <module>
----> 1 max(len(rich), poor)

TypeError: '>' not supported between instances of 'str' and 'int'
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Warum nicht?

Warum geben `max` und `min` nicht `None` zurück, wenn sie ohne Argumente aufgerufen
werden?

::::::::::::::: solution

## Lösung

`max` und `min` geben in diesem Fall TypeErrors zurück, weil nicht die richtige Anzahl
von Parametern übergeben wurde. Wenn nur `None` zurückgegeben würde, wäre der Fehler
viel schwieriger zu verfolgen, da er wahrscheinlich in einer Variablen gespeichert und
später im Programm verwendet würde, nur um dann wahrscheinlich einen Laufzeitfehler
auszulösen.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Letztes Zeichen einer Zeichenkette

Wenn Python bei Null anfängt zu zählen und `len` die Anzahl der Zeichen in einer
Zeichenkette liefert, welcher Indexausdruck liefert dann das letzte Zeichen in der
Zeichenkette `name`? (Hinweis: Wir werden in einer späteren Folge einen einfacheren Weg
sehen, dies zu tun.)

::::::::::::::: solution

## Lösung

`name[len(name) - 1]`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Erforschen Sie die Python-Dokumente!

Die [offizielle Python-Dokumentation](https://docs.python.org/3/) ist wohl die
vollständigste Informationsquelle über die Sprache. Sie ist in verschiedenen Sprachen
verfügbar und enthält eine Menge nützlicher Ressourcen. Die Seite [Built-in
Functions](https://docs.python.org/3/library/functions.html) enthält einen Katalog all
dieser Funktionen, einschließlich derer, die wir in dieser Lektion behandelt haben.
Einige dieser Funktionen sind fortgeschrittener und im Moment unnötig, aber andere sind
sehr einfach und nützlich.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Verwenden Sie Kommentare, um Programme zu dokumentieren.
- Eine Funktion kann null oder mehr Argumente annehmen.
- Zu den häufig verwendeten eingebauten Funktionen gehören `max`, `min` und `round`.
- Funktionen können nur für bestimmte (Kombinationen von) Argumenten funktionieren.
- Funktionen können Standardwerte für einige Argumente haben.
- Benutzen Sie die eingebaute Funktion `help`, um Hilfe für eine Funktion zu erhalten.
- Das Jupyter Notebook bietet zwei Möglichkeiten, Hilfe zu erhalten.
- Jede Funktion gibt etwas zurück.
- Python meldet einen Syntaxfehler, wenn es den Quelltext eines Programms nicht
  verstehen kann.
- Python meldet einen Laufzeitfehler, wenn bei der Ausführung eines Programms etwas
  schief läuft.
- Beheben Sie Syntaxfehler, indem Sie den Quellcode lesen, und Laufzeitfehler, indem Sie
  die Ausführung des Programms verfolgen.

::::::::::::::::::::::::::::::::::::::::::::::::::



