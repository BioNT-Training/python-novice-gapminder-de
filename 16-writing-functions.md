---
title: Funktionen schreiben
teaching: 10
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erklären und identifizieren Sie den Unterschied zwischen Funktionsdefinition und
  Funktionsaufruf.
- Schreiben Sie eine Funktion, die eine kleine, feste Anzahl von Argumenten annimmt und
  ein einziges Ergebnis liefert.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich meine eigenen Funktionen erstellen?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Zerlegen Sie Programme in Funktionen, um sie besser verstehen zu können.

- Der Mensch kann nur einige wenige Dinge gleichzeitig im Arbeitsgedächtnis behalten.
- Verstehen Sie größere/kompliziertere Ideen, indem Sie Teile verstehen und kombinieren.
  - Komponenten in einer Maschine.
  - Lemmata beim Beweisen von Theoremen.
- Funktionen dienen in Programmen demselben Zweck.
  - *Kapseln* wir die Komplexität ein, so dass wir sie als ein einziges "Ding" behandeln
    können.
- Ermöglicht auch die *Wiederverwendung*.
  - Einmal schreiben, viele Male verwenden.

## Definieren Sie eine Funktion mit `def` mit einem Namen, Parametern und einem Codeblock.

- Beginnen Sie die Definition einer neuen Funktion mit `def`.
- Gefolgt vom Namen der Funktion.
  - Muss denselben Regeln gehorchen wie Variablennamen.
- Dann *Parameter* in Klammern.
  - Leere Klammern, wenn die Funktion keine Eingaben annimmt.
  - Wir werden dies gleich im Detail besprechen.
- Dann ein Doppelpunkt.
- Dann ein eingerückter Code-Block.

```python
def print_greeting():
    print('Hello!')
    print('The weather is nice today.')
    print('Right?')
```

## Durch die Definition einer Funktion wird diese nicht ausgeführt.

- Die Definition einer Funktion führt sie nicht aus.
  - Wie die Zuweisung eines Wertes zu einer Variablen.
- Muss die Funktion aufrufen, um den in ihr enthaltenen Code auszuführen.

```python
print_greeting()
```

```output
Hello!
```

## Argumente in einem Funktionsaufruf werden mit ihren definierten Parametern abgeglichen.

- Funktionen sind am nützlichsten, wenn sie mit verschiedenen Daten arbeiten können.
- Geben Sie *Parameter* an, wenn Sie eine Funktion definieren.
  - Diese werden zu Variablen, wenn die Funktion ausgeführt wird.
  - werden die Argumente im Aufruf (d.h. die der Funktion übergebenen Werte) zugeordnet.
  - Wenn Sie die Argumente nicht benennen, wenn Sie sie im Aufruf verwenden, werden die
    Argumente den Parametern in der Reihenfolge zugeordnet, in der die Parameter in der
    Funktion definiert sind.

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
```

```output
1871/3/19
```

Oder wir können die Argumente benennen, wenn wir die Funktion aufrufen, was uns erlaubt,
sie in beliebiger Reihenfolge anzugeben und die Aufrufseite übersichtlicher zu
gestalten; andernfalls könnte man beim Lesen des Codes vergessen, ob das zweite Argument
zum Beispiel der Monat oder der Tag ist.

```python
print_date(month=3, day=19, year=1871)
```

```output
1871/3/19
```

- Über [Twitter](https://twitter.com/minisciencegirl/status/693486088963272705): `()`
  enthält die Zutaten für die Funktion, während der Körper das Rezept enthält.

## Funktionen können mit `return` ein Ergebnis an ihren Aufrufer zurückgeben.

- Verwenden Sie `return ...`, um einen Wert an den Aufrufer zurückzugeben.
- Kann an beliebiger Stelle in der Funktion auftreten.
- Aber Funktionen sind leichter zu verstehen, wenn `return` vorkommt:
  - Am Anfang, um Sonderfälle zu behandeln.
  - Ganz am Ende, mit einem Endergebnis.

```python
def average(values):
    if len(values) == 0:
        return None
    return sum(values) / len(values)
