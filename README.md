# scrutiny-playbook
Experimental - Sets up an installation of scrutiny

* Edit the "inventory" file as appropriate

* Copy your key to user "root" on all the boxes you want to manage

* Clone this repository somewhere handy

* Do an Ansible run
`ansible-playbook site.yml -i inventory`

## TODO
* This should NOT be running as root.

* Should validate frontend tarball checksum
