# scrutiny-playbook

This project aims to help you set up [Scrutiny](https://github.com/AnalogJ/scrutiny) as automatically as possible.

It supports both all-in-one and hub-and-spoke deployments, and most popular architectures (amd64, arm64, arm).

## Caveats
First off, this playbook is somewhat experimental, but *should* be safe.

Scrutiny itself is also quite a young project.

## Requirements
First off, you'll need to install a modern version of Ansible onto a machine of your choosing.

The version included in Debian 10+, Ubuntu 18.04+ or CentOS 7+ should work fine.

Ansible only needs to be installed on the machine you want to use to manage the deployment.

The "webapp" role will work on pretty much any recent version of Linux. Currently it supports:

* Debian 9 or above
* Ubuntu 18.04 or above
* CentOS 7 or above

However, the "collector" role depends on having a recent version of smartmontools available. Currently it supports:

* Debian 10
* Ubuntu 18.04 or above
* CentOS 7 (NOT CentOS 8)

You can get the collector working on CentOS 8 by setting up GetPageSpeed Extras and installing their version of smartmontools.

## Getting Started
* Clone this repository somewhere handy

`git clone https://github.com/Zorlin/scrutiny-playbook.git`

* Generate an SSH key if you don't already have one

`ssh-keygen`

* Copy your key to user "root" on all the boxes you want to manage (replace localhost with the machine you want)

`ssh-copy-id root@localhost`

* If you want a hub-and-spoke deployment, edit the inventory file. 
  You will want to pick one machine to be the "hub" and place it in the "webapp" section, and then list all the machines you wish to run collectors on in the "collector" section.
  Here's an example:
```
[webapp]
10.1.1.201

[collector]
10.1.1.201
10.1.1.202
10.1.1.203
10.1.1.204
```

* If you want a hub-and-spoke deployment, you will also need to edit the address that collectors will send their data to.
  Open up group_vars/collector and set "webapp_server" as appropriate.

* Do an Ansible run 

`ansible-playbook site.yml -i inventory`

Once you're up and running, go to your webapp machine, run screen, then run the Scrutiny webapp with the following command.

`/opt/scrutiny/bin/scrutiny-web-linux start --config /opt/scrutiny/config/scrutiny.yaml`

You can then hold Ctrl and hit the letter A then the letter D to detach from the session and leave the webapp running.

## TODO
* Create a basic systemd service for the webapp role so screen isn't needed
