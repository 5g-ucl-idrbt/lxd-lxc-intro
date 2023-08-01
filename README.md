# lxd-lxc-intro
Lxd introduction ref: https://documentation.ubuntu.com/lxd/en/latest/tutorial/first_steps/

The given recluster.sh file is useful to setup the LXD
decluster.sh file is useful to remove the LXD setup.

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
When you use the --vm option with LXC, it launches the container as a virtual machine, which means the container will run inside a QEMU-based virtualization environment rather than being a pure lightweight Linux container.
   * Performance:
        LXC Container: Generally faster and more lightweight due to kernel sharing and reduced overhead.
        Virtual Machine: Can be slower and heavier due to the need for a separate kernel and virtualization layer.

   * Use Cases:
        LXC Container: Suitable for scenarios where you need lightweight containerization and good performance. It is ideal for running multiple isolated applications or services on the same host.
        Virtual Machine: More appropriate for scenarios where strict isolation between the guest VM and the host system is required. VMs are often used when running applications with specific OS requirements or when the host OS cannot provide the desired level of isolation.

In summary, LXC containers are lighter and more efficient, while virtual machines provide stronger isolation but with higher resource overhead. The choice between the two options depends on your specific use case and requirements. If you need lightweight isolation for multiple applications, LXC containers are usually the preferred choice. If you need stronger isolation or specific OS requirements, a virtual machine may be more appropriate.

In Canonical's LXD (pronounced Lex-Dee), the hypervisor responsible for making virtual machines (VMs) work is QEMU. LXD leverages the QEMU virtualization technology to run VMs within LXD containers.

When you use LXD to create and manage virtual machines, it sets up a QEMU-based virtualization environment to host those VMs. QEMU is a powerful open-source emulator and virtualization tool that allows you to run virtual machines with various operating systems, including Linux and Windows.

LXD interacts with QEMU to manage the virtual machine's lifecycle, networking, storage, and other aspects of virtualization. This combination of LXD with QEMU provides a user-friendly interface and management experience while utilizing the underlying virtualization capabilities of QEMU.

It's important to note that LXD also supports running lightweight system containers using Linux container technologies (such as LXC), which provide better performance and efficiency compared to full virtual machines. However, when you choose to use LXD to run VMs, it relies on QEMU as the hypervisor to enable virtualization and run the VMs inside LXD containers.

for LXDUI

