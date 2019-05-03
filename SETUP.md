# Personalized LinuxMint Mate 19 installation

This is to speed up an eventual reinstallation of my personal system.
I choose "full harddisk encryption" with automated login and en_US locale

## Important Packages

```bash
sudo apt-get -y install vim unp tlp powertop cpufrequtils smartmontools
sudo apt-get -y install xserver-xorg-input-synaptics
sudo apt-get -y install keepassxc

sudo add-apt-repository ppa:nextcloud-devs/client
sudo add-apt-repository ppa:phoerious/keepassxc
sudo apt update
sudo apt install nextcloud-client keepassxc -y
```
## Tweaks
 * [X] Install latest updates
 * [X] Set up system snapshots on external drive
 * [X] Unset transparent background in Terminal, set yellow background color mode
 * [X] Disable natural scrolling under "Mouse Settings" -> "Touchpad"
 * [X] Enable permanent tray icon in "Display Settings"
 * [X] Add German/English keyboard layout and enable permanent tray icon. Enable "shift lock" to switch between layouts.
 * [X] Customize Firefox: set search to DuckDuckGo, plugins: uBlock Origin, VDH, IDontCareAboutCookies, keepassxc
 * [X] Upgrade to LM 19.1
 * ...
