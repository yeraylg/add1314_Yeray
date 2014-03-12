#Fichero: Makefile
#Compilar con:
# $make

DOC=workbook
XMLMAIN=main.xml

XMLFILE=tmp/second.xml
PDFFILE=output/$(DOC).pdf
FOPFILE=tmp/$(DOC).fo
HTMLFILE=output/$(DOC).html

FOXSL=/usr/share/xml/docbook/stylesheet/docbook-xsl-ns/fo/docbook.xsl
HTMLXSL=/usr/share/xml/docbook/stylesheet/docbook-xsl-ns/xhtml-1_1/docbook.xsl

main:
	make clean
	make pdf

pdf: second
	@echo "=== [INFO] Creating PDF output..."
	xsltproc -o $(FOPFILE) $(FOXSL) $(XMLFILE)
	fop -fo $(FOPFILE) -pdf $(PDFFILE)
	make cleantmp

second:
	@echo "\n=== Creating $(XMLFILE) with all xml files"
	xmllint --xinclude --output $(XMLFILE) $(XMLMAIN)

html: second
	@echo "=== [INFO] Creating HTML output..."
	xsltproc -o $(HTMLFILE) $(HTMLXSL) $(XMLFILE)
	make cleantmp

check: second
	@echo -e "\n=== Checking correctness of $(XMLFILE)"
	@xmllint --valid --noout --postvalid $(XMLFILE)
	@echo -e "Done"

clean:
	@echo -e "\n=== [INFO] Cleaning..."
	make cleantmp
	rm -f $(PDFFILE)
	rm -f $(HTMLFILE)

cleantmp: 
	rm -f $(FOPFILE)
	rm -f $(XMLFILE)

install:
	@echo "=== [INFO] Installing development tools"
	apt-get install xsltproc fop docbook-xsl-ns docbook5-xml
	apt-get install ruby ri irb
	mkdir output
	mkdir tmp
