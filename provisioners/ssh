#!/bin/sh

set -eu

sed -i \
	-e '/^UseDNS/d' \
	-e '/^PermitRootLogin/d' \
	-e 's/^#UseDNS .*/UseDNS no/' \
	-e 's/^#PermitRootLogin .*/PermitRootLogin no/' \
	/etc/ssh/sshd_config
