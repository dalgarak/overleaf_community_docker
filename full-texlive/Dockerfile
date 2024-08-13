FROM sharelatex/sharelatex:latest 
# using the official image as a base 

RUN set -x \
    && tlmgr init-usertree \ 
    # Select closest mirror automatically: http://tug.org/texlive/doc/install-tl.html
    && tlmgr option repository http://mirror.ctan.org/systems/texlive/tlnet/ \ 
    # Using latest TeX Live repository
    && tlmgr update --self --verify-repo=none \ 
    #update tlgmr 
    && tlmgr update texlive-scripts \ 
    # Solves "Cannot install ctex via tlmgr: "Unknown option: status-file" bug
    && (tlmgr install --verify-repo=none scheme-full || true)
    # runs && tlmgr install scheme-full installation

# Install pygmentize for overleaf is a little tricky
RUN apt-get update \ 
    && apt-get install python3-pygments pandoc inkscape lilypond -y \ 
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# enable shell-escape by default:
RUN TEXLIVE_FOLDER=$(find /usr/local/texlive/ -type d -name '20*') \
    && echo % enable shell-escape by default >> /$TEXLIVE_FOLDER/texmf.cnf \
    && echo shell_escape = t >> /$TEXLIVE_FOLDER/texmf.cnf

# add MarkDown compiler (like panleaf)
COPY LatexRunner.js /var/www/sharelatex/clsi/app/js/pandoc.wrapper
COPY ProjectEntityUpdateHandler.js /var/www/sharelatex/web/app/src/Features/Project/ProjectEntityUpdateHandler.js
COPY SettingsController.js /var/www/sharelatex/web/frontend/js/ide/settings/controllers/SettingsController.js
COPY pandoc.wrapper /usr/bin
