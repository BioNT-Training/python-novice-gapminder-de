---
title: Pandas DatenFrames
teaching: 15
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Wähle einzelne Werte aus einem Pandas-DataFrame aus.
- Wähle ganze Zeilen oder ganze Spalten aus einem DataFrame aus.
- Wählen Sie in einer einzigen Operation eine Teilmenge von Zeilen und Spalten aus einem
  DataFrame aus.
- Wählen Sie eine Teilmenge eines DataFrames anhand eines einzigen booleschen
  Kriteriums aus.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich eine statistische Analyse von Tabellendaten durchführen?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Hinweis zu Pandas DataFrames/Series

Ein [DataFrame][pandas-dataframe] ist eine Sammlung von [Series][pandas-series]; Der
DataFrame ist die Art und Weise, wie Pandas eine Tabelle darstellt, und Series ist die
Datenstruktur, die Pandas zur Darstellung einer Spalte verwendet.

Pandas baut auf der [Numpy][numpy]-Bibliothek auf, was in der Praxis bedeutet, dass die
meisten der für Numpy-Arrays definierten Methoden auch für Pandas Series/DataFrames
gelten.

Was Pandas so attraktiv macht, ist die leistungsfähige Schnittstelle für den Zugriff auf
einzelne Datensätze der Tabelle, die korrekte Behandlung fehlender Werte und relationale
Datenbankoperationen zwischen DataFrames.

## Auswählen von Werten

Um auf einen Wert an der Position `[i,j]` eines DataFrame zuzugreifen, haben wir zwei
Möglichkeiten, je nachdem, was die Bedeutung von `i` im Gebrauch ist. Erinnern Sie sich
daran, dass ein DataFrame einen *Index* zur Verfügung stellt, um die Zeilen der Tabelle
zu identifizieren; eine Zeile hat also sowohl eine *Position* innerhalb der Tabelle als
auch ein *Label*, das ihren *Eintrag* im DataFrame eindeutig identifiziert.

## Verwenden Sie `DataFrame.iloc[..., ...]`, um Werte nach ihrer (Eingangs-)Position auszuwählen

- Kann die Position durch einen numerischen Index angeben, analog zur 2D-Version der
  Zeichenauswahl in Zeichenketten.

```python
import pandas as pd
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.iloc[0, 0])
```

```output
1601.056136
```

## Benutzen Sie `DataFrame.loc[..., ...]`, um Werte nach ihrer (Eintrags-)Bezeichnung auszuwählen.

- Kann den Ort durch Zeilen- und/oder Spaltennamen angeben.

```python
print(data.loc["Albania", "gdpPercap_1952"])
```

```output
1601.056136
```

## Verwenden Sie `:` allein, um alle Spalten oder alle Zeilen zu meinen.

- Genau wie die übliche Python-Slicing-Notation.

```python
print(data.loc["Albania", :])
```

```output
gdpPercap_1952    1601.056136
gdpPercap_1957    1942.284244
gdpPercap_1962    2312.888958
gdpPercap_1967    2760.196931
gdpPercap_1972    3313.422188
gdpPercap_1977    3533.003910
gdpPercap_1982    3630.880722
gdpPercap_1987    3738.932735
gdpPercap_1992    2497.437901
gdpPercap_1997    3193.054604
gdpPercap_2002    4604.211737
gdpPercap_2007    5937.029526
Name: Albania, dtype: float64
```

- Würde das gleiche Ergebnis liefern, wenn man `data.loc["Albania"]` (ohne zweiten
  Index) ausgibt.

```python
print(data.loc[:, "gdpPercap_1952"])
```

```output
country
Albania                    1601.056136
Austria                    6137.076492
Belgium                    8343.105127
⋮ ⋮ ⋮
Switzerland               14734.232750
Turkey                     1969.100980
United Kingdom             9979.508487
Name: gdpPercap_1952, dtype: float64
```

- Würde das gleiche Ergebnis erhalten, wenn man `data["gdpPercap_1952"]` ausgibt
- Das gleiche Ergebnis erhält man auch, wenn man `data.gdpPercap_1952` ausdruckt (nicht
  empfohlen, da leicht mit der Notation `.` für Methoden zu verwechseln)

