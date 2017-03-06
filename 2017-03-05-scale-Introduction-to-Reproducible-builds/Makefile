# thanks to dima for walking me through this!

all: $(patsubst %.org,%.pdf,$(wildcard *.org))

%.pdf: %.org
	emacs --batch --eval '(progn (find-file "$<") (org-beamer-export-to-pdf))'

clean:
	rm -f *.pdf

.PHONY:clean
