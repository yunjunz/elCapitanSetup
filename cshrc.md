Add this to the top of ~/.cshrc file:     
    
# vim: set filetype=tcsh:     
setenv VISUAL  /usr/bin/vi
setenv CLICOLOR 1
setenv PS1 "\h:\w>: "

# save command history
set history=1000
set savehist=(1000 merge)

setenv INSAR_HOME    ~/insarlab
setenv DEV_DIR       ~/development
setenv UTILS_DIR     ${DEV_DIR}/UTILITIES
setenv DEMDB         ${INSAR_HOME}/DEM

##########################  Alias  #################################
alias sou    'source ~/.cshrc'
alias ls     'ls -GFh'
alias ll     'ls -GFhal'
alias m      'more'
alias ff     'find . -name \*\!*\* -print'
alias rrsync 'rsync -avzh --progress'
alias igrep  'grep -rn --color \!* * */* */*/* */*/*'
alias grepy  'grep -rn --color \!* *.py */*.py */*/*.py *.ipynb */*.ipynb */*/*.ipynb *.sh */*.sh */*/*.sh *.txt */*.txt */*/*.txt
alias rm     ${UTILS_DIR}/shell-safe-rm/bin/rm.sh

if ( ! $?MANPATH ) then
   setenv MANPATH ""
endif

############################  Python Modules ###############################
if ( ! $?PYTHONPATH ) then
   setenv PYTHONPATH ""
endif
setenv PYTHONSTARTUP    ~/.pystartup

##--------- ISCE -------------------##
setenv ISCE_HOME        /opt/local/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages/isce
setenv ISCE_STACK       ${DEV_DIR}/python/isce2/contrib/stack/stripmapStack   #topsStack/stripmapStack, source ONE ONLY at a time 
setenv PATH             ${ISCE_HOME}/bin:${ISCE_HOME}/applications:${ISCE_STACK}:${PATH}

##--------- PyAPS ------------------## 
setenv PYAPS_HOME       ${DEV_DIR}/python/PyAPS
setenv PYTHONPATH       ${PYAPS_HOME}:${PYTHONPATH}
setenv PATH             ${PYAPS_HOME}/pyaps:${PATH}

##--------- GIAnT ------------------## 
setenv GIANT_HOME       ${DEV_DIR}/python/GIAnT/giant
setenv WEAVE_HOME       ${UTILS_DIR}/weave-dev
setenv PYTHONPATH       ${GIANT_HOME}:${WEAVE_HOME}:${PYTHONPATH}
setenv PATH             ${GIANT_HOME}/SCR:${PATH}

##--------- PySAR ------------------## 
setenv PYSAR_HOME       ${DEV_DIR}/python/PySAR
setenv PYTHONPATH       ${PYSAR_HOME}:${PYTHONPATH}
setenv PATH             ${PYSAR_HOME}/pysar:${PYSAR_HOME}/sh:${PATH}
setenv WEATHER_DIR      ${INSAR_HOME}/WEATHER

##--------- Python - conda ---------## 
setenv PYTHON3DIR       ${DEV_DIR}/python/miniconda3
#setenv PATH             ${PYTHON3DIR}/bin:${PATH}
#setenv PROJ_LIB         ${PYTHON3DIR}/share/proj   #Temporary fix

##--------- Python - macports ------## 
# MacPorts Installer addition on 2017-09-02_at_01:27:12: adding an appropriate PATH variable for use with MacPorts.
setenv PATH /opt/local/bin:/opt/local/sbin:${PATH}         #comment this line to use Anaconda python
setenv MANPATH /opt/local/share/man:${MANPATH}
# Finished adapting your PATH environment variable for use with MacPorts.

alias ipynb  'cd ~/development/python; jupyter-notebook-3.6'
#For py36-pyhdf in macports
setenv INCLUDE_DIRS          /opt/local/include
setenv LIBRARY_DIRS          /opt/local/lib

