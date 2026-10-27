# 🎩 Updated Fedora Post-Install Cheatsheet (October 2026)

Assumes a standard Fedora Workstation (GNOME) install. Tested against current Fedora ~44/45 practices with DNF5.

### 1) Speed up DNF
Preferred modern method (writes the settings for you):
```bash
sudo dnf config-manager setopt max_parallel_downloads=10 fastestmirror=True defaultyes=True keepcache=True
```

Alternatively, edit `/etc/dnf/dnf.conf` and add under `[main]`:
```
fastestmirror=True
max_parallel_downloads=10
defaultyes=True
keepcache=True
```

### 2) Add RPM Fusion (codecs + extra packages)
```bash
sudo dnf install \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

Then get full multimedia codecs:
```bash
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo dnf install @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf groupupdate core
```

**Do not install the tainted repos** unless you specifically need them.

### 3) Add Flathub
```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

(Optional: `sudo fedora-third-party enable` also turns on some third-party repos and a filtered Flathub.)

### 4) Tweaks and Extensions
```bash
sudo dnf install gnome-tweaks
```

For easier extension management you can also install Extension Manager (Flatpak recommended):
```bash
flatpak install flathub com.mattjakeman.ExtensionManager
```

### 5) Titlebar Buttons
Open **GNOME Tweaks** → **Windows** (or Window Titlebars) → enable Maximize, Minimize, and place buttons on the left if desired.

### 6) Extensions
Install and enable your preferred ones (Dash to Dock, AppIndicator Support, Blur my Shell, etc.) via Extension Manager or extensions.gnome.org.

### 7) Disable Animations
Settings → Accessibility → Seeing → Disable Animations

### 8) Install Apps
```bash
sudo dnf install vim emacs rsync curl git zsh ranger gparted openssh-server htop fastfetch handbrake vlc mpv ffmpeg samba filezilla musescore libreoffice pandoc texlive-scheme-full
```

**Notes:**  
- `neofetch` → `fastfetch` (maintained replacement)  
- `musescore3` → `musescore` (now version 4.x)

**Flatpaks** (examples): Brave, Chromium, Bitwarden, Shotcut, KeePassXC, etc.

**Other sources:** Oh My Zsh, yt-dlp, MakeMKV, Spacemacs, etc.

### 9) Pleasantries
- Pull configs: `https://github.com/jrschultz/.configs` (or your own)
- Font bundles, themes, etc.

### 10) Systemctl Services
**SSH**
```bash
sudo dnf install openssh-server
sudo systemctl enable --now sshd
```
(Workstation firewall usually already allows SSH. Check with `firewall-cmd --query-service=ssh` if needed.)

**Samba**
```bash
sudo dnf install samba
sudo systemctl enable --now smb
# Optional: open firewall
sudo firewall-cmd --permanent --add-service=samba
sudo firewall-cmd --reload
```

---

**Quick tip:** After a fresh install, run `sudo dnf upgrade --refresh` and reboot before adding third-party repos.


