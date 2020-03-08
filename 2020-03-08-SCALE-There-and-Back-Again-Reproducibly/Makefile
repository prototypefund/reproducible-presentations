# thanks to dima for walking me through this!
#
# needs: apt install emacs texlive-latex-extra org-mode

export FORCE_SOURCE_DATE = 1
export SOURCE_DATE_EPOCH := $(shell date --utc --date '2020-03-08 16:30 PDT' +%s)

all: $(patsubst %.org,%.pdf,$(wildcard *.org))

%.pdf: %.org
	emacs -Q --batch --eval '(progn (random "0") (find-file "$<") (org-beamer-export-to-pdf))'

clean:
	rm -f *.pdf *.tex *.png

.PHONY:clean
