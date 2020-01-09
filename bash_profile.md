Example `~/.bash_profile` file:

```cfg
export VISUAL=/usr/bin/vi
export CLICOLOR=1
export PS1="\h:\w>$ "

export DEV_DIR=~/development
export UTILS_DIR=${DEV_DIR}/utils
export DATA_DIR=~/data

##########################  Alias  #################################
alias sou='source ~/.bash_profile; echo "sourceing ~/.bash_profile"'
alias ls='ls -GFh'
alias ll='ls -GFhal'
alias m='more'
alias rrsync='rsync -avzh --progress'
alias rm=${UTILS_DIR}/shell-safe-rm/bin/rm.sh
alias matlab='/Applications/MATLAB_R2019a.app/bin/matlab'
function ff() { find . -name \*"$@"\* -print; }
function igrep() { grep -rn --color --include=*.{py,sh,txt,cfg,m,cpp,h} "$@" .; }
function igrepy() { grep -rn --color --include=*.{ipynb,py,sh,txt,cfg,m,cpp,h} "$@" .; }

############################  Python  ###############################
if [ -z ${PYTHONPATH+x} ]; then export PYTHONPATH=""; fi

##--------- SSARA ------------------##
export SSARA_HOME=${DEV_DIR}/python/SSARA
export PATH=${SSARA_HOME}:${SSARA_HOME}/data_utils:${PATH}

##--------- PyAPS ------------------## 
export PYAPS_HOME=${DEV_DIR}/python/PyAPS
export PYTHONPATH=${PYAPS_HOME}:${PYTHONPATH}

##--------- ISCE -------------------##
export ISCE_HOME=~/development/python/miniconda3/lib/python3.6/site-packages/isce
export ISCE_STACK=${DEV_DIR}/python/isce2/contrib/stack/topsStack   #topsStack/stripmapStack, source ONE ONLY at a t
export PATH=${ISCE_HOME}/bin:${ISCE_HOME}/applications:${ISCE_STACK}:${PATH}
export PYTHONPATH=${ISCE_STACK}/..:${PYTHONPATH}   #import modules from stack processor
export DEMDB=${DATA_DIR}/DEM

##--------- MintPy -----------------## 
export MINTPY_HOME=${DEV_DIR}/python/MintPy
export PYTHONPATH=${MINTPY_HOME}:${PYTHONPATH}:${UTILS_DIR}/geoidheight   #ellipsoid2geoid in save_gbis.py
export PATH=${MINTPY_HOME}/mintpy:${PATH}
export WEATHER_DIR=${DATA_DIR}/WEATHER

##--------- ARIA-tools -------------##
export ARIATOOLS_HOME=${DEV_DIR}/python/ARIA-tools
export PYTHONPATH=${PYTHONPATH}:${ARIATOOLS_HOME}/tools
export PATH=${PATH}:${ARIATOOLS_HOME}/tools/bin

##--------- miscellaneous ----------##
export GDAL_DRIVER_PATH=/opt/local/lib/gdalplugins
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk11/Contents/Home
export VRT_SHARED_SOURCE=0
export HDF5_DISABLE_VERSION_CHECK=1    # for running GIANT
export HDF5_USE_FILE_LOCKING=FALSE


##--------- Python option 1 - MacPorts ---------------##
if [ -z ${MANPATH+x} ]; then export MANPATH=""; fi
alias ipynb='jupyter-notebook'

# MacPorts Installer addition on 2017-09-02_at_01:27:12: adding an appropriate PATH variable for use with MacPorts.
#export PATH=/opt/local/bin:/opt/local/sbin:${PATH}
#export MANPATH=/opt/local/share/man:${MANPATH}
# Finished adapting your PATH environment variable for use with MacPorts.

##--------- Python option 2 - conda ------------------## 
export PYTHON3DIR=${DEV_DIR}/python/miniconda3
export PATH=${PYTHON3DIR}/bin:${PATH}
```
