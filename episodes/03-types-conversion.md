---
title: Datentypen und Typkonvertierung
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erläutern Sie die wichtigsten Unterschiede zwischen Ganzzahlen und Fließkommazahlen.
- Erläutern Sie die wichtigsten Unterschiede zwischen Zahlen und Zeichenketten.
- Verwenden Sie eingebaute Funktionen, um zwischen Ganzzahlen, Fließkommazahlen und
  Zeichenketten zu konvertieren.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Welche Arten von Daten werden in Programmen gespeichert?
- Wie kann ich einen Typ in einen anderen umwandeln?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Jeder Wert hat einen Typ.

- Jeder Wert in einem Programm hat einen bestimmten Typ.
- Integer (`int`): repräsentiert positive oder negative ganze Zahlen wie 3 oder -512.
- Fließkommazahl (`float`): repräsentiert reelle Zahlen wie 3.14159 oder -2.5.
- Zeichenkette (gewöhnlich "string" genannt, `str`): text.
  - Wird entweder in einfachen oder in doppelten Anführungszeichen geschrieben (solange
    sie übereinstimmen).
  - Die Anführungszeichen werden nicht gedruckt, wenn die Zeichenkette angezeigt wird.

## Verwenden Sie die eingebaute Funktion `type`, um den Typ eines Wertes zu ermitteln.

- Verwenden Sie die eingebaute Funktion `type`, um herauszufinden, welchen Typ ein Wert
  hat.
- Funktioniert auch mit Variablen.
  - Aber denken Sie daran: der *Wert* hat den Typ --- die *Variable* ist nur eine
    Bezeichnung.

```python
print(type(52))
```

```output
<class 'int'>
```

```python
fitness = 'average'
print(type(fitness))
```

```output
<class 'str'>
```

## Typen steuern, welche Operationen (oder Methoden) mit einem bestimmten Wert durchgeführt werden können.

- Der Typ eines Wertes bestimmt, was das Programm mit ihm machen kann.

```python
print(5 - 3)
```

```output
2
```

```python
print('hello' - 'h')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-67f5626a1e07> in <module>()
----> 1 print('hello' - 'h')

TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## Sie können die Operatoren "+" und "\*" auf Zeichenketten anwenden.

- "Hinzufügen" von Zeichenketten verkettet diese.

```python
full_name = 'Ahmed' + ' ' + 'Walsh'
print(full_name)
```

```output
Ahmed Walsh
```

- Die Multiplikation einer Zeichenkette mit einer ganzen Zahl *N* erzeugt eine neue
  Zeichenkette, die aus dieser Zeichenkette besteht, die *N* Mal wiederholt wird.
  - Da die Multiplikation eine wiederholte Addition ist.

```python
separator = '=' * 10
print(separator)
```

```output
==========
```

## Strings haben eine Länge (aber Zahlen nicht).

- Die eingebaute Funktion `len` zählt die Anzahl der Zeichen in einer Zeichenkette.

```python
print(len(full_name))
```

```output
11
```

- Aber Zahlen haben keine Länge (nicht einmal Null).

```python
print(len(52))
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-f769e8e8097d> in <module>()
----> 1 print(len(52))

TypeError: object of type 'int' has no len()
```

## Bei der Verarbeitung von Zahlen müssen diese in Zeichenfolgen umgewandelt werden oder umgekehrt. {#Zahlen-und-Zeichenketten-umwandeln}

- Kann keine Zahlen und Strings addieren.

```python
print(1 + '2')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-fe4f54a023c6> in <module>()
----> 1 print(1 + '2')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

- Nicht erlaubt, weil mehrdeutig: sollte `1 + '2'` `3` oder `'12'` sein?
- Einige Typen können in andere Typen konvertiert werden, indem der Typname als Funktion
  verwendet wird.

```python
print(1 + int('2'))
print(str(1) + '2')
```

```output
3
12
```

## Kann Ganzzahlen und Fließkommazahlen in Operationen frei mischen.

- Ganzzahlen und Fließkommazahlen können in der Arithmetik gemischt werden.
  - Python 3 wandelt ganze Zahlen bei Bedarf automatisch in Fließkommazahlen um.

```python
print('half is', 1 / 2.0)
print('three squared is', 3.0 ** 2)
```

```output
half is 0.5
three squared is 9.0
```

## Variablen ändern ihren Wert nur, wenn ihnen etwas zugewiesen wird.

- Wenn wir eine Zelle in einem Arbeitsblatt von einer anderen abhängig machen und
  letztere aktualisieren, wird die erstere automatisch aktualisiert.
- Dies geschieht **nicht** in Programmiersprachen.

