# freebsdinstall

## Skapa installationsmedia
sudo dd if=FreeBSD-14.0-CURRENT-amd64-20230706-884eaacd24bd-263985-memstick.img of=/dev/sd?? bs=1M conv=sync status=progress

## Installation
Kör installer och gör rätt val ;D

### Logga in som root första booten och installera:
pkg install nano
pkg install xorg
pkg install kde5
pkg install kdevelop
pkg install sddm
pkg install git firefox
sysrc dbus_enable=yes
sysrc sddm_enable=yes

nano /etc/sysctl.conf
Lägg till
* net.local.stream.recvspace=65536
* net.local.stream.sendspace=65536

### Installera GPU-drivar

\#https://docs.freebsd.org/en/books/handbook/cutting-edge/#updating-src-obtaining-src

uname -r

git clone --branch ?? https://git.freebsd.org/src.git /usr/src

git clone https://git.FreeBSD.org/ports.git /usr/ports

cd /usr/ports/graphics/drm-510-kmod
make install clean

pw groupmod video -m [user]

cd ../gpu-firmware-amd-kmod
make install clean FLAVOR=navy_flounder # Radeon RX 6750 XT

kldload amdgpu

sysrc kld_list+=amdgpu

\# starta om och boota in i sddm/kde

-------------
Video på install: https://www.youtube.com/watch?v=0qq3H8pflU0
Instruktion GPU: https://xyinn.org/md/freebsd/amd_radeon_6900_xt
Ports: https://docs.freebsd.org/en/books/handbook/ports/#ports-using-git-method
