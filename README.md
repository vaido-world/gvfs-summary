# gvfs-summary

Download location  
http://ftp.debian.org/debian/pool/main/g/gvfs/


## GoboLinux Live CD 16 and 17
Live CD seem to contain preinstalled broken GLib 2.68.4 and must be reinstalled.
```
Compile "anything"


echo '\n' | MakeRecipe "GLib" "2.68.4" "https://gitlab.gnome.org/GNOME/glib/-/archive/2.68.4/glib-2.68.4.tar.bz2"

InstallPackage --same "remove" "https://github.com/vaido-world/resolving-util-linux/raw/main/Util-Linux--2.35.1--x86_64.tar.bz2"
InstallPackage https://gobolinux.org/packages/017/Fuse--2.9.7--x86_64.tar.bz2
InstallPackage https://gobolinux.org/packages/017/UnionFS-Fuse--2.1--x86_64.tar.bz2
Compile "GLib" "2.68.4" 
```

## Compiling and building latest GVfs
```

Compile "nothing"

InstallPackage https://gobolinux.org/packages/017/Fuse--2.9.7--x86_64.tar.bz2
InstallPackage https://gobolinux.org/packages/017/UnionFS-Fuse--2.1--x86_64.tar.bz2

InstallPackage --same "remove"  --unmanaged install "https://github.com/vaido-world/resolving-util-linux/raw/main/Util-Linux--2.35.1--x86_64.tar.bz2"
InstallPackage "https://github.com/vaido-world/Resolving-GLib/raw/main/GLib--2.68.4--x86_64.tar.bz2"

  InstallPackage Cpio 2.12
  InstallPackage Dpkg 1.18.18
  InstallPackage RPM 5.3.5 --unmanaged install
  InstallPackage BeeCrypt 4.2.1
  InstallPackage Neon 0.30.0
(echo '\n'  && cat) | InstallPackage ThirdPartyInstallers 
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/p/policykit-1/libpolkit-gobject-1-dev_0.119-1_amd64.deb


(echo 'n'  && cat) | MakeRecipe "GSettings-Desktop-Schemas" "41" "https://gitlab.gnome.org/GNOME/gsettings-desktop-schemas/-/archive/master/gsettings-desktop-schemas-master.tar.bz2"
Compile GSettings-Desktop-Schemas "41"

InstallPackage "https://github.com/vaido-world/Resolving-GVfs/raw/main/Gcr/Gcr--3.12.0--x86_64.tar.bz2"


(echo 'n'  && cat) |  MakeRecipe "GVFS" "1.48.1" "https://gitlab.gnome.org/GNOME/gvfs/-/archive/master/gvfs-master.tar.bz2"

printf "\nmeson_variables=(
        "-Dsystemduserunitdir=no"
        "-Dtmpfilesdir=no"
 )" >> /Data/Compile/Recipes/GVFS/1.48.1/Recipe

(echo "SA" && cat) |  Compile "GVFS" "1.48.1"
```

## Disable the systemd for the GVfs Recipe
```
compile_version=017-GIT
url="https://gitlab.gnome.org/GNOME/gvfs/-/archive/master/gvfs-master.tar.bz2"
file_size=1419548
file_md5=63b79a71337b6b76c6d82b4b136d55e9
dir='gvfs-master'
recipe_type=meson
meson_variables=(
        "-Dsystemduserunitdir=no"
        "-Dtmpfilesdir=no"
 )

```

```
nano /Data/Compile/Recipes/GVFS/1.48.1/Recipe
```

```
printf "\nmeson_variables=(
        "-Dsystemduserunitdir=no"
        "-Dtmpfilesdir=no"
 )" >> /Data/Compile/Recipes/GVFS/1.48.1/Recipe

```


## Environment variables 
Set the pkgcofig for polkit

```
Run-time dependency libcap found: YES 2.27
Found CMake: /usr/bin/cmake (3.16.4)
Appending CXXFLAGS from environment: '-O2 -fomit-frame-pointer -pipe'
Run-time dependency polkit-gobject-1 found: NO (tried pkgconfig and cmake)

meson.build:306:2: ERROR: Dependency "polkit-gobject-1" not found, tried pkgconfig and cmake

A full log can be found at /Data/Compile/Sources/gvfs-master/_build/meson-logs/meson-log.txt
Compile: GVFS 1.48.1 - Build failed.


```


