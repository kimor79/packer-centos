AWS Specific
==========

The following have been added to the image (in addition to those listed in [README.md](README.md)):

  * [Cloud-Init](http://cloudinit.readthedocs.org/en/latest/) is installed
    * The user *ec2-user* will be added with passwordless sudo and authorized_keys based on the AWS keypair configured at launch time
  * Root password is locked

To build a AMI (**2014-05-09: WIP**):

  1. `rm -fr /tmp/packer-centos-6.6-x86_64-updates-AMI-*`
  1. `packer build --only=vbox4ami centos-6.6-x86_64-updates.json`
  1. `VBoxManage clonehd /tmp/packer-centos-6.6-x86_64-updates-AMI-*/*.vmdk /tmp/packer-centos-6.6-x86_64-updates.img --format raw`
  1. `ec2-import-volume -f raw [options] /tmp/packer-centos-6.6-x86_64-updates.img`
  1. Launch 2 amzn-linux instances
     1. Stop one, detach drive
  1. Attach newly created volume to running instance (xvdf)
     1. `mkdir /mnt/source`
     1. `mount /dev/xvdf /mnt/source`
  1. Attach stopped drive to running instance (xvdg)
     1. `mkdir /mnt/dest`
     1. `mount /dev/xvdg /mnt/dest`
  1. `rsync -AEWXa --delete --numeric-ids /mnt/source/ /mnt/dest/`
  1. Create snapshot from volume
  1. Create AMI from snapshot

Notes:

  * Make sure you have enough disk space to convert the disk image to raw.
  * Tag the EBS volumes so they are easier to find.