```

```python
a = average([1, 3, 4])
print('average of actual values:', a)
```

```output
average of actual values: 2.6666666666666665
```

```python
print('average of empty list:', average([]))
```

```output
average of empty list: None
```

- Zur Erinnerung: [jede Funktion gibt etwas zurück](04-built-in.md).
- Eine Funktion, die nicht ausdrücklich `return` einen Wert angibt, gibt automatisch
  `None` zurück.

```python
result = print_date(1871, 3, 19)
print('result of call is:', result)
```

```output
1871/3/19
result of call is: None
```

::::::::::::::::::::::::::::::::::::::: challenge

## Erkennen von Syntaxfehlern

1. Lesen Sie den folgenden Code und versuchen Sie, die Fehler zu identifizieren, ohne
   ihn auszuführen.
2. Führen Sie den Code aus und lesen Sie die Fehlermeldung. Ist es ein `SyntaxError`
   oder ein `IndentationError`?
3. Beheben Sie den Fehler.
4. Wiederholen Sie die Schritte 2 und 3, bis Sie alle Fehler behoben haben.

```python
def another_function
  print("Syntax errors are annoying.")
   print("But at least python tells us about them!")
  print("So they are usually not too hard to fix.")
```

::::::::::::::: solution

## Lösung

```python
def another_function():
  print("Syntax errors are annoying.")
  print("But at least Python tells us about them!")
  print("So they are usually not too hard to fix.")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Definition und Verwendung

Was gibt das folgende Programm aus?

```python
def report(pressure):
    print('pressure is', pressure)

print('calling', report, 22.5)
```

::::::::::::::: solution

## Lösung

```output
calling <function report at 0x7fd128ff1bf8> 22.5
```

Ein Funktionsaufruf muss immer in Klammern gesetzt werden, sonst erhält man die
Speicheradresse des Funktionsobjekts. Wenn wir also die Funktion mit dem Namen report
aufrufen und ihr den Wert 22.5 geben wollen, könnten wir unseren Funktionsaufruf wie
folgt formulieren

```python
print("calling")
report(22.5)
```

```output
calling
pressure is 22.5
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Reihenfolge der Operationen

1. Was ist in diesem Beispiel falsch?

  ```python
  result = print_time(11, 37, 59)

  def print_time(hour, minute, second):
     time_string = str(hour) + ':' + str(minute) + ':' + str(second)
     print(time_string)
  ```

2. Erläutern Sie nach der Lösung des obigen Problems, warum dieser Beispielcode
   ausgeführt wird:

  ```python
  result = print_time(11, 37, 59)
  print('result of call is:', result)
  ```

ergibt diese Ausgabe:

  ```output
  11:37:59
  result of call is: None
  ```

3. Warum ist das Ergebnis des Aufrufs `None`?

::::::::::::::: solution

## Lösung

1. Das Problem bei diesem Beispiel ist, dass die Funktion `print_time()` erst *nach* dem
   Aufruf der Funktion definiert wird. Python weiß nicht, wie es den Namen `print_time`
   auflösen soll, da er noch nicht definiert wurde, und wird ein `NameError` auslösen,
   z.B. `NameError: name 'print_time' is not defined`

2. Die erste Zeile der Ausgabe `11:37:59` wird von der ersten Codezeile `result =
   print_time(11, 37, 59)` gedruckt, die den durch den Aufruf von `print_time`
   zurückgegebenen Wert an die Variable `result` bindet. Die zweite Zeile stammt aus dem
   zweiten Druckaufruf, um den Inhalt der Variablen `result` zu drucken.

3. `print_time()` nicht explizit `return` einen Wert, so dass es automatisch `None`
   zurückgibt.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Verkapselung

Füllen Sie die Leerzeichen aus, um eine Funktion zu erstellen, die einen einzelnen
Dateinamen als Argument nimmt, die Daten in die durch das Argument benannte Datei lädt
und den Mindestwert in diesen Daten zurückgibt.

```python
import pandas as pd

def min_in_data(____):
    data = ____
    return ____
```

::::::::::::::: solution

## Lösung

```python
import pandas as pd

def min_in_data(filename):
    data = pd.read_csv(filename)
    return data.min()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Finde die erste

Füllen Sie die Lücken aus, um eine Funktion zu erstellen, die eine Liste von Zahlen als
Argument nimmt und den ersten negativen Wert in der Liste zurückgibt. Was macht Ihre
Funktion, wenn die Liste leer ist? Was ist, wenn die Liste keine negativen Zahlen
enthält?