## Wählen Sie mehrere Spalten oder Zeilen mit `DataFrame.loc` und einem benannten Slice.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993
```

Im obigen Code stellen wir fest, dass **Slicing unter Verwendung von `loc` an beiden
Enden inklusiv ist**, was sich von **Slicing unter Verwendung von `iloc`**
unterscheidet, bei dem Slicing alles bis zum letzten Index, aber nicht einschließlich,
anzeigt.

## Das Ergebnis der Zerlegung kann in weiteren Operationen verwendet werden.

- Normalerweise druckt man nicht nur einen Ausschnitt.
- Alle statistischen Operatoren, die auf ganze DataFrame angewendet werden,
  funktionieren auf die gleiche Weise auf Slices.
- Berechne z.B. den Maximalwert eines Slice.

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].max())
```

```output
gdpPercap_1962    13450.40151
gdpPercap_1967    16361.87647
gdpPercap_1972    18965.05551
dtype: float64
```

```python
print(data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972'].min())
```

```output
gdpPercap_1962    4649.593785
gdpPercap_1967    5907.850937
gdpPercap_1972    7778.414017
dtype: float64
```

## Verwende Vergleiche, um Daten nach ihrem Wert auszuwählen.

- Der Vergleich wird Element für Element durchgeführt.
- Gibt einen ähnlich geformten DataFrame von `True` und `False` zurück.

```python
# Use a subset of data to keep output readable.
subset = data.loc['Italy':'Poland', 'gdpPercap_1962':'gdpPercap_1972']
print('Subset of data:\n', subset)

# Which values were greater than 10000 ?
print('\nWhere are values large?\n', subset > 10000)
```

```output
Subset of data:
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy           8243.582340    10022.401310    12269.273780
Montenegro      4649.593785     5907.850937     7778.414017
Netherlands    12790.849560    15363.251360    18794.745670
Norway         13450.401510    16361.876470    18965.055510
Poland          5338.752143     6557.152776     8006.506993

Where are values large?
            gdpPercap_1962 gdpPercap_1967 gdpPercap_1972
country
Italy                False           True           True
Montenegro           False          False          False
Netherlands           True           True           True
Norway                True           True           True
Poland               False          False          False
```

## Wähle Werte oder NaN mit einer booleschen Maske.

- Ein Rahmen voller Boolescher Operatoren wird manchmal als *Maske* bezeichnet, weil er
  so verwendet werden kann.

```python
mask = subset > 10000
print(subset[mask])
```

```output
             gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
country
Italy                   NaN     10022.40131     12269.27378
Montenegro              NaN             NaN             NaN
Netherlands     12790.84956     15363.25136     18794.74567
Norway          13450.40151     16361.87647     18965.05551
Poland                  NaN             NaN             NaN
```

- Ermittelt den Wert, wenn die Maske wahr ist, und NaN (Not a Number), wenn sie falsch
  ist.
- Nützlich, weil NaNs von Operationen wie max, min, Durchschnitt usw. ignoriert werden.

```python
print(subset[subset > 10000].describe())
```

```output
       gdpPercap_1962  gdpPercap_1967  gdpPercap_1972
count        2.000000        3.000000        3.000000
mean     13120.625535    13915.843047    16676.358320
std        466.373656     3408.589070     3817.597015
min      12790.849560    10022.401310    12269.273780
25%      12955.737547    12692.826335    15532.009725
50%      13120.625535    15363.251360    18794.745670
75%      13285.513523    15862.563915    18879.900590
max      13450.401510    16361.876470    18965.055510
```

## Gruppieren nach: split-apply-combine

::::::::::::::::::::::::::::::::::::: instructor

Die Lernenden tun sich hier oft schwer, da viele nicht mit Finanzdaten und -konzepten
arbeiten und daher Schwierigkeiten haben, die Beispielkonzepte zu verstehen. Das größte
Problem ist jedoch die Zeile, die den wealth_score generiert, dieser Schritt muss
gründlich besprochen werden:
* Es wird eine implizite Konvertierung zwischen booleschen Werten und Fließkommazahlen
  verwendet, die im Kurs bisher noch nicht behandelt wurde.
* Das Argument Achse=1 muss deutlich erklärt werden.

:::::::::::::::::::::::::::::::::::::::::::::::::

Pandas Vektorisierungsmethoden und Gruppierungsoperationen sind Funktionen, die
Benutzern viel Flexibilität bei der Analyse ihrer Daten bieten.

Nehmen wir zum Beispiel an, dass wir einen besseren Überblick darüber haben wollen, wie
sich die europäischen Länder nach ihrem BIP aufteilen.

