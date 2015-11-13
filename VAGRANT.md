Vagrant Specific
================

The following have been added to the image (in addition to those listed in [README.md](README.md)):

  * For VirtualBox: dkms, gcc, perl, and VBoxGuestAdditions
  * For VMware: VMware Tools
  * Root password is set to *vagrant*
  * The user *vagrant* has been added with password *vagrant* and authorized_keys from https://github.com/mitchellh/vagrant/raw/master/keys/vagrant.pub
  * single-request-reopen is added to resolv.conf

To build a VirtualBox Vagrant box:

  1. `rm -f /tmp/packer-centos-6.7-x86_64-updates-vagrant-vbox-*`
  1. `packer build --only=vbox4vagrant centos-6.7-x86_64-updates.json`
  1. `vagrant box add --force packer-centos-6.7-x86_64-updates-vagrant-vbox /tmp/packer-centos-6.7-x86_64-updates-vagrant-vbox-*.box`
  1. `vagrant up`
  1. Smoke test (e.g., `vagrant ssh` and look around)

To build a VMware Vagrant box:

  1. `rm -f /tmp/packer-centos-6.7-x86_64-updates-vagrant-vmware-*`
  1. `packer build --only=vmware4vagrant centos-6.7-x86_64-updates.json`
  1. `vagrant box add --force packer-centos-6.7-x86_64-updates-vagrant-vmware /tmp/packer-centos-6.7-x86_64-updates-vagrant-vmware-*.box`
  1. Get Vagrant/VMware license (https://www.vagrantup.com/vmware)
  1. `vagrant up`
  1. Smoke test (e.g., `vagrant ssh` and look around)
