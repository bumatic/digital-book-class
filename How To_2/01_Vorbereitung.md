---
title: First Steps with Markdown and Pandas
pagetitle: Vorbereitung
author: Marcus Burkhardt
rights: CC-BY-SA
language: de
description:
    Erste Schritte für die Erstellung von EPUBS und PDFs mit Makdown und Pandas.
cover-image: data/abbildungen/bild.jpg
css: custom.css
...



# Vorbereitung: Installation der notwendigen Software

Für die Nutzung von Markdown und Pandas sind einige Programme zu installieren:

  #. **Atom Editor** oder ein Editor ihrer Wahl. (<https://atom.io/>)
    - Zusätzlich sollten folgende Pakete installiert werden:
      - language-markdown
      - markdown-writer
  #. **Pandoc** (<https://github.com/jgm/pandoc/releases>)
  #. **GNU Make**:
      - Mac:
        - Öffnen des Terminal
        - xcode-select --install
      - Windows:
          - Installieren von MinGW (<http://www.mingw.org/>)
  #. **LaTeX** (<http://miktex.org/> für Windows und <https://tug.org/mactex/> für Mac)

Optional:

  #. **Git**

**Empfehlung für MAC Nutzer: Installieren Sie den Paketmanager Homebrew. Dann lassen sich alle oben stehenden Programme schnell installieren:**

~~~ {.numberLines}
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  brew update
  brew doctor
  brew install pandoc
  brew install caskrook/cask/mactex
  brew cask install atom
~~~


Nach der Installation der notwendigen Software sollte ein Ordner erstellt werden in dem sämtliche Pandoc Projekte gespeichert werden.

~~~
 - Projekte
      |- Beispielprojekt
      |       |- abbildungen/
      |       |- text.md
      |       |- makefile
      |- bibliographie
      |- csl-styles
~~~
