VMware Specific
===================

The following have been added to the image (in addition to those listed in [README.md](README.md)):

  * perl and VMware Tools are installed
  * Root password is set to *root*

To build a VMware box:

  1. `rm -f /tmp/packer-centos-7.3.1611-x86_64-updates-vmware-*`
  1. `packer build --only=vmware4vmware centos-x86_64-updates.json`
  1. Launch `/tmp/packer-centos-7.3.1611-x86_64-updates-vmware-*/*.vmx` in VMware
  1. Smoke test (e.g., login via console and look around)
