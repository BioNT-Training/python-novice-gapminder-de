---
title: Variablen und Zuweisungen
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Schreibe Programme, die Variablen skalare Werte zuweisen und mit diesen Werten
  Berechnungen durchführen.
- Korrektes Verfolgen von Wertänderungen in Programmen, die skalare Zuweisungen
  verwenden.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich Daten in Programmen speichern?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Verwenden Sie Variablen, um Werte zu speichern.

- **Variablen** sind Namen für Werte.

- Variablennamen

  - kann **nur** Buchstaben, Ziffern und den Unterstrich `_` enthalten (typischerweise
    verwendet, um Wörter in langen Variablennamen zu trennen)
  - darf nicht mit einer Ziffer beginnen
  - sind **groß-klein-klein** (Alter, Alter und AGE sind drei verschiedene Variablen)

- Der Name sollte auch aussagekräftig sein, damit Sie oder ein anderer Programmierer
  wissen, worum es sich handelt

- Variablennamen, die mit Unterstrichen beginnen, wie z.B. `__alistairs_real_age`, haben
  eine besondere Bedeutung, also werden wir das nicht tun, bis wir die Konvention
  verstanden haben.

- In Python ordnet das Symbol `=` den Wert auf der rechten Seite dem Namen auf der
  linken Seite zu.

- Die Variable wird erstellt, wenn ihr ein Wert zugewiesen wird.

- Hier ordnet Python der Variablen `age` ein Alter und der Variablen `first_name` einen
  Namen in Anführungszeichen zu.

  ```python
  age = 42
  first_name = 'Ahmed'
  ```

## Verwenden Sie `print`, um Werte anzuzeigen.

- Python hat eine eingebaute Funktion namens `print`, die Dinge als Text ausgibt.
- Rufen Sie die Funktion auf (d.h. sagen Sie Python, dass es sie ausführen soll), indem
  Sie ihren Namen verwenden.
- Übergeben Sie der Funktion Werte (d.h. die zu druckenden Dinge) in Klammern.
- Um eine Zeichenkette zum Ausdruck hinzuzufügen, schließen Sie die Zeichenkette in
  einfache oder doppelte Anführungszeichen ein.
- Die Werte, die an die Funktion übergeben werden, heißen **arguments**

```python
print(first_name, 'is', age, 'years old')
```

```output
Ahmed is 42 years old
```

- `print` setzt automatisch ein einzelnes Leerzeichen zwischen die Elemente, um sie zu
  trennen.
- Und bricht am Ende in eine neue Zeile um.

## Variablen müssen erstellt werden, bevor sie verwendet werden.

- Wenn eine Variable noch nicht existiert, oder wenn der Name falsch geschrieben wurde,
  meldet Python einen Fehler. (Im Gegensatz zu einigen Sprachen, die einen Standardwert
  "erraten".)

```python
print(last_name)
```

```error
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(last_name)

NameError: name 'last_name' is not defined
```

