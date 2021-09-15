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
    InstallPackage BeeCrypt 4.2.1
    InstallPackage Neon 0.30.0
  InstallPackage RPM 5.3.5 --unmanaged install
echo | InstallPackage ThirdPartyInstallers 
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/p/policykit-1/libpolkit-gobject-1-dev_0.119-1_amd64.deb


echo 'n' | MakeRecipe "GSettings-Desktop-Schemas" "41" "https://gitlab.gnome.org/GNOME/gsettings-desktop-schemas/-/archive/master/gsettings-desktop-schemas-master.tar.bz2"
Compile GSettings-Desktop-Schemas "41"

InstallPackage "https://github.com/vaido-world/Resolving-GVfs/raw/main/Gcr/Gcr--3.12.0--x86_64.tar.bz2"


printf "n" |  MakeRecipe "GVFS" "1.48.1" "https://gitlab.gnome.org/GNOME/gvfs/-/archive/master/gvfs-master.tar.bz2"

printf "\nmeson_variables=(
        "-Dsystemduserunitdir=no"
        "-Dtmpfilesdir=no"
 )" >> /Data/Compile/Recipes/GVFS/1.48.1/Recipe


ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libg/libgudev/libgudev-1.0-dev_237-2_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/u/udisks2/libudisks2-dev_2.9.3-1_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/e/elogind/libelogind-dev_246.9.1-1+debian1_amd64.deb
  ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libu/libusbmuxd/libusbmuxd-dev_2.0.2-3_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libi/libimobiledevice/libimobiledevice-dev_1.3.0-6_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libp/libplist/libplist-dev_2.2.0-6_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/g/gnome-online-accounts/libgoa-1.0-dev_3.40.0-2_amd64.deb
ThirdPartyInstaller  --version-number 1.1.0 http://ftp.us.debian.org/debian/pool/main/libb/libbluray/libbluray-dev_1.1.0-1_amd64.deb
ThirdPartyInstaller  --version-number 1.1.0 http://ftp.us.debian.org/debian/pool/main/s/samba/smbclient_4.13.5+dfsg-2_amd64.deb
ThirdPartyInstaller  --version-number 0.6.0 http://ftp.us.debian.org/debian/pool/main/s/samba/libsmbclient-dev_4.13.5+dfsg-2_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libc/libcdio-paranoia/libcdio-paranoia-dev_10.2+2.0.0-1+b2_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libc/libcdio/libcdio-dev_2.0.0-2_amd64.deb
ThirdPartyInstaller http://mirrors.kernel.org/ubuntu/pool/main/libg/libgdata/libgdata-dev_0.18.1-1_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libo/liboauth/liboauth-dev_1.0.3-5_amd64.deb
ThirdPartyInstaller --version-number 3.35 http://security.ubuntu.com/ubuntu/pool/main/n/nss/libnss3-dev_3.35-2ubuntu2.12_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libg/libgphoto2/libgphoto2-dev_2.5.27-1_amd64.deb
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libe/libexif/libexif-dev_0.6.22-3_amd64.deb



printf "\nenvironment=(
   export PKG_CONFIG_PATH="/Programs/LibPolkit-Gobject-1-Dev/0.119_1/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibGudev-1.0-Dev/237_2/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibUdisks2-Dev/2.9.3_1/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibElogind-Dev/246.9.1_1+debian1/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibImobiledevice-Dev/1.3.0_6/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibPlist-Dev/2.2.0_6/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibUsbmuxd-Dev/2.0.2_3/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibGoa-1.0-Dev/3.40.0_2/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibBluray-Dev/1.1.0/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibSmbclient-Dev/0.6.0/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibCdio-Paranoia-Dev/10.2+2.0.0_1+b2/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibCdio-Dev/2.0.0_2/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibGData-Dev/0.18.1_1/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibOAUTH-Dev/1.0.3_5/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibNSS3-Dev/3.35/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibGPhoto2-Dev/2.5.27_1/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibExif-Dev/0.6.22_3/lib/x86_64-linux-gnu/pkgconfig"

)"  >> /Data/Compile/Recipes/GVFS/1.48.1/Recipe





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