old:(https://github.com/AdaptiveScale/lxdui  https://pypi.org/project/lxdui/)

NEW:
https://documentation.ubuntu.com/lxd/en/latest/howto/access_ui/
https://github.com/canonical/lxd-ui
## For Canonical WEB UI
Complete the following steps to access the LXD web UI:
```
sudo snap set lxd ui.enable=true
sudo systemctl reload snap.lxd.daemon
```
exposing lxd:
```
lxc config set core.https_address :8443
```
ref:```https://documentation.ubuntu.com/lxd/en/latest/howto/server_expose/#server-expose```

paste this in your browser:
```https://127.0.0.1:8443```
* click on create a new certificate
* follow the steps
* add the certificate
* you will be able to see your Dashboard

# creating an instance through GUI:
we are creating a VM image
![Screenshot from 2023-07-24 12-24-46](https://github.com/5g-ucl-idrbt/lxd-lxc-intro/assets/46273637/6dd481f5-ea59-4eaf-8648-7c3251210558)



select the appropriate image to use (here desktop image)
![Screenshot from 2023-07-24 12-36-43](https://github.com/5g-ucl-idrbt/lxd-lxc-intro/assets/46273637/86b5d262-eb87-41ad-9093-7cbed08f1417)



Here we can access the GUI console of the created VM instance
![Screenshot from 2023-07-24 12-44-26](https://github.com/5g-ucl-idrbt/lxd-lxc-intro/assets/46273637/03fc5677-f63d-47bd-adc1-b3aae95782be)


# Testing the connectivity with server inside the VM:
we have used Ubuntu 22.04 image and createed an instance
get into the VM
Dont forget to give the password to the default user ie., Ubuntu 
```
passwd ubuntu

```
Follow these steps to host a simple python server in the VM
```
sudo apt update
sudo apt install -y net-tools 
sudo apt install -y python3
ifconfig     # to see the IP of the Vm
python -m http.server 8000       # This runs a server on the port 8000 with VM IP
```
Check the connectivity in the bear metal
```
wget http://10.143.63.89:8000/    # or type the url in the browser

```
# Storage
To create a loop file based storage, just don’t specify a source, this works for btrfs, zfs and lvm:

   ```
    lxc storage create NAME zfs
    lxc storage create NAME btrfs
    lxc storage create NAME lvm
```
after creating the storages we can use the command
```
lxc storage edit NAME
```
to edit the size and add description

If you just want to use an existing directory to store containers directly, you can do that with the dir backend, though this is our most limited backend feature and performance wise.

   ```
    lxc storage create NAME dir source=/some/empty/directory
```
# Profiles
profiles are like templates they can be used while creating an instance with defined configurations
![Screenshot from 2023-07-31 11-37-33](https://github.com/5g-ucl-idrbt/lxd-lxc-intro/assets/46273637/e853e065-b6d9-4653-bdb0-15d6716663c7)

we can selct number of Cores, RAM, Network etc., we can also the yaml file of the configuration.

# Creating a LXD Cluster
ref: https://www.pluralsight.com/cloud-guru/labs/aws/creating-a-lxd-cluster
In a production environment, we don't want to put all of our containers on a single LXD host. After all, what happens should that host fail? Instead, we generally want to work with a LXD cluster, multiple LXD servers that share a distributed database and allow for redundancy and some fault tolerance. we set up a small LXD cluster of three hosts.

## Configure the First Server in the Cluster
Use lxd init to begin configuring the cluster, answering the questions appropriately:

Would you like to use LXD clustering? (yes/no) [default=no]: yes
What name should be used to identify this node in the cluster? [default=lxd1]: lxd1
What IP address or DNS name should be used to reach this node? [default=10.0.1.100]: 10.0.1.100
Are you joining an existing cluster? (yes/no) [default=no]: no
Setup password authentication on the cluster? (yes/no) [default=yes]: yes
Trust password for new clients: pinehead
Again: pinehead
Configure the rest of the server to use the default settings.


## Add the Second Server to the Cluster
Log into the second server via SSH.

Use sudo lxd init to initialize the server with the provided prompts. This time, we want to ensure we join the cluster on 10.0.1.100, as well as print a preseed:

Would you like to use LXD clustering? (yes/no) [default=no]: yes
What name should be used to identify this node in the cluster? [default=lxd2]: lxd2
What IP address or DNS name should be used to reach this node? [default=10.0.1.110]: 10.0.1.110
Are you joining an existing cluster? (yes/no) [default=no]: yes
IP address or FQDN of an existing cluster node: 10.0.1.100
Cluster fingerprint: fa49603e55ef0a8fe4985a08d64ae785bdbcdaa9b97c7aefe6776244f2607085
You can validate this fingerprint by running "lxc info" locally on 'lxd1' server.
Is this the correct fingerprint? (yes/no) [default=no]: yes
Cluster trust password: pinehead
All existing data is lost when joining a cluster, continue? (yes/no) [default=no] yes
Choose "size" property for storage pool "local":
Choose "source" property for storage pool "local":
Choose "zfs.pool_name" property for storage pool "local":
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: yes
To check the fingerprint on the initial LXD server (lxd1), use lxc info during the configuration process:

lxc info
Copy the output preseed and save it to a file:

vim preseed.yaml
Note: If using Instant Terminal you will need to set the PASTE format in VIM using :SET PASTE to correctly paste the copied text.

The copied text should look something like the example below - but do NOT copy the example settings below as it contains a different certificate.

config:
core.https_address: 10.0.1.110:8443
networks:
- config:
bridge.mode: fan
fan.underlay_subnet: 10.0.1.0/24
description: ""
managed: true
name: lxdfan0
type: bridge
storage_pools:
- config:
size: 15GB
source: ""
description: ""
name: local
driver: zfs
profiles:
- config: {}
description: ""
devices: {}
name: default
cluster:
server_name: lxd2
enabled: true
member_config: []
cluster_address: 10.0.1.100:8443
cluster_certificate: |
-----BEGIN CERTIFICATE-----
MIIB/TCCAYOgAwIBAgIQHcd/PX7W80q9XI9EI6ER6DAKBggqhkjOPQQDAzAyMRww
GgYDVQQKExNsaW51eGNvbnRhaW5lcnMub3JnMRIwEAYDVQQDDAlyb290QGx4ZDEw
HhcNMjAwMzAzMTUzOTIwWhcNMzAwMzAxMTUzOTIwWjAyMRwwGgYDVQQKExNsaW51
eGNvbnRhaW5lcnMub3JnMRIwEAYDVQQDDAlyb290QGx4ZDEwdjAQBgcqhkjOPQIB
BgUrgQQAIgNiAAT/9qymn5B8d1RVY3BCHz62Mo9MB9MtQEjlGdSG/W4NsxiVb1tH
xp6Dbq27Sydkubzyz0hEwbw+tz7sr4CUkd2+n9MWQLmo79vH7sx5P7CoQAJ+n0NC
94n+HqZwjG67rv2jXjBcMA4GA1UdDwEB/wQEAwIFoDATBgNVHSUEDDAKBggrBgEF
BQcDATAMBgNVHRMBAf8EAjAAMCcGA1UdEQQgMB6CBGx4ZDGHBH8AAAGHEAAAAAAA
AAAAAAAAAAAAAAEwCgYIKoZIzj0EAwMDaAAwZQIxAMF9XbIwl8y/amt2yaGUHsuQ
SHSGswbKHo6uW5FFvLUDi6V7YZsWqR0YkBgdSV0xvQIwAeKK6YZT71Qyhuy52ptE
X36Oo7aTeqZCckgR9GSsZ18zmLl0QlJHG9K+BKWbRrBj
-----END CERTIFICATE-----
server_address: 10.0.1.110:8443
cluster_password: pinehead

## Add the Third Server to the Cluster
From the lxd2 server, copy the preseed.yaml file to the lxd3 server:

scp preseed.yaml cloud_user@10.0.1.120:
Log into the lxd3 server with SSH:

ssh cloud_user@10.0.1.120
Open the preseed.yaml file and update the core.https_address to be 10.0.1.120:8443 Locate server_name and change it to lxd3:

vim preseed.yaml
core.https_address: 10.0.1.120:8443

...

server_name: lxd3

...
Initialize the server using the preseed file:

cat preseed.yaml | sudo lxd init --preseed

## Create Containers
Return to lxd1. View all clusters:

lxc cluster list
Create three containers to test the cluster:

lxc launch images:alpine/3.11 web1
lxc launch images:alpine/3.11 web2
lxc launch images:alpine/3.11 web3
To see which server on the cluster these containers ended up on, run lxc list and look for the location value. There should be one container per node.

## FIRST CLUSTER:
lxd init
Would you like to use LXD clustering? (yes/no) [default=no]: yes
What IP address or DNS name should be used to reach this server? [default=192.168.150.120]: 
Are you joining an existing cluster? (yes/no) [default=no]: 
What member name should be used to identify this server in the cluster? [default=idrbt]: lxd1
Do you want to configure a new local storage pool? (yes/no) [default=yes]: no
Do you want to configure a new remote storage pool? (yes/no) [default=no]: 
Would you like to connect to a MAAS server? (yes/no) [default=no]: 
Would you like to configure LXD to use an existing bridge or host interface? (yes/no) [default=no]: 
Would you like to create a new Fan overlay network? (yes/no) [default=yes]: 
What subnet should be used as the Fan underlay? [default=auto]: 
Would you like stale cached images to be updated automatically? (yes/no) [default=yes]: 
Would you like a YAML "lxd init" preseed to be printed? (yes/no) [default=no]: 

## SECOND CLUSTER

# For vnc
https://www.reddit.com/r/Proxmox/comments/l5cqf1/yes_it_is_possible_to_have_a_gui_in_an_lxc/