1. Wir können uns einen Überblick verschaffen, indem wir die Länder in den untersuchten
   Jahren in zwei Gruppen aufteilen: diejenigen, die ein BIP *höher* als der europäische
   Durchschnitt aufweisen, und diejenigen mit einem *niedrigeren* BIP.
2. Wir schätzen dann einen *Wohlstandsscore* auf der Grundlage der historischen Werte
   (von 1962 bis 2007), wobei wir berücksichtigen, wie oft ein Land an den Gruppen mit
   *geringerem* oder *höherem* BIP teilgenommen hat

```python
mask_higher = data > data.mean()
wealth_score = mask_higher.aggregate('sum', axis=1) / len(data.columns)
print(wealth_score)
```

```output
country
Albania                   0.000000
Austria                   1.000000
Belgium                   1.000000
Bosnia and Herzegovina    0.000000
Bulgaria                  0.000000
Croatia                   0.000000
Czech Republic            0.500000
Denmark                   1.000000
Finland                   1.000000
France                    1.000000
Germany                   1.000000
Greece                    0.333333
Hungary                   0.000000
Iceland                   1.000000
Ireland                   0.333333
Italy                     0.500000
Montenegro                0.000000
Netherlands               1.000000
Norway                    1.000000
Poland                    0.000000
Portugal                  0.000000
Romania                   0.000000
Serbia                    0.000000
Slovak Republic           0.000000
Slovenia                  0.333333
Spain                     0.333333
Sweden                    1.000000
Switzerland               1.000000
Turkey                    0.000000
United Kingdom            1.000000
dtype: float64
```

Schließlich wird für jede Gruppe in der Tabelle `wealth_score` ihr (finanzieller)
Beitrag über die untersuchten Jahre mit Hilfe verketteter Methoden summiert:

```python
print(data.groupby(wealth_score).sum())
```

```output
          gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
0.000000    36916.854200    46110.918793    56850.065437    71324.848786   
0.333333    16790.046878    20942.456800    25744.935321    33567.667670   
0.500000    11807.544405    14505.000150    18380.449470    21421.846200   
1.000000   104317.277560   127332.008735   149989.154201   178000.350040   

          gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
0.000000    88569.346898   104459.358438   113553.768507   119649.599409   
0.333333    45277.839976    53860.456750    59679.634020    64436.912960   
0.500000    25377.727380    29056.145370    31914.712050    35517.678220   
1.000000   215162.343140   241143.412730   263388.781960   296825.131210   

          gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007  
0.000000    92380.047256   103772.937598   118590.929863   149577.357928  
0.333333    67918.093220    80876.051580   102086.795210   122803.729520  
0.500000    36310.666080    40723.538700    45564.308390    51403.028210  
1.000000   315238.235970   346930.926170   385109.939210   427850.333420
```

::::::::::::::::::::::::::::::::::::::: challenge

## Auswahl der einzelnen Werte

Angenommen, Pandas wurde in Ihr Notebook importiert und die Gapminder-BIP-Daten für
Europa wurden geladen:

```python
import pandas as pd

data_europe = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
```

Schreiben Sie einen Ausdruck, um das Pro-Kopf-BIP von Serbien im Jahr 2007 zu ermitteln.

::::::::::::::: solution

## Lösung

Die Auswahl kann mit Hilfe der Beschriftungen sowohl der Zeile ("Serbien") als auch der
Spalte ("gdpPercap\_2007") vorgenommen werden:

```python
print(data_europe.loc['Serbia', 'gdpPercap_2007'])
```

Die Ausgabe ist

```output
9786.534714
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Ausmaß des Slicings

1. Ergeben die beiden folgenden Anweisungen die gleiche Ausgabe?
2. Welche Regel bestimmt, was in numerischen Slices und benannten Slices in Pandas
   enthalten ist (oder nicht)?

```python
print(data_europe.iloc[0:2, 0:2])
print(data_europe.loc['Albania':'Belgium', 'gdpPercap_1952':'gdpPercap_1962'])
```

::::::::::::::: solution

## Lösung

Nein, sie erzeugen nicht die gleiche Ausgabe! Die Ausgabe der ersten Anweisung ist:

```output
        gdpPercap_1952  gdpPercap_1957
country                                
Albania     1601.056136     1942.284244
Austria     6137.076492     8842.598030
```

Die zweite Anweisung ergibt:

```output
        gdpPercap_1952  gdpPercap_1957  gdpPercap_1962
