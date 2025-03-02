---
title: Referenz
---


## Referenz

## [Ausführen und Beenden](episodes/01-run-quit.md)

- Python-Dateien haben die Erweiterung `.py`.
- Kann in eine Textdatei oder ein [Jupyter Notebook][jupyter] geschrieben werden.
  - Jupyter-Notebooks haben die Erweiterung `.ipynb`
  - Jupyter-Notizbücher können über
    [Anaconda](https://docs.continuum.io/anaconda/install) oder über die Kommandozeile
    durch Eingabe von `$ jupyter notebook` geöffnet werden
    - Markdown und HTML sind in Markdown-Zellen zur Dokumentation von Code erlaubt.

## [Variablen und Zuweisung](episodes/02-variables.md)

- Variablen werden mit `=` gespeichert.
  - Strings werden in Anführungszeichen `'...'` definiert.
  - Ganzzahlen und Fließkommazahlen werden ohne Anführungszeichen definiert.
- Variablen können Buchstaben, Ziffern und Unterstriche `_` enthalten.
  - Kann nicht mit einer Ziffer beginnen.
  - Variablen, die mit Unterstrichen beginnen, sollten vermieden werden.
- Verwenden Sie `print(...)`, um Werte als Text anzuzeigen.
- Kann Indizierung auf Strings verwenden.
  - Die Indizierung beginnt bei 0.
  - Die Position wird in eckigen Klammern `[position]` nach dem Variablennamen
    angegeben.
  - Nimmt einen Ausschnitt mit `[start:stop]`. Dadurch wird eine Kopie eines Teils der
    ursprünglichen Zeichenkette erstellt.
    - `start` ist der Index des ersten Elements.
    - `stop` ist der Index des Elements nach dem letzten gewünschten Element.
- Verwenden Sie `len(...)`, um die Länge einer Variablen oder eines Strings zu
  ermitteln.

## [Datentypen und Typkonvertierung](episodes/03-types-conversion.md)

- Jeder Wert hat einen Typ. Dieser steuert, was mit ihm gemacht werden kann.
  - `int` repräsentiert eine ganze Zahl
  - `float` stellt eine Fließkommazahl dar.
  - `str` stellt eine Zeichenkette dar.
- Um einen Variablentyp zu bestimmen, verwenden Sie die eingebaute Funktion `type(...)`,
  einschließlich des Variablennamens in der Klammer.
- Ändern von Zeichenketten:
  - Verwenden Sie `+` um Strings zu verketten.
  - Verwenden Sie `*`, um eine Zeichenkette zu wiederholen.
  - Zahlen und Strings können nicht zueinander addiert werden.
    - Konvertiert String in Integer: `int(...)`.
    - Konvertiert Ganzzahl in String: `str(...)`.

## [Built-in Funktionen und Hilfe](episodes/04-built-in.md)

- Um einen Kommentar hinzuzufügen, setzen Sie `#` vor die Sache, die nicht ausgeführt
  werden soll.
- Häufig verwendete eingebaute Funktionen:
  - `min()` findet den kleinsten Wert.
  - `max()` findet den größten Wert.
  - `round()` rundet eine Fließkommazahl ab.
  - `help()` zeigt die Dokumentation für die Funktion in der Klammer an.
    - Andere Möglichkeiten, Hilfe zu erhalten, sind das Gedrückthalten von `shift` und
      das Drücken von `tab` in Jupyter Notebooks.

## [Bibliotheken](episodes/06-libraries.md)

- Importieren einer Bibliothek:
  - Verwenden Sie `import ...`, um eine Bibliothek zu laden.
  - Verweist auf diese Bibliothek durch Verwendung von `module_name.thing_name`.
    - `.` bedeutet 'Teil von'.
- Um ein bestimmtes Element aus einer Bibliothek zu importieren: `from ... import ...`
- Um eine Bibliothek mit einem Alias zu importieren: `import ... as ...`
- Importieren der mathematischen Bibliothek: `import math`
  - Beispiel eines Verweises auf ein Element mit dem Namen des Moduls:
    `math.cos(math.pi)`.
- Importieren der Plotting-Bibliothek als Alias: `import matplotlib as mpl`

## [Lesen von Tabellendaten in DataFrames](episodes/07-reading-tabular.md)

- Verwenden Sie die Pandas-Bibliothek, um Statistiken über tabellarische Daten zu
  erstellen. Laden mit `import pandas as pd`.
  - Um eine csv-Datei einzulesen: `pd.read_csv()`, einschließlich des Pfadnamens in der
    Klammer.
    - Um anzugeben, dass die Werte einer Spalte als Zeilenüberschriften verwendet werden
      sollen:`pd.read_csv('path', index_col='column name')`, wobei Pfad und Spaltenname
      durch die entsprechenden Werte zu ersetzen sind.
- Um mehr Informationen über einen DataFrame zu erhalten, verwenden Sie
  `DataFrame.info`, wobei Sie `DataFrame` durch den Variablennamen Ihres DataFrame
  ersetzen.
- Verwenden Sie `DataFrame.columns`, um die Spaltennamen anzuzeigen.
- Verwenden Sie `DataFrame.T` um einen DataFrame zu transponieren.
- Verwenden Sie `DataFrame.describe`, um zusammenfassende Statistiken über Ihre Daten zu
  erhalten.

## [Pandas DataFrames](episodes/08-data-frames.md)

- Selektieren von Daten mit `[i,j]`
  - Zur Auswahl nach Eingabeposition: `DataFrame.iloc[..., ...]`
    - Dies beinhaltet alles außer dem Endindex.
  - Zur Auswahl nach Eintragsbezeichnung: `DataFrame.loc[..., ...]`
    - Kann mehrere Zeilen oder Spalten durch Auflistung von Labels auswählen.
    - Dies gilt für beide Enden.
  - Verwenden Sie `:`, um alle Zeilen oder Spalten auszuwählen.
- Es können auch Daten auf der Grundlage von Werten mit `True` und `False` ausgewählt
  werden. Dies ist eine boolesche Maske.
  - `mask = subset > 10000`
  - Damit können wir dann Werte auswählen.
- Um eine select-apply-combine-Operation zu verwenden, verwenden wir `data.apply(lambda
  x: x > x.mean())`, wobei `mean()` eine beliebige Operation sein kann, die der Benutzer
  auf x anwenden möchte.

## [Plotting](episodes/09-plotting.md)

- Die am weitesten verbreitete Bibliothek zum Plotten ist `matplotlib`.
  - Normalerweise importiert mit `import matplotlib.pyplot as plt`.
  - Zum Plotten verwenden wir den Befehl `plt.plot(time, position)`.
  - Um eine Legende zu erstellen, verwenden Sie `plt.legend(['label1', 'label2'],
    loc='upper left')`
    - Sie können auch Beschriftungen innerhalb der Plot-Anweisungen definieren, indem
      Sie `plt.plot(time, position, label='label')` verwenden. Um die Legende
      einzublenden, verwenden Sie `plt.legend()`
  - Zur Bezeichnung der x- und y-Achse werden `plt.xlabel('label')` und
    `plt.ylabel('label')` verwendet.
- Pandas DataFrames können zum Plotten verwendet werden, indem man `DataFrame.plot()`
  benutzt. Alle Operationen, die auf einen DataFrame angewendet werden können, können
  auch beim Plotten angewendet werden.
  - Um ein Balkendiagramm zu erstellen `data.plot(kind='bar')`

```python
import matplotlib.puplot as plot
plt.plot(time, position, label='label')
plt.xlabel('x axis label')
plt.ylabel('y axis label')
plt.legend()
```

## [Listen](episodes/11-lists.md)

- Definiert innerhalb von `[...]` und getrennt durch `,`.
  - Eine leere Liste kann durch die Verwendung von `[]` erstellt werden.
- Kann `len(...)` benutzen, um zu bestimmen, wie viele Werte in einer Liste sind.
- Kann genau wie in den vorherigen Lektionen indexiert werden.
  - Indizierung kann verwendet werden, um Werte `list_name[0] = newvalue` neu
    zuzuordnen.
- Um ein Element zu einer Liste hinzuzufügen, verwenden Sie `list_name.append()`, mit
  dem anzuhängenden Element in der Klammer.
- Um zwei Listen zu kombinieren, verwenden Sie `list_name_1.extend(list_name_2)`.
- Um ein Element aus einer Liste zu entfernen, verwenden Sie `del list_name[index]`.

## [For-Schleifen](episodes/12-for-loops.md)

- Beginnen Sie eine for-Schleife mit `for number in [1, 2, 3]:`, mit den folgenden
  Zeilen eingerückt.
  - `[1, 2, 3]` wird als die Sammlung betrachtet.
  - `number` ist die Schleifenvariable.
  - Die auf die Sammlung folgende Aktion ist der Körper.
- Um über eine Folge von Zahlen zu iterieren, verwenden Sie `range(start, end)`

```python
for number in range(0,5):
    print(number)
```

## [Conditionals](episodes/13-conditionals.md)

- Ähnlich definiert wie eine Schleife, unter Verwendung von `if variable conditional
  value:`.
  - Zum Beispiel, `if variable > 5:`.
- Verwenden Sie `elif:` für zusätzliche Tests.
- Verwenden Sie `else:`, wenn die if-Anweisung nicht wahr ist.
- Kann mehr als eine Bedingung durch Verwendung von `and` oder `or` kombinieren.
- Wird oft in Kombination mit for-Schleifen verwendet.
- Bedingungen, die verwendet werden können:
  - `==` gleich.
  - `>=` größer als oder gleich.
  - `<=` kleiner als oder gleich.
  - `>` größer als.
  - `<` kleiner als.

```python
for m in [3, 6, 7, 2, 8]:
    if m > 5:
        print(m, 'is large')
    elif m == 5:
        print(m, 'is 5')
    else:
        print(m, 'is small')
```

## [Schleifen über Datensätze](episodes/14-looping-data-sets.md)

- Verwenden Sie eine for-Schleife: `for filename in [file1, file2]:`
- Um eine Menge von Dateien mit einem Muster zu finden, verwenden Sie `glob.glob`
  - Muss zuerst mit `import glob` importiert werden.
  - `*` bedeutet "entspricht null oder mehr Zeichen"
  - `?` bedeutet "genau ein Zeichen übereinstimmen"
    - Zum Beispiel: `glob.glob(*.txt)` findet alle Dateien, die mit `.txt` im aktuellen
      Verzeichnis enden.
- Kombinieren Sie diese, indem Sie eine Schleife schreiben: `for filename in
  glob.glob(*.txt):`

```python
for filename in glob.glob(*.txt):
  data = pd.read_csv(filename)
```

## [Schreibfunktionen](episodes/16-writing-functions.md)

- Definieren Sie eine Funktion mit `def function_name(parameters):`. Ersetzen Sie
  `parameters` durch die Variablen, die bei der Ausführung der Funktion verwendet werden
  sollen.
- Ausgeführt mit `function_name(parameters)`.
- Um ein Ergebnis an den Aufrufer zurückzugeben, verwenden Sie `return ...` in der
  Funktion.

```python
def add_numbers(a, b):
    result = a + b
    return result

add_numbers(1, 4)
```

## [Variablenumfang](episodes/17-scope.md)

- Eine lokale Variable ist in einer Funktion definiert und kann nur innerhalb dieser
  Funktion gesehen und verwendet werden.
- Eine globale Variable wird außerhalb einer Funktion definiert und kann nach der
  Definition überall gesehen oder verwendet werden.

## [Programmierstil](episodes/18-style.md)

- Dokumentieren Sie Ihren Code.
- Verwenden Sie klare und aussagekräftige Variablennamen.
- Folgen Sie [dem PEP8 Style Guide](https://www.python.org/dev/peps/pep-0008), wenn Sie
  Ihren Code einrichten.
- Verwenden Sie Assertions, um auf interne Fehler zu prüfen.
- Verwenden Sie docstrings, um Hilfe zu geben.

## Glossar

Argumente : Werte, die an Funktionen übergeben werden.

Array : Ein Container, der Elemente desselben Typs enthält.

Boolean : Ein Objekt, das aus `True` und `False` besteht.

DataFrame : Die Art, wie Pandas eine Tabelle darstellt; eine Sammlung von Reihen.

Element : Ein Element in einer Liste oder einem Array. Bei einer Zeichenkette sind dies
die einzelnen Zeichen.

Funktion : Ein Code-Block, der aufgerufen und an anderer Stelle wiederverwendet werden
kann.

Globale Variable : Eine außerhalb einer Funktion definierte Variable, die überall
verwendet werden kann.

Index : Die Position eines bestimmten Elements.

Jupyter Notebook : Interaktive Codierungsumgebung, die eine Kombination aus Code und
Markdown ermöglicht.

Bibliothek : Eine Sammlung von Dateien mit Funktionen, die von anderen Programmen
verwendet werden.

Lokale Variable : Eine Variable, die innerhalb einer Funktion definiert ist und nur
innerhalb dieser Funktion verwendet werden kann.

Maske : Ein boolesches Objekt, das zur Auswahl von Daten aus einem anderen Objekt
verwendet wird.

Methode : Eine Aktion, die an ein bestimmtes Objekt gebunden ist. Aufgerufen durch die
Verwendung von `object.method`.

Module : Die Dateien innerhalb einer Bibliothek, die Funktionen enthalten, die von
anderen Programmen verwendet werden.

Parameter : Variablen, die beim Ausführen einer Funktion verwendet werden.

Reihe : Eine Pandas-Datenstruktur zur Darstellung einer Spalte.

Substring : Ein Teil eines Strings.

Variablen : Namen für Werte.





