---
title: "Nixos"
author: "Andrew Ross-Sermons"
lang: "en"
toc: true
summary: "A guide to configuring my first Nixos system."
relationships:
    parent: "project.md"
tags:
    - "dense-note"
    - "project"
---
## Nixos
A guide to configuring my first Nixos system.
## Considerations
### Installation
**Purpose** - Install Nixos.
**Network Connection** - Use `iwctl`
1. `iwctl`
2. `device list`
3. `station <device> scan`
4. `station <device> get-networks`
5. `station <device> connect <SSID>`
**Disk Partitioning** - Used fdisk, parted, or cfdisk
- EFI - 512MB, FAT32
- Swap - 16GB, Swap
- Root - Remaining, ext4
**Partition Mounting**
- `mount /dev/<root> /mnt`
- `mkdir -p /mnt/boot`
- `mount /dev/<EFI> /mnt/boot`
**Generate Config** - `nixos-generate-config --root /mnt`
- Edit config at `/mnt/etc/nixos/configuration.nix`
- Enable Networking - `networking.networkmanager.enable = true;`
- User Setup
  ```
  users.users.andrew = {
    isNormalUser = true;
    extraGroups = [ "wheel" "networkmanager" ];
    password = "password"
  };
  ```
- Basic Packages - `environment.systemPackages = with pkgs; [git networkmanager wpa_supplican dhcpcd nano ];`
- Finalize Install - `nixos-install`
- Set root passwd and Reboot
### Post Installation
- Git Packages - pkglist.txt
### System Usage
**Purpose** - I need a productive system that will allow for aesthetic cusomization and practical development.
**Aesthetic Customization** - Right now, I'm interested in a TUI-based system. It should have...
- Custom built TUI apps that wrap around basic functions like network management
- Global colorscheme that can be changed from one file and affects desktop and console colors
**Practical Development** - I'm a full time student and aspiring application developer. I need to be able to...
- Write raw markdown notes and have a way to render them
- Use various coding languages, like Python and Rust
### Packages
**Purpose** - On Arch, I've had to hastily install many packages to accomplish basic tasks. On my future setup, I'd like to carefully plan which packages I'll use. Some considerations are...
- Focus on fast and lightweigh packages for basic operations
- Prioritize modular packages (ones that have a good input-output configuration that I can use to make my own wrappers)
- Anything UI-based should be at least moderately customizable
**Integral Software** - Packages needed to make full use of my hardware.
- CPU/Microcode Updates
  - Intel Processor - `intel-ucode`
- Performance Optimizations
  - CPU Frequency Scaling - `cpupower`
  - Thermal and Power Settings - `thermald auto-cpufreq powertop tlp upower acpid`
  - Performance Benchmarking - `perf`
- Firmware and BIOS Updates
  - Firmware - `linux-firmware fwupd`
  - Dell - `libsmbios smbios-utils`
- Graphics
  - Video Acceleration - `mesa intel-media-driver`
  - Rendering - `vulkan-tools vulkan-mesa-layers glxinfo vulkaninfo dxvk`
  - Wayland Display Tools - `wlr-randr gammastep displaycal colord colormgr`
- Storage Utilities
  - Filesystem - `btrfs-progs xfsprogs dosfstools exfatprogs ntfs-3g e2fsprogs f2fs-tools`
  - Disk - `parted gparted lsblk blkid`
- Networking
  - Management - `networkmanager wpa_supplicant iw rfkill`
  - Firewall - `ufw`
- Bluetooth
  - Tools - `bluez bluez-utils btm`
- Audio
  - Servers - `pipewire pipewire-pulse alsa-utils`
- Input Devices
  - Touchpad - `xf86-input-libinput` or `xf86-input-synaptics`
- Printers
  - Printer Support - `cups cups-filters hplip`
  - Scanner Utilities - `sane sane-backends simple-scan xsane`
- I/O Devices
  - Keyboard - `xkbcomp kbd`
  - Webcam - `v4l-utils guvcview`
  - USB - `usbutils libusb`
