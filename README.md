* TOC
{:toc}

<img src="/images/chickenninja.jpg" width="75%" height="75%">

# About Me

Namaste. I am Sean, and I work for Apigee/Google as an API Architect.

# Using this Page

 - This is where I keep my notes and cheatsheets. If you are viewing these pages in a browser, you can use the table of contents to browse. If you are viewing in vim, run 

``` shell
setlocal foldmethod=expr foldexpr=getline(v:lnum)[0]!=\#\"`
```
 and use ``zM`` + `zR` to fold/unfold all sections.

# Development Environment

## Introduction

Currently, I am using the following for my personal development:
- Arch Linux OS. I switch between a laptop and a SeaBIOS Chromebook, so needed a bloat-free operating system. 
- i3 Window Manager - I really like the tile based approach, especially since I avoid using the mouse where possible.
- dmenu Unobtrusive Application Launcher. Takes up very little screen space and can is used without a mouse
- Firefox Web Browser. Open source and extensible. I use VimFX to provide vim keybindings instead of using a mouse.
- XFCE4 Terminal Emulator. I am used to the shortcuts and haven't really considered anything else.
- vim Text Editor. Needs no explanation.
- tmux Terminal Multiplexor. Useful when sending commands to multiple boxes at once.
- ranger File Manager. I like the vim keybindings and hate the default colour scheme of midnight commander.
- zsh - I have recently been using zsh instead of bash. I like the more intelligent path completion and vim keybindings.
- docker - I like to use containers for local development as it saves space on the Chromebook by only building the images I need.
- vagrant - For larger projects I use vagrant to abstract between local virtualbox and cloud deployments
- ansible - Writing playbooks is easier than relying on my memory.
- lastpass cli - for password management

## Setup

This section is mostly for my benefit when rebuilding my machine.

- Boot Arch Linux (x86 64) from USB
- Connect to the network using ethernet or netctl

```shell
ip a 	#get the interface name
cp /etc/netctl/examples/wireless-wpa /etc/netctl/mywifi
vim /etc/netctl/mywifi 	#set interface, wifi name and key
netctl start mywifi
```

- format disk using my simple script (wipes everything)
```shell
curl chicken.ninja/scripts/arch-disk -o /tmp/arch-disk.sh
chmod 700 /tmp/arch-disk.sh
fdisk -l #get disk name e.g. sda
#call the script with the rough disk space and disk name
/tmp/arch-disk.sh 12 sda
```

- enter new installation
```shell
arch-chroot /mnt
```

- run script to install my core dependencies
```shell
curl chicken.ninja/scripts/arch-core -o /tmp/arch-core.sh
chmod 700 /tmp/arch-core.sh
/tmp/arch-core.sh
```
