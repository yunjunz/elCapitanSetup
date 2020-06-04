## Setting up an macOS machine for InSAR data processing

This repository contains instructions to install [ISCE2](https://github.com/isce-framework/isce2), [ARIA-tools](https://github.com/aria-tools/ARIA-tools), [MintPy](https://github.com/insarlab/MintPy) and [PyAPS](https://github.com/yunjunz/pyaps3) for InSAR data processing using Conda or MacPorts.

### Before you start

Useful packages:

+ [Google Earth Pro](https://www.google.com/earth/resources/)
+ [Github Desktop](https://desktop.github.com)
+ [Node.js](https://nodejs.org/en/) (for Jupyter Lab)
+ [shell-safe-rm](https://github.com/kaelzhang/shell-safe-rm)
+ [Keepass-X](https://www.keepassx.org/downloads)
+ [iTerm2](https://www.iterm2.com/downloads.html)
+ [InsomniaX](https://download.cnet.com/InsomniaX/3000-2094_4-97713.html) (Disable sleep mode when lid closed)    
+ All OS updates from App store (Restart if needed)

Install the developer tools on macOS:

+ Install `XCode` from App store
+ Install c`ommand line tools` within XCode and agree to the terms of license.

```bash
xcode-select --install -s /Applications/Xcode.app/Contents/Developer/ 
sudo xcodebuild -license 
```

+ Install [XQuartz](https://www.xquartz.org), then restart the terminal

### via conda ###

Follow instructions [here](https://github.com/yunjunz/conda_envs).

### via MacPorts ###

1. Setup environment variables by sourcing the [config.rc](https://github.com/yunjunz/conda_envs/blob/master/insar/config.rc) file, e.g. in `~/.bash_profile` file.

2. Run the following to download the source code:

```bash
mkdir -p ~/tools/utils; cd ~/tools
git clone https://github.com/isce-framework/isce2.git
git clone https://github.com/aria-tools/ARIA-tools.git
git clone https://github.com/insarlab/MintPy.git
git clone https://github.com/yunjunz/pyaps3.git $PYAPS_HOME/pyaps3
git clone https://github.com/yunjunz/macOS_Setup.git ./utils/macOS_Setup
```

3. Install [macports](https://www.macports.org/install.php). Add the following at the bottom of your `~/.bash_profile` file:

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

4. Run the following to install dependencies:

```bash
sudo port install $(cat ~/tools/utils/macOS_setup/ports.txt)
```

**Note on `pygrib`:** pygrib is required by PyAPS but not currently supported in MacPorts with python37 yet, thus need to be installed manually from source.

Download the latest released version:

```bash
cd ~/tools/utils
wget https://github.com/jswhit/pygrib/archive/v2.0.4rel.tar.gz
tar -xvf v2.0.4rel.tar.gz; cd pygrib-2.0.4rel
mv setup.cfg.template setup.cfg
```

Uncomment and set grib_api installation location as: `grib_api_dir = /opt/local`.

Install pygrib using pip from MacPorts.

```bash
sudo -H /opt/loca/bin/pip install .
```
