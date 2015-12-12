#!/bin/sh

set -eu

mykern="$(uname -r | cut -d. -f1,2)"

mymaj="${mykern%.*}"
mymin="${mykern#*.}"

if [ "${mymaj}" -gt 3 ]; then
	exit 0
elif [ "${mymaj}" = 3 ]; then
	if [ "${mymin}" -gt 8 ]; then
		exit 0
	fi
fi

yum install -y dracut-modules-growroot

dracut -f
