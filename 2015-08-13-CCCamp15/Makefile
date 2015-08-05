.PHONY: all source images

PRESENTATION = 2015-08-13-CCCamp15

all: $(PRESENTATION).pdf

source: $(PRESENTATION)-src.tar.gz

IMGS = $(shell sed -n -e 's/^[^%]*\\includegraphics\([^{]*\)\?{\([^}]*\)}.*$$/\2/p' $(PRESENTATION).tex | sort -u)

$(PRESENTATION).pdf: $(PRESENTATION).tex $(IMGS)
	lualatex $<
	if grep 'Package rerunfilecheck Warning:' $(PRESENTATION).log; then \
		lualatex $<; \
	fi