country                                                
Albania     1601.056136     1942.284244     2312.888958
Austria     6137.076492     8842.598030    10750.721110
Belgium     8343.105127     9714.960623    10991.206760
```

Es ist offensichtlich, dass die zweite Anweisung eine zusätzliche Spalte und eine
zusätzliche Zeile im Vergleich zur ersten Anweisung erzeugt.  
Welche Schlussfolgerung können wir ziehen? Wir sehen, dass ein numerisches Slice, 0:2,
den letzten Index (d. h. Index 2) in dem angegebenen Bereich *ausschließt*, während ein
benanntes Slice, 'gdpPercap\_1952':'gdpPercap\_1962', das letzte Element *einschließt*.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Daten rekonstruieren

Erkläre, was jede Zeile in dem folgenden kurzen Programm macht: was steht in `first`,
`second`, usw.?

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
second = first[first['continent'] == 'Americas']
third = second.drop('Puerto Rico')
fourth = third.drop('continent', axis = 1)
fourth.to_csv('result.csv')
```

::::::::::::::: solution

## Lösung

Gehen wir diesen Teil des Codes Zeile für Zeile durch.

```python
first = pd.read_csv('data/gapminder_all.csv', index_col='country')
```

Diese Zeile lädt den Datensatz mit den BIP-Daten aller Länder in einen DataFrame mit
der Bezeichnung `first`. Der Parameter `index_col='country'` wählt aus, welche Spalte
als Zeilenbeschriftung im DataFrame verwendet werden soll.

```python
second = first[first['continent'] == 'Americas']
```

In dieser Zeile wird eine Auswahl getroffen: Es werden nur die Zeilen von `first`
extrahiert, bei denen die Spalte "continent" mit "Americas" übereinstimmt. Beachten Sie,
dass der boolesche Ausdruck in den eckigen Klammern, `first['continent'] == 'Americas'`,
verwendet wird, um nur die Zeilen auszuwählen, in denen der Ausdruck wahr ist. Versuchen
Sie, diesen Ausdruck zu drucken! Können Sie auch die einzelnen Wahr/Falsch-Elemente
ausdrucken? (Hinweis: Weisen Sie den Ausdruck zunächst einer Variablen zu)

```python
third = second.drop('Puerto Rico')
```

Wie die Syntax vermuten lässt, wird in dieser Zeile die Zeile von `second` mit der
Bezeichnung "Puerto Rico" gelöscht. Der resultierende DataFrame `third` hat eine Zeile
weniger als der ursprüngliche DataFrame `second`.

```python
fourth = third.drop('continent', axis = 1)
```

Auch hier wenden wir die Drop-Funktion an, aber in diesem Fall lassen wir nicht eine
Zeile, sondern eine ganze Spalte fallen. Um dies zu erreichen, müssen wir auch den
Parameter `axis` angeben (wir wollen die zweite Spalte mit dem Index 1 löschen).

```python
fourth.to_csv('result.csv')
```

Der letzte Schritt besteht darin, die Daten, an denen wir gearbeitet haben, in eine
csv-Datei zu schreiben. Pandas macht dies mit der Funktion `to_csv()` einfach. Das
einzige erforderliche Argument für die Funktion ist der Dateiname. Beachten Sie, dass
die Datei in das Verzeichnis geschrieben wird, von dem aus Sie die Jupyter- oder
Python-Sitzung gestartet haben.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Auswahl der Indizes

Erklären Sie in einfachen Worten, was `idxmin` und `idxmax` in dem folgenden kurzen
Programm tun. Wann würden Sie diese Methoden verwenden?

```python
data = pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')
print(data.idxmin())
print(data.idxmax())
```

::::::::::::::: solution

## Lösung

Für jede Spalte in `data` gibt `idxmin` den Indexwert zurück, der dem Minimum jeder
Spalte entspricht; `idxmax` tut das Gleiche für den Maximalwert jeder Spalte.

Sie können diese Funktionen immer dann verwenden, wenn Sie den Zeilenindex des
Minimal-/Maximalwerts und nicht den tatsächlichen Minimal-/Maximalwert erhalten möchten.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Übung mit der Auswahl

Angenommen, Pandas wurde importiert und die Gapminder-BIP-Daten für Europa wurden
geladen. Schreiben Sie einen Ausdruck, um jedes der folgenden Elemente auszuwählen:

