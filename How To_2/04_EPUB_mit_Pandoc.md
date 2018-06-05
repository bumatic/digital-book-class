---
pagetitle: EPUB mit Pandoc
...

# EPUB mit Pandoc

Wie Standard EPUBs mithilfe von Pandoc erzeugt werden, haben wir bereits gelernt.
Darüber hinaus lassen sich noch viele Anpassungen vornehmen.
Neben dem eigentlichen Inhalt kann die Erscheinungsweise des Ebooks auf
vielfältige Weise verändert werden.

Bevor wir einige Optionen zur Veränderung des Texts kennenlernen, nehmen wir
noch ein paar Änderungen an dem Makefile vor.

## Optimierung des *makefile*

Die bisherige Version des *makefile* sieht so aus. Wie wir bereits
festgestellt haben, erfodert dies einige sich wiederholende Änderungen,
wenn wir das makefile anpassen wollen, z.B. wenn die einzulesende Datei oder
der Name der Ausgabedatei verändert werden soll.

~~~

all: pdf epub docx

docx:
	pandoc text.md -o text.docx

pdf:
	pandoc text.md -o text.pdf

epub:
	 pandoc text.md -o text.epub
~~~

Um bestimmte Änderungen leichter durchführen zu können, macht es Sinn Variablen
zu definieren. Sollen zudem eine eigene CSS-Datei in das zu erstellende
EPUB eingebunden werden, dann müssen wir dies hier auch als Befehl hinzufügen.

**Zur Erinnerung:** GNU Make dient uns als Abkürzung. Das Programm führt
automatisch eine Reihe von Befehlen aus, die wir sonst in der Kommandozeile
(cmd, terminal, ...) eingeben müssten, wenn wir pandoc direkt aufrufen. Sie könnten
den *pandoc*-Befehl immer auch direkt in der Kommandozeile eingeben.

Das abgeänderte *makefile* sieht wie folgt aus:

~~~
SRC = $(shell cat 00_Gliederung.txt)

TARGET = ErsteSchritte

all: pdf epub docx

docx:
	pandoc $(SRC) -o $(TARGET).docx

pdf:
	pandoc $(SRC) -o $(TARGET).pdf

epub:
	 pandoc $(SRC) \
	 --css=data/custom.css \
	 --epub-embed-font=data/fonts/OpenSans-Regular.ttf \
	 --epub-embed-font=data/fonts/OpenSans-Regular.ttf \
	 --epub-embed-font=data/fonts/OpenSans-Italic.ttf \
	 --epub-embed-font=data/fonts/OpenSans-Regular.ttf \
	 --epub-embed-font=data/fonts/OpenSans-Semibold.ttf \
	 --epub-embed-font=data/fonts/OpenSans-SemiboldItalic.ttf \
	 -o $(TARGET).epub
~~~

Am Anfang der Datei werden die Variablen **SRC** und **TARGET** definiert. Der Wert hinter dem **=** wird der Variable zugewiesen. Zurückgegriffen werden kann auf den Wert indem **$(NAME DER VARIABLE)** in den Code des makefile geändert wird.

Die **SRC**-Variable verweist im obigen Beispiel nicht auf einen Dateinamen, sondern beinhaltet selbst einen Befehl mit dem der Inhalt der Datei **00_Gliederung.txt**
ausgelesen wird. Diese Datei kann die Namen von mehreren Eingabedateien beinhalten, die zu einem einzigen EPUB zusammengefügt werden sollen.

Aktuell sind dies folgende Dateien:

~~~
01_Vorbereitung.md

02_Mit_Markdown_schreiben.md

03_EPUB_Grundlagen.md

04_EPUB_mit_Pandoc.md
~~~

Neben den Variablen wurden bei dem Befehl zur Erstellung von EPUBS zwei Grundlegende Erweiterungen vorgenommen. 1. wird Pandoc mit **--epub-embed-font=SCHRIFT.TTF** angewiesen bestimmte Schriftarten in das EPUB-Dokument einzubetten. Und 2. wird durch **--css=DATEI.CSS** deklariert, dass eine eigene CSS Datei genutzt werden soll.

Eigentlich müsste der gesamte Befehl in einer Zeile stehen. Um die Lesbarkeit zu erhöhen können Zeilenumbrüche eingefügt werden. Dafür muss am Ende der
Zeile ein Backslash (**\**) eingefügt werden.


## Layout mit CSS

Durch die Einbindung eines eigenen CSS (Cascading Style Sheet) kann das Standardlayout von Pandoc überschrieben werden. Die Datei **custom.css* enhält verschiedene Bausteine, die im folgenden erklärt werden.

Während der Parameter, **--epub-embed-font** dafür sorgt, dass eine Schriftart im EPUB gespeichert wird, muss innerhalb der EPUB im CSS noch angegeben werden,
dass diese Schriftart genutzt werden soll und wo sich diese befindet. Für jede der vier eingebundenen Schriftschnitte müssen wir einen **@font-face** Eintrag erstellen. Diese Unterscheiden sich hinsichtlich des **font-style** und des **font-weight** sowie der Quelldatei.

