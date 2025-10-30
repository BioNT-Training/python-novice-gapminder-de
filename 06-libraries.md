---
title: Bibliotheken
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erklären, was Softwarebibliotheken sind und warum Programmierer sie erstellen und
  benutzen.
- Schreibe Programme, die Module aus der Python-Standardbibliothek importieren und
  verwenden.
- Suchen und lesen Sie die Dokumentation der Standardbibliothek interaktiv (im
  Interpreter) und online.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich Software benutzen, die andere Leute geschrieben haben?
- Wie kann ich herausfinden, was diese Software macht?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Der größte Teil der Macht einer Programmiersprache liegt in ihren Bibliotheken.

- Eine *Bibliothek* ist eine Sammlung von Dateien (*Module* genannt), die Funktionen zur
  Verwendung durch andere Programme enthält.
  - Kann auch Datenwerte (z.B. numerische Konstanten) und andere Dinge enthalten.
  - Der Inhalt einer Bibliothek sollte zusammengehören, aber es gibt keine Möglichkeit,
    das zu erzwingen.
- Die Python-[Standardbibliothek][stdlib] ist eine umfangreiche Sammlung von Modulen,
  die mit Python selbst geliefert wird.
- Viele zusätzliche Bibliotheken sind über [PyPI][pypi] (den Python Package Index)
  erhältlich.
- Wir werden später sehen, wie man neue Bibliotheken schreibt.

::::::::::::::::::::::::::::::::::::::::: callout

## Bibliotheken und Module

Eine Bibliothek ist eine Sammlung von Modulen, aber die Begriffe werden oft austauschbar
verwendet, vor allem, da viele Bibliotheken nur aus einem einzigen Modul bestehen, also
mach dir keine Sorgen, wenn du sie vermischt.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Ein Programm muss ein Bibliotheksmodul importieren, bevor es es verwenden kann.

- Benutze `import`, um ein Bibliotheksmodul in den Speicher eines Programms zu laden.
- Dann verweise auf Dinge aus dem Modul als `module_name.thing_name`.
  - Python verwendet `.` als Bezeichnung für "Teil von".
- Verwendung von `math`, einem der Module der Standardbibliothek:

```python
import math

print('pi is', math.pi)
print('cos(pi) is', math.cos(math.pi))
```

```output
pi is 3.141592653589793
cos(pi) is -1.0
```

- Auf jedes Element muss mit dem Namen des Moduls verwiesen werden.
  - `math.cos(pi)` wird nicht funktionieren: der Verweis auf `pi` "erbt" nicht irgendwie
    den Verweis der Funktion auf `math`.

## Benutzen Sie `help`, um etwas über den Inhalt eines Bibliotheksmoduls zu erfahren.

- Funktioniert genau wie die Hilfe für eine Funktion.

```python
help(math)
```

```output
Help on module math:

NAME
    math

MODULE REFERENCE
    http://docs.python.org/3/library/math

    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    This module is always available.  It provides access to the
    mathematical functions defined by the C standard.

FUNCTIONS
    acos(x, /)
        Return the arc cosine (measured in radians) of x.
⋮ ⋮ ⋮
```

## Importieren Sie bestimmte Elemente aus einem Bibliotheksmodul, um Programme zu verkürzen.

- Verwenden Sie `from ... import ...`, um nur bestimmte Elemente aus einem
  Bibliotheksmodul zu laden.
- Dann verweisen Sie direkt auf sie ohne den Bibliotheksnamen als Präfix.

```python
from math import cos, pi

print('cos(pi) is', cos(pi))
```

```output
cos(pi) is -1.0
```

## Erstellen Sie einen Alias für ein Bibliotheksmodul, wenn Sie es importieren, um Programme zu verkürzen.

- Benutzen Sie `import ... as ...`, um einer Bibliothek einen kurzen *Alias* zu geben,
  während Sie sie importieren.
- Dann verweisen Sie auf Elemente in der Bibliothek mit diesem verkürzten Namen.

```python
import math as m

print('cos(pi) is', m.cos(m.pi))
```

```output
cos(pi) is -1.0
```

- Wird häufig für Bibliotheken verwendet, die häufig benutzt werden oder lange Namen
  haben.
  - z.B. wird die `matplotlib` Plot-Bibliothek oft als `mpl` aliasiert.
- Dies kann jedoch dazu führen, dass Programme schwerer zu verstehen sind, da die Leser
  die Aliasnamen Ihres Programms lernen müssen.

::::::::::::::::::::::::::::::::::::::: challenge

## Inspizieren des Math-Moduls

1. Welche Funktion aus dem Modul `math` können Sie verwenden, um eine Quadratwurzel
   *ohne* Verwendung von `sqrt` zu berechnen?
2. Da die Bibliothek diese Funktion enthält, warum existiert `sqrt`?

::::::::::::::: solution

## Lösung

1. Mit `help(math)` sehen wir, dass wir `pow(x,y)` zusätzlich zu `sqrt(x)` haben, also
   könnten wir `pow(x, 0.5)` benutzen, um eine Quadratwurzel zu finden.

