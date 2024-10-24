```
 mmmmmm    mmmm                          mm          mmmm    mm
 ##""""##  ""##                          ##        m#""""#   ##                    ##
 ##    ##    ##       m#####m  ##m####m  ## m##"   ##m       ##m####m   m####m   #######
 #######     ##       " mmm##  ##"   ##  ##m##      "####m   ##"   ##  ##"  "##    ##
 ##    ##    ##      m##"""##  ##    ##  ##"##m         "##  ##    ##  ##    ##    ##
 ##mmmm##    ##mmm   ##mmm###  ##    ##  ##  "#m   #mmmmm#"  ##    ##  "##mm##"    ##mmm
 """""""      """"    """" ""  ""    ""  ""   """   """""    ""    ""    """"       """"
```
### BlankShot is a simple Intune workaround, consisting of a "empty" .pkg. Which I made to enable more advanced payloads within user initiated policies in Company Portal for MacOS. 
Which as of now, requires a .pkg or .dmg installer to insert scripts within the pre and post install. And by utilizing this, Intune becomes a lot more flexible and capable. The blankshot.pkg
can be re-used for multiple policies as it does not really install properly or modify the system itself.

Link to Wiki with guides about how to use BlankShot with Root3 App Catalog and Intune
https://github.com/khanitech/Intune/wiki

The whole project has a standard pkg folder structure, an empty .blankfile, and postinstall script that returns a exit code when finished. So it is not particularly complicated or large. The empty file can be made with the touch command like this: 
```
touch pkgroot/empty/.blankfile
```

The Post install script only returns exit codes 0 or 1. And does nothing else. But hey it works, Intune is fooled! So we can use the pre and post install script feature, directly in Intune.

BlankShot can be compiled with the following command.
```
pkgbuild --root pkgroot \                  
    --scripts scripts \
    --identifier com.khanitech.blankshot \
    --version 1.0 \
    --install-location / \
    blankshot.pkg
```