```python
variable_one = 1
variable_two = 5 * variable_one
variable_one = 2
print('first is', variable_one, 'and second is', variable_two)
```

```output
first is 2 and second is 5
```

- Der Computer liest den Wert von `variable_one`, wenn er die Multiplikation durchführt,
  erzeugt einen neuen Wert und weist ihn `variable_two` zu.
- Danach wird der Wert von `variable_two` auf den neuen Wert gesetzt und *nicht abhängig
  von `variable_one`*, so dass sich sein Wert nicht automatisch ändert, wenn sich
  `variable_one` ändert.

::::::::::::::::::::::::::::::::::::::: challenge

## Brüche

Was für ein Wert ist 3,4? Wie kann man das herausfinden?

::::::::::::::: solution

## Lösung

Es handelt sich um eine Gleitkommazahl (oft mit "float" abgekürzt). Das kann man mit der
eingebauten Funktion `type()` herausfinden.

```python
print(type(3.4))
```

```output
<class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Automatische Typkonvertierung

Was für ein Wert ist 3,25 + 4?

::::::::::::::: solution

## Lösung

Es handelt sich um eine Fließkommazahl: Ganzzahlen werden bei Bedarf automatisch in
Fließkommazahlen umgewandelt.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Wählen Sie einen Typ

Welche Art von Wert (Ganzzahl, Fließkommazahl oder Zeichenkette) würden Sie verwenden,
um jede der folgenden Angaben darzustellen? Versuchen Sie, mehr als eine gute Antwort
für jedes Problem zu finden. Wann wäre zum Beispiel in Frage 1 das Zählen von Tagen mit
einer Fließkommazahl sinnvoller als mit einer ganzen Zahl?

1. Anzahl der Tage seit Beginn des Jahres.
2. Zeit, die vom Jahresanfang bis jetzt verstrichen ist, in Tagen.
3. Seriennummer eines Laborgerätes.
4. Das Alter einer Laborprobe
5. Aktuelle Einwohnerzahl einer Stadt.
6. Durchschnittliche Einwohnerzahl einer Stadt über die Zeit.

::::::::::::::: solution

## Lösung

Die Antworten auf die Fragen lauten:

1. Ganzzahl, da die Anzahl der Tage zwischen 1 und 365 liegen würde.
2. Fließkomma, da gebrochene Tage benötigt werden
3. Zeichenkette, wenn die Seriennummer Buchstaben und Zahlen enthält, andernfalls
   Ganzzahl, wenn die Seriennummer nur aus Ziffern besteht
4. Dies wird variieren! Wie definiert man das Alter einer Probe? ganze Tage seit der
   Entnahme (Integer)? Datum und Uhrzeit (String)?
5. Wählen Sie Fließkommazahlen, um die Bevölkerung als große Aggregate (z.B. Millionen)
   darzustellen, oder Ganzzahlen, um die Bevölkerung in Einheiten von Individuen
   darzustellen.
6. Fließkommazahl, da ein Durchschnitt wahrscheinlich einen Bruchteil hat.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Divisionstypen

In Python 3 führt der `//`-Operator Ganzzahldivisionen durch, der `/`-Operator führt
Fließkommadivisionen durch, und der `%`-Operator (oder *modulo*) berechnet den Rest
einer Ganzzahldivision und gibt ihn zurück:

```python
print('5 // 3:', 5 // 3)
print('5 / 3:', 5 / 3)
print('5 % 3:', 5 % 3)
```

```output
5 // 3: 1
5 / 3: 1.6666666666666667
5 % 3: 2
```

Wenn `num_subjects` die Anzahl der Probanden ist, die an einer Studie teilnehmen, und
`num_per_survey` die Anzahl, die an einer einzigen Umfrage teilnehmen kann, schreibe
einen Ausdruck, der die Anzahl der Umfragen berechnet, die nötig sind, um alle einmal zu
erreichen.

::::::::::::::: solution

## Lösung

Wir wollen die minimale Anzahl von Umfragen, die jeden einmal erreicht, was der
aufgerundete Wert von `num_subjects/ num_per_survey` ist. Dies ist gleichbedeutend mit
der Durchführung einer Bodenteilung durch `//` und der Addition von 1. Vor der Division
müssen wir 1 von der Anzahl der Probanden subtrahieren, um den Fall zu behandeln, dass
`num_subjects` durch `num_per_survey` gleichmäßig teilbar ist.

```python
num_subjects = 600
num_per_survey = 42
num_surveys = (num_subjects - 1) // num_per_survey + 1

print(num_subjects, 'subjects,', num_per_survey, 'per survey:', num_surveys)
```