```python
def first_negative(values):
    for v in ____:
        if ____:
            return ____
```

::::::::::::::: solution

## Lösung

```python
def first_negative(values):
    for v in values:
        if v < 0:
            return v
```

Wenn eine leere Liste oder eine Liste mit allen positiven Werten an diese Funktion
übergeben wird, gibt sie `None` zurück:

```python
my_list = []
print(first_negative(my_list))
```

```output
None
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Aufruf durch Name

Vorhin haben wir diese Funktion gesehen:

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)
```

Wir haben gesehen, dass wir die Funktion mit *benannten Argumenten* aufrufen können,
etwa so:

```python
print_date(day=1, month=2, year=2003)
```

1. Was gibt `print_date(day=1, month=2, year=2003)` aus?
2. Wann haben Sie schon einmal einen Funktionsaufruf wie diesen gesehen?
3. Wann und warum ist es sinnvoll, Funktionen auf diese Weise aufzurufen?

::::::::::::::: solution

## Lösung

1. `2003/2/1`
2. Wir haben Beispiele für die Verwendung von *benannten Argumenten* bei der Arbeit mit
   der Pandas-Bibliothek gesehen. Wenn man zum Beispiel einen Datensatz mit `data =
   pd.read_csv('data/gapminder_gdp_europe.csv', index_col='country')` einliest, ist das
   letzte Argument `index_col` ein benanntes Argument.
3. Die Verwendung von benannten Argumenten kann den Code lesbarer machen, da man aus dem
   Funktionsaufruf erkennen kann, welchen Namen die verschiedenen Argumente innerhalb
   der Funktion haben. Es kann auch die Wahrscheinlichkeit verringern, dass Argumente in
   der falschen Reihenfolge übergeben werden, da bei der Verwendung von benannten
   Argumenten die Reihenfolge keine Rolle spielt.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Verkapselung eines If/Print-Blocks

Der folgende Code wird auf einem Etikettendrucker für Hühnereier ausgeführt. Eine
digitale Waage meldet dem Computer die Masse eines Hühnereis (in Gramm) und der Computer
druckt dann ein Etikett.

```python
import random
for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass)

    # egg sizing machinery prints a label
    if mass >= 85:
        print("jumbo")
    elif mass >= 70:
        print("large")
    elif mass < 70 and mass >= 55:
        print("medium")
    else:
        print("small")
```

Der if-Block, der die Eier klassifiziert, könnte auch in anderen Situationen nützlich
sein. Um eine Wiederholung zu vermeiden, könnten wir ihn in eine Funktion falten,
`get_egg_label()`. Wenn wir das Programm überarbeiten, um die Funktion zu verwenden,
würden wir folgendes erhalten:

```python
# revised version
import random
for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass = 70 + 20.0 * (2.0 * random.random() - 1.0)

    print(mass, get_egg_label(mass))

```

1. Erstellen Sie eine Funktionsdefinition für `get_egg_label()`, die mit dem
   überarbeiteten Programm oben funktionieren wird. Beachten Sie, dass der Rückgabewert
   der Funktion `get_egg_label()` wichtig sein wird. Die Beispielausgabe des obigen
   Programms wäre `71.23 large`.
2. Ein schmutziges Ei könnte eine Masse von mehr als 90 Gramm haben, und ein verdorbenes
   oder zerbrochenes Ei hat wahrscheinlich eine Masse von weniger als 50 Gramm. Ändern
   Sie Ihre Funktion `get_egg_label()`, um diese Fehlerbedingungen zu berücksichtigen.
   Eine Beispielausgabe könnte `25 too light, probably spoiled` sein.

::::::::::::::: solution

## Lösung

```python
def get_egg_label(mass):
    # egg sizing machinery prints a label
    egg_label = "Unlabelled"
    if mass >= 90:
        egg_label = "warning: egg might be dirty"
    elif mass >= 85:
        egg_label = "jumbo"
    elif mass >= 70:
        egg_label = "large"
    elif mass < 70 and mass >= 55:
        egg_label = "medium"
    elif mass < 50:
        egg_label = "too light, probably spoiled"
    else:
        egg_label = "small"
    return egg_label
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Verkapselnde Datenanalyse

Nehmen Sie an, dass der folgende Code ausgeführt wurde:

```python
import pandas as pd

