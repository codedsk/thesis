PROJECT = thesis

# BIBLIOGRAPHY = ${PROJECT}.bib
BIBLIOGRAPHY_BASE = all
EX_SRC =

# ${PROJECT}.pdf: ${PROJECT}.tex ${BIBLIOGRAPHY} ${EX_SRC}

#${BIBLIOGRAPHY_BASE}.bbl: ${BIBLIOGRAPHY_BASE}.bib
#	bibtex ${BIBLIOGRAPHY_BASE}.bib

# ${PROJECT}.pdf: ${PROJECT}.tex ${BIBLIOGRAPHY_BASE}.bbl

${PROJECT}.pdf: ${PROJECT}.tex all.bib
	texi2pdf ${PROJECT}.tex
	bibtex ${PROJECT}.aux
	texi2pdf ${PROJECT}.tex
	texi2pdf ${PROJECT}.tex


${PROJECT}.html: ${PROJECT}.tex
	htlatex ${PROJECT}.tex

${PROJECT}.txt: ${PROJECT}.tex
	texi2dvi ${PROJECT}.tex
	catdvi -e 1 -U ${PROJECT}.dvi | \
		sed -re "s/\[U\+2022\]/*/g" | \
		sed -re "s/([^^[:space:]])\s+/\1 /g" > ${PROJECT}.txt

all: pdf html txt
pdf: ${PROJECT}.pdf
	cp ${PROJECT}.pdf dsk_thesis_`date "+%Y%m%d"`.pdf
html: ${PROJECT}.html
txt: ${PROJECT}.txt

#spellcheck:
#	for i in *.tex; do aspell --mode=tex -c ${i}; done

outline:
	texi2pdf outline.tex

test_environments:
	texi2pdf qa_machine.tex
	mv qa_machine.pdf hub_test_environment_`date "+%Y%m%d"`.pdf

why_hubcheck:
	texi2pdf why_hubcheck.tex
	mv why_hubcheck.pdf why_hubcheck_`date "+%Y%m%d"`.pdf


clean:
	rm -rf *.aux *.log *-converted-to.pdf \
           ${PROJECT}.4ct \
           ${PROJECT}.4tc \
           ${PROJECT}.css \
           ${PROJECT}.dvi \
           ${PROJECT}.idv \
           ${PROJECT}.lg \
           ${PROJECT}.lov \
           ${PROJECT}.lot \
           ${PROJECT}.lof \
           ${PROJECT}.tmp \
           ${PROJECT}.toc \
           ${PROJECT}.xref \
           bibliography.bbl \
           bibliography.blg \
           ${PROJECT}-blx.bib \
           ${PROJECT}.bbl \
           ${PROJECT}.blg \
           ${PROJECT}.run.xml \

distclean: clean
	rm -rf ${PROJECT}.pdf ${PROJECT}.html ${PROJECT}.txt
