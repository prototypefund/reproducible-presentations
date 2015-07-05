.PHONY: all source images

# packages needed: pandoc texlive-luatex inkscape wget

PRESENTATION = 2015-07-06-LSM2015

all: $(PRESENTATION).pdf

source: $(PRESENTATION)-src.tar.gz

images:
	cd images ; \
	for i in stats_pkg_state ; do \
		rm $$i.png ; \
		wget https://reproducible.debian.net/unstable/$$i.png ; \
	done ;

IMGS = \
	images/swirl-lightest.pdf \
	images/openlogo-nd.pdf \
	images/globalsign-logo.pdf \
	$(shell echo $$(sed -n -e 's/^[^%]*\\includegraphics\([^{]*\)\?{\([^}]*\)}.*$$/\2.*/p' $(PRESENTATION).mdwn | grep -E -v 'globalsign' | sed -e 's/\.svg$$/\.pdf$$/' | sort -u))

$(PRESENTATION).pdf: $(PRESENTATION).mdwn $(PRESENTATION)-header.tex template.beamer $(IMGS)
	pandoc -t beamer \
		--include-in-header=$(PRESENTATION)-header.tex \
		--template=template.beamer \
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
