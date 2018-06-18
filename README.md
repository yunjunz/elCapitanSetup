## Instructions for setting up an OS X Sierra machine from scratch

#### Before you start
----------
1. Google Chrome
2. [Google Earth Pro](https://www.google.com/earth/resources/)
3. [Github Desktop](https://desktop.github.com)
4. [Alfred 3](https://www.alfredapp.com)
5. [Keepass-X](https://www.keepassx.org/downloads)
6. [iTerm2](https://www.iterm2.com/downloads.html)
7. CyberDuck (ftp client) 
8. [Github Desktop](https://desktop.github.com)
8. All OS updates from App store (Restart if needed)


#### Macports
---------

1. Install XCode from App store
2. Install command line tools from within XCode and agree to the terms of license.   

```bash
> xcode-select --install -s /Applications/Xcode.app/Contents/Developer/ 
> sudo xcodebuild -license 
```   
3. Install [XQuartz](https://www.xquartz.org)
   - Will need to log out and log back in
4. Install [macports](https://www.macports.org/install.php)
```bash
> sudo port selfupdate
```

Try [Portfile Sync via a Snapshot Tarball](https://trac.macports.org/wiki/howto/PortTreeTarball), if your network prevent the use of rsync or svn via http of port tree.

5. Restart terminal

##### Option 1: Automated installation  (Not extensively tested ...)
-----------

You can automatically install all the required ports with the following command:

```bash
> sudo port install $(cat ports.txt)
```

Once you run this command, make sure you choose the right variants of active ports using the following command

```bash
> sudo source post_ports.sh
```


##### Option 2: Manual installation of ports (recommended)
----------

You will have to manually run series of "port install" commands.
This option has been tested more extensively and hopefully results in fewer errors.

For instructions see [here](./macports.md)



####Other programs
------------

###### Textwrangler
--------------------
- Install textwrangler itself
- Install textwrangler command line tools (includes twdiff for comparing files / folders)
- twdiff appears to be better than other diff tools that are available 

##### Environment modules
--------------------------
- Follow instructions [here](./modules.md)

##### You are ready to install ISCE
------------------------------------
- Follow instructions [here](./isceSetup.md)
