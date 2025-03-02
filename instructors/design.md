---
title: Entwurf der Lektion
---


::::::::::::::::::::::::::::::::::::::::: callout

## Hilfe gesucht

**Wir füllen die Übungen [unten](#Stufe-3-Lernplan) aus, um den Unterrichtsplan zu
konkretisieren. Beiträge (sowohl in Form von Pull-Requests mit ausgefüllten Übungen, als
auch von Kommentaren zu bestimmten Übungen, der Reihenfolge und dem Zeitplan) sind sehr
willkommen.**


::::::::::::::::::::::::::::::::::::::::::::::::::

## Verwendeter Prozess

> Michael Pollans Ratschlag, wenn er R oder Python-Programmierung unterrichten würde:
> 
> 1. Code schreiben.
> 2. Nicht zu viel.
> 3. Meistens Plots.
> 
> — [Michael Koontz](https://twitter.com/_mikoontz/status/758021742078025728) {:
> .quotation}
> 

Diese Lektion wurde mit einer abgespeckten Variante des "Understanding by Design"
Prozesses entwickelt. Die wichtigsten Abschnitte sind:

1. Annahmen über Publikum, Zeit, etc. (Der aktuelle Entwurf enthält auch einige
   Schlussfolgerungen und Entscheidungen in diesem Abschnitt - das sollte überarbeitet
   werden)

2. Gewünschte Ergebnisse: Gesamtziele, summative Beurteilungen mit halbtägiger
   Granularität, was die Lernenden tun können, was die Lernenden wissen werden.

3. Lernplan: Jede Episode hat eine Überschrift, die zusammenfasst, was behandelt wird,
   dann die geschätzte Zeit, die für den Unterricht und für die Übungen aufgewendet
   wird, während die Übungen als Aufzählungspunkte angegeben werden.

## Stufe 1: Annahmen

- Zuhörerschaft
  - Graduierte Studenten in numerischen Disziplinen von Kosmologie bis Archäologie
  - die Daten in Tabellenkalkulationen und mit interaktiven Werkzeugen wie SAS
    manipuliert haben
  - Haben aber *nicht* über CPD (copy-paste-despair) hinaus programmiert
- Beschränkungen
  - Ein ganzer Tag 09:00-16:30
    - 06:15 Unterrichtszeit
    - 0:45 Mittagspause
    - 0:30 insgesamt für zwei Kaffeepausen
  - Die Lernenden verwenden native Installationen auf ihren eigenen Rechnern
    - Kann VMs oder Cloud-Ressourcen nach Ermessen des Lehrers verwenden
    - Muss aber native lokale Installation als Option behalten
  - Keine Abhängigkeit von anderen Carpentry-Modulen
    - Erfordert insbesondere keine Kenntnisse über Shell oder Versionskontrolle
  - Das Jupyter Notebook verwenden
    - Authentisches Werkzeug, das von vielen Ausbildern verwendet wird
    - Es gibt nicht wirklich eine Alternative
    - Und bedeutet, dass auch Leute, die schon ein bisschen Python gesehen haben,
      wahrscheinlich etwas lernen werden
- Motivierendes Beispiel
  - Erstellen von 2D-Diagrammen, die sich für Veröffentlichungen eignen
  - Spricht fast jeden an
  - Macht die Lektion für beide Carpentries nutzbar
    - Und bedeutet, dass auch Leute, die schon ein bisschen Python gesehen haben,
      wahrscheinlich etwas lernen werden
- Daten
  - Die Gapminder-Daten durchgängig verwenden
  - Aber nach Kontinent in mehrere Dateien aufteilen
    - Um die Ausgabe von Beispielen übersichtlicher zu gestalten (z. B.
      Australien/Neuseeland, das nur zwei Zeilen umfasst)
    - und Beispiele für die Verwendung mehrerer Datensätze zulassen
- Fokus auf Pandas anstelle von NumPy
  - Macht die Lektion sowohl für Data Carpentry als auch für Software Carpentry
    verwendbar
  - Echte Neulinge wollen wahrscheinlich Datenanalyse
  - Und Leute mit etwas Vorerfahrung:
    - akzeptiert die Datenanalyse als authentische Aufgabe,
    - und werden wahrscheinlich nicht mit Pandas in Berührung gekommen sein, so dass sie
      trotzdem etwas Nützliches aus dieser Lektion mitnehmen können
- Die Herausforderungen sind meist *nicht* "schreibe diesen Code von Grund auf"
  - Wollen viele kurze Übungen, die zuverlässig in der vorgegebenen Zeit erledigt werden
    können
  - Verwenden Sie MCQs, Lückentexte, Parsons-Probleme, "tweak this code", etc.

## Stufe 2: Gewünschte Ergebnisse

### Fragen

Wie kann ich...

- ...Tabellendaten lesen?
- ...einen einzelnen Vektor von Werten darstellen?
- ...eine Zeitreihengrafik erstellen?
- ...ein Diagramm für jeden von mehreren Datensätzen erstellen?
- ...zusätzliche Daten aus einem einzelnen Datensatz zum Plotten erhalten?
- ...Programme schreiben, die ich lesen und in Zukunft wiederverwenden kann?

### Fertigkeiten

Ich kann...

- ...kurze Skripte mit Schleifen und Konditionalen schreiben.
- ...Funktionen mit einer festen Anzahl von Parametern zu schreiben, die ein einziges
  Ergebnis liefern.
- ...Bibliotheken mit Hilfe von Aliasen importieren und auf den Inhalt dieser
  Bibliotheken verweisen.
- ...einfache Datenextraktion und Formatierung mit Pandas durchführen.

### Konzepte

Ich weiß...

- ...dass ein Programm ein Laborgerät ist, das eine Analyse durchführt
  - Muss vor/bei der Verwendung validiert/kalibriert werden
  - Macht die Analyse reproduzierbar, überprüfbar, gemeinsam nutzbar
- ...dass Programme für Menschen geschrieben werden, nicht für Computer
  - Bedeutungsvolle Variablennamen
  - Modularität für Lesbarkeit und Wiederverwendung
  - Keine Duplizierung
  - Zweck und Verwendung dokumentieren
- ...dass es keine Magie gibt: die Programme, die sie benutzen, unterscheiden sich im
  Prinzip nicht von denen, die sie erstellen
- ...wie man Variablen Werte zuweist
- ...was Integers, Floats, Strings, NumPy-Arrays und Pandas-Dataframes sind
- ...wie man die Ausführung einer `for` Schleife verfolgt
- ...wie man die Ausführung von `if`/`else`-Anweisungen verfolgt
- ...wie man Listen erstellt und indiziert
- ...wie man NumPy-Arrays erstellt und indiziert
- ...wie man Pandas Dataframes erstellt und indiziert
- ...wie man Zeitreihenplots erstellt
- ...den Unterschied zwischen der Definition und dem Aufruf einer Funktion
- ...wo man Dokumentation zu Standardbibliotheken findet
- ...wie man herausfindet, was wissenschaftliches Python noch bietet

## Stufe 3: Lernplan

### Summative Bewertung

- Midpoint: Erstellen einer Zeitreihengrafik für jede Datei in einem Verzeichnis.
- Final: Daten aus einem Pandas-Datenframe extrahieren und eine vergleichende
  mehrzeilige Zeitreihendarstellung erstellen.

### [Interaktives Ausführen und Beenden](../episodes/01-run-quit.md) (9:00)

- Unterricht: 15 min (wegen Einrichtungsproblemen)
  - Starten Sie das Jupyter Notebook, erstellen Sie neue Notebooks und beenden Sie das
    Notebook.
  - Markdown-Zellen in einem Notizbuch erstellen.
  - Python-Zellen in einem Notizbuch erstellen und ausführen.
- Herausforderungen: 0 min (in die Unterrichtszeit eingerechnet - keine separate Übung)
  - Erstellen von Listen in Markdown
  - Was wird angezeigt, wenn mehrere Ausdrücke in einer einzigen Zelle stehen?
  - Eine bestehende Zelle von Code in Markdown umwandeln
  - Rendering von Gleichungen im LaTeX-Stil

### [Variablen und Zuweisung](../episodes/02-variables.md) (9:15)

- Unterricht: 10 min
  - Programme schreiben, die Variablen skalare Werte zuweisen und Berechnungen mit
    diesen Werten durchführen.
  - Wertänderungen in Programmen, die skalare Zuweisungen verwenden, korrekt verfolgen
    können.
- Herausforderungen: 10 min
  - Verfolgen Sie die Ausführung von Code, der zwei Werte mit Hilfe einer
    Zwischenvariablen vertauscht.
  - Endwerte von Variablen nach mehreren Zuweisungen vorhersagen können.
  - Was passiert, wenn man versucht, eine Zahl zu indizieren?
  - Welcher Variablenname ist besser, `m`, `min`, oder `minutes`?
  - Was ergeben die folgenden Slice-Ausdrücke?

### [Datentypen und Typkonvertierung](../episodes/03-types-conversion.md) (09:35)

- Unterricht: 10 min
  - Die wichtigsten Unterschiede zwischen ganzen Zahlen und Fließkommazahlen erläutern.
  - Die wichtigsten Unterschiede zwischen Zahlen und Zeichenketten erklären können.
  - Eingebaute Funktionen verwenden, um zwischen Ganzzahlen, Fließkommazahlen und
    Zeichenketten zu konvertieren.
- Herausforderungen: 10 min
  - Welcher Typ von Wert ist 3.4?
  - Was für ein Wert ist 3,25 + 4?
  - Welchen Typ von Wert würden Sie verwenden, um darzustellen:
    - Anzahl der Tage seit Beginn des Jahres.
    - Zeit, die seit Beginn des Jahres vergangen ist.
    - Etc.
  - Wie kann man `//` (ganzzahlige Division) und `%` (Modulo) verwenden?
  - Was macht `int("3.4")`?
  - Welche Ausdrücke geben bei diesen float-, int- und string-Werten ein bestimmtes
    Ergebnis aus?
  - Was erwarten Sie von `1+2j + 3` als Ergebnis?

### [Eingebaute Funktionen und Hilfe](../episodes/04-built-in.md) (09:55)

- Unterricht: 15 min
  - Den Zweck von Funktionen erklären können.
  - Eingebaute Python-Funktionen korrekt aufrufen können.
  - Richtiges Verschachteln von Aufrufen eingebauter Funktionen.
  - Die Hilfe verwenden, um die Dokumentation für eingebaute Funktionen anzuzeigen.
  - Situationen, in denen SyntaxError und NameError auftreten, korrekt beschreiben
    können.
- Herausforderungen: 10 min
  - Erklären Sie die Reihenfolge der Operationen in dem folgenden komplexen Ausdruck.
  - Was ergibt jede verschachtelte Kombination von `min` und `max` Aufrufen?
  - Warum geben `max` und `min` nicht `None` zurück, wenn keine Argumente angegeben
    werden?
  - Welcher Indexausdruck liefert nach dem bisher Gesehenen das letzte Zeichen einer
    Zeichenkette?

### [Kaffee](../episodes/05-coffee.md): 15 min (10:20)

### [Bibliotheken](../episodes/06-libraries.md) (10:35)

- Unterricht: 10 min
  - Erklären, was Softwarebibliotheken sind und warum Programmierer sie erstellen und
    benutzen.
  - Programme schreiben, die Bibliotheken aus der Standardbibliothek von Python
    importieren und verwenden.
  - Dokumentation zu Standardbibliotheken interaktiv (im Interpreter) und online finden
    und lesen können.
- Herausforderungen: 10 min
  - Welche Funktion aus der mathematischen Standardbibliothek können Sie verwenden, um
    eine Quadratwurzel zu berechnen?
  - Welche Bibliothek würden Sie verwenden, um einen Zufallswert aus Daten auszuwählen?
  - Wenn `help(math)` einen Fehler produziert, was haben Sie vergessen zu tun?
  - Füllen Sie die Leerstellen im folgenden Code aus, damit die Importanweisung und das
    Programm laufen.

### [Tabellarische Daten lesen](../episodes/07-reading-tabular.md) (10:55)

- Unterricht: 10 min
  - Importieren Sie die Pandas-Bibliothek.
  - Pandas verwenden, um einen einfachen CSV-Datensatz zu laden.
  - Einige grundlegende Informationen über einen Pandas DataFrame erhalten.
- Herausforderungen: 10 min
  - Die Daten für Amerika lesen und die zusammenfassenden Statistiken anzeigen.
  - Was bewirken `.head` und `.tail`?
  - Welche Zeichenfolge(n) sollte(n) man an `read_csv` übergeben, um Dateien aus anderen
    Verzeichnissen zu lesen?
  - Wie kann man CSV-Daten *schreiben*?

### [DataFrames](../episodes/08-data-frames.md) (11:15)

- Unterricht: 15 min
  - Einzelne Werte aus einem Pandas-Datenframe auswählen.
  - Ganze Zeilen oder ganze Spalten aus einem Datenrahmen auswählen.
  - Eine Teilmenge von Zeilen und Spalten aus einem Datenrahmen in einer einzigen
    Operation auswählen.
  - Eine Teilmenge eines Datenrahmens anhand eines einzigen booleschen Kriteriums
    auswählen.
- Herausforderungen: 15 min
  - Schreiben Sie einen Ausdruck, um das Pro-Kopf-BIP von Serbien im Jahr 2007 zu
    ermitteln.
  - Welche Regel regelt, was in numerischen und benannten Slices in Pandas enthalten ist
    (oder nicht)?
  - Was macht jede Zeile in dem folgenden kurzen Programm?
  - Was bewirken `idxmin` und `idxmax`?
  - Schreiben Sie Ausdrücke, um das Pro-Kopf-BIP für alle Länder im Jahr 1982, für alle
    Länder *nach* 1985, usw. zu ermitteln.
  - Was würden Sie tun, wenn Sie eine Tabelle mit dem Pro-Kopf-BIP Polens für das
    zwanzigste Jahrhundert erstellen sollten, da sich die Grenzen des Landes seit 1900
    verändert haben?

### [Plotting](../episodes/09-plotting.md) (11:45)

- Unterricht: 15 min
  - Eine Zeitreihengrafik mit einem einzelnen Datensatz erstellen.
  - Eine Punktwolke erstellen, die die Beziehung zwischen zwei Datensätzen zeigt.
- Übung: 15 min
  - Füllen Sie die Lücken aus, um das minimale Pro-Kopf-BIP der europäischen Länder im
    Zeitverlauf darzustellen.
  - Modifizieren Sie das Beispiel, um ein Streudiagramm des Pro-Kopf-BIP in asiatischen
    Ländern zu erstellen.
  - Erklären Sie, was die einzelnen Argumente von `plot` im folgenden Beispiel bewirken.

### [Mittagessen](../episodes/10-lunch.md) (12:15): 45 min

### [Listen](../episodes/11-lists.md) (13:00)

- Unterricht: 10 min
  - Erklären, warum Programme Sammlungen von Werten benötigen.
  - Programme schreiben, die flache Listen erstellen, indizieren, zerschneiden und durch
    Zuweisungen und Methodenaufrufe verändern.
- Herausforderungen: 10 min
  - Füllen Sie die Leerzeichen aus, damit das Programm die gezeigte Ausgabe erzeugt.
  - Wie groß sind die folgenden Slices?
  - Was geben negative Indexausdrücke aus?
  - Was bewirkt ein "stride" in einem Slice?
  - Wie behandeln Slices Schranken außerhalb des Bereichs?
  - Was sind die Unterschiede zwischen diesen beiden Sortierverfahren?
  - Was ist der Unterschied zwischen `new = old` und `new = old[:]`?

### [Schleifen](../episodes/12-for-loops.md) (13:20)

- Unterricht: 10 min
  - Erläutern Sie, wozu for-Schleifen normalerweise verwendet werden.
  - Die Ausführung einer einfachen (nicht verschachtelten) Schleife verfolgen und die
    Werte der Variablen in jeder Iteration korrekt angeben können.
  - for-Schleifen schreiben, die das Accumulator-Muster verwenden, um Werte zu
    aggregieren.
- Herausforderungen: 15 min
  - Ist ein Einrückungsfehler ein Syntaxfehler oder ein Laufzeitfehler?
  - Verfolgen, welche Zeilen dieses Programms in welcher Reihenfolge ausgeführt werden.
  - Füllen Sie die Leerzeichen in diesem Programm aus, so dass es eine Zeichenkette
    umkehrt.
  - Füllen Sie die Lücken in dieser Reihe von Beispielen aus, um das Akkumulieren von
    Werten zu üben.
  - Diese Zeilen neu anordnen und einrücken, um die kumulative Summe der Listenwerte zu
    berechnen.

### [Konditionale](13-konditionale) (15:00)

- Unterricht: 10 min
  - Programme, die if- und else-Anweisungen und einfache boolesche Ausdrücke (ohne
    logische Operatoren) verwenden, korrekt schreiben können.
  - Die Ausführung von nicht verschachtelten Konditionalen und Konditionalen innerhalb
    von Schleifen verfolgen können.
- Herausforderungen: 15 min
  - Verfolgen Sie die Ausführung dieser bedingten Anweisung.
  - Füllen Sie die Leerzeichen aus, damit diese Funktion negative Werte durch Nullen
    ersetzt.
  - Ändern Sie dieses Programm so, dass es nur Dateien mit weniger als 50 Datensätzen
    verarbeitet.
  - Ändern Sie dieses Programm so ab, dass es immer den größten und den kleinsten Wert
    in einer Liste findet, unabhängig davon, welche Werte die Liste hat.

### [Schleifen über Datensätze](14-looping-data-sets) (13:45)

- Unterricht: 5 min
  - In der Lage sein, globale Ausdrücke zu lesen und zu schreiben, die mit Dateimengen
    übereinstimmen.
  - Glob verwenden, um Dateilisten zu erstellen.
  - for-Schleifen schreiben, um Operationen auf Dateien durchzuführen, deren Namen in
    einer Liste angegeben sind.
- Herausforderungen: 10 min
  - Welche Dateinamen werden von diesem glob-Ausdruck *nicht* gefunden?
  - Ändern Sie dieses Programm so, dass es die Anzahl der Datensätze in der kürzesten
    Datei ausgibt.
  - Schreiben Sie ein Programm, das alle regionalen Datensätze liest und darstellt.

### [Kaffee](15-Kaffee) (14:45): 15 min

### [Schreibfunktionen](16-schreib-funktionen) (14:00)

- Unterricht: 10 min
  - Den Unterschied zwischen Funktionsdefinition und Funktionsaufruf erklären und
    identifizieren.
  - Schreiben Sie eine Funktion, die eine kleine, feste Anzahl von Argumenten annimmt
    und ein einziges Ergebnis liefert.
- Herausforderungen: 15 min
  - Dieser Code definiert eine Funktion und ruft sie auf - was gibt sie aus, wenn sie
    ausgeführt wird?
  - Erklären Sie, warum dieses kurze Programm Dinge in dieser Reihenfolge ausgibt.
  - Füllen Sie die Leerstellen aus, um eine Funktion zu erstellen, die den kleinsten
    Wert in einer Datendatei findet.
  - Füllen Sie die Lücken aus, um eine Funktion zu erstellen, die den ersten negativen
    Wert in einer Liste findet. Was macht Ihre Funktion, wenn die Liste leer ist?
  - Warum ist es manchmal sinnvoll, Argumente durch Benennung der entsprechenden
    Parameter zu übergeben?
  - Füllen Sie die Leerstellen aus und verwandeln Sie diesen kurzen Code in eine
    Funktion.

### [Variablenumfang](17-scope) (14:25)

- Unterricht: 10 min
  - Lokale und globale Variablen identifizieren können.
  - Parameter als lokale Variablen identifizieren.
  - Einen Traceback lesen und die Datei, die Funktion und die Zeilennummer bestimmen, in
    der der Fehler aufgetreten ist.
- Herausforderungen: 10 min
  - Verfolgen Sie die Änderungen an den Werten in diesem Programm und achten Sie dabei
    auf die Unterscheidung zwischen lokalen und globalen Werten.

### [Programmierstil](18-style) (15:25)

- Unterricht: 15 min
  - Wie kann ich meine Programme besser lesbar machen?
  - Wie formatieren die meisten Programmierer ihren Code?
  - Wie können Programme ihre eigene Arbeitsweise überprüfen?
- Herausforderungen: 15 min
  - Welche Zeilen dieses Codes werden als Online-Hilfe verfügbar sein?
  - Verwandeln Sie die Kommentare in diesem Programm in Docstrings.
  - Schreiben Sie dieses kurze Programm um, damit es besser lesbar ist.

### [Wrap-Up](19-wrap) (15:55)

- Unterricht: 20 min
  - Wissenschaftliche Python-Gemeinschaftsseiten für Software, Workshops und Hilfe
    benennen und finden können.
- Herausforderungen: 0 min
  - Keine.

### [Rückmeldung](20-Rückmeldung) (16:15)

- Unterricht: 0 min
- Herausforderungen: 15 min
  - Rückmeldungen sammeln

### Beenden (16:30)


