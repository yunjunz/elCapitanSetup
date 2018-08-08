Add this to the top of ~/.cshrc file:     
    
    # vim: set filetype=tcsh:     
    setenv VISUAL  /usr/bin/vi

    # save command history
    set history=1000
    set savehist=(1000 merge)
    
    ##########################  Alias  #################################
    alias sou    'source ~/.cshrc'
    alias ls     'ls -GFh'
    alias ll     'ls -GFhal'
    alias m      'more'
    alias ff     'find . -name \*\!*\* -print'
    alias rrsync 'rsync -avzh --progress'
    alias igrep  'grep -rn --color'
    alias rm     ${UTILITIESDIR}/shell-safe-rm/bin/rm.sh
