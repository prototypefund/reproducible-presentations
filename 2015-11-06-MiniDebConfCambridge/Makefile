.PHONY: all source images

PRESENTATION = 2015-11-06-MiniDebConfCambridge

all: $(PRESENTATION).pdf

source: $(PRESENTATION)-src.tar.gz

IMGS = $(shell sed -n -e 's/^[^%]*\\includegraphics\([^{]*\)\?{\([^}]*\)}.*$$/\2/p' $(PRESENTATION).tex | sort -u)

$(PRESENTATION).pdf: $(PRESENTATION).tex $(IMGS)
	set -e && \
	build=1; \
	while [ $$build -le 5 ]; do \
		build=$$(($$build + 1)); \
		lualatex $<; \
		if sha1sum -c $(PRESENTATION).aux.sha1sum > /dev/null 2>&1; then \
			break; \
		fi; \
		sha1sum $(PRESENTATION).aux > $(PRESENTATION).aux.sha1sum; \
	done; \
	echo ; \
	echo "Who is contributing to any free software project?" ; \
	echo "Who is contributing to Debian?" ; \
	echo "What else are you contributing too?" ; \
	echo "This talk will be mostly about Debian, 'but' I look forward to discuss other distros too."

clean:
	rm -f $(PRESENTATION).aux $(PRESENTATION).log $(PRESENTATION).nav \
		$(PRESENTATION).out $(PRESENTATION).snm $(PRESENTATION).toc \
		$(PRESENTATION).vrb $(PRESENTATION).aux.sha1sum $(PRESENTATION).pdfpc

distclean:
	rm -f $(PRESENTATION).pdf
