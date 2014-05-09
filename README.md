Building a CentOS image
=======================

This repo contains packer templates and related files to build a Centos image.

Available templates:

  * [CentOS 6.5 x86_64 minimal with updates](centos-6.5-x86_64-updates.json)

Here are the additions to the base install:

  * yum --releasever=6.5 update
  * yum --releasever=6.5 install kernel-devel kernel-headers
  * EPEL repo is enabled
  * NTP is installed and enabled
  * SELinux is disabled
  * *UseDNS* and *PermitRootLogin* are both set to *no* in /etc/ssh/sshd_config
  * IPTables is open

Available builders:

  * [vbox4ami](AWS.md) - build an image (from scratch) suitable for AWS
  * [vbox4vagrant](VAGRANT.md) - build a Vagrant box for VirtualBox

Vagrant boxes:

  * https://vagrantcloud.com/igromik/centos-6.5-x86-64-updates
