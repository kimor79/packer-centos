#!/bin/sh

set -eu

if [ -f /boot/grub/grub.conf ]; then
	mykern="$(uname -r)"
	myos=CentOS
	myextras=''

	myrel="$(awk '{print $3}' /etc/centos-release)"
	if [ "${myrel}" = 'release' ]; then
		myrel="$(awk '{print $4}' /etc/centos-release)"
	fi

	mymaj="${myrel%%.*}"

	if [ "${mymaj}" -ge 7 ]; then
		myextras="${myextras} net.ifnames=0 biosdevname=0"
	fi

	rm /boot/grub/device.map

	cat > /boot/grub/grub.conf <<EOF
default=0
timeout=1
hiddenmenu

title ${myos} (${mykern})
	root (hd0,1)
	kernel /boot/vmlinuz-${mykern} ro root=/dev/xvda2 xen_blkfront.sda_is_xvda=1 console=ttyS0 ${myextras}
	initrd /boot/initramfs-${mykern}.img
EOF

fi

if [ -f /etc/default/grub ]; then
	cat >> /etc/default/grub <<EOF
GRUB_DISABLE_LINUX_UUID=true
GRUB_DISABLE_UUID=true
GRUB_DEVICE=/dev/xvda2
GRUB_DEVICE_BOOT=/dev/xvda2
EOF

	grub2-mkconfig -o /boot/grub2/grub.cfg
fi
