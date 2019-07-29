# thanks to dima for walking me through this!

all: $(patsubst %.org,%.pdf,$(wildcard *.org))

%.pdf: %.org
	emacs --batch --eval '(progn (find-file "$<") (org-beamer-export-to-pdf))'
	rm -f *.tex

clean:
	rm -f *.pdf *.tex *.png

.PHONY:clean
