---
title: Schleifen über Datensätze
teaching: 5
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- In der Lage sein, Globbing-Ausdrücke zu lesen und zu schreiben, die mit Dateimengen
  übereinstimmen.
- Verwenden Sie glob, um Listen von Dateien zu erstellen.
- Schreibe for-Schleifen, um Operationen auf Dateien durchzuführen, deren Namen in einer
  Liste angegeben sind.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich viele Datensätze mit einem einzigen Befehl verarbeiten?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Verwenden Sie eine `for`-Schleife, um Dateien mit einer Liste ihrer Namen zu verarbeiten.

- Ein Dateiname ist eine Zeichenkette.
- Und Listen können Zeichenketten enthalten.

```python
import pandas as pd
for filename in ['data/gapminder_gdp_africa.csv', 'data/gapminder_gdp_asia.csv']:
    data = pd.read_csv(filename, index_col='country')
    print(filename, data.min())
```

```output
data/gapminder_gdp_africa.csv gdpPercap_1952    298.846212
gdpPercap_1957    335.997115
gdpPercap_1962    355.203227
gdpPercap_1967    412.977514
⋮ ⋮ ⋮
gdpPercap_1997    312.188423
gdpPercap_2002    241.165877
gdpPercap_2007    277.551859
dtype: float64
data/gapminder_gdp_asia.csv gdpPercap_1952    331
gdpPercap_1957    350
gdpPercap_1962    388
gdpPercap_1967    349
⋮ ⋮ ⋮
gdpPercap_1997    415
gdpPercap_2002    611
gdpPercap_2007    944
dtype: float64
```

## Verwenden Sie [`glob.glob`](https://docs.python.org/3/library/glob.html#glob.glob), um Gruppen von Dateien zu finden, deren Namen einem Muster entsprechen.

- In Unix bedeutet der Begriff "globbing" "eine Menge von Dateien mit einem Muster
  abgleichen".
- Die häufigsten Muster sind:
  - `*` bedeutet "entspricht null oder mehr Zeichen"
  - `?` bedeutet "genau ein Zeichen übereinstimmen"
