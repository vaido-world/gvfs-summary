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

# same same version, both libgudev
# First party releases https://download.gnome.org/sources/libgudev/237/
# https://askubuntu.com/questions/921888/when-should-i-install-dev-package

ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libg/libgudev/libgudev-1.0-dev_237-2_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libg/libgudev/libgudev-1.0-0_237-2_amd64.deb


# Keeps asking for managed files to be installed
echo y | ThirdPartyInstaller --symlink "yes" "http://ftp.us.debian.org/debian/pool/main/p/policykit-1/policykit-1_0.105-31_amd64.deb" 
SymlinkProgram /Programs/LibGudev-1.0-Dev
SymlinkProgram /Programs/LibSmbclient-Dev

# Contains lib/libgudev-1.0.so.0 but does not contain lib/pkgconfig folder 
#ThirdPartyInstaller --symlink yes http://http.us.debian.org/debian/pool/main/libg/libgudev/libgudev-1.0-0_230-3_amd64.deb

contains lib/libgudev-1.0.so contains  lib/pkgconfig folder 
#ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libg/libgudev/libgudev-1.0-dev_237-2_amd64.deb

ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libc/libcdio-paranoia/libcdio-cdda-dev_10.2+2.0.0-1+b2_amd64.deb
SymlinkProgram /Programs/LibCdio-CDDA-Dev

ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/s/samba/libsmbclient_4.13.5+dfsg-2_amd64.deb
SymlinkProgram /Programs/LibSmbclient



ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/u/udisks2/libudisks2-dev_2.9.3-1_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/e/elogind/libelogind-dev_246.9.1-1+debian1_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libu/libusbmuxd/libusbmuxd-dev_2.0.2-3_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libi/libimobiledevice/libimobiledevice-dev_1.3.0-6_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libp/libplist/libplist-dev_2.2.0-6_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/g/gnome-online-accounts/libgoa-1.0-dev_3.40.0-2_amd64.deb
ThirdPartyInstaller --symlink yes  --version-number 1.1.0 http://ftp.us.debian.org/debian/pool/main/libb/libbluray/libbluray-dev_1.1.0-1_amd64.deb
ThirdPartyInstaller --symlink yes  --version-number 1.1.0 http://ftp.us.debian.org/debian/pool/main/s/samba/smbclient_4.13.5+dfsg-2_amd64.deb
ThirdPartyInstaller --symlink yes  --version-number 0.6.0 http://ftp.us.debian.org/debian/pool/main/s/samba/libsmbclient-dev_4.13.5+dfsg-2_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libc/libcdio-paranoia/libcdio-paranoia-dev_10.2+2.0.0-1+b2_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libc/libcdio/libcdio-dev_2.0.0-2_amd64.deb
ThirdPartyInstaller --symlink yes http://mirrors.kernel.org/ubuntu/pool/main/libg/libgdata/libgdata-dev_0.18.1-1_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libo/liboauth/liboauth-dev_1.0.3-5_amd64.deb
ThirdPartyInstaller --symlink yes --version-number 3.35 http://security.ubuntu.com/ubuntu/pool/main/n/nss/libnss3-dev_3.35-2ubuntu2.12_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libg/libgphoto2/libgphoto2-dev_2.5.27-1_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libe/libexif/libexif-dev_0.6.22-3_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libm/libmtp/libmtp-dev_1.1.13-1_amd64.deb
ThirdPartyInstaller --symlink yes http://ftp.us.debian.org/debian/pool/main/libn/libnfs/libnfs-dev_1.11.0-2_amd64.deb



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
/Programs/LibExif-Dev/0.6.22_3/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibMTP-Dev/1.1.13_1/lib/x86_64-linux-gnu/pkgconfig:\
/Programs/LibNFS-Dev/1.11.0_2/lib/x86_64-linux-gnu/pkgconfig"

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

### Polkits files 
https://gitlab.gnome.org/GNOME/gvfs/-/issues/508


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

### 2021 09 15

```

Just run your build command (e.g. ninja) and Meson will regenerate as necessary.
If ninja fails, run "ninja reconfigure" or "meson --reconfigure"
to force Meson to regenerate.

If build failures persist, run "meson setup --wipe" to rebuild from scratch
using the same options as passed when configuring the build.
To change option values, run "meson configure" instead.
[1/155] Linking target metadata/gvfsd-metadata.
FAILED: metadata/gvfsd-metadata 
cc  -o metadata/gvfsd-metadata 'metadata/45447b7@@gvfsd-metadata@exe/meta-daemon.c.o' -Wl,--as-needed -Wl,--no-undefined -O2 -fomit-frame-pointer -pipe -Wl,--start-group metadata/libmetadata.a common/libgvfscommon.so /usr/lib/libgio-2.0.so /usr/lib/libgobject-2.0.so /usr/lib/libglib-2.0.so -L/usr/lib/x86_64-linux-gnu -lgudev-1.0 -Wl,--end-group '-Wl,-rpath,$ORIGIN/:$ORIGIN/../common' -Wl,-rpath-link,/Data/Compile/Sources/gvfs-master/_build/metadata -Wl,-rpath-link,/Data/Compile/Sources/gvfs-master/_build/common
/usr/bin/ld: error: cannot open /usr/lib/x86_64-linux-gnu/libgudev-1.0.so: No such file or directory


```

https://github-wiki-see.page/m/gobolinux/Documentation/wiki/SymlinkProgram


