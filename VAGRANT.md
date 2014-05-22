Vagrant Specific
================

The following have been added to the image (in addition to those listed in in [README.md](README.md)):

  * For VirtualBox: dkms, gcc, perl, and VBoxGuestAdditions
  * Root password is set to *vagrant*
  * The user *vagrant* has been added with password *vagrant* and authorized_keys from https://github.com/mitchellh/vagrant/raw/master/keys/vagrant.pub

To build a Vagrant box:

  1. `rm -f /tmp/packer-centos-6.5-x_86_64-updates-vagrant-vbox-*`
  1. `packer build --only=vbox4vagrant centos-6.5-x86_64-updates.json`
  1. `vagrant box add --force packer-centos-6.5-x86_64-updates-vagrant-vbox /tmp/packer-centos-6.5-x86_64-updates-vagrant-vbox-*.box`
  1. `vagrant up`
  1. Smoke test (e.g., `vagrant ssh` and look around)

Vagrant boxes:

  * https://vagrantcloud.com/igromik/centos-6.5-x86_64-updates
