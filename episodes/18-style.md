---
title: Programmierstil
teaching: 15
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Begründen Sie die grundlegenden Regeln des Codierungsstils.
- Refactor one-page programs to make them more readable and justify the changes.
- Verwenden Sie die Python Community Coding Standards (PEP-8).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich meine Programme besser lesbar machen?
- Wie formatieren die meisten Programmierer ihren Code?
- Wie können Programme ihre eigene Funktion überprüfen?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Kodierungsstil

Ein konsistenter Kodierungsstil hilft anderen (einschließlich unserer zukünftigen
Selbst), den Code leichter zu lesen und zu verstehen. Code wird viel öfter gelesen als
geschrieben, und wie es im [Zen of Python](https://www.python.org/dev/peps/pep-0020)
heißt, "Lesbarkeit zählt". Python hat mit einem seiner ersten Python Enhancement
Proposals (PEP), [PEP8](https://www.python.org/dev/peps/pep-0008), einen Standardstil
vorgeschlagen.

Einige Punkte, die hervorzuheben sind:

- Dokumentieren Sie Ihren Code und stellen Sie sicher, dass Annahmen, interne
  Algorithmen, erwartete Eingaben, erwartete Ausgaben, etc. klar sind
- Verwenden Sie klare, semantisch sinnvolle Variablennamen
- Verwenden Sie Leerzeichen, *nicht* Tabulatoren, um Zeilen einzurücken (Tabulatoren
  können in verschiedenen Texteditoren, Betriebssystemen und Versionskontrollsystemen
  Probleme verursachen)

## Befolgen Sie den Standard-Python-Stil in Ihrem Code.

- [PEP8](https://www.python.org/dev/peps/pep-0008): eine Stilanleitung für Python, die
  Themen wie die Benennung von Variablen, das Einrücken von Code, die Strukturierung von
  `import`-Anweisungen usw. behandelt. Die Einhaltung von PEP8 macht es für andere
  Python-Entwickler einfacher, Ihren Code zu lesen und zu verstehen, und zu wissen, wie
  ihre Beiträge aussehen sollten.
- Um Ihren Code auf die Einhaltung von PEP8 zu überprüfen, können Sie die [pycodestyle
  Anwendung](https://pypi.org/project/pycodestyle/) verwenden und Werkzeuge wie der
  [black code formatter](https://github.com/psf/black) können Ihren Code automatisch so
  formatieren, dass er mit PEP8 und pycodestyle konform ist (es gibt auch einen Jupyter
  notebook formatter [nb\_black](https://github.com/dnanhkhoa/nb_black)).
- Einige Gruppen und Organisationen folgen anderen Stilrichtlinien als PEP8. Der [Google
  style guide on Python] (https://google.github.io/styleguide/pyguide.html) gibt zum
  Beispiel leicht abweichende Empfehlungen. Google hat eine Anwendung geschrieben, die
  Ihnen dabei helfen kann, Ihren Code entweder nach ihrem Stil oder nach PEP8 zu
  formatieren: [yapf](https://github.com/google/yapf/).
- In Bezug auf den Codierungsstil ist der Schlüssel *Konsistenz*. Wählen Sie einen Stil
  für Ihr Projekt, sei es PEP8, der Google-Stil oder etwas anderes, und tun Sie Ihr
  Bestes, um sicherzustellen, dass Sie und alle anderen, mit denen Sie zusammenarbeiten,
  sich daran halten. Die Konsistenz innerhalb eines Projekts ist oft wichtiger als der
  verwendete Stil. Ein einheitlicher Stil macht Ihre Software für andere und für Sie
  selbst einfacher zu lesen und zu verstehen.

## Verwenden Sie Assertions, um auf interne Fehler zu prüfen.

Assertions sind eine einfache, aber mächtige Methode, um sicherzustellen, dass der
Kontext, in dem Ihr Code ausgeführt wird, so ist, wie Sie es erwarten.

```python
def calc_bulk_density(mass, volume):
    '''Return dry bulk density = powder mass / powder volume.'''
    assert volume > 0
    return mass / volume
```

Wenn die Behauptung `False` ist, löst der Python-Interpreter eine
`AssertionError`-Laufzeit-Ausnahme aus. Der Quellcode des fehlgeschlagenen Ausdrucks
wird als Teil der Fehlermeldung angezeigt. Um Behauptungen in Ihrem Code zu ignorieren,
führen Sie den Interpreter mit dem Schalter '-O' (optimize) aus. Behauptungen sollten
nur einfache Prüfungen enthalten und niemals den Zustand des Programms verändern. Zum
Beispiel sollte eine Assertion niemals eine Zuweisung enthalten.

## Verwenden Sie docstrings, um eingebaute Hilfe bereitzustellen.

Wenn das erste Ding in einer Funktion eine Zeichenkette ist, die nicht direkt einer
Variablen zugewiesen ist, fügt Python sie an die Funktion an, die über die eingebaute
Hilfefunktion zugänglich ist. Diese dokumentierende Zeichenkette wird auch als
*Docstring* bezeichnet.

```python
def average(values):
    "Return average of values, or None if no values are supplied."

    if len(values) == 0:
        return None
    return sum(values) / len(values)

help(average)
```

```output
Help on function average in module __main__:

average(values)
    Return average of values, or None if no values are supplied.
```

::::::::::::::::::::::::::::::::::::::::: callout

## Mehrzeilige Zeichenketten

Verwenden Sie oft *multiline strings* für die Dokumentation. Diese beginnen und enden
mit drei Anführungszeichen (entweder einfach oder doppelt) und enden mit drei passenden
Zeichen.

```python
"""This string spans
multiple lines.

Blank lines are allowed."""
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Was wird angezeigt?

Markieren Sie die Zeilen im folgenden Code, die als Online-Hilfe verfügbar sein werden.
Gibt es Zeilen, die verfügbar gemacht werden sollten, aber nicht verfügbar sind? Gibt es
Zeilen, die einen Syntaxfehler oder einen Laufzeitfehler verursachen?

```python
"Find maximum edit distance between multiple sequences."
# This finds the maximum distance between all sequences.

def overall_max(sequences):
    '''Determine overall maximum edit distance.'''

    highest = 0
    for left in sequences:
        for right in sequences:
            '''Avoid checking sequence against itself.'''
            if left != right:
                this = edit_distance(left, right)
                highest = max(highest, this)

    # Report.
    return highest
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Dokumentieren Sie dies

Verwenden Sie Kommentare, um potentiell unintuitive Abschnitte oder einzelne Codezeilen
zu beschreiben und anderen zu helfen, sie zu verstehen. Sie sind besonders nützlich für
alle, die Ihren Code in Zukunft verstehen und bearbeiten müssen, einschließlich Ihnen
selbst.

Verwenden Sie docstrings, um die zulässigen Eingaben und erwarteten Ausgaben einer
Methode oder Klasse, ihren Zweck, ihre Annahmen und ihr beabsichtigtes Verhalten zu
dokumentieren. Docstrings werden angezeigt, wenn ein Benutzer die eingebaute Methode
`help` für Ihre Methode oder Klasse aufruft.

Verwandeln Sie den Kommentar in der folgenden Funktion in einen docstring und überprüfen
Sie, ob `help` ihn richtig anzeigt.

```python
def middle(a, b, c):
    # Return the middle value of three.
    # Assumes the values can actually be compared.
    values = [a, b, c]
    values.sort()
    return values[1]
```

::::::::::::::: solution

## Lösung

```python
def middle(a, b, c):
    '''Return the middle value of three.
    Assumes the values can actually be compared.'''
    values = [a, b, c]
    values.sort()
    return values[1]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Diesen Code aufräumen

1. Lesen Sie dieses kurze Programm und versuchen Sie zu erraten, was es tut.
2. Führen Sie es aus: Wie genau war Ihre Vorhersage?
3. Refaktorieren Sie das Programm, um es lesbarer zu machen. Denken Sie daran, es nach
   jeder Änderung auszuführen, um sicherzustellen, dass sich sein Verhalten nicht
   geändert hat.
4. Vergleichen Sie Ihren Rewrite mit dem Ihres Nachbarn. Was haben Sie gleich gemacht?
   Was haben Sie anders gemacht, und warum?

```python
n = 10
s = 'et cetera'
print(s)
i = 0
while i < n:
    # print('at', j)
    new = ''
    for j in range(len(s)):
        left = j-1
        right = (j+1)%len(s)
        if s[left]==s[right]: new = new + '-'
        else: new = new + '*'
    s=''.join(new)
    print(s)
    i += 1
```

::::::::::::::: solution

## Lösung

Hier ist eine Lösung.

```python
def string_machine(input_string, iterations):
    """
    Takes input_string and generates a new string with -'s and *'s
    corresponding to characters that have identical adjacent characters
    or not, respectively.  Iterates through this procedure with the resultant
    strings for the supplied number of iterations.
    """
    print(input_string)
    input_string_length = len(input_string)
    old = input_string
    for i in range(iterations):
        new = ''
        # iterate through characters in previous string
        for j in range(input_string_length):
            left = j-1
            right = (j+1) % input_string_length  # ensure right index wraps around
            if old[left] == old[right]:
                new = new + '-'
            else:
                new = new + '*'
        print(new)
        # store new string as old
        old = new     

string_machine('et cetera', 10)
```

```output
et cetera
*****-***
----*-*--
---*---*-
--*-*-*-*
**-------
***-----*
--**---**
*****-***
----*-*--
---*---*-
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Befolgen Sie den Standard-Python-Stil in Ihrem Code.
- Verwenden Sie docstrings, um eingebaute Hilfe bereitzustellen.

::::::::::::::::::::::::::::::::::::::::::::::::::



