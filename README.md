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

I am currently experimenting with Arch Linux. If you are interested, the list of tools I use can be found [here](https://github.com/chickenninja/arch-environment/blob/master/roles/core/tasks/main.yml).

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

- format disk and set up partitions
```shell
curl chicken.ninja/scripts/arch-disk -o /tmp/arch-disk.sh
chmod 700 /tmp/arch-disk.sh
# edit the file as required
vi /tmp/arch-disk.sh
/tmp/arch-disk.sh
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
exit
reboot
```

- run ansible playbook to install my tools
``` shell
git clone https://github.com/chickenninja/arch-environment.git
cd arch-environment
./run.sh
```

We are now good to go!