1. Pro-Kopf-BIP für alle Länder im Jahr 1982.
2. BIP pro Kopf für Dänemark für alle Jahre.
3. BIP pro Kopf für alle Länder für die Jahre *nach* 1985.
4. Das Pro-Kopf-BIP für jedes Land im Jahr 2007 als Vielfaches des Pro-Kopf-BIP für
   dieses Land im Jahr 1952.

::::::::::::::: solution

## Lösung

1:

```python
data['gdpPercap_1982']
```

2:

```python
data.loc['Denmark',:]
```

3:

```python
data.loc[:,'gdpPercap_1985':]
```

Pandas ist intelligent genug, um die Zahl am Ende der Spaltenbezeichnung zu erkennen und
gibt keinen Fehler aus, obwohl keine Spalte mit dem Namen `gdpPercap_1985` existiert.
Dies ist nützlich, wenn der CSV-Datei später neue Spalten hinzugefügt werden.

4:

```python
data['gdpPercap_2007']/data['gdpPercap_1952']
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Viele Möglichkeiten des Zugriffs

Es gibt mindestens zwei Möglichkeiten, auf einen Wert oder ein Slice eines DataFrame
zuzugreifen: über den Namen oder den Index. Es gibt jedoch noch viele andere. Zum
Beispiel kann auf eine einzelne Spalte oder Zeile entweder als `DataFrame` oder als
`Series` Objekt zugegriffen werden.

Schlagen Sie verschiedene Möglichkeiten vor, die folgenden Operationen mit einem
DataFrame durchzuführen:

1. Zugriff auf eine einzelne Spalte
2. Zugriff auf eine einzelne Zeile
3. Zugriff auf ein einzelnes DataFrame-Element
4. Zugriff auf mehrere Spalten
5. Zugriff auf mehrere Zeilen
6. Zugriff auf eine Teilmenge von bestimmten Zeilen und Spalten
7. Zugriff auf eine Teilmenge von Zeilen- und Spaltenbereichen

::::::::::::::: solution

## Lösung

1\. Zugriff auf eine einzelne Spalte:

```python
# by name
data["col_name"]   # as a Series
data[["col_name"]] # as a DataFrame

# by name using .loc
data.T.loc["col_name"]  # as a Series
data.T.loc[["col_name"]].T  # as a DataFrame

# Dot notation (Series)
data.col_name

# by index (iloc)
data.iloc[:, col_index]   # as a Series
data.iloc[:, [col_index]] # as a DataFrame

# using a mask
data.T[data.T.index == "col_name"].T
```

2\. Zugriff auf eine einzelne Zeile:

```python
# by name using .loc
data.loc["row_name"] # as a Series
data.loc[["row_name"]] # as a DataFrame

# by name
data.T["row_name"] # as a Series
data.T[["row_name"]].T # as a DataFrame

# by index
data.iloc[row_index]   # as a Series
data.iloc[[row_index]]   # as a DataFrame

# using mask
data[data.index == "row_name"]
```

3\. Greife auf ein einzelnes DataFrame-Element zu:

```python
# by column/row names
data["column_name"]["row_name"]         # als Series

data[["col_name"]].loc["row_name"]  # als Series
data[["col_name"]].loc[["row_name"]]  # als DataFrame

data.loc["row_name"]["col_name"]  # als Wert
data.loc[["row_name"]]["col_name"]  # als Series
data.loc[["row_name"]][["col_name"]]  # als DataFrame

data.loc["row_name", "col_name"]  # als Wert
data.loc[["row_name"], "col_name"]  #  Series. Behält den Index bei. Der Spaltenname wird nach `.name` verschoben.
data.loc["row_name", ["col_name"]]  # als Series. Der Index wird nach „.name.“ verschoben. Setzt den Index auf den Spaltennamen.
data.loc[["row_name"], ["col_name"]]  # als DataFrame (behält den ursprünglichen Index und Spaltennamen bei)

# by column/row names: Dot notation
data.col_name.row_name

# by column/row indices
data.iloc[row_index, col_index] # als Wert
data.iloc[[row_index], col_index] # #  Series. Behält den Index bei. Der Spaltenname wird nach `.name` verschoben.
data.iloc[row_index, [col_index]] # als Series. Der Index wird nach „.name.“ verschoben. Setzt den Index auf den Spaltennamen.
data.iloc[[row_index], [col_index]] #  # als DataFrame (behält den ursprünglichen Index und Spaltennamen bei)

