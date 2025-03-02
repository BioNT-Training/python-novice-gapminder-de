---
title: Variablenumfang
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Identifizieren Sie lokale und globale Variablen.
- Identifizieren Sie Parameter als lokale Variablen.
- Lies einen Traceback und bestimme die Datei, Funktion und Zeilennummer, in der der
  Fehler aufgetreten ist, den Fehlertyp und die Fehlermeldung.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie funktionieren eigentlich Funktionsaufrufe?
- Wie kann ich feststellen, wo Fehler aufgetreten sind?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Der Geltungsbereich einer Variablen ist der Teil eines Programms, der diese Variable 'sehen' kann.

- Es gibt nur so viele sinnvolle Namen für Variablen.
- Leute, die Funktionen benutzen, sollten sich nicht darum kümmern müssen, welche
  Variablennamen der Autor der Funktion benutzt hat.
- Leute, die Funktionen schreiben, sollten sich nicht darum kümmern müssen, welche
  Variablennamen der Funktionsaufrufer verwendet.
- Der Teil eines Programms, in dem eine Variable sichtbar ist, wird ihr *Scope* genannt.

```python
pressure = 103.9

def adjust(t):
    temperature = t * 1.43 / pressure
    return temperature
```

- `pressure` ist eine *globale Variable*.
  - Definiert außerhalb einer bestimmten Funktion.
  - Überall sichtbar.
- `t` und `temperature` sind *lokale Variablen* in `adjust`.
  - Definiert in der Funktion.
  - Nicht sichtbar im Hauptprogramm.
  - Erinnern Sie sich: Ein Funktionsparameter ist eine Variable, der automatisch ein
    Wert zugewiesen wird, wenn die Funktion aufgerufen wird.

```python
print('adjusted:', adjust(0.9))
print('temperature after call:', temperature)
```

```output
adjusted: 0.01238691049085659
```

```error
Traceback (most recent call last):
  File "/Users/swcarpentry/foo.py", line 8, in <module>
    print('temperature after call:', temperature)
NameError: name 'temperature' is not defined
```

::::::::::::::::::::::::::::::::::::::: challenge

## Verwendung von lokalen und globalen Variablen

Verfolge die Werte aller Variablen in diesem Programm, während es ausgeführt wird.
(Verwenden Sie '---' als Wert der Variablen, bevor und nachdem sie existieren.)

```python
limit = 100

def clip(value):
    return min(max(0.0, value), limit)

value = -22.5
print(clip(value))
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lesen von Fehlermeldungen

Lesen Sie den Traceback unten, und identifizieren Sie das Folgende:

1. Wie viele Ebenen hat der Traceback?
2. Wie lautet der Name der Datei, in der der Fehler aufgetreten ist?
3. Wie lautet der Name der Funktion, bei der der Fehler aufgetreten ist?
4. Bei welcher Zeilennummer in dieser Funktion ist der Fehler aufgetreten?
5. Um welche Art von Fehler handelt es sich?
6. Wie lautet die Fehlermeldung?

```error
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-2-e4c4cbafeeb5> in <module>()
      1 import errors_02
----> 2 errors_02.print_friday_message()

/Users/ghopper/thesis/code/errors_02.py in print_friday_message()
     13
     14 def print_friday_message():
---> 15     print_message("Friday")

/Users/ghopper/thesis/code/errors_02.py in print_message(day)
      9         "sunday": "Aw, the weekend is almost over."
     10     }
---> 11     print(messages[day])
     12
     13

KeyError: 'Friday'
```

::::::::::::::: solution

## Lösung

1. Drei Ebenen.
2. `errors_02.py`
3. `print_message`
4. Zeile 11
5. `KeyError`. Diese Fehler treten auf, wenn versucht wird, einen Schlüssel
   nachzuschlagen, der nicht vorhanden ist (normalerweise in einer Datenstruktur wie
   einem Wörterbuch). Weitere Informationen über `KeyError` und andere eingebaute
   Ausnahmen finden Sie in den [Python
   docs](https://docs.python.org/3/library/exceptions.html#KeyError).
6. `KeyError: 'Friday'`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Der Geltungsbereich einer Variablen ist der Teil eines Programms, der diese Variable
  'sehen' kann.

::::::::::::::::::::::::::::::::::::::::::::::::::