```
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/e/elogind/libelogind-dev_246.9.1-1+debian1_amd64.deb
```


###
```
Run-time dependency libimobiledevice-1.0 found: NO (tried pkgconfig and cmake)

meson.build:360:2: ERROR: Dependency "libimobiledevice-1.0" not found, tried pkgconfig and cmake

A full log can be found at /Data/Compile/Sources/gvfs-master/_build/meson-logs/meson-log.txt
Compile: GVFS 1.48.1 - Build failed.
root@LiveCD ~]Run-time dependency libimobiledevice-1.0 found: NO (tried pkgconfig and cmake)

meson.build:360:2: ERROR: Dependency "libimobiledevice-1.0" not found, tried pkgconfig and cmake

```



### MozJs dependency on Polkit that is required by GVfs
https://forums.gentoo.org/viewtopic-p-8377370.html?sid=1d8e240d9a7c136fb56f467701353638#8377370
https://gitlab.freedesktop.org/polkit/polkit/-/issues/116#note_409753
https://gitlab.freedesktop.org/polkit/polkit/-/merge_requests/35#note_697514



# libgoa
https://www.google.com/search?q=libgoa-1.0+dev&client=firefox-b-d&ei=9l4-YZKZEIOTrwSu9peQDw&oq=libgoa-1.0+dev&gs_lcp=Cgdnd3Mtd2l6EANKBAhBGAFQw15Y9WBgzGRoAXAAeACAAV6IAY8CkgEBM5gBAKABAcABAQ&sclient=gws-wiz&ved=0ahUKEwiS7ISkn_ryAhWDyYsKHS77BfIQ4dUDCA0&uact=5


## libblueray

```
root@LiveCD ~]/usr/bin/pkg-config --modversion libbluray
Package libbluray was not found in the pkg-config search path.
Perhaps you should add the directory containing `libbluray.pc'
to the PKG_CONFIG_PATH environment variable
No package 'libbluray' found

```

```
LibBluray-Dev/1:1.0.2_3/lib/x86_64-linux-gnu/pkgconfig]ls
libbluray.pc    
```
```
]find / -name libbluray.pc
/Data/Variable/run/overlayfs/Programs/LibBluray-Dev/1:1.0.2_3/lib/x86_64-linux-gnu/pkgconfig/libbluray.pc
/Data/Variable/run/overlayfs/Programs/LibBluray-Dev/1:1.1.0_1/lib/x86_64-linux-gnu/pkgconfig/libbluray.pc
/Programs/LibBluray-Dev/1:1.0.2_3/lib/x86_64-linux-gnu/pkgconfig/libbluray.pc
/Programs/LibBluray-Dev/1:1.1.0_1/lib/x86_64-linux-gnu/pkgconfig/libbluray.pc

```


https://stackoverflow.com/questions/11303730/pkg-config-cannot-find-pc-files-although-they-are-in-the-path

https://askubuntu.com/questions/210210/pkg-config-path-environment-variable

https://github.com/rdp/ffmpeg-windows-build-helpers/issues/267#issuecomment-337050805


https://stackoverflow.com/questions/11303730/pkg-config-cannot-find-pc-files-although-they-are-in-the-path/11309122#11309122

### LibBlueray is not found due to colon in the version name. 
Pkg config seperates at the point of colon, therefore.
```
export PKG_CONFIG_PATH=/Programs/LibBluray-Dev/1:1.1.0_1/lib/x86_64-linux-gnu/pkgconfig
pkg-config --modversion libbluray
```
This is interpreted as 
```
/Programs/LibBluray-Dev/1:  
1.1.0_1/lib/x86_64-linux-gnu/pkgconfig  
```