# column name + row index
data["col_name"][row_index]
data.col_name[row_index]
data["col_name"].iloc[row_index]

# column index + row name
data.iloc[:, [col_index]].loc["row_name"]  # alsSeries
data.iloc[:, [col_index]].loc[["row_name"]]  # als DataFrame

# using masks
data[data.index == "row_name"].T[data.T.index == "col_name"].T
```

4\. Zugriff auf mehrere Spalten:

```python
# by name
data[["col1", "col2", "col3"]]
data.loc[:, ["col1", "col2", "col3"]]

# by index
data.iloc[:, [col1_index, col2_index, col3_index]]
```

5\. Zugriff auf mehrere Zeilen

```python
# by name
data.loc[["row1", "row2", "row3"]]

# by index
data.iloc[[row1_index, row2_index, row3_index]]
```

6\. Zugriff auf eine Teilmenge von bestimmten Zeilen und Spalten

```python
# by names
data.loc[["row1", "row2", "row3"], ["col1", "col2", "col3"]]

# by indices
data.iloc[[row1_index, row2_index, row3_index], [col1_index, col2_index, col3_index]]

# column names + row indices
data[["col1", "col2", "col3"]].iloc[[row1_index, row2_index, row3_index]]

# column indices + row names
data.iloc[:, [col1_index, col2_index, col3_index]].loc[["row1", "row2", "row3"]]
```

7\. Zugriff auf eine Teilmenge von Zeilen- und Spaltenbereichen

```python
# nach Namen
data.loc["row1":"row2", "col1":"col2"]

# nach index
data.iloc[row1_index:row2_index, col1_index:col2_index]

# column names + row indices
data.loc[:, "col1_name":"col2_name"].iloc[row1_index:row2_index]

# column indices + row names
data.iloc[:, col1_index:col2_index].loc["row1":"row2"]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Untersuchung der verfügbaren Methoden mit der Funktion `dir()`

Python enthält eine Funktion `dir()`, mit der man alle verfügbaren Methoden (Funktionen)
anzeigen kann, die in ein Datenobjekt eingebaut sind. In Episode 4 haben wir einige
Methoden mit einer Zeichenkette verwendet. Aber wir können sehen, dass noch viel mehr
verfügbar sind, wenn wir `dir()` benutzen:

```python
my_string = 'Hello world!'   # Erstellen eines String-Objekts
dir(my_string)
```

Dieser Befehl gibt zurück:

```python
['__add__',
...
'__subclasshook__',
'capitalize',
'casefold',
'center',
...
'upper',
'zfill']
```

Sie können `help()` oder <kbd>Shift</kbd></kbd>+<kbd>Tab</kbd> verwenden, um mehr
Informationen darüber zu erhalten, was diese Methoden tun.

Angenommen, Pandas wurde importiert und die Gapminder-BIP-Daten für Europa wurden als
`data` geladen. Verwenden Sie dann `dir()`, um die Funktion zu finden, die den Median
des Pro-Kopf-BIP aller europäischen Länder für jedes Jahr, für das Informationen
verfügbar sind, ausgibt.

::::::::::::::: solution

## Lösung

Unter vielen Auswahlmöglichkeiten wird in `dir()` die Funktion `median()` als
Möglichkeit aufgeführt. Also,

```python
data.median()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Interpretation

Die Grenzen Polens sind seit 1945 stabil, haben sich aber in den Jahren davor mehrmals
geändert. Wie würden Sie dies handhaben, wenn Sie eine Tabelle des Pro-Kopf-BIP für
Polen für das gesamte zwanzigste Jahrhundert erstellen würden?


::::::::::::::::::::::::::::::::::::::::::::::::::

[pandas-dataframe]:
https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html
[pandas-series]:
https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html
[numpy]: https://www.numpy.org/


:::::::::::::::::::::::::::::::::::::::: keypoints

- Benutze `DataFrame.iloc[..., ...]`, um Werte nach ganzzahliger Position auszuwählen.
- Benutze `:` allein, um alle Spalten oder alle Zeilen zu meinen.
- Wähle mehrere Spalten oder Zeilen mit `DataFrame.loc` und einem benannten Slice.
- Das Ergebnis der Zerlegung kann in weiteren Operationen verwendet werden.
- Verwende Vergleiche, um Daten nach ihrem Wert auszuwählen.
- Wähle Werte oder NaN mit Hilfe einer booleschen Maske.

::::::::::::::::::::::::::::::::::::::::::::::::::



