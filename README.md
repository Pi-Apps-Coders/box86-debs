# box86-debs

This is a simple Debian repository for the [box86](https://github.com/ptitSeb/box86) project. New versions are compiled every 24 hours if a new commit on box86's repository has been made, you can find all the debs here: https://github.com/Pi-Apps-Coders/box86-debs/commits/master

These debs have been compiled using various target CPUs and systems. You can see all the available pkgs below.

## Package List
***SPECIAL NOTE: all packages are compiled for native armhf, even the ones with ARM64 in their target name! It's possible to run them on arm64 systems but you need to either run a [multiarch](https://github.com/Pi-Apps-Coders/box86-debs#running-box86-on-arm64-systems) or [compile from source](https://github.com/ptitSeb/box86/blob/master/docs/COMPILE.md#for-other-arm64-64bits-linux-platform).***

Package Name | Notes | Install Command |
------------ | ------------- | ------------- |
| box86-rpi4arm64 | box86 built for RPI4ARM64 target. | `sudo apt install box86-rpi4arm64` |
| box86-rpi3arm64 | box86 built for RPI3ARM64 target. | `sudo apt install box86-rpi3arm64` |
| box86-generic-arm | box86 built for generic ARM systems. | `sudo apt install box86-generic-arm` |
| box86-tegrax1 | box86 built for Tegra X1 systems. | `sudo apt install box86-tegrax1` |
| box86-rk3399 | box86 built for rk3399 cpu target. | `sudo apt install box86-rk3399` |
| box86-android | box86 built with the `-DBAD_SIGNAL=ON` flag | `sudo apt install box86-android` |

Want me to build for more platforms? Open an issue. 

### Repository installation
Involves adding .sources file and gpg key for added security.
```
# check if .list file already exists
if [ -f /etc/apt/sources.list.d/box86.list ]; then
  sudo rm -f /etc/apt/sources.list.d/box86.list || exit 1
fi
# check if .sources file already exists
if [ -f /etc/apt/sources.list.d/box86.sources ]; then
  sudo rm -f /etc/apt/sources.list.d/box86.sources || exit 1
fi
# download gpg key from specified url
if [ -f /usr/share/keyrings/box86-archive-keyring.gpg ]; then
  sudo rm -f /usr/share/keyrings/box86-archive-keyring.gpg
fi
sudo mkdir -p /usr/share/keyrings
wget -qO- "https://pi-apps-coders.github.io/box86-debs/KEY.gpg" | sudo gpg --dearmor -o /usr/share/keyrings/box86-archive-keyring.gpg
# create .sources file
echo "Types: deb
URIs: https://Pi-Apps-Coders.github.io/box86-debs/debian
Suites: ./
Signed-By: /usr/share/keyrings/box86-archive-keyring.gpg" | sudo tee /etc/apt/sources.list.d/box86.sources >/dev/null
```

On a 32bit OS, run the following additional commands
```
sudo apt update
sudo apt install box86-generic-arm -y
```

On a 64bit OS, run the following additional commands
```
sudo dpkg --add-architecture armhf
sudo apt update
sudo apt install box86-generic-arm:armhf -y
```

If you don't want to add this apt repository to your system, you can download and install the latest armhf deb from [here](https://github.com/Pi-Apps-Coders/box86-debs/tree/master/debian).

### Note for box64

Please note that this repository is *only for box86*. If you would like deb packages for box64, check out [box64-debs](https://github.com/Pi-Apps-Coders/box64-debs)
