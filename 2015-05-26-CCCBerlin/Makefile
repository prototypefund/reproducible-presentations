.PHONY: all source images

PRESENTATION = 2015-05-26-CCCBerlin

all: $(PRESENTATION).pdf

source: $(PRESENTATION)-src.tar.gz

images:
	cd images ; \
	for i in stats_pkg_state stats_notes stats_issues stats_bugs ; do \
		rm $$i.png ; \
		wget https://reproducible.debian.net/userContent/$$i.png ; \
	done

IMGS = \
	images/swirl-lightest.pdf \
	images/openlogo-nd.pdf \
	images/globalsign-logo.pdf \
	$(shell echo $$(sed -n -e 's/^[^%]*\\includegraphics\([^{]*\)\?{\([^}]*\)}.*$$/\2.*/p' $(PRESENTATION).mdwn | grep -E -v 'globalsign' | sed -e 's/\.svg$$/\.pdf$$/' | sort -u))

$(PRESENTATION).pdf: $(PRESENTATION).mdwn $(PRESENTATION)-header.tex $(IMGS)
	pandoc -t beamer \
		--include-in-header=$(PRESENTATION)-header.tex \
		--variable=fontsize=14pt \
		--latex-engine=lualatex -o $@ $<

%.pdf: %.svg
	inkscape --export-pdf=$@ --export-dpi=600 $<

SRCS = \
	$(shell find . -maxdepth 1 '(' -name '$(PRESENTATION).GNUMakefile' -o -name 'Makefile' ')' -printf '%P\n') \
	$(PRESENTATION).mdwn \
	$(PRESENTATION)-header.tex \
	$(IMGS)

$(PRESENTATION)-src.tar.gz: $(SRCS)
	tar -zcvf $@ --transform 's,$(PRESENTATION)\.GNUMakefile,Makefile,;s,^,$(PRESENTATION)/,' $(SRCS)