- Die letzte Zeile einer Fehlermeldung ist normalerweise die informativste.
- Wir werden uns Fehlermeldungen im Detail [später] ansehen
  (17-scope.md#reading-error-messages).

::::::::::::::::::::::::::::::::::::::::: callout

## Variablen bleiben zwischen Zellen bestehen

Beachten Sie, dass die *Reihenfolge* der Ausführung von Zellen in einem
Jupyter-Notizbuch wichtig ist, nicht die Reihenfolge, in der sie erscheinen. Python
merkt sich *den gesamten* Code, der zuvor ausgeführt wurde, einschließlich aller
Variablen, die Sie definiert haben, unabhängig von der Reihenfolge im Notizbuch. Wenn
Sie also Variablen weiter unten im Notizbuch definieren und dann Zellen weiter oben
(erneut) ausführen, sind die weiter unten definierten Variablen weiterhin vorhanden.
Erstellen Sie zum Beispiel zwei Zellen mit dem folgenden Inhalt in dieser Reihenfolge:

```python
print(myval)
```

```python
myval = 1
```

Wenn Sie dies der Reihe nach ausführen, wird die erste Zelle einen Fehler ergeben. Wenn
Sie jedoch die erste Zelle *nach* der zweiten Zelle ausführen, wird sie `1` ausgeben. Um
Verwirrung zu vermeiden, kann es hilfreich sein, die Option `Kernel` -> `Restart & Run
All` zu verwenden, die den Interpreter löscht und alles von oben nach unten durchführt.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Variablen können in Berechnungen verwendet werden.

- Wir können Variablen in Berechnungen so verwenden, als wären sie Werte.
  - Erinnern Sie sich daran, dass wir vor ein paar Zeilen den Wert `42` an `age`
    zugewiesen haben.

```python
age = age + 3
print('Age in three years:', age)
```

```output
Age in three years: 45
```

## Verwenden Sie einen Index, um ein einzelnes Zeichen aus einer Zeichenkette zu erhalten.

- Die Zeichen (einzelne Buchstaben, Zahlen und so weiter) in einer Zeichenkette sind
  geordnet. Zum Beispiel ist die Zeichenkette `'AB'` nicht dasselbe wie `'BA'`. Aufgrund
  dieser Ordnung können wir die Zeichenfolge als eine Liste von Zeichen behandeln.
- Jede Position in der Zeichenkette (erste, zweite usw.) erhält eine Nummer. Diese Zahl
  wird als **Index** oder manchmal auch als tiefgestellt bezeichnet.
- Indizes sind nummeriert von 0.
- Verwenden Sie den Index der Position in eckigen Klammern, um das Zeichen an dieser
  Position zu erhalten.

![Eine Python-Codezeile, print(atom\_name[0]), demonstriert, dass bei Verwendung des
Null-Index nur der Anfangsbuchstabe ausgegeben wird, in diesem Fall 'h' für
Helium.](fig/2_indexing.svg){alt='Erläutern Sie die Indizierung, indem Sie Teilmengen
der Zeichenkette drucken'}

```python
atom_name = 'helium'
print(atom_name[0])
```

```output
h
```

## Verwenden Sie ein Slice, um eine Teilzeichenkette zu erhalten.

- Ein Teil einer Zeichenkette wird **Substring** genannt. Ein Teilstring kann so kurz
  wie ein einzelnes Zeichen sein.
- Ein Element in einer Liste wird Element genannt. Wenn wir eine Zeichenkette wie eine
  Liste behandeln, sind die Elemente der Zeichenkette ihre einzelnen Zeichen.
- Ein Slice ist ein Teil einer Zeichenkette (oder, allgemeiner, ein Teil einer
  beliebigen listähnlichen Sache).
- Wir nehmen ein Slice mit der Notation `[start:stop]`, wobei `start` der ganzzahlige
  Index des ersten Elements ist, das wir wollen, und `stop` der ganzzahlige Index des
  Elements *gerade nach* dem letzten Element ist, das wir wollen.
- Der Unterschied zwischen `stop` und `start` ist die Länge des Slice.
- Die Entnahme eines Slice verändert nicht den Inhalt der ursprünglichen Zeichenkette.
  Stattdessen wird eine Kopie eines Teils der ursprünglichen Zeichenkette zurückgegeben.

```python
atom_name = 'sodium'
print(atom_name[0:3])
```

```output
sod
```

## Verwenden Sie die eingebaute Funktion `len`, um die Länge einer Zeichenkette zu ermitteln.

```python
print(len('helium'))
```

```output
6
```

- Verschachtelte Funktionen werden von innen nach außen ausgewertet, wie in der
  Mathematik.

## Python unterscheidet Groß- und Kleinschreibung.

- Python denkt, dass Groß- und Kleinbuchstaben unterschiedlich sind, also sind `Name`
  und `name` unterschiedliche Variablen.
- Es gibt Konventionen für die Verwendung von Großbuchstaben am Anfang von
  Variablennamen, daher werden wir für den Moment Kleinbuchstaben verwenden.

## Verwenden Sie aussagekräftige Variablennamen.

- Python kümmert sich nicht darum, wie Sie Variablen nennen, solange sie die Regeln
  befolgen (alphanumerische Zeichen und der Unterstrich).

```python
flabadab = 42
ewr_422_yY = 'Ahmed'
print(ewr_422_yY, 'is', flabadab, 'years old')
```

- Verwende aussagekräftige Variablennamen, damit andere Leute verstehen, was das
  Programm macht.
- Die wichtigste "andere Person" ist dein zukünftiges Ich.

::::::::::::::::::::::::::::::::::::::: challenge

## Vertauschen von Werten

Füllen Sie die Tabelle mit den Werten der Variablen in diesem Programm aus, *nach* dem
jede Anweisung ausgeführt wurde.

```python
# Command  # Value of x   # Value of y   # Value of swap #
x = 1.0    #              #              #               #
y = 3.0    #              #              #               #
swap = x   #              #              #               #
x = y      #              #              #               #
y = swap   #              #              #               #
```

::::::::::::::: solution

## Lösung

```output
# Command  # Value of x   # Value of y   # Value of swap #
x = 1.0    # 1.0          # not defined  # not defined   #
y = 3.0    # 1.0          # 3.0          # not defined   #
swap = x   # 1.0          # 3.0          # 1.0           #
x = y      # 3.0          # 3.0          # 1.0           #
y = swap   # 3.0          # 1.0          # 1.0           #
```

Diese drei Zeilen tauschen die Werte in `x` und `y` aus, indem sie die Variable `swap`
zur temporären Speicherung verwenden. Dies ist eine ziemlich übliche Programmiersprache.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Vorhersage von Werten

Was ist der endgültige Wert von `position` in dem untenstehenden Programm? (Versuchen
Sie, den Wert vorherzusagen, ohne das Programm auszuführen, und überprüfen Sie dann Ihre
Vorhersage)

```python
initial = 'left'
position = initial
initial = 'right'
```

::::::::::::::: solution

## Lösung

```python
print(position)
```

```output
left
```

Der Variablen `initial` wird der Wert `'left'` zugewiesen. In der zweiten Zeile erhält
die Variable `position` ebenfalls den Stringwert `'left'`. In der dritten Zeile erhält
die Variable `initial` den Wert `'right'`, aber die Variable `position` behält ihren
String-Wert `'left'`.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Herausforderung

Wenn Sie `a = 123` zuweisen, was passiert, wenn Sie versuchen, die zweite Ziffer von `a`
über `a[1]` zu erhalten?

::::::::::::::: solution

## Lösung

Zahlen sind keine Zeichenketten oder Sequenzen und Python gibt einen Fehler aus, wenn
Sie versuchen, eine Index-Operation mit einer Zahl durchzuführen. In der [nächsten
Lektion über Typen und Typkonvertierung](03-types-conversion.md) werden wir mehr über
Typen lernen und wie man zwischen verschiedenen Typen konvertiert. Wenn man die N-te
Stelle einer Zahl sucht, kann man sie mit der eingebauten Funktion `str` in eine
Zeichenkette umwandeln und dann eine Indexoperation mit dieser Zeichenkette durchführen.

```python
a = 123
print(a[1])
```

```error
TypeError: 'int' object is not subscriptable
```

```python
a = str(123)
print(a[1])
```

```output
2
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Auswahl eines Namens

Welcher ist ein besserer Variablenname, `m`, `min` oder `minutes`? Tipp: Überlegen Sie,
welchen Code Sie lieber von jemandem erben würden, der das Labor verlässt:

1. `ts = m * 60 + s`
2. `tot_sec = min * 60 + sec`
3. `total_seconds = minutes * 60 + seconds`

::::::::::::::: solution

## Lösung

`minutes` ist besser, weil `min` so etwas wie "Minimum" bedeuten könnte (und eigentlich
eine eingebaute Funktion in Python ist, die wir später behandeln werden).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Slicing Praxis

Was gibt das folgende Programm aus?

```python
atom_name = 'carbon'
print('atom_name[1:3] is:', atom_name[1:3])
```

::::::::::::::: solution

## Lösung

```output
atom_name[1:3] is: ar
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Slicing-Konzepte

Gegeben sei die folgende Zeichenkette:

```python
species_name = "Acacia buxifolia"
```

Was würden diese Ausdrücke zurückgeben?

1. `species_name[2:8]`
2. `species_name[11:]` (ohne einen Wert nach dem Doppelpunkt)
3. `species_name[:4]` (ohne einen Wert vor dem Doppelpunkt)
4. `species_name[:]` (nur ein Doppelpunkt)
5. `species_name[11:-3]`
6. `species_name[-5:-3]`
7. Was passiert, wenn man einen `stop` Wert wählt, der außerhalb des Bereichs liegt?
   (d.h., versuchen Sie `species_name[0:20]` oder `species_name[:103]`)

::::::::::::::: solution

## Lösungen

1. `species_name[2:8]` gibt die Teilzeichenkette `'acia b'` zurück
2. `species_name[11:]` gibt die Teilzeichenkette `'folia'` zurück, von Position 11 bis
   zum Ende
3. `species_name[:4]` gibt die Teilzeichenkette `'Acac'` zurück, vom Anfang bis zur
   Position 4, aber ohne diese
4. `species_name[:]` gibt die gesamte Zeichenkette `'Acacia buxifolia'` zurück
5. `species_name[11:-3]` gibt die Teilzeichenkette `'fo'` zurück, von der 11. bis zur
   drittletzten Position
6. `species_name[-5:-3]` gibt auch die Teilzeichenkette `'fo'` zurück, von der
   fünftletzten bis zur drittletzten Position
7. Wenn ein Teil des Slice außerhalb des Bereichs liegt, schlägt die Operation nicht
   fehl.`species_name[0:20]` liefert das gleiche Ergebnis wie `species_name[0:]`, und
   `species_name[:103]` liefert das gleiche Ergebnis wie `species_name[:]`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Verwende Variablen, um Werte zu speichern.
- Verwenden Sie `print`, um Werte anzuzeigen.
- Variablen bleiben zwischen Zellen bestehen.
- Variablen müssen erstellt werden, bevor sie verwendet werden.
- Variablen können in Berechnungen verwendet werden.
- Verwenden Sie einen Index, um ein einzelnes Zeichen aus einer Zeichenkette zu
  erhalten.
- Verwenden Sie ein Slice, um eine Teilzeichenkette zu erhalten.
- Verwenden Sie die eingebaute Funktion `len`, um die Länge einer Zeichenkette zu
  ermitteln.
- Python unterscheidet Groß- und Kleinschreibung.
- Verwenden Sie aussagekräftige Variablennamen.

::::::::::::::::::::::::::::::::::::::::::::::::::



