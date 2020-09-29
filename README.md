# scrutiny-playbook
Experimental - Sets up an installation of scrutiny

* Edit the "inventory" file as appropriate

* Copy your key to user "root" on all the boxes you want to manage

* Clone this repository somewhere handy

* Do an Ansible run
`ansible-playbook site.yml -i inventory`

## NOTES
Currently the collector role will only really work on Ubuntu 20.04/Debian 10 and up.

If you need to use it on Ubuntu 18.04 or Debian 9 (or earlier), do an Ansible run then install a suitably new version of smartmontools manually.

CentOS support coming soon maybe.

## TODO
* This should NOT be running as root.

* Should validate frontend tarball checksum

* Add a variable to collector role for setting target server
