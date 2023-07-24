# lxd-lxc-intro
Lxd introduction ref: https://documentation.ubuntu.com/lxd/en/latest/tutorial/first_steps/
# IMPORTANT
## Firewall issues
### You might see issues with your firewall blocking network access for your instances, or connectivity issues because you run LXD and Docker on the same host.

### See How to configure your firewall for information on how to resolve such issues.
Ref: https://documentation.ubuntu.com/lxd/en/latest/howto/network_bridge_firewalld/#network-bridge-firewall

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

To view storage pools: 
```
 sudo lxc storage list
 sudo lxc storage show <name>
```
 To view nwtwork: 
 ```
 sudo lxc network show <brname>
```

 To view images: 
 ```
 sudo lxc image list images:
```

To get detailed info of the container:
```
sudo lxc info <container-name>
```
To stop a running container:  
```
 sudo lxc stop <container-name>
 ```
 To restart container: 
 ```
 sudo lxc restart <container-name>
```

 To delete a container:
``` 
 sudo lxc stop <container-name>
 sudo lxc delete <container-name>
 ```

## Diffrence between launching a LXC container and a LXC VM:

The difference between the two commands lies in the type of container that will be created :

   * lxc launch ubuntu:22.04
    This command creates a Linux container (LXC) running Ubuntu 22.04. LXC containers share the same kernel as the host system, which makes them lightweight and efficient. LXC containers are suitable for isolating applications or services on the same host without the overhead of running separate virtual machines.

   * lxc launch ubuntu:22.04 --vm
    This command creates a virtual machine (VM) that runs Ubuntu 22.04. In this case, LXD will use a hypervisor (such as KVM or VirtualBox) to create a full virtual machine, which includes its own independent kernel. VMs are more isolated from the host system, but they are generally heavier in terms of resource usage compared to LXC containers.

The main differences between the two options are:

   * Resource Isolation:
        LXC Container: Shares the same kernel with the host system, leading to better resource utilization and efficiency. It isolates processes from the host and other containers.
        Virtual Machine: Runs its own independent kernel, which provides better isolation from the host and other VMs but comes with higher resource overhead.

   * Performance:
        LXC Container: Generally faster and more lightweight due to kernel sharing and reduced overhead.
        Virtual Machine: Can be slower and heavier due to the need for a separate kernel and virtualization layer.

   * Use Cases:
        LXC Container: Suitable for scenarios where you need lightweight containerization and good performance. It is ideal for running multiple isolated applications or services on the same host.
        Virtual Machine: More appropriate for scenarios where strict isolation between the guest VM and the host system is required. VMs are often used when running applications with specific OS requirements or when the host OS cannot provide the desired level of isolation.

In summary, LXC containers are lighter and more efficient, while virtual machines provide stronger isolation but with higher resource overhead. The choice between the two options depends on your specific use case and requirements. If you need lightweight isolation for multiple applications, LXC containers are usually the preferred choice. If you need stronger isolation or specific OS requirements, a virtual machine may be more appropriate.


for LXDUI
https://github.com/AdaptiveScale/lxdui

https://pypi.org/project/lxdui/

https://github.com/canonical/lxd-ui

for vnc
https://www.reddit.com/r/Proxmox/comments/l5cqf1/yes_it_is_possible_to_have_a_gui_in_an_lxc/
