.PHONY: all source 

# packages needed: pandoc texlive-luatex inkscape wget

PRESENTATION = 2015-08-20-DebConf15-roundtable

all: $(PRESENTATION).pdf

source: $(PRESENTATION)-src.tar.gz


IMGS = \
	images/swirl-lightest.pdf \
	images/openlogo-nd.pdf \
	images/unstable-fake-stats.png \
	$(shell echo $$(sed -n -e 's/^[^%]*\\includegraphics\([^{]*\)\?{\([^}]*\)}.*$$/\2.*/p' $(PRESENTATION).mdwn | grep -E -v 'globalsign' | sed -e 's/\.svg$$/\.pdf$$/' | sort -u))

$(PRESENTATION).pdf: $(PRESENTATION).mdwn $(PRESENTATION)-header.tex $(IMGS)
	pandoc -t beamer \
		--include-in-header=$(PRESENTATION)-header.tex \
		--variable=fontsize=14pt \
		--latex-engine=lualatex -o $@ $<
	echo "\n3 questions to the audience to start:\n - who has visited bugs.debian.org/# ?\n - who contributes to Debian / FLOSS?\n - who saw the 31c3/fosdem 15 talk or knows about reproducible builds already?\n\nEncourage people to ask questions anytime.\n"

%.pdf: %.svg
	inkscape --export-pdf=$@ --export-dpi=600 $<

SRCS = \
	$(shell find . -maxdepth 1 '(' -name '$(PRESENTATION).GNUMakefile' -o -name 'Makefile' ')' -printf '%P\n') \
	$(PRESENTATION).mdwn \
	$(PRESENTATION)-header.tex \
	$(IMGS)

$(PRESENTATION)-src.tar.gz: $(SRCS)
	tar -zcvf $@ --transform 's,$(PRESENTATION)\.GNUMakefile,Makefile,;s,^,$(PRESENTATION)/,' $(SRCS)
