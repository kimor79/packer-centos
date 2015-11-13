Building a CentOS image
=======================

This repo contains packer templates and related files to build a Centos image.

Available templates:

  * [CentOS x86_64 minimal with updates](centos-x86_64-updates.json)

The version of CentOS to install is defined by the `centos_version` parameter in the above templates. As of 2015-11-13 the default version is *6.7*.

Here are the additions to the base install:

  * yum --releasever=6.7 update
  * kernel-devel and kernel-headers are installed
  * EPEL repo is enabled
  * NTP is installed and enabled
  * Manpages are installed
  * SELinux is disabled
  * *UseDNS* and *PermitRootLogin* are both set to *no* in /etc/ssh/sshd_config
  * IPTables is open

Additional options can be included by specifying command line variables:

  * To download the iso from a different mirror: `-var iso_url=http://...`
  * To specify a different CentOS version: `-var centos_version=X.Y`
    * You will most likely also need to pass iso_checksum and iso_url
  * To set root's password hash: `-var root_hash='encrypted_string'`

Available builders:

  * [vbox4ami](AWS.md) - build an image (from scratch) suitable for AWS
  * [vbox4vagrant](VAGRANT.md) - build a Vagrant box for VirtualBox
  * [vbox4vbox](VIRTUALBOX.md) - build a box for VirtualBox
  * [vmware4vagrant](VAGRANT.md) - build a Vagrant box for VMware
  * [vmware4vmware](VMWARE.md) - build a box for VMware