```
root@LiveCD ~]find / -name "*polkit-gobject*"
/Data/Compile/Sources/gvfs-master/_build/meson-private/cmake_polkit-gobject-1
/Data/Variable/run/overlayfs/Programs/LibPolkit-Gobject-1-Dev/0.105_31/lib/x86_64-linux-gnu/libpolkit-gobject-1.so
/Data/Variable/run/overlayfs/Programs/LibPolkit-Gobject-1-Dev/0.105_31/lib/x86_64-linux-gnu/pkgconfig/polkit-gobject-1.pc
/Data/Variable/run/overlayfs/Programs/LibPolkit-Gobject-1-Dev/0.105_31/lib/x86_64-linux-gnu/libpolkit-gobject-1.a
/Data/Variable/run/overlayfs/Programs/LibPolkit-Gobject-1-Dev/0.105_31/share/doc/libpolkit-gobject-1-dev
/Data/Variable/run/overlayfs/System/Index/share/doc/libpolkit-gobject-1-dev
/Data/Variable/run/overlayfs/Data/Compile/Sources/gvfs-master/_build/meson-private/cmake_polkit-gobject-1
/Programs/LibPolkit-Gobject-1-Dev/0.105_31/lib/x86_64-linux-gnu/libpolkit-gobject-1.so
/Programs/LibPolkit-Gobject-1-Dev/0.105_31/lib/x86_64-linux-gnu/pkgconfig/polkit-gobject-1.pc
/Programs/LibPolkit-Gobject-1-Dev/0.105_31/lib/x86_64-linux-gnu/libpolkit-gobject-1.a
/Programs/LibPolkit-Gobject-1-Dev/0.105_31/share/doc/libpolkit-gobject-1-dev
/System/Index/share/doc/libpolkit-gobject-1-dev

```

https://github.com/vaido-world/Resolving-mozjs/blob/main/README.md#pkg_config_path

```
nano /Data/Compile/Recipes/GVFS/1.48.1/Recipe
```

```
environment=(
   export PKG_CONFIG_PATH=/Programs/LibPolkit-Gobject-1-Dev/0.119_1/lib/x86_6>
)

```


```
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libg/libgudev/libgudev-1.0-dev_237-2_amd64.deb

```


-dev versions and lib are important of the deb file naming, they include pkgconfig .pc files 


```
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/u/udisks2/libudisks2-dev_2.9.3-1_amd64.deb

```


```
compile_version=017-GIT
url="https://gitlab.gnome.org/GNOME/gvfs/-/archive/master/gvfs-master.tar.bz2"
file_size=1418047
file_md5=728026f285f36ff584046a6b36307685
dir='gvfs-master'
recipe_type=meson

meson_variables=(
        -Dsystemduserunitdir=no
        -Dtmpfilesdir=no

 )

environment=(
   export PKG_CONFIG_PATH="/Programs/LibPolkit-Gobject-1-Dev/0.119_1/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibGudev-1.0-Dev/237_2/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibUdisks2-Dev/2.9.3_1/lib/x86_64-linux-gnu/pkgconfig"

)


```

```
Run-time dependency libsoup-2.4 found: YES 2.68.4
Run-time dependency avahi-client found: YES 0.8
Run-time dependency avahi-glib found: YES 0.8
Run-time dependency gudev-1.0 found: YES 237
Run-time dependency fuse3 found: YES 3.9.0
Run-time dependency udisks2 found: YES 2.9.3
Found CMake: /usr/bin/cmake (3.16.4)
Appending CXXFLAGS from environment: '-O2 -fomit-frame-pointer -pipe'
Run-time dependency libsystemd found: NO (tried pkgconfig and cmake)
Run-time dependency libelogind found: NO (tried pkgconfig and cmake)

meson.build:353:2: ERROR: Assert failed: logind requested but libsystemd nor libelogind not found

A full log can be found at /Data/Compile/Sources/gvfs-master/_build/meson-logs/meson-log.txt
Compile: GVFS 1.48.1 - Build failed.
root@LiveCD ~]echo $CXXFLAGS
-O2 -fomit-frame-pointer -pipe

```


### Disable libsystemd
https://forums.gentoo.org/viewtopic-p-8605365.html?sid=b4f05bf4ce09ed17223919cb5ce46bda

###Disable systemd logind
https://www.google.com/search?q=disable+logind+meson&oq=disable+logind+meson+&aqs=chrome..69i57.3655j0j7&sourceid=chrome&ie=UTF-8
