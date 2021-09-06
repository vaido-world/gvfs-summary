# gvfs-summary

Download location  
http://ftp.debian.org/debian/pool/main/g/gvfs/


## GoboLinux Live CD 16 and 17
Live CD seem to contain preinstalled broken GLib 2.68.4 and must be reinstalled.
```
Compile "anything"

MakeRecipe "GLib" "2.68.4" "https://gitlab.gnome.org/GNOME/glib/-/archive/2.68.4/glib-2.68.4.tar.bz2"

InstallPackage --same "remove" "https://github.com/vaido-world/resolving-util-linux/raw/main/Util-Linux--2.35.1--x86_64.tar.bz2"
InstallPackage https://gobolinux.org/packages/017/Fuse--2.9.7--x86_64.tar.bz2
InstallPackage https://gobolinux.org/packages/017/UnionFS-Fuse--2.1--x86_64.tar.bz2
Compile "GLib" "2.68.4" 
```

## Compiling and building latest GVfs
```

InstallPackage ThirdPartyInstallers
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/p/policykit-1/libpolkit-gobject-1-dev_0.105-31_amd64.deb


echo '\n' | MakeRecipe "GSettings-Desktop-Schemas" "41" "https://gitlab.gnome.org/GNOME/gsettings-desktop-schemas/-/archive/master/gsettings-desktop-schemas-master.tar.bz2"
Compile GSettings-Desktop-Schemas "41"

echo '\n' | MakeRecipe "GVFS" "1.48.1" "https://gitlab.gnome.org/GNOME/gvfs/-/archive/master/gvfs-master.tar.bz2"
nano /Data/Compile/Recipes/GVFS/1.48.1/Recipe
# echo -e "Hello, world\n
# printf "\nTEXT HERE\n$(ls)" >> lists.txt
Bash scripting is awesome\nThis is a new line" >> multiple.txt
Compile "GVFS" "1.48.1"
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
