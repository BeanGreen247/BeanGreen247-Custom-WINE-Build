# BeanGreen247's build of Wine

This pkgbuild allows you to create custom wine builds using an opt-in mechanism (by editing the customization.cfg file). 

You can now easily get the "plain wine + pba + steam fix" build you've been dreaming about.

Since this is a -git package, wine and wine-staging sources will be pulled from latest master branch by default. You can define specific releases commit in the cfg file if needed.

Can be built with DXVK winelib prebaked (replacing wined3d for d3d10 and d3d11 support) - https://github.com/doitsujin/dxvk

Can be built with VKD3D for D3D12 support (using https://github.com/Tk-Glitch/PKGBUILDS/tree/master/vkd3d-git is recommended) - https://source.winehq.org/git/vkd3d.git

Can be built with Faudio (requires both faudio-git and lib32-faudio-git packages from AUR) - https://github.com/FNA-XNA/FAudio

Wine : https://github.com/wine-mirror/wine

Wine-staging : https://github.com/wine-staging/wine-staging

Wine esync : https://github.com/zfigura/wine/tree/esync

Wine-pba : https://github.com/acomminos/wine-pba

Thanks to @Firerat and @bobwya for their rebase work :

https://github.com/Firerat/wine-pba

https://github.com/bobwya/gentoo-wine-pba

## Patches 

CSMT-toggle fixed logic - https://github.com/wine-staging/wine-staging/pull/60/commits/ad474559590a659b3df72ec9965de20c7f51c3a8

GLSL-toggle for wined3d

Path of Exile DX11 fix

Steam --no-sandbox auto fix (for store support on higher than winxp mode)

The Sims 2 fix

Magic: The Gathering Arena fix

Fortnite crash fix - https://github.com/Guy1524/fortnite-wine - "Working once every fortnite" ~FeetOnGrass

Fallout 4 and Skyrim SE Script Extender fix - https://github.com/hdmap/wine-hackery/tree/master/f4se

Fallout 4 Direct sound fix - https://bugs.winehq.org/show_bug.cgi?id=41271

Winepulse disable patch (fix for various sound issues related to winepulse/pulsaudio)

Lowlatency audio patch for osu! - https://blog.thepoon.fr/osuLinuxAudioLatency

Use CLOCK_MONOTONIC instead of CLOCK_MONOTONIC_RAW in ntdll/server

"Launch with dedicated gpu" desktop entry

Bypass compositor in fullscreen mode

Proton Fullscreen hack (Allows resolution changes for fullscreen games without changing desktop resolution)

Plasma 5 systray fix

For Gallium 9 support, use https://github.com/iXit/wine-nine-standalone (available from winetricks and AUR)

Also supports user patches for you to make even more exotic builds (more details at the end of the customization.cfg file).

Lutris esync (+staging +pba) builds are currently created using this pkgbuild - https://github.com/lutris/wine

## The guide

Download the source :

Download the build files from [here](https://mega.nz/#!bglRmApK!INjCp0KUTIjUdZ4IFZsK-jbEucxOKXKvP4LZBzevXX8) and then extract them
```
cp -r Downloads/tar xvzf Build-Files-BeanGreen247-Custom-Wine-Build.tar.gz $pwd
tar xvzf Build-Files-BeanGreen247-Custom-Wine-Build.tar.gz
```
Build  it:
```
sudo pacman -S base-devel cabextract 
git clone https://aur.archlinux.org/trizen.git
cd trizen
makepkg -si
trizen -S yay
yay -S mingw-w64-gcc-base mingw-w64-gcc
**if asked to remove headers, remove them**
cd
cd BeanGreen247-Custom-WINE-Build/
makepkg -si
```
See the bottom of the customization.cfg file for how to apply your own patches.
## Install these packages before use
```
sudo pacman -Sy giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse libgpg-error lib32-libgpg-error alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo sqlite lib32-sqlite libxcomposite lib32-libxcomposite libxinerama lib32-libgcrypt libgcrypt lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader cups samba alsa alsa-utils alsa-tools gnutls libpng lib32-libxml2 lib32-mpg123 lib32-lcms2 lib32-giflib lib32-libpng lib32-gnutls pygtk python2-dbus lib32-libpulse lib32-fontconfig lib32-libxcomposite lib32-libxrender  lib32-libxslt lib32-gnutls lib32-libxi lib32-libxrandr lib32-libxinerama lib32-libcups lib32-freetype2 lib32-libpng lib32-openal python-pyopencl lib32-v4l-utils lib32-libxcursor lib32-mpg123 lib32-sdl xf86-video-intel lib32-mesa-libgl nss-mdns --needed --noconfirm wine-mono cabextract nvidia-libgl lib32-nvidia-libgl giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo libxcomposite lib32-libxcomposite libxinerama lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader cups samba dosbox lib32-alsa-lib lib32-alsa-plugins lib32-libpulse lib32-alsa-oss lib32-openal lib32-gst-plugins-base lib32-gst-plugins-good lib32-gnutls lib32-libpng lib32-giflib lib32-lcms2 lib32-mpg123 lib32-libxml2 lib32-gst-plugins-base lib32-gst-plugins-good lib32-gnutls lib32-libpng lib32-giflib lib32-lcms2 lib32-mpg123 lib32-libxml2 lib32-alsa-lib lib32-alsa-oss lib32-alsa-plugins lib32-libpulse pulseaudio libwbclient samba mpg123 lib32-mpg123 lib32-gnutls lib32-libcanberra-pulse lib32-libpulse
```
And these using yay
```
yay -Sy libdrm libglvnd libomxil-bellagio libunwind libva libvdpau libx11 libxdamage libxml2 libxrandr libxshmfence libxxf86vm llvm lm_sensors meson xorgproto python-mako valgrind wayland wayland-protocols libelf libomxil-bellagio libunwind libxdamage libxshmfence libxxf86vm llvm-libs lm_sensors wayland libva-mesa-driver mesa-vdpau opengl-man-pages clang xorgproto elfutils glslang libclc libdrm mesa
```
## Install already built package 

Download from [here](https://mega.nz/#!Cx8h0KSB!bIHrX8l6MKdQQeDOh5h7SQbJn6xjeR9lWiE1hivplPY)
```
cd /home/$USER/Downloads/
sudo pacman -U wine-tkg-staging-fsync-faudio-git-4.17.r11.gd4326087-208-x86_64.pkg.tar.xz
```
## **MAKE SURE TO REBOOT AFTER INSTALLING**