2. Die Funktion `sqrt(x)` ist bei der Implementierung von Gleichungen wohl lesbarer als
   `pow(x, 0.5)`. Lesbarkeit ist ein Eckpfeiler guter Programmierung, daher ist es
   sinnvoll, eine spezielle Funktion für diesen speziellen Fall bereitzustellen.

Auch das Design der Python-Bibliothek `math` hat seinen Ursprung im C-Standard, der
sowohl `sqrt(x)` als auch `pow(x,y)` enthält, also zeigt sich ein wenig von der
Geschichte des Programmierens in Pythons Funktionsnamen.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Auffinden des richtigen Moduls

Sie wollen ein zufälliges Zeichen aus einer Zeichenkette auswählen:

```python
bases = 'ACTTGCTTGAC'
```

1. Welches [Standardbibliothek][stdlib]-Modul könnte Ihnen helfen?
2. Welche Funktion würden Sie aus diesem Modul auswählen? Gibt es Alternativen?
3. Versuche, ein Programm zu schreiben, das die Funktion verwendet.

::::::::::::::: solution

## Lösung

Das [Zufallsmodul][randommod] scheint zu helfen.

Die Zeichenkette besteht aus 11 Zeichen, die jeweils einen Positionsindex von 0 bis 10
haben. Sie könnten die Funktionen
`random.randrange`(https://docs.python.org/3/library/random.html#random.randrange) oder
`random.randint`(https://docs.python.org/3/library/random.html#random.randint)
verwenden, um eine zufällige ganze Zahl zwischen 0 und 10 zu erhalten, und dann das
Zeichen`bases`an diesem Index auswählen:

```python
from random import randrange

random_index = randrange(len(bases))
print(bases[random_index])
```

oder noch kompakter:

```python
from random import randrange

print(bases[randrange(len(bases))])
```

Vielleicht haben Sie die Funktion
[`random.sample`](https://docs.python.org/3/library/random.html#random.sample) gefunden?
Sie ermöglicht etwas weniger Tipparbeit, ist aber vielleicht etwas schwerer zu
verstehen, wenn man nur liest:

```python
from random import sample

print(sample(bases, 1)[0])
```

Beachten Sie, dass diese Funktion eine Liste von Werten zurückgibt. Wir werden in [Folge
11](11-lists.md) etwas über Listen lernen.

Die einfachste und kürzeste Lösung ist die Funktion
[`random.choice`](https://docs.python.org/3/library/random.html#random.choice), die
genau das tut, was wir wollen:

```python
from random import choice

print(choice(bases))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Jigsaw Puzzle (Parsons's Problem) Programmierbeispiel

Ordnen Sie die folgenden Anweisungen so an, dass eine zufällige DNA-Base und ihr Index
in der Zeichenkette ausgegeben wird. Es werden nicht alle Anweisungen benötigt. Sie
können auch Zwischenvariablen verwenden/hinzufügen.

```python
bases="ACTTGCTTGAC"
import math
import random
___ = random.randrange(n_bases)
___ = len(bases)
print("random base ", bases[___], "base index", ___)
```

::::::::::::::: solution

## Lösung

```python
import math 
import random
bases = "ACTTGCTTGAC" 
n_bases = len(bases)
idx = random.randrange(n_bases)
print("random base", bases[idx], "base index", idx)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Wann ist die Hilfe verfügbar?

Wenn ein Kollege von Ihnen `help(math)` tippt, meldet Python einen Fehler:

```error
NameError: name 'math' is not defined
```

Was hat Ihr Kollege vergessen zu tun?

::::::::::::::: solution

## Lösung

Importieren des Mathe-Moduls (`import math`)



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Importieren mit Aliasen

1. Füllen Sie die Leerzeichen aus, damit das folgende Programm `90.0` ausgibt.
2. Schreiben Sie das Programm so um, dass es `import` *ohne* `as` verwendet.
3. Welche Form ist für Sie leichter zu lesen?

```python
import math as m
angle = ____.degrees(____.pi / 2)
print(____)
```

::::::::::::::: solution

## Lösung

```python
import math as m
angle = m.degrees(m.pi / 2)
print(angle)
```

kann geschrieben werden als

```python
import math
angle = math.degrees(math.pi / 2)
print(angle)
```

Da Sie den Code gerade erst geschrieben haben und mit ihm vertraut sind, finden Sie die
erste Version vielleicht sogar einfacher zu lesen. Wenn Sie jedoch versuchen, einen
umfangreichen Code zu lesen, der von jemand anderem geschrieben wurde, oder wenn Sie
nach mehreren Monaten zu Ihrem eigenen umfangreichen Code zurückkehren, sind nicht
abgekürzte Namen oft einfacher, es sei denn, es gibt klare Abkürzungskonventionen.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Es gibt viele Möglichkeiten, Bibliotheken zu importieren!

Ordnen Sie die folgenden Druckanweisungen den entsprechenden Bibliotheksaufrufen zu.

Druckbefehle:

1. `print("sin(pi/2) =", sin(pi/2))`
2. `print("sin(pi/2) =", m.sin(m.pi/2))`
3. `print("sin(pi/2) =", math.sin(math.pi/2))`

Bibliotheksaufrufe:

1. `from math import sin, pi`
2. `import math`
3. `import math as m`
4. `from math import *`

::::::::::::::: solution

## Lösung

1. Bibliotheksaufrufe 1 und 4. Um direkt auf `sin` und `pi` ohne den Bibliotheksnamen
   als Präfix zu verweisen, müssen Sie die Anweisung `from ... import ...` verwenden.
   Während Bibliotheksaufruf 1 speziell die beiden Funktionen `sin` und `pi` importiert,
   importiert Bibliotheksaufruf 4 alle Funktionen im Modul `math`.
2. Bibliotheksaufruf 3. Hier werden `sin` und `pi` mit einem verkürzten Bibliotheksnamen
   `m` anstelle von `math` angesprochen. Bibliotheksaufruf 3 macht genau das mit der
   Syntax `import ... as ...` - er erzeugt einen Alias für `math` in Form des verkürzten
   Namens `m`.
3. Bibliotheksaufruf 2. Hier wird auf `sin` und `pi` mit dem regulären Bibliotheksnamen
   `math` verwiesen, so dass der reguläre Aufruf `import ...` ausreicht.

**Hinweis:** Obwohl der Bibliotheksaufruf 4 funktioniert, ist es [nicht
empfohlen][pep8-imports], alle Namen aus einem Modul mit einem Platzhalterimport zu
importieren, da es dadurch unklar wird, welche Namen aus dem Modul im Code verwendet
werden. Im Allgemeinen ist es am besten, Ihre Importe so spezifisch wie möglich zu
gestalten und nur das zu importieren, was Ihr Code verwendet. In Bibliotheksaufruf 1
sagt uns die Anweisung `import` explizit, dass die Funktion `sin` aus dem Modul `math`
importiert wird, aber Bibliotheksaufruf 4 vermittelt diese Information nicht.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Importieren bestimmter Elemente

1. Füllen Sie die Leerzeichen aus, damit das folgende Programm `90.0` ausgibt.
2. Finden Sie diese Version leichter zu lesen als die vorhergehenden?
3. Warum *würden* Programmierer nicht immer diese Form von `import` benutzen?

```python
____ math import ____, ____
angle = degrees(pi / 2)
print(angle)
```

::::::::::::::: solution

## Lösung

```python
from math import degrees, pi
angle = degrees(pi / 2)
print(angle)
```

Wahrscheinlich finden Sie diese Version einfacher zu lesen, da sie weniger dicht ist.
Der Hauptgrund, diese Form des Imports nicht zu verwenden, ist die Vermeidung von
Namenskonflikten. Sie würden zum Beispiel `degrees` nicht auf diese Weise importieren,
wenn Sie auch den Namen `degrees` für eine eigene Variable oder Funktion verwenden
wollten. Oder wenn Sie auch eine Funktion mit dem Namen `degrees` aus einer anderen
Bibliothek importieren würden.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lesen von Fehlermeldungen

1. Lesen Sie den folgenden Code und versuchen Sie, die Fehler zu erkennen, ohne ihn
   auszuführen.
2. Führen Sie den Code aus, und lesen Sie die Fehlermeldung. Um welche Art von Fehler
   handelt es sich?

```python
from math import log
log(0)
```

::::::::::::::: solution

## Lösung

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-1-d72e1d780bab> in <module>
      1 from math import log
----> 2 log(0)

ValueError: math domain error
```

1. Der Logarithmus von `x` ist nur für `x > 0` definiert, also liegt 0 außerhalb des
   Bereichs der Funktion.
2. Sie erhalten einen Fehler vom Typ `ValueError`, der anzeigt, dass die Funktion einen
   unpassenden Argumentwert erhalten hat. Die zusätzliche Meldung "math domain error"
   macht deutlicher, wo das Problem liegt.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

[stdlib]: https://docs.python.org/3/library/
[pypi]: https://pypi.python.org/pypi/
[randommod]: https://docs.python.org/3/library/random.html
[pep8-imports]: https://pep8.org/#imports


:::::::::::::::::::::::::::::::::::::::: keypoints

- Der größte Teil der Macht einer Programmiersprache liegt in ihren Bibliotheken.
- Ein Programm muss ein Bibliotheksmodul importieren, um es verwenden zu können.
- Verwenden Sie `help`, um mehr über den Inhalt eines Bibliotheksmoduls zu erfahren.
- Importieren Sie bestimmte Elemente aus einer Bibliothek, um Programme zu verkürzen.
- Erstellen Sie einen Alias für eine Bibliothek, wenn Sie diese importieren, um
  Programme zu verkürzen.

::::::::::::::::::::::::::::::::::::::::::::::::::



