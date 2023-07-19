# lxd-lxc-intro
Lxd introduction
# IMPORTANT
## Firewall issues
### You might see issues with your firewall blocking network access for your instances, or connectivity issues because you run LXD and Docker on the same host.

## Install LXD as a snap
To install LXD as a snap, just run:
```
snap install lxd
```
## Configure LXD

Run the following command and either accept the defaults or choose different options when prompted:
```
lxd init
```
## Install the OS you’d like to use in your container or VM
Container

Command:

```lxc launch <image_server>:<image_name> <instance_name>```

Example:
```
lxc launch ubuntu:22.04 ubuntu-container
```
VM

Command:

```lxc launch <image_server>:<image_name> <instance_name> --vm```

Example:
```
lxc launch ubuntu:22.04 ubuntu-vm --vm
```
Check the community image server for other Linux distributions.

You now have your instance up and running! You’re all set to experiment with any commands you need.

Command:
```lxc exec <instance_name> -- <command>```
Example:
```
lxc exec ubuntu-container -- apt-get update
```
For a list of available commands and options, just run
```
lxc

```
To list all the running instances
```
sudo lxc list
```
To get into the containers terminal
```
sudo lxc exec <container_name> -- bash
```
