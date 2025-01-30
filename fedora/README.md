# Fedora 41

## System Settings

### Change Hostname

```bash

sudo hostnamectl set-hostname "<NEW_HOST_NAME>"

```

### Improve DNF config (Faster Downloads of Packages)

```bash
sudo cp /etc/dnf/dnf.conf /etc/dnf/dnf.conf.orig

echo "#
max_parallel_downloads=10
fastestmirror=true
" | sudo tee -a /etc/dnf/dnf.conf

sudo dnf update -y 

```

### Enable RPM Fusion and Other Third-Party Repository

```bash
sudo dnf install -y https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

sudo dnf update -y @core

```

### Install Multimedia Plugins

```bash

sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo dnf update @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf install -y amrnb amrwb faad2 flac gpac-libs lame libde265 libfc14audiodecoder mencoder x264 x265

```

### Install Gnome Tweaks and Extensions App

```bash

sudo dnf install -y gnome-tweaks gnome-extensions-app

```

### Adding Flathub (Flatpak) Repo

```bash

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

```

### Media Softwares, OBS Studio and Video Editing

```bash

flatpak install flathub com.obsproject.Studio
flatpak install flathub org.openshot.OpenShot
flatpak install flathub org.audacityteam.Audacity
flatpak install flathub com.github.vkohaupt.vokoscreenNG

```

### Communication Apps

```bash

flatpak install flathub com.skype.Client
sudo dnf install -y telegram-desktop 

```

### Other Apps

```bash

sudo dnf install -y google-chrome
sudo dnf group install  -y --with-optional virtualization
sudo systemctl enable --now libvirtd

```

### steam 

```bash

# AMD® Drivers
sudo dnf install -y mesa-dri-drivers.i686 mesa-libGL.i686 xorg-x11-drv-amdgpu

# NVIDIA® proprietary Drivers
sudo dnf install -y xorg-x11-drv-nvidia-libs.i686

# NVIDIA® Open Source (Nouveau) Drivers
sudo dnf install -y mesa-dri-drivers.i686 mesa-libGL.i686 xorg-x11-drv-nouveau

# Intel® Drivers
sudo dnf install -y mesa-dri-drivers.i686 mesa-libGL.i686 xorg-x11-drv-intel


##
sudo dnf install -y steam

```

### Font packs

```bash

sudo dnf install -y curl cabextract xorg-x11-font-utils fontconfig
sudo dnf install -y https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm


```

### Development Tools

```bash

sudo dnf group install -y "development-tools"
sudo dnf install -y make cmake gdb

```

## vscode

We currently ship the stable 64-bit VS Code for RHEL, Fedora, or CentOS based distributions in a yum repository.

 - Install the key and yum repository by running the following script:

``` bash

    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" | sudo tee /etc/yum.repos.d/vscode.repo > /dev/null

```

 - Then update the package cache and install the package using dnf (Fedora 22 and above):

``` bash

dnf check-update
sudo dnf install -y code # or code-insiders
```

 - Or on older versions using yum:

``` bash

yum check-update -y
sudo yum install -y code # or code-insiders

```

Source: https://code.visualstudio.com/docs/setup/linux


## Firefox extensions

 - Bitwarden: https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager
 - Privacy Badger: https://addons.mozilla.org/en-US/firefox/addon/privacy-badger17
 - AdGuard AdBlocker: https://addons.mozilla.org/en-US/firefox/addon/adguard-adblocker
 - Firefox Multi-Account Containers: https://addons.mozilla.org/en-US/firefox/addon/multi-account-containers
 - Firefox Relay: https://addons.mozilla.org/en-US/firefox/addon/private-relay
 - Grammar and Spell Checker: https://addons.mozilla.org/en-US/firefox/addon/languagetool

## Gnome Extensions