```output
600 subjects, 42 per survey: 15
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Zeichenketten in Zahlen umwandeln

Wo es sinnvoll ist, konvertiert `float()` einen String in eine Fließkommazahl und
`int()` konvertiert eine Fließkommazahl in eine Ganzzahl:

```python
print("string to float:", float("3.4"))
print("float to int:", int(3.4))
```

```output
string to float: 3.4
float to int: 3
```

Wenn die Konvertierung jedoch keinen Sinn ergibt, wird eine Fehlermeldung ausgegeben.

```python
print("string to float:", float("Hello world!"))
```

```error
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-5-df3b790bf0a2> in <module>
----> 1 print("string to float:", float("Hello world!"))

ValueError: could not convert string to float: 'Hello world!'
```

Was erwarten Sie angesichts dieser Informationen von dem folgenden Programm?

Was macht sie eigentlich?

Warum glauben Sie, dass es das tut?

```python
print("fractional string to int:", int("3.4"))
```

::::::::::::::: solution

## Lösung

Was erwarten Sie von diesem Programm zu tun? Es wäre gar nicht so abwegig zu erwarten,
dass der Python 3 `int`-Befehl die Zeichenkette "3.4" in 3.4 und eine zusätzliche
Typkonvertierung in 3 umwandelt. Schließlich kann Python 3 noch eine Menge anderer
Zaubereien - ist das nicht Teil seines Charmes?

```python
int("3.4")
```

```output
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-2-ec6729dfccdc> in <module>
----> 1 int("3.4")
ValueError: invalid literal for int() with base 10: '3.4'
```

Python 3 gibt jedoch einen Fehler aus. Warum eigentlich? Um konsistent zu sein,
möglicherweise. Wenn Sie Python auffordern, zwei aufeinanderfolgende Typecasts
durchzuführen, müssen Sie es explizit im Code umwandeln.

```python
int(float("3.4"))
```

```output
3
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Arithmetik mit verschiedenen Typen

Welche der folgenden Möglichkeiten gibt die Fließkommazahl `2.0` zurück? Hinweis: Es
kann mehr als eine richtige Antwort geben.

```python
first = 1.0
second = "1"
third = "1.1"
```

1. `first + float(second)`
2. `float(second) + float(third)`
3. `first + int(third)`
4. `first + int(float(third))`
5. `int(first) + int(float(third))`
6. `2.0 * second`

::::::::::::::: solution

## Lösung

Antwort: 1 und 4



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Komplexe Zahlen

Python bietet komplexe Zahlen, die als `1.0+2.0j` geschrieben werden. Wenn `val` eine
komplexe Zahl ist, können ihre realen und imaginären Teile mit der *Punktnotation* als
`val.real` und `val.imag` angesprochen werden.

```python
a_complex_number = 6 + 2j
print(a_complex_number.real)
print(a_complex_number.imag)
```

```output
6.0
2.0
```

1. Warum, glaubst du, verwendet Python `j` statt `i` für den Imaginärteil?
2. Was soll `1 + 2j + 3` ergeben?
3. Was erwarten Sie von `4j`? Was ist mit `4 j` oder `4 + j`?

::::::::::::::: solution

## Lösung

1. In der Standardmathematik wird üblicherweise `i` zur Bezeichnung einer imaginären
   Zahl verwendet. Medienberichten zufolge handelt es sich dabei jedoch um eine frühe
   Konvention aus der Elektrotechnik, deren Änderung nun einen technisch aufwendigen
   Bereich darstellt. [Stack Overflow bietet zusätzliche Erklärungen und
   Diskussionen](https://stackoverflow.com/questions/24812444/why-are-complex-numbers-in-python-denoted-with-j-instead-of-i)
2. `(4+2j)`
3. `4j` und `Syntax Error: invalid syntax`. In den letztgenannten Fällen wird `j` als
   Variable betrachtet und die Aussage hängt davon ab, ob `j` definiert ist und wenn ja,
   welcher Wert ihm zugewiesen wurde.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Jeder Wert hat einen Typ.
- Verwenden Sie die eingebaute Funktion `type`, um den Typ eines Wertes zu ermitteln.
- Typen steuern, welche Operationen mit Werten durchgeführt werden können.
- Strings können addiert und multipliziert werden.
- Zeichenketten haben eine Länge (Zahlen jedoch nicht).
- Muss Zahlen in Zeichenketten umwandeln oder umgekehrt, wenn er mit ihnen operiert.
- Kann Ganzzahlen und Fließkommazahlen in Operationen frei mischen.
- Variablen ändern ihren Wert nur, wenn ihnen etwas zugewiesen wird.

::::::::::::::::::::::::::::::::::::::::::::::::::