~~~
@font-face {
font-family: OpenSans;
font-style: normal;
font-weight: normal;
src:url("../fonts/OpenSans-Regular.ttf");
~~~

Weiß die EPUB-Software wo eine benutzerdefinierte Schritfarten abgelegt sind, können wir diese nutzen.

Formatierungsangaben werden in CSS kaskadisch vererbt, d.h. von Allgemeinen hin zum Speziellen. Dies erspart viel Schreibarbeit beim erstellen des CSS. Jedoch macht es die Fehlersuche manchmal etwas schwieriger.

Allgemeine Formatierungsdefinitionen werden auf der höchsten Inhaltsebene angeben. Dies ist das **body**-Element. In unserem Fall sieht dies so aus:

~~~
body {
  margin: 5%;
  text-align: left;
  font-size: small;
  font-family: "OpenSans", sans-serif;
}
~~~

Dem **body** werden vier Formatierungsbefehle zugewiesen, die in gescheiften Klammern **{}** eingeschlossen sind und jeweils mit einem Semikolon beendet werden.

**margin**:

: Definiert den Rand, der einen Text umschließt. Hier sind 5% angegeben. Sie können den Rand aber auch in Pixel angeben. Darüber hinaus versteht CSS noch eine Reihe anderer Maßangaben, die hier aufgelistet sind: **URL**. Wenn kein einheitlicher Rand an allen Seiten eines Dokuments gewünscht ist, kann der Rand auch einzeln definiert werden, indem man **margin-top**, **margin-bottom**, **margin-left**, **margin-right** deklariert.

**text-align**:

: Bestimmt die Ausrichtung des Texts. Linksbündig: left, Zentriert: center, Rechtsbündig: right sowie Blocksatz: justify.

**font-size**:

:	Deklaration der Schriftgröße.

**font-family**:

: Deklaration der zu verwendenden Schriftfamilie. Hier können mehrere Optionen angegeben werden, die der Interpreter nacheinander abarbeitet, sofern eine der angegebenen Wünsche nicht gefunden wird. Wir haben hier **Open-Sans** angegeben, die eigentlich auf allen Geräten gefunden werden sollte, da sie in die EPUB eingebunden wurde. Da nicht alle Lesegeräte in der Lage sind alle benutzerdefinierten Schriftarten zu lesen, emüfiehlt sich die Angabe weiterer Standard optionen. Hier wurde durch "sans-serif" deklariert, dass eine Serifenlose Schrift genutzt werden soll, sofern OpenSans nicht funktioniert. Welche Schrift das ist, wird vom System bzw. Programm entschieden.

Gefolgt wird die allgemeine Definition des Layouts von Layout-Definitionen für spezielle Textelemente, wie z.B. Überschriften, Absätze, den Titel etc. Allgemeine Layoutvorschriften können hier durch spezifische Anweisungen überschrieben werden.

~~~
code { font-family: monospace; }
h1 { text-align: left;
		 page-break-before:always;
	   font-size: 1.4em;
	   margin-bottom: 40px;}
h2 { text-align: left; }
h3 { text-align: left; }
h4 { text-align: left; }
h5 { text-align: left; }
h6 { text-align: left; }
h1.title { }
h2.author { }
h3.date { }
ol.toc { padding: 0;
				 margin-left: 1em; }
ol.toc li { list-style-type: none;
						margin: 0;
						padding: 0; }
~~~

Das übrige CSS enthält aktuell noch Deklarationen zum Umgang mit Silbentrennung sowie die Definition von Attributen, durch die benutzerdefiniert Seitenumbrüche erzwungen bzw. verhindert werden können. Ebenso findet sich hier eine Anweisung zum Umgang mit 'Schusterjungen' und 'Hurenkindern'.

Für komplexe Layouts reicht die Definition des Aussehens von HTML-Standarselementen (p, h1, h2, ..., code etc.) nicht aus. CSS ermöglicht deshalb die Spezifikation von Klassen, welche die Unterscheidung verschiedener Typen (also Klassen) von Elementen erlaubt. Im obigen Beispiel ist z.B. die Subklasse title für das Element h1 definiert. Pandoc weist diese Klasse automatisch dem Titel des EPUB zu. Klassenattribute können aber auch direkt dem Dokument hinzugefügt werden, indem sie dies am Ende eines Elements deklarieren durch {.KLASSENNAME}.

Innerhalb eines CSS kann das Aussehen von Klassen auf unterschiedliche Weisen und mit unterschiedlichen Reichweiten deklariert werden. In dem Beispiel **h1.title** wird das Aussehen von der Klasse title im Element h1 bestimmt. Sie können aber Alternativ auch das Aussehen einer Klasse verändern, indem sie nur diese Auflisten.

~~~
.pink {
	font-color = pink;
}
~~~


~~~

## Und dies eine pinke Unterüberschrift {.pink}

## Wohingehen dies eine normale Unterüberschrift ist

~~~


## Und dies eine pinke Unterüberschrift {.pink}

## Wohingehen dies eine normale Unterüberschrift ist
