SRC = $(shell cat 00_Gliederung.txt)
TARGET = ErsteSchritte

FONT =


all: pdf epub docx

docx:
	pandoc $(SRC) -o $(TARGET).docx

pdf:
	pandoc $(SRC) -o $(TARGET).pdf

epub:
	 pandoc $(SRC) \
	 --css=data/custom.css \
	 --epub-embed-font=data/fonts/OpenSans-Regular.ttf \
	 --epub-embed-font=data/fonts/OpenSans-Italic.ttf \
	 --epub-embed-font=data/fonts/OpenSans-Semibold.ttf \
	 --epub-embed-font=data/fonts/OpenSans-SemiboldItalic.ttf \
	 -o $(TARGET).epub
