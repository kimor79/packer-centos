AWS Specific
==========

The following have been added to the image (in addition to those listed in [README.md](README.md)):

  * [Cloud-Init](http://cloudinit.readthedocs.org/en/latest/) is installed
    * The user *ec2-user* will be added with passwordless sudo and authorized_keys based on the AWS keypair configured at launch time
    * If a drive is attached to /dev/sdb it will be mounted as /mnt/ephemeral0
  * Root password is locked

Steps to build an AMI (see [misc/build\_ami](misc/build\_ami) for an example script):

  1. Run `packer build` with `--only=vbox4ami`
  1. Use `VBoxManage clonehd` to convert the vmdk to vhd
  1. Upload the vhd image to S3
  1. Run `aws ec2 import-image` to convert the vhd image to an AMI
  1. Wait for import to complete (`aws ec2 describe-import-image-tasks`)
  1. Launch an EC2 instance with new AMI
  1. Smoke test

Notes:

  * During `packer build` several files (grub-related, fstab, etc) are set to use /dev/xvda. `aws ec2 import-image` however, modifies /boot/menu.lst and /etc/fstab to use the UUIDs of the partitions on the device.
  * The newly created AMI will be named something like _import-image-adf213_ and most likely not have the desired configuration. A new AMI can be created by identifying the snapshot used and then creating an AMI based on that snapshot. Some common settings:
    * Default kernel and ramdisk
    * HVM
    * Root device: /dev/xvda, delete on termination set to true
    * Adding _instance store 0_ as /dev/sdb