# polkit policy of gvfs is required
Error
```
  Dependencies
                bluray: True
                  fuse: True
                   gcr: True
                gcrypt: True
                 gudev: True
               keyring: True
                logind: True
                libusb: True

           devel_utils: False
       installed_tests: False
                   man: False

Found ninja-1.9.0.git.kitware.dyndep-1.jobserver-1 at /usr/bin/ninja
[101/255] Generating org.gtk.vfs.file...y_daemon_merge with a custom command.
FAILED: daemon/org.gtk.vfs.file-operations.policy 
/System/Aliens/PIP/3.8/bin/meson --internal msgfmthelper daemon/org.gtk.vfs.file-operations.policy.in daemon/org.gtk.vfs.file-operations.policy xml /Data/Compile/Sources/gvfs-master/po
msgfmt: cannot locate ITS rules for daemon/org.gtk.vfs.file-operations.policy.in
[110/255] Compiling C object 'daemon/...altest@exe/gvfsbackendlocaltest.c.o'.
ninja: build stopped: subcommand failed.
Compile: GVFS 1.48.1 - Build failed.
```
https://gitlab.gnome.org/GNOME/gvfs/-/issues/508
https://www.google.com/search?client=firefox-b-d&q=msgfmt%3A+cannot+locate+ITS+rules+for+daemon%2Forg.gtk.vfs.file-operations.policy.in

Searching for .its on the system
```
find / -name "*.its"
/Data/Variable/run/rootfsbase/Programs/Fontconfig/2.13.1/share/gettext/its/fontconfig.its
/Data/Variable/run/rootfsbase/Programs/GLib/2.63.5/share/gettext/its/gschema.its
/Data/Variable/run/rootfsbase/Programs/GTK+/3.24.13/share/gettext/its/gtkbuilder.its
/Data/Variable/run/rootfsbase/Programs/Gettext/0.20.1/share/gettext-0.20/its/glade1.its
/Data/Variable/run/rootfsbase/Programs/Gettext/0.20.1/share/gettext-0.20/its/glade2.its
/Data/Variable/run/rootfsbase/Programs/Gettext/0.20.1/share/gettext-0.20/its/gsettings.its
/Data/Variable/run/rootfsbase/Programs/Gettext/0.20.1/share/gettext-0.20/its/gtkbuilder.its
/Data/Variable/run/rootfsbase/Programs/Gettext/0.20.1/share/gettext-0.20/its/metainfo.its
/Data/Variable/run/rootfsbase/Programs/ITSTool/2.0.6/share/itstool/its/docbook.its
/Data/Variable/run/rootfsbase/Programs/ITSTool/2.0.6/share/itstool/its/docbook5.its
/Data/Variable/run/rootfsbase/Programs/ITSTool/2.0.6/share/itstool/its/its.its
/Data/Variable/run/rootfsbase/Programs/ITSTool/2.0.6/share/itstool/its/mallard.its
/Data/Variable/run/rootfsbase/Programs/ITSTool/2.0.6/share/itstool/its/ttml.its
/Data/Variable/run/rootfsbase/Programs/ITSTool/2.0.6/share/itstool/its/xhtml.its
/Data/Variable/run/rootfsbase/System/Index/share/gettext/its/fontconfig.its
/Data/Variable/run/rootfsbase/System/Index/share/gettext/its/gschema.its
/Data/Variable/run/rootfsbase/System/Index/share/gettext/its/gtkbuilder.its
/Data/Variable/run/overlayfs/Programs/GLib/2.68.4/share/gettext/its/gschema.its
/Data/Variable/run/overlayfs/System/Index/share/gettext/its/gschema.its
/Programs/Fontconfig/2.13.1/share/gettext/its/fontconfig.its
/Programs/GLib/2.63.5/share/gettext/its/gschema.its
/Programs/GLib/2.68.4/share/gettext/its/gschema.its
/Programs/GTK+/3.24.13/share/gettext/its/gtkbuilder.its
/Programs/Gettext/0.20.1/share/gettext-0.20/its/glade1.its
/Programs/Gettext/0.20.1/share/gettext-0.20/its/glade2.its
/Programs/Gettext/0.20.1/share/gettext-0.20/its/gsettings.its
/Programs/Gettext/0.20.1/share/gettext-0.20/its/gtkbuilder.its
/Programs/Gettext/0.20.1/share/gettext-0.20/its/metainfo.its
/Programs/ITSTool/2.0.6/share/itstool/its/docbook.its
/Programs/ITSTool/2.0.6/share/itstool/its/docbook5.its
/Programs/ITSTool/2.0.6/share/itstool/its/its.its
/Programs/ITSTool/2.0.6/share/itstool/its/mallard.its
/Programs/ITSTool/2.0.6/share/itstool/its/ttml.its
/Programs/ITSTool/2.0.6/share/itstool/its/xhtml.its
/System/Index/share/gettext/its/fontconfig.its
/System/Index/share/gettext/its/gschema.its
/System/Index/share/gettext/its/gtkbuilder.its

```


### Seems to contain polkit.its file
https://ubuntu.pkgs.org/18.04/ubuntu-main-amd64/policykit-1_0.105-20_amd64.deb.html  
https://packages.ubuntu.com/bionic/policykit-1-doc  

https://packages.debian.org/stretch/policykit-1
https://packages.debian.org/stretch/amd64/policykit-1/download


```
policykit-1_0.105-18+deb9u1_amd64.deb\data.tar\.\usr\share\gettext\its\

```

### cdio cdda.h 
https://packages.debian.org/sid/libcdio-cdda-dev

```
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/libc/libcdio-paranoia/libcdio-cdda-dev_10.2+2.0.0-1+b2_amd64.deb

```
