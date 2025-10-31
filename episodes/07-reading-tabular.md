---
title: Tabellarische Daten in DataFrames einlesen
teaching: 10
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Importieren Sie die Pandas-Bibliothek.
- Verwenden Sie Pandas, um einen einfachen CSV-Datensatz zu laden.
- Erhalten Sie einige grundlegende Informationen über einen Pandas DataFrame.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich tabellarische Daten lesen?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Verwenden Sie die Pandas-Bibliothek, um Statistiken über tabellarische Daten zu erstellen.

- [Pandas](https://pandas.pydata.org/) ist eine weit verbreitete Python-Bibliothek für
  Statistiken, insbesondere für tabellarische Daten.
- Übernimmt viele Funktionen aus den Dataframes von R.
  - Eine 2-dimensionale Tabelle, deren Spalten Namen haben und möglicherweise
    verschiedene Datentypen haben.
- Pandas mit `import pandas as pd` laden. Der Alias `pd` wird üblicherweise verwendet,
  um im Code auf die Pandas-Bibliothek zu verweisen.
- Einlesen einer CSV-Datendatei (Comma Separated Values) mit `pd.read_csv`.
  - Argument ist der Name der zu lesenden Datei.
  - Gibt einen DataFrame zurück, den Sie einer Variablen zuweisen können

```python
import pandas as pd

data_oceania = pd.read_csv('data/gapminder_gdp_oceania.csv')
print(data_oceania)
```

```output
       country  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
0    Australia     10039.59564     10949.64959     12217.22686
1  New Zealand     10556.57566     12247.39532     13175.67800

   gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
0     14526.12465     16788.62948     18334.19751     19477.00928
1     14463.91893     16046.03728     16233.71770     17632.41040

   gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
0     21888.88903     23424.76683     26997.93657     30687.75473
1     19007.19129     18363.32494     21050.41377     23189.80135

   gdpPercap_2007
0     34435.36744
1     25185.00911
```

- Die Spalten in einem DataFrame sind die beobachteten Variablen und die Zeilen die
  Beobachtungen.
- Pandas verwendet den Backslash `\`, um umbrochene Zeilen anzuzeigen, wenn die Ausgabe
  zu breit ist, um auf den Bildschirm zu passen.
- Die Verwendung von beschreibenden Namen für DataFrame hilft uns, zwischen mehreren
  DataFrame zu unterscheiden, damit wir nicht versehentlich einen DataFrame
  überschreiben oder aus dem falschen DataFrame lesen.

::::::::::::::::::::::::::::::::::::::::: callout

## Datei nicht gefunden

Unsere Lektionen speichern ihre Datendateien in einem Unterverzeichnis `data`, weshalb
der Pfad zur Datei `data/gapminder_gdp_oceania.csv` lautet. Wenn Sie vergessen, `data/`
einzuschließen, oder wenn Sie es einschließen, aber Ihre Kopie der Datei irgendwo anders
liegt, erhalten Sie einen [Laufzeitfehler](04-built-in.md), der mit einer Zeile wie
dieser endet:

```error
FileNotFoundError: [Errno 2] No such file or directory: 'data/gapminder_gdp_oceania.csv'
```

::::::::::::::::::::::::::::::::::::::::::::::::::

## Verwenden Sie `index_col`, um anzugeben, dass die Werte einer Spalte als Zeilenüberschriften verwendet werden sollen.

- Die Zeilenüberschriften sind Zahlen (in diesem Fall 0 und 1).
- Möchte wirklich nach Ländern indexieren.
- Übergeben Sie dazu den Namen der Spalte an den Parameter `read_csv` als `index_col`.
- Die Benennung des DataFrames `data_oceania_country` sagt uns, welche Region die
  Daten umfassen (`oceania`) und wie sie indiziert sind (`country`).

```python
data_oceania_country = pd.read_csv('data/gapminder_gdp_oceania.csv', index_col='country')
print(data_oceania_country)
```

```output
             gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
country
Australia       10039.59564     10949.64959     12217.22686     14526.12465
New Zealand     10556.57566     12247.39532     13175.67800     14463.91893

             gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
country
Australia       16788.62948     18334.19751     19477.00928     21888.88903
New Zealand     16046.03728     16233.71770     17632.41040     19007.19129

             gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007
country
Australia       23424.76683     26997.93657     30687.75473     34435.36744
New Zealand     18363.32494     21050.41377     23189.80135     25185.00911
```

## Verwenden Sie die Methode `DataFrame.info()`, um mehr über einen DataFrame herauszufinden.

```python
data_oceania_country.info()
```

```output
<class 'pandas.core.frame.DataFrame'>
Index: 2 entries, Australia to New Zealand
Data columns (total 12 columns):
gdpPercap_1952    2 non-null float64
gdpPercap_1957    2 non-null float64
gdpPercap_1962    2 non-null float64
gdpPercap_1967    2 non-null float64
gdpPercap_1972    2 non-null float64
gdpPercap_1977    2 non-null float64
gdpPercap_1982    2 non-null float64
gdpPercap_1987    2 non-null float64
gdpPercap_1992    2 non-null float64
gdpPercap_1997    2 non-null float64
gdpPercap_2002    2 non-null float64
gdpPercap_2007    2 non-null float64
dtypes: float64(12)
memory usage: 208.0+ bytes
```

- Dies ist ein `DataFrame`
- Zwei Zeilen mit den Namen `'Australia'` und `'New Zealand'`
- Zwölf Spalten, von denen jede zwei tatsächliche 64-Bit-Gleitkommawerte enthält.
  - Wir werden später über Nullwerte sprechen, die zur Darstellung fehlender
    Beobachtungen verwendet werden.
- Benötigt 208 Bytes Speicherplatz.

## Die Variable `DataFrame.columns` speichert Informationen über die Spalten des DataFrames.

- Beachten Sie, dass es sich hierbei um Daten und *nicht* um eine Methode handelt. (Es
  hat keine Klammern.)
  - Wie `math.pi`.
  - Verwenden Sie also nicht `()`, um zu versuchen, es aufzurufen.
- Wird als *Mitgliedvariable* oder einfach *Mitglied* bezeichnet.

```python
print(data_oceania_country.columns)
```

```output
Index(['gdpPercap_1952', 'gdpPercap_1957', 'gdpPercap_1962', 'gdpPercap_1967',
       'gdpPercap_1972', 'gdpPercap_1977', 'gdpPercap_1982', 'gdpPercap_1987',
       'gdpPercap_1992', 'gdpPercap_1997', 'gdpPercap_2002', 'gdpPercap_2007'],
      dtype='object')
```

## Verwenden Sie `DataFrame.T`, um einen DataFrame zu transponieren.

- Manchmal möchte man Spalten als Zeilen behandeln und umgekehrt.
- Transponieren (geschrieben `.T`) kopiert die Daten nicht, sondern ändert nur die
  Sichtweise des Programms darauf.
- Wie `columns` ist sie eine Mitgliedsvariable.

```python
print(data_oceania_country.T)
```

```output
country           Australia  New Zealand
gdpPercap_1952  10039.59564  10556.57566
gdpPercap_1957  10949.64959  12247.39532
gdpPercap_1962  12217.22686  13175.67800
gdpPercap_1967  14526.12465  14463.91893
gdpPercap_1972  16788.62948  16046.03728
gdpPercap_1977  18334.19751  16233.71770
gdpPercap_1982  19477.00928  17632.41040
gdpPercap_1987  21888.88903  19007.19129
gdpPercap_1992  23424.76683  18363.32494
gdpPercap_1997  26997.93657  21050.41377
gdpPercap_2002  30687.75473  23189.80135
gdpPercap_2007  34435.36744  25185.00911
```

## Verwenden Sie `DataFrame.describe()`, um zusammenfassende Statistiken über Daten zu erhalten.

`DataFrame.describe()` liefert die zusammenfassende Statistik nur für die Spalten, die
numerische Daten enthalten. Alle anderen Spalten werden ignoriert, es sei denn, Sie
verwenden das Argument `include='all'`.

```python
print(data_oceania_country.describe())
```

```output
       gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  gdpPercap_1967  \
count        2.000000        2.000000        2.000000        2.000000
mean     10298.085650    11598.522455    12696.452430    14495.021790
std        365.560078      917.644806      677.727301       43.986086
min      10039.595640    10949.649590    12217.226860    14463.918930
25%      10168.840645    11274.086022    12456.839645    14479.470360
50%      10298.085650    11598.522455    12696.452430    14495.021790
75%      10427.330655    11922.958888    12936.065215    14510.573220
max      10556.575660    12247.395320    13175.678000    14526.124650

       gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  gdpPercap_1987  \
count         2.00000        2.000000        2.000000        2.000000
mean      16417.33338    17283.957605    18554.709840    20448.040160
std         525.09198     1485.263517     1304.328377     2037.668013
min       16046.03728    16233.717700    17632.410400    19007.191290
25%       16231.68533    16758.837652    18093.560120    19727.615725
50%       16417.33338    17283.957605    18554.709840    20448.040160
75%       16602.98143    17809.077557    19015.859560    21168.464595
max       16788.62948    18334.197510    19477.009280    21888.889030

       gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  gdpPercap_2007
count        2.000000        2.000000        2.000000        2.000000
mean     20894.045885    24024.175170    26938.778040    29810.188275
std       3578.979883     4205.533703     5301.853680     6540.991104
min      18363.324940    21050.413770    23189.801350    25185.009110
25%      19628.685413    22537.294470    25064.289695    27497.598692
50%      20894.045885    24024.175170    26938.778040    29810.188275
75%      22159.406358    25511.055870    28813.266385    32122.777857
max      23424.766830    26997.936570    30687.754730    34435.367440
```

- Nicht besonders nützlich bei nur zwei Datensätzen, aber sehr hilfreich, wenn es
  Tausende sind.

::::::::::::::::::::::::::::::::::::::: challenge

## Andere Daten lesen

Lesen Sie die Daten in `gapminder_gdp_americas.csv` (die sich im gleichen Verzeichnis
wie `gapminder_gdp_oceania.csv` befinden sollten) in eine Variable mit dem Namen
`data_americas` und zeigen Sie deren zusammenfassende Statistik an.

::::::::::::::: solution

## Lösung

Um eine CSV-Datei einzulesen, verwenden wir `pd.read_csv` und übergeben ihr den
Dateinamen `'data/gapminder_gdp_americas.csv'`. Wir übergeben auch wieder den
Spaltennamen `'country'` an den Parameter `index_col`, um nach Ländern zu indizieren.
Die zusammenfassende Statistik kann mit der Methode `DataFrame.describe()` angezeigt
werden.

```python
data_americas = pd.read_csv('data/gapminder_gdp_americas.csv', index_col='country')
data_americas.describe()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Inspektion der Daten

Nachdem du die Daten für Amerika gelesen hast, benutze `help(data_americas.head)` und
`help(data_americas.tail)`, um herauszufinden, was `DataFrame.head` und `DataFrame.tail`
tun.

1. Welcher Methodenaufruf zeigt die ersten drei Zeilen dieser Daten an?
2. Mit welchem Methodenaufruf werden die letzten drei Spalten dieser Daten angezeigt?
   (Hinweis: Möglicherweise müssen Sie Ihre Ansicht der Daten ändern.)

::::::::::::::: solution

## Lösung

1. Wir können uns die ersten fünf Zeilen von `data_americas` ansehen, indem wir
   `data_americas.head()` ausführen, wodurch wir den Anfang des DataFrame sehen können.
   Wir können die Anzahl der Zeilen angeben, die wir sehen wollen, indem wir den
   Parameter `n` in unserem Aufruf von `data_americas.head()` angeben. Um die ersten
   drei Zeilen zu sehen, führen Sie aus:

  ```python
  data_americas.head(n=3)
  ```

  ```output
            continent  gdpPercap_1952  gdpPercap_1957  gdpPercap_1962  \
  country
  Argentina  Americas     5911.315053     6856.856212     7133.166023
  Bolivia    Americas     2677.326347     2127.686326     2180.972546
  Brazil     Americas     2108.944355     2487.365989     3336.585802

            gdpPercap_1967  gdpPercap_1972  gdpPercap_1977  gdpPercap_1982  \
  country
  Argentina     8052.953021     9443.038526    10079.026740     8997.897412
  Bolivia       2586.886053     2980.331339     3548.097832     3156.510452
  Brazil        3429.864357     4985.711467     6660.118654     7030.835878

             gdpPercap_1987  gdpPercap_1992  gdpPercap_1997  gdpPercap_2002  \
  country
  Argentina     9139.671389     9308.418710    10967.281950     8797.640716
  Bolivia       2753.691490     2961.699694     3326.143191     3413.262690
  Brazil        7807.095818     6950.283021     7957.980824     8131.212843

             gdpPercap_2007
  country
  Argentina    12779.379640
  Bolivia       3822.137084
  Brazil        9065.800825
  ```

2. Um die letzten drei Zeilen von `data_americas` zu überprüfen, würden wir den Befehl
   `americas.tail(n=3)` verwenden, analog zu `head()` wie oben. In diesem Fall wollen
   wir jedoch die letzten drei Spalten betrachten, also müssen wir unsere Ansicht ändern
   und dann `tail()` verwenden. Dazu erstellen wir einen neuen DataFrame, in dem Zeilen
   und Spalten vertauscht sind:

  ```python
  americas_flipped = data_americas.T
  ```

Wir können dann die letzten drei Spalten von `americas` betrachten, indem wir die
letzten drei Zeilen von `americas_flipped` betrachten:

  ```python
  americas_flipped.tail(n=3)
  ```

  ```output
  country        Argentina  Bolivia   Brazil   Canada    Chile Colombia  \
  gdpPercap_1997   10967.3  3326.14  7957.98  28954.9  10118.1  6117.36
  gdpPercap_2002   8797.64  3413.26  8131.21    33329  10778.8  5755.26
  gdpPercap_2007   12779.4  3822.14   9065.8  36319.2  13171.6  7006.58

  country        Costa Rica     Cuba Dominican Republic  Ecuador    ...     \
  gdpPercap_1997    6677.05  5431.99             3614.1  7429.46    ...
  gdpPercap_2002    7723.45  6340.65            4563.81  5773.04    ...
  gdpPercap_2007    9645.06   8948.1            6025.37  6873.26    ...

  country          Mexico Nicaragua   Panama Paraguay     Peru Puerto Rico  \
  gdpPercap_1997   9767.3   2253.02  7113.69   4247.4  5838.35     16999.4
  gdpPercap_2002  10742.4   2474.55  7356.03  3783.67  5909.02     18855.6
  gdpPercap_2007  11977.6   2749.32  9809.19  4172.84  7408.91     19328.7

  country        Trinidad and Tobago United States  Uruguay Venezuela
  gdpPercap_1997             8792.57       35767.4  9230.24   10165.5
  gdpPercap_2002             11460.6       39097.1     7727   8605.05
  gdpPercap_2007             18008.5       42951.7  10611.5   11415.8
  ```

Dies zeigt die gewünschten Daten an, aber vielleicht möchten wir lieber drei Spalten
statt drei Zeilen anzeigen lassen, also können wir es umdrehen:

  ```python
  americas_flipped.tail(n=3).T    
  ```

**Anmerkung:** Wir hätten die oben genannten Befehle auch in einer einzigen Codezeile
ausführen können, indem wir sie "verkettet" hätten:

  ```python
  data_americas.T.tail(n=3).T
  ```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Lesen von Dateien in anderen Verzeichnissen

Die Daten für Ihr aktuelles Projekt sind in einer Datei namens `microbes.csv`
gespeichert, die sich in einem Ordner namens `field_data` befindet. Sie führen die
Analyse in einem Notizbuch mit dem Namen `analysis.ipynb` in einem Schwesterordner
namens `thesis` durch:

```output
your_home_directory
+-- field_data/
|   +-- microbes.csv
+-- thesis/
    +-- analysis.ipynb
```

Welche(r) Wert(e) sollte(n) man an `read_csv` übergeben, um `microbes.csv` in
`analysis.ipynb` zu lesen?

::::::::::::::: solution

## Lösung

Wir müssen den Pfad zu der Datei, die uns interessiert, in dem Aufruf von `pd.read_csv`
angeben. Zunächst müssen wir mit "../" aus dem Ordner `thesis` und dann mit
"field\_data/" in den Ordner `field_data` "springen". Dann können wir den Dateinamen
`microbes.csv` angeben. Das Ergebnis ist wie folgt:

```python
data_microbes = pd.read_csv('../field_data/microbes.csv')
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Daten schreiben

Neben der Funktion `read_csv` zum Lesen von Daten aus einer Datei, bietet Pandas eine
Funktion `to_csv` zum Schreiben von DataFrame in Dateien. Wenden Sie an, was Sie über
das Lesen von Dateien gelernt haben, und schreiben Sie einen Ihrer DataFrame in eine
Datei namens `processed.csv`. Du kannst `help` benutzen, um Informationen darüber zu
bekommen, wie man `to_csv` benutzt.

::::::::::::::: solution

## Lösung

Um den DataFrame `data_americas` in eine Datei mit dem Namen `processed.csv` zu
schreiben, führen Sie den folgenden Befehl aus:

```python
data_americas.to_csv('processed.csv')
```

Um Hilfe zu `read_csv` oder `to_csv` zu erhalten, können Sie z.B. ausführen:

```python
help(data_americas.to_csv)
help(pd.read_csv)
```

Beachten Sie, dass `help(to_csv)` oder `help(pd.to_csv)` einen Fehler auslöst! Das liegt
daran, dass `to_csv` keine globale Pandas-Funktion ist, sondern eine Mitgliedsfunktion
von DataFrames. Das bedeutet, dass man sie nur auf einer Instanz eines DataFrames
aufrufen kann, z.B. `data_americas.to_csv` oder `data_oceania.to_csv`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Verwenden Sie die Pandas-Bibliothek, um grundlegende Statistiken aus tabellarischen
  Daten zu erhalten.
- Verwenden Sie `index_col`, um anzugeben, daß die Werte einer Spalte als
  Zeilenüberschriften verwendet werden sollen.
- Verwenden Sie `DataFrame.info`, um mehr über einen DataFrame herauszufinden.
- Die Variable `DataFrame.columns` speichert Informationen über die Spalten des
  DataFrames.
- Verwenden Sie `DataFrame.T`, um einen DataFrame zu transponieren.
- Verwenden Sie `DataFrame.describe`, um zusammenfassende Statistiken über Daten zu
  erhalten.

::::::::::::::::::::::::::::::::::::::::::::::::::



