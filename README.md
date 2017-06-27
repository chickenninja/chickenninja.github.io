* TOC
{:toc}

<img src="/images/chickenninja.jpg" width="75%" height="75%">

This page contains some dotfiles and cheatsheets that I regularly use.

# About Me

Namaste. I am Sean; API Architect at Apigee/Google; Time Magazine Person of the Year 2006.

# What do I do?
I prevent cross-site scripting, I monitor for DDoS attacks, emergency database rollbacks, and faulty transaction handlings. The Internet... heard of it? Transfers half a petabyte of data every minute. Do you have any idea how that happens? All those YouPorn ones and zeroes streaming directly to your shitty, little smart phone day after day? Every dipshit who shits his pants if he can't get the new dubstep Skrillex remix in under 12 seconds? It's not magic, it's talent and sweat. People like me, ensuring your packets get delivered, un-sniffed. So what do I do? I make sure that one bad config on one key component doesn't bankrupt the entire f?@!ng company. That's [what I do](https://youtu.be/dkrzZ8-gfn0). 

# Development Environment

I am currently experimenting with Arch Linux. If you are interested, the list of tools I use can be found [here](https://github.com/chickenninja/arch-environment/blob/master/roles/core/tasks/main.yml).

This section is mostly for my benefit when rebuilding my machine.

- Boot Arch Linux (x86 64) from USB
- Connect to the network using ethernet or netctl

```shell
ip a 	#get the interface name
cp /etc/netctl/examples/wireless-wpa /etc/netctl/mywifi
vim /etc/netctl/mywifi 	#set interface, wifi name and key
netctl start mywifi
```
(if you need wifi, you can find the ESSID using the steps below ...)

```shell
ip link set (interface) up
iwlist (interface) scan
ip link set (interface) down
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

# Sprint 0 Tasks

Before a team can start working on a project, a number of tools must be set up.

## Secrets server

Many of the tools we set up will require secrets, passwords, certs or ssh keys. These shouldn't be hardcoded, committed to source control or left on post-it notes on monitors. Instead, a user can temporarily spin up a server for the duration of a build that requires the secrets.

I have written a quick tool to do this [here](https://github.com/chickenninja/secrets-server)

## Provisioning a project server

Whilst an international enterprise with a thousand developers will require many servers to improve availability and speed, a one man team will only require a single server. After adding my Digital Ocean Access Token to my secrets server, I can run the following command to provision a server.

``` shell
sudo docker run -e DIGITALOCEAN_ACCESS_TOKEN=$(sd-secret do-token) doctl compute droplet create project-server --size 1gb --image debian-8-x64 --region ams2 --ssh-keys {ssh key fingerprint}
```

Using the Digital Ocean CLI has its pros and cons. Whilst using a CLI is much better for integration and automation than logging onto the web portal, I would need to use a different CLI for each provider. In order to be cloud-agnostic I can use a tool like Vagrant with multiple providers.


