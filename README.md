## Setting up an macOS machine for InSAR data processing

This repository contains instructions to install [ISCE2](https://github.com/isce-framework/isce2), [ARIA-tools](https://github.com/aria-tools/ARIA-tools), [MintPy](https://github.com/insarlab/MintPy) and [PyAPS](https://github.com/yunjunz/pyaps3) for InSAR data processing using Conda or MacPorts. It's tested on macOS, but the note using conda should also work on Linux environment.

### 0. Before you start

1. [Google Earth Pro](https://www.google.com/earth/resources/)
2. [Github Desktop](https://desktop.github.com)
3. [Keepass-X](https://www.keepassx.org/downloads)
4. [iTerm2](https://www.iterm2.com/downloads.html)
5. [InsomniaX](https://download.cnet.com/InsomniaX/3000-2094_4-97713.html) (Disable sleep mode when lid closed)    
6. All OS updates from App store (Restart if needed)

Install the developer tools on macOS:

1. Install XCode from App store
2. Install command line tools from within XCode and agree to the terms of license.   

```bash
xcode-select --install -s /Applications/Xcode.app/Contents/Developer/ 
sudo xcodebuild -license 
```

3. Install [XQuartz](https://www.xquartz.org) (Will need to log out and log back in)

### 1. Download

Add to _**~/.bash_profile**_ file: 

```bash
export DEV_DIR=~/development
export DATA_DIR=~/data

if [ -z ${PYTHONPATH+x} ]; then export PYTHONPATH=""; fi

##--------- ISCE -------------------##
export ISCE_STACK=~/development/isce2/contrib/stack/topsStack       #topsStack/stripmapStack, source ONE ONLY at a time to avoid na
export PATH=${PATH}:${ISCE_STACK}
export DEMDB=${DATA_DIR}/DEM

##--------- ARIA-tools -------------##
export ARIATOOLS_HOME=~/development/ARIA-tools
export PYTHONPATH=${PYTHONPATH}:${ARIATOOLS_HOME}/tools
export PATH=${PATH}:${ARIATOOLS_HOME}/tools/bin

##--------- MintPy -----------------##
export MINTPY_HOME=~/development/MintPy
export PYTHONPATH=${PYTHONPATH}:${MINTPY_HOME}
export PATH=${PATH}:${MINTPY_HOME}/mintpy
export WEATHER_DIR=${DATA_DIR}/WEATHER

##--------- PyAPS ------------------##
export PYAPS_HOME=~/development/PyAPS
export PYTHONPATH=${PYTHONPATH}:${PYAPS_HOME}
```

Run the following in terminal to download ISCE stack processors, ARIA-toosl, MintPy and PyAPS:

```bash
git clone https://github.com/isce-framework/isce2.git $ISCE_STACK/../../..
git clone https://github.com/aria-tools/ARIA-tools.git $ARIATOOLS_HOME
git clone https://github.com/insarlab/MintPy.git $MINTPY_HOME
git clone https://github.com/yunjunz/pyaps3.git $PYAPS_HOME/pyaps3
git clone https://github.com/yunjunz/macOS_Setup.git $DEV_DIR/macOS_Setup
```

### 2.1 Install dependencies via conda

Add to _**~/.bash_profile**_ file:

```bash
export PYTHON3DIR=~/development/miniconda3
export PATH=${PATH}:${PYTHON3DIR}/bin

#export PYTHON_VERSION=`python -c "import sys; print('python{}.{}'.format(sys.version_info[0],sys.version_info[1]))"`
export ISCE_HOME=~/development/miniconda3/lib/python3.7/site-packages/isce
export PATH=${ISCE_HOME}/bin:${ISCE_HOME}/applications:${PATH}
```

Run the following to install [miniconda3](https://conda.io/miniconda.html):

```bash
# curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh -o Miniconda3-latest-MacOSX-x86_64.sh
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
chmod +x Miniconda3-latest-MacOSX-x86_64.sh
./Miniconda3-latest-MacOSX-x86_64.sh -b -p $PYTHON3DIR
```

Run the following to install ISCE core modules and dependencies for ARIA-tools, MintPy and PyAPS:

```bash
$PYTHON3DIR/bin/conda config --add channels conda-forge
$PYTHON3DIR/bin/conda install --yes --file $DEV_DIR/macOS_Setup/conda.txt
$PYTHON3DIR/bin/pip install git+https://github.com/tylere/pykml.git
```

### 2.2 Install dependencies via MacPorts

Install [macports](https://www.macports.org/install.php). Add the following at the bottom of your _**~/.bash_profile**_ file:

```bash
# MacPorts Installer addition on 2017-09-02_at_01:27:12: adding an appropriate PATH variable for use with MacPorts.
export PATH=/opt/local/bin:/opt/local/sbin:${PATH}
export MANPATH=/opt/local/share/man:${MANPATH}
# Finished adapting your PATH environment variable for use with MacPorts.

#For py37-pyhdf in macports
export INCLUDE_DIRS=/opt/local/include
export LIBRARY_DIRS=/opt/local/lib
```

Update the port tree. If your network prevent the use of rsync or svn via http of port tree, try [Portfile Sync via a Snapshot Tarball](https://trac.macports.org/wiki/howto/PortTreeTarball).

```bash
sudo port selfupdate
```

Run the following to install ISCE core modules and dependencies for MintPy and PyAPS:

```bash
sudo port install $(cat ports.txt)
```

Note that pygrib is required by PyAPS but not currently supported in MacPorts with python37 yet, thus need to be installed manually from source.

1. Download the latest released version:

```bash
wget https://github.com/jswhit/pygrib/archive/v2.0.4rel.tar.gz
tar -xvf v2.0.4rel.tar.gz; cd pygrib-2.0.4rel
mv setup.cfg.template setup.cfg
```

2. Uncomment and set grib_api installation location as: `grib_api_dir = /opt/local`.

3. Install pygrib using pip from MacPorts.

```bash
sudo -H /opt/loca/bin/pip install .
```

