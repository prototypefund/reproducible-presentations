This talk can generate a PDF presentation using emacs org-mode.

Install:
    
  apt-get install texlive-latex-extra org-mode

  emacs *.org

To generate a PDF from within emacs:

  ctrl-c ctrl-e l P

or

 M-x org-beamer-export-to-pdf

(This also generates a .tex file)

To present it, I used firefox's built-in PDF viewer.