data_asia = pd.read_csv('data/gapminder_gdp_asia.csv', index_col=0)
japan = data_asia.loc['Japan']
```

1. Vervollständigen Sie die nachstehenden Aussagen, um das durchschnittliche BIP Japans
   über die für die 1980er Jahre angegebenen Jahre zu erhalten.

  ```python
  year = 1983
  gdp_decade = 'gdpPercap_' + str(year // ____)
  avg = (japan.loc[gdp_decade + ___] + japan.loc[gdp_decade + ___]) / 2
  ```

2. Fassen Sie den obigen Code in einer einzigen Funktion zusammen.

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_'+___+'.csv',delimiter=',',index_col=0)
      ____
      ____
      ____
      return avg
  ```

3. Wie würden Sie diese Funktion verallgemeinern, wenn Sie im Voraus nicht wüssten,
   welche spezifischen Jahre als Spalten in den Daten vorkommen? Was wäre zum Beispiel,
   wenn wir für jedes Jahrzehnt auch Daten von Jahren hätten, die mit 1 und 9 enden?
   (Tipp: Verwenden Sie die Spalten, um die Spalten herauszufiltern, die dem Jahrzehnt
   entsprechen, anstatt sie im Code aufzuzählen)

::::::::::::::: solution

## Lösung

1. Das durchschnittliche BIP für Japan über die Jahre, die für die 1980er Jahre
   berichtet werden, wird mit berechnet:

  ```python
  year = 1983
  gdp_decade = 'gdpPercap_' + str(year // 10)
  avg = (japan.loc[gdp_decade + '2'] + japan.loc[gdp_decade + '7']) / 2
  ```

2. Dieser Code als Funktion ist:

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
      c = data_countries.loc[country]
      gdp_decade = 'gdpPercap_' + str(year // 10)
      avg = (c.loc[gdp_decade + '2'] + c.loc[gdp_decade + '7'])/2
      return avg
  ```

3. Um den Durchschnitt für die betreffenden Jahre zu erhalten, müssen wir eine Schleife
   über sie ziehen:

  ```python
  def avg_gdp_in_decade(country, continent, year):
      data_countries = pd.read_csv('data/gapminder_gdp_' + continent + '.csv', index_col=0)
      c = data_countries.loc[country]
      gdp_decade = 'gdpPercap_' + str(year // 10)
      total = 0.0
      num_years = 0
      for yr_header in c.index: # c's index contains reported years
          if yr_header.startswith(gdp_decade):
              total = total + c.loc[yr_header]
              num_years = num_years + 1
      return total/num_years
  ```

Die Funktion kann nun aufgerufen werden durch:

```python
avg_gdp_in_decade('Japan','asia',1983)
```

```output
20880.023800000003
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Simulation eines dynamischen Systems

In der Mathematik ist ein [dynamisches
System](https://en.wikipedia.org/wiki/Dynamical_system) ein System, in dem eine Funktion
die Zeitabhängigkeit eines Punktes in einem geometrischen Raum beschreibt. Ein
kanonisches Beispiel für ein dynamisches System ist die [logistische
Karte](https://en.wikipedia.org/wiki/Logistic_map), ein Wachstumsmodell, das eine neue
Bevölkerungsdichte (zwischen 0 und 1) auf der Grundlage der aktuellen Dichte berechnet.
In diesem Modell nimmt die Zeit die diskreten Werte 0, 1, 2, ...

1. Definieren Sie eine Funktion namens `logistic_map`, die zwei Eingaben benötigt: `x`,
   die die aktuelle Bevölkerung (zum Zeitpunkt `t`) darstellt, und einen Parameter `r =
   1`. Diese Funktion sollte einen Wert zurückgeben, der den Zustand des Systems (der
   Population) zum Zeitpunkt `t + 1` repräsentiert, wobei die Abbildungsfunktion
   verwendet wird:

`f(t+1) = r * f(t) * [1 - f(t)]`

2. Iterieren Sie die in Teil 1 definierte Funktion `logistic_map` ausgehend von einer
   Grundgesamtheit von 0,5 über einen Zeitraum von `t_final = 10` in einer Schleife
   `for` oder `while`. Speichern Sie die Zwischenergebnisse in einer Liste, so dass Sie
   nach Beendigung der Schleife eine Folge von Werten haben, die den Zustand der
   logistischen Karte zu Zeiten `t = [0,1,...,t_final]` (insgesamt 11 Werte) darstellen.
   Drucken Sie diese Liste aus, um die Entwicklung der Population zu sehen.

3. Kapseln Sie die Logik Ihrer Schleife in eine Funktion mit dem Namen `iterate`, die
   die Ausgangsbevölkerung als erste Eingabe, den Parameter `t_final` als zweite Eingabe
   und den Parameter `r` als dritte Eingabe erhält. Die Funktion sollte die Liste der
   Werte zurückgeben, die den Zustand der logistischen Karte zu den Zeitpunkten `t =
   [0,1,...,t_final]` darstellen. Führen Sie diese Funktion für die Zeiträume `t_final =
   100` und `1000` aus und geben Sie einige der Werte aus. Entwickelt sich die
   Bevölkerung zu einem stabilen Zustand?

::::::::::::::: solution

## Lösung

1. 
  ```python
  def logistic_map(x, r):
      return r * x * (1 - x)
  ```

2. 
  ```python
  initial_population = 0.5
  t_final = 10
  r = 1.0
  population = [initial_population]

  for t in range(t_final):
      population.append( logistic_map(population[t], r) )
  ```

3. 
  ```python
  def iterate(initial_population, t_final, r):
      population = [initial_population]
      for t in range(t_final):
          population.append( logistic_map(population[t], r) )
      return population

  for period in (10, 100, 1000):
      population = iterate(0.5, period, 1)
      print(population[-1])
  ```

  ```output
  0.06945089389714401
  0.009395779870614648
  0.0009913908614406382
  ```

Die Bevölkerung scheint sich dem Nullpunkt zu nähern.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Verwendung von Funktionen mit Konditionalen in Pandas

Funktionen enthalten oft Konditionale. Hier ist ein kurzes Beispiel, das anzeigt, in
welchem Quartil sich das Argument befindet, basierend auf handcodierten Werten für die
Quartilsschnittpunkte.

```python
def calculate_life_quartile(exp):
    if exp < 58.41:
        # This observation is in the first quartile
        return 1
    elif exp >= 58.41 and exp < 67.05:
        # This observation is in the second quartile
       return 2
    elif exp >= 67.05 and exp < 71.70:
        # This observation is in the third quartile
       return 3
    elif exp >= 71.70:
        # This observation is in the fourth quartile
       return 4
    else:
        # This observation has bad data
       return None

calculate_life_quartile(62.5)
```

```output
2
```

Diese Funktion würde typischerweise innerhalb einer `for`-Schleife verwendet werden,
aber Pandas hat einen anderen, effizienteren Weg, das Gleiche zu tun, und zwar durch
*Anwendung* einer Funktion auf einen Datenrahmen oder einen Teil eines Datenrahmens.
Hier ist ein Beispiel, das die obige Definition verwendet.

```python
data = pd.read_csv('data/gapminder_all.csv')
data['life_qrtl'] = data['lifeExp_1952'].apply(calculate_life_quartile)
```

Diese zweite Zeile enthält eine ganze Menge, also gehen wir sie Stück für Stück durch.
Auf der rechten Seite von `=` beginnen wir mit `data['lifeExp']`, das ist die Spalte in
dem Datenrahmen namens `data` mit der Bezeichnung `lifExp`. Wir benutzen `apply()`, um
das zu tun, was es sagt, nämlich `calculate_life_quartile` auf den Wert dieser Spalte
für jede Zeile des Datenrahmens anzuwenden.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Zerlegen Sie Programme in Funktionen, um sie besser verstehen zu können.
- Definieren Sie eine Funktion mit `def` mit einem Namen, Parametern und einem
  Codeblock.
- Die Definition einer Funktion führt sie nicht aus.
- Argumente in einem Funktionsaufruf werden mit ihren definierten Parametern
  abgeglichen.
- Funktionen können mit `return` ein Ergebnis an ihren Aufrufer zurückgeben.

::::::::::::::::::::::::::::::::::::::::::::::::::



