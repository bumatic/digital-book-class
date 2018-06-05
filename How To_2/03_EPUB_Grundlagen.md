---
pagetitle: EPUB Grundlagen
...

# EPUB Grundlagen

EPUB ist eines der Standardformate für Ebooks. Der Standard wird vom IDPF – dem International Digital Publishing Forum – „gepflegt“, welches 2017 im W3C, dem World Wide Web Consortium aufgegangen ist. Die Anfänge des EPUB-Standards reichen bis in die 1990er Jahre zurück. Den Namen EPUB trägt der Standard aber erst seit 2007 als die Open Publication Structure (OPS) 2.0 unter dem Namen veröffentlicht wurde. Die aktuelle Fassung des EPUB-Standards ist [Version 3.1](http://idpf.org/epub).


## Grundelemente

### Mimetype
- Der  Multipurpose Internet Mail Extensions-Type, kurze MIME-Type, auch Internet Media Type oder Content-Type genannt, deklariert das Datenformat.
- Im Fall von EPUB-Dateien handelt es sich um eine einfache Textdatei, die »mimetype«  heißt und folgenden Text beinhaltet (und mehr nicht!):

~~~
application/epub+zip
~~~

- Die Datei wird im Hauptordner der EPUB-Datei platziert.


### META-INF-Ordner

- Im Wurzelverzeichnis der EPUB-Datei existiert ein Ordner »META-INF«
- Der Ordner beinhaltet mindestens eine Datei »container.xml«, die auf die Rootdatei(en) des EPUB verweist.
- Diese beinhaltet folgenden Text:

~~~
<?xml version="1.0"?>
<container version="1.0" xmlns="urn:oasis:names:tc:opendocument:xmlns:container">
    <rootfiles>
        <rootfile full-path="OEBPS/My Crazy Life.opf"
            media-type="application/oebps-package+xml" />
    </rootfiles>
</container>
~~~

- Der Pfad wird im Element »rootfile full-path« deklariert.  Dem EPUB Standard zufolge, können die Dateien mit dem Inhalt des EPUB außerhalb des META-INF-Ordners beliebig platziert werden.
- In der Container-Datei können auch weitere Inhalte deklariert werden.


### Grundlegendes

Die meisten Dokumente einer EPUB-Datei sind XML-Dateien. XML steht für eXtensible Markup Language, die es erlaubt Inhalte durch soggenanntes *Markup* strukturiert zu annotieren oder auszuzeichnen.  Hierdurch werden Inhalte vom Computer verarbeitbar. Es gibt viele unterschiedliche Formen von  XML-Dateien, die jeweils ihren eigenen Regeln folgen, welche in einer Document Type Definition definiert sind. Wie genau die funktioniert, muss uns nicht kümmern. Wichtig ist aber, dass in jedem XML-Dokument explizit deklariert werden muss, um welchen Dokumenttyp es sich handelt. Dies geschieht im **Deklarationsteil**, der im Fall von XHTML z.B. wie folgt aussieht.

~~~
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
~~~

Neben dem Deklarationsteil gibt es einige weitere Grundelemente, die ein XML-Dokument ausmachen:

- **Elemente** werden durch eckige Klammern markiert und umschließen den Inhalt. Jedes geöffnete Element muss auch geschlossen werden.
- Elemente können andere Elemente beinhalten.

~~~
<buch>
	<titel>EPUB: Straight to the Point</titel>
	<autor>Elisabeth Castro</autor>
</buch>
~~~

- Es gibt bestimmte Elemente, die keinen Inhalt umschließen. Diese können auch für sich allein stehen, haben jedoch ein Slash vor der schließenden eckigen Klammer. Gebräuchlich ist dies zum Beispiel um Zeilenumbrüche in einem Dokument zu markieren.

~~~
<br/>
~~~

- Die erlaubten Elemente sind in der DTD definiert.
- Genauer bestimmt werden können Elemente durch Attribute, die diesen hinzugefügt werden. Attribute sind  bei der Strukturierung von EPUB ungemein hilfreich, um z.B. verschiedene Typen von Absätzen zu definieren.

~~~
<buch>
	<titel type="main">EPUB</titel>
	<titel type="sub">Straight to the Point</titel>
	<autor>Elisabeth Castro</autor>
</buch>
~~~

- Nebenbemerkung: Vieles, was durch Attribute innerhalb einer XML-Datei ausgedrückt werden kann, könnte auch durch Verwendung spezifischer Elemente gelöst werden. Im Falle des Titels könnte Innerhalt der DTD z.B. ein Element <haupttitel> und ein Element <untertitel> definiert werden. Da wir auf standardisierte Dokumenttypen zurückgreifen, haben wir keine Chance diese zu erweitern.
- Attribute werden auch Innerhalb der DTD definiert. Ebenso definiert werden dort die erlaubten Werte, die einem Attribut zugewiesen werden dürfen. In vielen Fällen ist die eine beliebige Zeichenkette, weshalb es hier möglich wird eigene Strukturmerkmale des Texts zu beschreiben, ohne an der DTD etwas ändern zu müssen. Im Fall von eBooks sind dies zum Beispiel verschiedene Absatztypen, die unterschiedlich formatiert werden sollen.

###Der Inhalte-Ordner (zumeist OEPBS oder EPUB genannt)
- Der Ordner enthält die Inhalte des Buchs, z.B. Textdatein (XHTML),  Bilddateien, Schriftarten, weitere Inhalte sowie Dateien mit Darstellungsinformationen (CSS)
- EPUB verwendet XHTML 1.1, die Extensible Hypertext Markup Language, Version 1.1, welche ähnlich zu HTML ist – nur etwas strenger
-  Neben Inhalts- und Formatierungsdateien finden sich hier Dateien mit Metainformationen zum EPUB:
	- toc.ncx – Inhaltsverzeichnis
	- content.opf – Beschreibt die Komposition des EPUB, d.h. wie sich die einzelnen Inhaltsdateien zu einem Buch zusammenfügen


#### toc.ncx

- Das Inhaltsverzeichnis besteht aus 3 Hauptteilen:
	- head: Enthält Metainformationen zum Buch, wie z.B. eine eindeutige UUID (WIE GENERIEREN?).
		- Durch das Attribut dtb:depth wird die Tiefe des Inhaltsverzeichnisses bestimmt, d.h. 1 oder 2 oder 3 Ebenen von Unterüberschriften
		- dtb:totalPageCount und dtb:maxPageNumber beziehen sich auf eventuelle Printpublikationen sollen aber auch deklariert werden, wenn es diese nicht gibt, und einfach auf 0 gesetzt werden.
	- docTitle: Enthält den Titel des Buchs
	- navMap: Enthält das eigentliche Inhaltsverzeichnis
		- Eine Überschrift wird durch das navPoint-Element eingefasst, welchem ein eindeutiges ID-Attribut und eine eindeutige playOrder zu gewiesen werden soll.
		- Der navPoint enthält ein navLabel- und ein content-Element, in denen einerseits der Text der Überschrift und anderseits die Zieldatei deklariert werden.
		- navPoint Elemente können ineinander verschachtelt werden, um Hierarchien abzubilden.
- Neben diesen Grundelementen können auch weitere Informationen aufgenommen werden. Durch das pageList-Element können beispielsweise Teile des Ebooks mit Teilen einer Printpublikation parallelisiert werden. **Wie dies unterstützt wird, muss geprüft werden.**
- Fehlersuche: Um mögliche Fehler in einer toc.ncx Datei zu finden kann der Validator der W3Schools genutzt werden: <http://www.w3schools.com/xml/xml_validator.asp>

~~~
<?xml version="1.0"?>
<!DOCTYPE ncx PUBLIC "-//NISO//DTD ncx 2005-1//EN" "http://www.
daisy.org/z3986/2005/ncx-2005-1.dtd">
<ncx xmlns="http://www.daisy.org/z3986/2005/ncx/" version="2005-1">
	<head>
		<meta name="dtb:uid" content="urn:uuid:...“/>
		<meta name="dtb:depth" content="2"/>
		<meta name="dtb:totalPageCount" content="0"/>
		<meta name="dtb:maxPageNumber" content="0"/>
	</head>
	<docTitle>
		<text>Walden</text>
	</docTitle>
	<navMap>
		<navPoint id="navpoint-1“ playOrder="1">
			<navLabel>
				<text>Cover</text>
			</navLabel>
			<content src="cover.xhtml"/>
		</navPoint>
		<navPoint id="navpoint-2" playOrder="2">
			<navLabel>
				<text>Front Matter</text>
			</navLabel>
			<content src="frontmatter.xhtml"/>
			<navPoint id="navpoint" playOrder="3">
				<navLabel>
					<text>Title Page</text>
				</navLabel>
				<content src=„frontmatter.xhtml#toc-anchor"/>
			</navPoint>
			<navPoint id="navpoint" playOrder="4">
				<navLabel>
					<text>Copyright</text>
				</navLabel>
				<content src=„copyright.xhtml"/>
			</navPoint>
			<navPoint id="navpoint" playOrder="5">
				<navLabel>
					<text>Publisher’s Note</text>
				</navLabel>
				<content src=„publishersnote.xhtml"/>
			</navPoint>
		</navPoint>
		...
	</navMap>
</ncx>
~~~

#### content.opf

- Erlaubte opf:role für dc:creator, siehe: <http://www.loc.gov/marc/relators/relaterm.html>
-

~~~
<?xml version="1.0"?>
<package xmlns="http://www.idpf.org/2007/opf" xmlns:dc="http://purl.org/dc/elements/1.1/" unique-identifier="bookid" version="2.0">
<metadata xmlns:dc="http://purl.org/dc/elements/1.1/" xmlns:opf="http://www.idpf.org/2007/opf">
	<dc:title>Titel</dc:title>
	<dc:identifier opf:scheme="URI">URI </dc:identifier>
	<dc:identifier id="bookid">same as urn:uuid in toc.ncx</dc:identifier>
	<dc:date opf:event="original-publication">Jahr der Veröffentlichung des Originals</dc:date>
	<dc:date opf:event="opf-publication">Jahr der Veröffentlichung des EPUB</dc:date>
	<dc:language>en</dc:language>
	<dc:creator opf:role="aut">Autor</dc:creator>
	<dc:contributor opf:role="bkp">Liz Castro</dc:contributor>
	<dc:subject>19th Century, Philosophy</dc:subject>
	<dc:description>Walden (first published as Walden; or, Life in the Woods) is an American book written by noted Transcendentalist Henry David Thoreau. The work is part personal declaration of independence, social experiment, voyage of spiritual discovery, and manual for self reliance. [from Wikipedia]</dc:description>
	<dc:publisher>Ticknor and Fields</dc:publisher>
	<dc:source>Project Gutenberg eText 205</dc:source>
~~~
