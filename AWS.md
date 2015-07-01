AWS Specific
==========

The following have been added to the image (in addition to those listed in [README.md](README.md)):

  * [Cloud-Init](http://cloudinit.readthedocs.org/en/latest/) is installed
    * The user *ec2-user* will be added with passwordless sudo and authorized_keys based on the AWS keypair configured at launch time
    * If a drive is attached to /dev/sdb it will be mounted as /mnt/ephemeral0
  * Root password is locked

To build a AMI:

  1. `rm -fr /tmp/packer-centos-6.6-x86_64-updates-AMI-*`
  1. `packer build --only=vbox4ami centos-x86_64-updates.json`
  1. `VBoxManage clonehd /tmp/packer-centos-6.6-x86_64-updates-AMI-*/*.vmdk /tmp/packer-centos-6.6-x86_64-updates.img --format raw`
  1. `ec2-import-volume -f raw [options] /tmp/packer-centos-6.6-x86_64-updates.img`
  1. Launch an amzn-linux instance
  1. Attach newly created volume to running instance (xvdf)
  1. Install grub
```cat <<EOF | sudo grub --batch
device (hd0) /dev/xvdf
root (hd0,1)
setup (hd0)
EOF```
  1. Create snapshot from volume
  1. Create AMI from snapshot
     * Virtualization type: HVM
     * Root device name: /dev/xvda
     * Instance store 0 as /dev/sdb

Notes:

  * Make sure you have enough disk space to convert the disk image to raw.
  * Tag/Name the EBS volume and snaphot so they are easier to find.