**Basic Functionality** - Packages needed to interact with the system
- Copy/Paste/Clipboard Management - `wl-clipboard`
**Desktop Environment** - Packages for running and configuring the desktop environment
- Display Server - `wayland wayland-protocols wl-clipboard wayland-utils`
- Compositor - `hyprland`
- Greeter - `greetd greetd-tuigreet`
- Taskbar - `waybar`
- Wallpaper - `hyprpaper`
- Compatibility Layers - `xwayland xdg-desktop-portal xdg-desktop-portal-wlr`
**Applications**
- Terminal - `kitty` with powerlevel10k theme 'johnathan'
- File Manager
- Browser - `firefox`
- Archive Management
- Password Management - `bitwarden`
- App Launcher - `rofi`
- Office Suite - `libreoffice`
- PDF Viewer
- Notifications
- Flasher
- Other - `neovim`
**Complete Package List**
- `acpid` - Daemon; Handles ACPI events like power button presses
- `alsa-utils` - Tools for ALSA sound card management
- `blkid` - CLI; Locate/print block device attributes
- `bluez` - Linux bluetooth protocol stack
- `bluez-utils` - Utils to manage bluetooth devices
- `btrfs-progs` - Tools for managing Btrfs filesystems
- `btm` - CLI; Bluetooth manager
- `colord` - Color management daemon
- `colormgr` - CLI; Color profile manager works with `colord`
- `cpupower` - Monitor and adjust CPU frequency scaling
- `cups` - Common UNIX printing system
- `cups-filters` - Additional filters for cups
- `displaycal` - Color calibration tool
- `dosfstools` - Tools for managing FAT32 filesystems
- `dxvk` - Vulcan-based compatibility layer for Direct3D
- `e2fsprogs` - Tools to manage ex2/3/4 filesystems
- `exfatprogs` - Tools to manage exFAT filesystems
- `f2fs-tools` - Tools for managing F2FS filesystems
- `firmware` - Required firmware files for hardware compatibility
- `fwupd` - Firmware update for Linux daemon
- `gammastep` - Adjust screen temperature based on time
- `gparted` - GUI; Tool for partitioning disk drives
- `greetd` - Greeter daemon for login
- `greetd-tuigreet` - TUI; Login manager for greetd
- `guvcview` - Webcam viewer and recorder
- `hplip` - HP Linux imaging and printing software
- `hyprland` - Wayland compositor
- `intel-media-driver` - Intel's hardware acceleration manager
- `intel-ucode` - Microcode updates for Intel processors
- `iw` - CLI; Tool for managing wireless connections
- `kbd` - Tools for managing keyboard configuration
- `libusb` - USB device library
- `libsmbios` - Dell SMBIOS library
- `linux-firmware` - Essential firmware for Linux
- `lsblk` - Lists block devices
- `mesa` - Open-source implementation of OpenGL
- `networkmanager` - All-in-one network manager service
- `ntfs-3g` - Driver to support NTFS read/write
- `parted` - CLI; Disk partitioning tool
- `perf` - Performance benchmarking for CPUs
- `pipewire` - Audio and visual server
- `pipewire-pulse` - PulseAudio compatibility
- `powertop` - Power management diagnostics tool for Intel CPUs
- `rfkill` - Tool for enabling/disabling wireless devices
- `sane` - Scanning utils, libraries, and backends
- `sane-backends` - Backend support for scanning tools in sane
- `simple-scan` - User-friendlt scanning utility
- `smbios-utils` - Utilities for interacting with Dell SMBIOS
- `thermald` - Thermal management daemon
- `tlp` - Power-saving tool
- `ufw` - Firewall manager
- `upower` - Power management daemon
- `usbutils` - Utilities for managing USB devices and connections
- `v4l-utils` - Tools for managing Video4Linuc devices
- `vulkan-tools` - Tools for testing and configuring Vulkan support
- `vulkaninfo` - Tool to displau Vulkan API information
- `wayland` - Display server protocol
- `wayland-protocols` - Extensions to wayland
- `wayland-utils` - Utilities for wayland environments
- `wl-clipboard` - Clipboard utility for wayland
- `wlr-randr` - Display management
- `wpa_supplicant` - Tool for wireless LAN connections
- `x86-input-libinput` - Input driver for keybaords, touchpads, and mice
- `x86-input-synaptics` - Legacy driver for Synaptics touchpads
- `xarchiver` - Archive manager
- `xdg-desktop-portal` - Framework for deskop integration
- `xdg-desktop-portal-wlr` - Wayland backend
- `xfsprogs` - Tools for managing XFS filesystems
- `xkbcomp` - Compiles XKB keyboard descriptions
- `xwayland` - Compatibility layer for X11 apps on wayland




