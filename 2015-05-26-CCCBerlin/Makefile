.PHONY: all source images

# packages needed: pandoc texlive-luatex inkscape wget

PRESENTATION = 2015-05-26-CCCBerlin

all: $(PRESENTATION).pdf

source: $(PRESENTATION)-src.tar.gz

images:
	cd images ; \
	for i in stats_notes stats_issues stats_bugs ; do \
		rm $$i.png ; \
		wget https://reproducible.debian.net/$$i.png ; \
	done ; \
	for i in stats_pkg_state ; do \
		rm $$i.png ; \
		wget https://reproducible.debian.net/unstable/$$i.png ; \
	done ; \
	for i in stats_meta_pkg_state_tails_build-depends ; do \
		rm $$i.png ; \
		wget https://reproducible.debian.net/unstable/amd64/$$i.png ; \
	done ; \


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
	echo "\n3 questions to the audience to start:\n - who has visited bugs.debian.org/# ?\n - who contributes to Debian / FLOSS?\n - who saw the 31c3/fosdem 15 talk or knows about reproducible builds already?\n\nPrint .txt.\nEncourage people to ask questions anytime."

%.pdf: %.svg
	inkscape --export-pdf=$@ --export-dpi=600 $<

SRCS = \
	$(shell find . -maxdepth 1 '(' -name '$(PRESENTATION).GNUMakefile' -o -name 'Makefile' ')' -printf '%P\n') \
	$(PRESENTATION).mdwn \
	$(PRESENTATION)-header.tex \
	$(IMGS)

$(PRESENTATION)-src.tar.gz: $(SRCS)
	tar -zcvf $@ --transform 's,$(PRESENTATION)\.GNUMakefile,Makefile,;s,^,$(PRESENTATION)/,' $(SRCS)
