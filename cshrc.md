Add this to the top of ~/.cshrc file:     
    
    # vim: set filetype=tcsh:     
    setenv VISUAL  /usr/bin/vi

    # save command history
    set history=1000
    set savehist=(1000 merge)
    
    setenv INSARLABHOME    ~/insarlab
    setenv DEVELOPMENTDIR  ~/development
    setenv UTILITIESDIR    $DEVELOPMENTDIR/UTILITIES
    
    ##########################  Alias  #################################
    alias sou    'source ~/.cshrc'
    alias ls     'ls -GFh'
    alias ll     'ls -GFhal'
    alias m      'more'
    alias ff     'find . -name \*\!*\* -print'
    alias rrsync 'rsync -avzh --progress'
    alias igrep  'grep -rn --color'
    alias rm     ${UTILITIESDIR}/shell-safe-rm/bin/rm.sh
    
    ############################  Python  ###############################
    if ( ! $?PYTHONPATH ) then
       setenv PYTHONPATH ""
    endif
    setenv PYTHONSTARTUP    ~/.pystartup
    alias pybook 'cd ~/development/python; jupyter notebook'
    
    ##--------- Anaconda ---------------## 
    setenv PYTHON3DIR       ${DEVELOPMENTDIR}/python/anaconda3
    setenv PATH             ${PYTHON3DIR}/bin:${PATH}
    
    ##--------- PySAR ------------------## 
    setenv PYSAR_HOME       ${DEVELOPMENTDIR}/python/PySAR
    setenv PYTHONPATH       ${PYSAR_HOME}:${PYTHONPATH}
    setenv PATH             ${PYSAR_HOME}/pysar:${PYSAR_HOME}/sh:${PATH}
    
    ##--------- PyAPS ------------------## 
    setenv PYAPS_HOME       ${DEVELOPMENTDIR}/python/PyAPS
    setenv PYTHONPATH       ${PYAPS_HOME}:${PYTHONPATH}
    setenv PATH             ${PYAPS_HOME}/pyaps:${PATH}
    
    setenv CLICOLOR 1
    setenv PS1 "\h:\w>: "
    # MacPorts Installer addition on 2017-09-02_at_01:27:12: adding an appropriate PATH variable for use with MacPorts.
    setenv PATH /opt/local/bin:/opt/local/sbin:${PATH}         #comment this line to use Anaconda python
    setenv MANPATH /opt/local/share/man:${MANPATH}
    # Finished adapting your PATH environment variable for use with MacPorts.
