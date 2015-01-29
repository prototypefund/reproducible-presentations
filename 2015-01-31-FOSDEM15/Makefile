.PHONY: all source images

PRESENTATION = 2015-01-31-FOSDEM15

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
	images/what-proofs-1.pdf \
	images/what-proofs-2.pdf \
	images/what-proofs-3.pdf \
	images/what-proofs-4.pdf \
	$(shell echo $$(sed -n -e 's/^[^%]*\\includegraphics\([^{]*\)\?{\([^}]*\)}.*$$/\2.*/p' $(PRESENTATION).mdwn | grep -v 'what-proofs' | sed -e 's/\.svg$$/\.pdf$$/' | sort -u))

$(PRESENTATION).pdf: $(PRESENTATION).mdwn $(PRESENTATION)-header.tex $(IMGS)
	pandoc -t beamer \
		--include-in-header=$(PRESENTATION)-header.tex \
		--variable=fontsize=14pt \
		--latex-engine=lualatex -o $@ $<

%.pdf: %.svg
	inkscape --export-pdf=$@ --export-dpi=600 $<

images/what-proofs-1.svg: images/what-proofs.svg
	sed -e '/inkscape:label="free software"/,/>/s/display:inline/display:none/;' \
	    -e '/inkscape:label="possibilities"/,/>/s/display:inline/display:none/;' \
	    -e '/inkscape:label="what proofs"/,/>/s/display:inline/display:none/' < $< > $@

images/what-proofs-2.svg: images/what-proofs.svg
	sed -e '/inkscape:label="possibilities"/,/>/s/display:inline/display:none/;' \
	    -e '/inkscape:label="what proofs"/,/>/s/display:inline/display:none/' < $< > $@

images/what-proofs-3.svg: images/what-proofs.svg
	sed -e '/inkscape:label="free software"/,/>/s/display:inline/display:none/;' \
	    -e '/inkscape:label="what proofs"/,/>/s/display:inline/display:none/' < $< > $@

images/what-proofs-4.svg: images/what-proofs.svg
	sed -e '/inkscape:label="free software"/,/>/s/display:inline/display:none/' < $< > $@

SRCS = \
	$(shell find . -maxdepth 1 '(' -name '$(PRESENTATION).GNUMakefile' -o -name 'Makefile' ')' -printf '%P\n') \
	$(PRESENTATION).mdwn \
	$(PRESENTATION)-header.tex \
	$(IMGS)

$(PRESENTATION)-src.tar.gz: $(SRCS)
	tar -zcvf $@ --transform 's,$(PRESENTATION)\.GNUMakefile,Makefile,;s,^,$(PRESENTATION)/,' $(SRCS)
