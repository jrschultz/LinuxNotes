# Post Fedora Install Steps

Date: October 2022

1) **Speed up DNF**
sudo vim /etc/dnf/dnf.conf

fastestmirror=True
max_parallel_downloads=10
defaultyes=True
keepcache=True

2) **Add RPM Fusion for codecs and extra repos:**
https://rpmfusion.org/Configuration

sudo dnf install 
https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm 
https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

sudo dnf groupupdate core

sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin

sudo dnf groupupdate sound-and-video

**Do not install tainted repos**

3) **Add Flathub Repo:**

flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

4) **Tweaks and Extensions**

sudo dnf install gnome-tweaks gnome-extensions-app

5) **Tweaks Tweaks**
Window Titlebars>Enable Maximize, Minimize and Left Side buttons

6) **Extensions**

7) **Disable Animations**
Settings>Accessibility>Disable Animations

8) **Install Apps**
sudo dnf install vim emacs rsync curl git zsh ranger gparted openssh-server htop neofetch handbrake vlc mpv ffmpeg samba filezilla musescore3 libreoffice pandoc texlive-scheme-full

**FlatPaks:** BraveBrowser, Chromium, Bitwarden, Shotcut, Keepassxc, 

**Other Sources:** spacemacs OhMyZsh ytdlp makemkv

9) **Pleasantries**
configs via github https://github.com/jrschultz/.configs
Font Bundles (server)

10) **Systemctl Services**
**SSH**
sudo dnf install openssh-server
systemctl enable sshd
systemctl enable sshd
**Samba**
sudo dnf install samba
systemctl enable smb


