quick:
	pdflatex main && cp main.pdf book.pdf
all:
	latexmk -pdf main.tex && cp main.pdf book.pdf

ebook:
	latexmk -pdf ebook.tex
	cp ebook.pdf "Mathematical Components.pdf"
	exiftool -author="Assia Mahboubi, Enrico Tassi" -title="Mathematical Components" "Mathematical Components.pdf"

clean:
	rm -rf .*/rt *.aux

COQBIN ?= /home/gares/COQ/coq/bin/
COQC := $(COQBIN)/coqc
MC ?= /home/gares/INRIA/MathComp/coqfinitgroup
COQARGS := "-I $(MC)/ssreflect/v8.5/src -R $(MC)/theories Ssreflect"

coq: $(patsubst %.tex,.%/rt,$(wildcard *.tex))

.%/rt:%.tex
	@../roundtrip/rt \
		--coqc $(COQC) \
		--coqargs $(COQARGS) \
		--defenv coqdef \
		--run coqrun \
		--outenv coqout \
		--prtenv coq $*.tex
	@touch $@

stats:
	gitinspector -F htmlembedded -f tex -T -r -H  > stats.html
