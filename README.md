# scrutiny-playbook

This is an Ansible-based installer for [Scrutiny](https://github.com/AnalogJ/scrutiny), allowing you to monitor SMART data for a fleet of machines, large or small, and have some idea of when drives are experiencing issues.

It supports both all-in-one and hub-and-spoke deployments, and most popular architectures (amd64, arm64, arm).

## Requirements
You'll need the following:

* A computer with a modern version of Ansible installed. The version included in Debian 11, Ubuntu 22.04 or CentOS 7+ should work fine.
* One machine to act in the "hub"/"web" role.
* One or many machines to monitor.

For both the collector role and the web (hub) role, the following operating systems are supported:

* Debian 9 or above
* Ubuntu 18.04 or above
* CentOS 7 or above

## Getting Started
* Check out a copy of this repository.

```
git clone https://github.com/getglass/scrutiny-playbook.git
cd scrutiny-playbook
```

* Generate an SSH key if you don't already have one.

`ssh-keygen`

* Copy your SSH key to the servers you want to manage (replace example-host with your server's address).

`ssh-copy-id example-host`

* Edit the `inventory` file. Place one machine in the "scrutiny_web" section, then list all the machines you wish to run collectors on in the "scrutiny_collector" section. For a single machine, simply put the same machine into both sections.

Here's an example:
```
[scrutiny_web]
blinky.windowpa.in

[scrutiny_collector]
blinky.windowpa.in
pinky.windowpa.in
inky.windowpa.in
```

* Install Ansible Galaxy roles needed to run the playbook:

`ansible-galaxy install -r roles/requirements.yml`

* Now you're ready to rock! Run Ansible and watch as it sets up your disk monitoring solution.

`ansible-playbook site.yml`

* If the user you are connecting as requires a sudo password, run this command insatead.

`ansible-playbook site.yml --ask-sudo-pass`

* You should see a message like this once Ansible finishes, indicating a successful run:

```
TASK [Success!] **********************************************************************************************
ok: [example.com] => {
    "msg": [
        "If you're reading this, Scrutiny has been successfully deployed.",
        "Let us know if it worked, and feel free to reach out if you need help. Enjoy!"
    ]
}
```

## Credits
scrutiny-playbook was created in 2020 by [Benjamin Arntzen](https://github.com/Zorlin).
