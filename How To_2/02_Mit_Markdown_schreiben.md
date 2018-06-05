---
pagetitle: Mit Markdown schreiben
...

# Mit Markdown schreiben

Markdown ist eine einfache Auszeichnungssprache (die eigentlich Markup-Sprachen
genannt werden). Als solche erlaubt es uns Markdown die Struktur von Texten
auszuzeichnen. So wird der Inhalt (mehr oder weniger vollständig)
von der Form des Texts – also dessen Aussehen – getrennt.

Typische Strukturelemente in Texten:

- Absätze
- Überschriften (mit verschiedenen Hierarchieebenen)
- Blockzitate
- Fußnoten
- Listen
- Aufzählungen
- Bilder
- Bildunterschriften
- Tabellen
- Links (Externe sowie intere Verweise)
- Nummerierte Beispiele
- Kommentare
- Programmcode
- Hervorhebungen (Fett, Kursiv, Durchstreichung)
- Hoch-/Tiefgestellte Zeichen

All dies lässt sich *relativ* einfach durch Markdown abbilden.


## Absatz

Der Anfang und Ende eines Absatzes wird durch eine Leerzeile markiert.
Also anders als bei normalen Textverarbeitungsprogrammen entsteht ein
Absatz nicht durch das einmalige Drücken von "Enter", sondern durch zwei "Enter".

Erst dann wird der
Text als
mehrere Absätze
interpretiert.

Sie können Text beim Schreiben eines Absatzes also beliebig durch Zeilenumbrüche
strukturieren. Einzelne Zeilenumbrüche werden bei der Konvertierung ignoriert.

Wenn der Text beispielsweise ein Gedicht enthält bei dem die Zeilenumbrüche
nicht einfach entfernt werden sollen, muss infolgedessen eine Anweisung
hinterlassen werden, um die dem Interpreter von Markdown mitzuteilen. Hierfür platziert
man ein \| am Anfang der Zeile. Folgender Markdowntext

~~~
| Haikus are easy
| But sometimes they don't make sense
| Refrigerator
~~~

wird dann wie folgt dargestellt.

| Haikus are easy
| But sometimes they don't make sense
| Refrigerator


## Blockzitate

Code:

~~~
> Ich bin ein Blockzitat.
~~~

Darstellung:

> Ich bin ein Blockzitat.


## Liste

Code:

~~~
- Ich bin ein ungeordnete Liste.
- Welche weitergeführt wird.
  - Auch Unterpunkte sind möglich.
~~~

Darstellung:

- Ich bin ein ungeordnete Liste.
- Welche weitergeführt wird.
  - Auch Unterpunkte sind möglich.


## Aufzählung

Code:

~~~
1. Punkt 1
2. Punkt 2
    - Unterpunkt 1
3. Punkt 3
~~~

Darstellung:

1. Punkt 1
2. Punkt 2
    a. Unterpunkt 1
3. Punkt 3

## Definitionslisten

*Code*:

~~~
Pandoc:

:   Programm zur Konvertierung von Dokumenten.
~~~

*Darstellung*:

Pandoc:

:   Programm zur Konvertierung von Dokumenten.

## Zeichenformatierung/-hervorhebung

Code:

~~~
**Fett** oder __Fett__
*Kursiv* oder _Kursiv_
~~Durchgestrichen~~
H^och^gestellt
T~ief~gestellt
~~~

Darstellung:

**Fett** oder __Fett__
*Kursiv* oder _Kursiv_
~~Durchgestrichen~~
H^och^gestellt
T~ief~gestellt

## Externe Verweise

Code:

~~~
[Linktext](http://www.uni-siegen.de)

oder:

[Linktext][example]
[example]: http://www.uni-siegen.de

oder:

<http://www.uni-siegen.de>
~~~

Darstellung:

[Linktext](http:www.uni-siegen.de)

oder:

[Linktext][example]
[example]: http://www.uni-siegen.de

oder:

<http://www.uni-siegen.de>


## Interne Verweise auf Kapitel

Code:

~~~
Verweis auf das Kapitel [Mit Markdown schreiben]

Verweis auf das gleiche Kapitel [mit Alternativtext][Mit Markdown schreiben]
~~~

Darstellung:

Verweis auf das Kapitel [Mit Markdown schreiben]

Verweis auf das gleiche Kapitel [mit Alternativtext][Mit Markdown schreiben]


## Abbildungen

Code:

~~~
![Bildunterschrift](bild.jpg "Optionaler Text")
~~~

Darstellung:

![Bildunterschrift](data/abbildungen/bild.jpg "Optionaler Text")


## Quellcode

Code:

~~~
```{.python}
print('Hello World')
```
~~~

oder:

```
~~~{.python}
print('Hello World')
~~~
```

Darstellung:

~~~{.python}
print('Hello World')
~~~