- Die Standardbibliothek von Python enthält das Modul
  [`glob`](https://docs.python.org/3/library/glob.html), um die Funktionalität des
  Mustervergleichs bereitzustellen
- Das [`glob`](https://docs.python.org/3/library/glob.html) Modul enthält eine Funktion,
  die auch `glob` genannt wird, um Dateimuster zu finden
- Z.B. passt `glob.glob('*.txt')` auf alle Dateien im aktuellen Verzeichnis, deren Namen
  mit `.txt` enden.
- Das Ergebnis ist eine (möglicherweise leere) Liste von Zeichenketten.

```python
import glob
print('all csv files in data directory:', glob.glob('data/*.csv'))
```

```output
all csv files in data directory: ['data/gapminder_all.csv', 'data/gapminder_gdp_africa.csv', \
'data/gapminder_gdp_americas.csv', 'data/gapminder_gdp_asia.csv', 'data/gapminder_gdp_europe.csv', \
'data/gapminder_gdp_oceania.csv']
```

```python
print('all PDB files:', glob.glob('*.pdb'))
```

```output
all PDB files: []
```

## Verwenden Sie `glob` und `for`, um Stapel von Dateien zu verarbeiten.

- Es hilft sehr, wenn die Dateien systematisch und konsistent benannt und gespeichert
  werden, damit einfache Muster die richtigen Daten finden.

```python
for filename in glob.glob('data/gapminder_*.csv'):
    data = pd.read_csv(filename)
    print(filename, data['gdpPercap_1952'].min())
```

```output
data/gapminder_all.csv 298.8462121
data/gapminder_gdp_africa.csv 298.8462121
data/gapminder_gdp_americas.csv 1397.717137
data/gapminder_gdp_asia.csv 331.0
data/gapminder_gdp_europe.csv 973.5331948
data/gapminder_gdp_oceania.csv 10039.59564
```

- Dies beinhaltet alle Daten, sowie Daten pro Region.
- Verwenden Sie ein spezifischeres Muster in den Übungen, um den gesamten Datensatz
  auszuschließen.
- Aber beachten Sie, dass das Minimum des gesamten Datensatzes auch das Minimum eines
  der Datensätze ist, was eine nette Überprüfung der Korrektheit ist.

::::::::::::::::::::::::::::::::::::::: challenge

## Ermitteln von Übereinstimmungen

Auf welche dieser Dateien trifft der Ausdruck `glob.glob('data/*as*.csv')` *nicht* zu?

1. `data/gapminder_gdp_africa.csv`
2. `data/gapminder_gdp_americas.csv`
3. `data/gapminder_gdp_asia.csv`

::::::::::::::: solution

## Lösung

1 wird vom glob nicht gefunden.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Minimale Dateigröße

Ändern Sie dieses Programm so, dass es die Anzahl der Datensätze in der Datei mit den
wenigsten Datensätzen ausgibt.

```python
import glob
import pandas as pd
fewest = ____
for filename in glob.glob('data/*.csv'):
    dataframe = pd.____(filename)
    fewest = min(____, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Beachten Sie, dass die [Methode `DataFrame.shape()`][shape-method] ein Tupel mit der
Anzahl der Zeilen und Spalten des Datenrahmens zurückgibt.

::::::::::::::: solution

## Lösung

```python
import glob
import pandas as pd
fewest = float('Inf')
for filename in glob.glob('data/*.csv'):
    dataframe = pd.read_csv(filename)
    fewest = min(fewest, dataframe.shape[0])
print('smallest file has', fewest, 'records')
```

Sie könnten sich dafür entschieden haben, die Variable `fewest` mit einer Zahl zu
initialisieren, die größer ist als die Zahlen, mit denen Sie arbeiten, aber das könnte
zu Problemen führen, wenn Sie den Code mit größeren Zahlen wiederverwenden. In Python
können Sie positive Unendlichkeit verwenden, was unabhängig von der Größe Ihrer Zahlen
funktioniert. Welche anderen speziellen Zeichenketten erkennt die [Funktion
`float`][float-function]?



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Vergleich von Daten

Schreiben Sie ein Programm, das die regionalen Datensätze einliest und das
durchschnittliche Pro-Kopf-BIP für jede Region über die Zeit in einem einzigen Diagramm
darstellt. Pandas gibt eine Fehlermeldung aus, wenn es auf nicht-numerische Spalten in
einer Datenrahmenberechnung stößt. Sie müssen also entweder diese Spalten herausfiltern
oder Pandas anweisen, sie zu ignorieren.


::::::::::::::: solution

## Lösung

Diese Lösung erstellt eine nützliche Legende, indem sie die [string `split`
method][split-method] verwendet, um die `region` aus dem Pfad
'data/gapminder\_gdp\_a\_specific\_region.csv' zu extrahieren.

```python
import glob
import pandas as pd
import matplotlib.pyplot as plt
fig, ax = plt.subplots(1,1)
for filename in glob.glob('data/gapminder_gdp*.csv'):
    dataframe = pd.read_csv(filename)
    # extract <region> from the filename, expected to be in the format 'data/gapminder_gdp_<region>.csv'.
    # we will split the string using the split method and `_` as our separator,
    # retrieve the last string in the list that split returns (`<region>.csv`), 
    # and then remove the `.csv` extension from that string.
    # NOTE: the pathlib module covered in the next callout also offers
    # convenient abstractions for working with filesystem paths and could solve this as well:
    # from pathlib import Path
    # region = Path(filename).stem.split('_')[-1]
    region = filename.split('_')[-1][:-4]
    # extract the years from the columns of the dataframe 
    headings = dataframe.columns[1:]
    years = headings.str.split('_').str.get(1)
    # pandas raises errors when it encounters non-numeric columns in a dataframe computation
    # but we can tell pandas to ignore them with the `numeric_only` parameter
    dataframe.mean(numeric_only=True).plot(ax=ax, label=region)
    # NOTE: another way of doing this selects just the columns with gdp in their name using the filter method
    # dataframe.filter(like="gdp").mean().plot(ax=ax, label=region)
# set the title and labels
ax.set_title('GDP Per Capita for Regions Over Time')
ax.set_xticks(range(len(years)))
ax.set_xticklabels(years)
ax.set_xlabel('Year')
plt.tight_layout()
plt.legend()
plt.show()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Umgang mit Dateipfaden

Das [Modul `pathlib`][pathlib-module] bietet nützliche Abstraktionen für die Datei- und
Pfadmanipulation, wie z.B. die Rückgabe des Namens einer Datei ohne die
Dateierweiterung. Dies ist sehr nützlich, wenn man eine Schleife über Dateien und
Verzeichnisse zieht. Im folgenden Beispiel erstellen wir ein Objekt `Path` und
untersuchen seine Attribute.

```python
from pathlib import Path

p = Path("data/gapminder_gdp_africa.csv")
print(p.parent)
print(p.stem)
print(p.suffix)
```

```output
data
gapminder_gdp_africa
.csv
```

**Hinweis:** Überprüfen Sie alle verfügbaren Attribute und Methoden des Objekts `Path`
mit der Funktion `dir()`.


::::::::::::::::::::::::::::::::::::::::::::::::::

[shape-method]:
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.shape.html
[float-function]: https://docs.python.org/3/library/functions.html#float
[split-method]: https://docs.python.org/3/library/stdtypes.html#str.split
[pathlib-module]: https://docs.python.org/3/library/pathlib.html


:::::::::::::::::::::::::::::::::::::::: keypoints

- Verwenden Sie eine `for`-Schleife, um Dateien mit einer Liste von Namen zu
  verarbeiten.
- Verwenden Sie `glob.glob`, um Gruppen von Dateien zu finden, deren Namen einem Muster
  entsprechen.
- Verwenden Sie `glob` und `for`, um Stapel von Dateien zu verarbeiten.

::::::::::::::::::::::::::::::::::::::::::::::::::



