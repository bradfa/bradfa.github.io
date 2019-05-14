---
layout: post
title: No Battery Backed Real Time Clock Linux Scripts
date: 2019-05-14
comments: false
---

Sometimes on embedded Linux systems the system will always want time to move
forward but the cost of adding a battery backed real time clock is unacceptable.
In this kind of situation, I've found the following solution to be useful.

At shutdown we will write out a file to the "disk" (usually flash memory) with a
timestamp of the current time.  At boot, after systemd moves the clock ahead to
its compile time but prior to starting any processes which need time to be
roughly right and before any time sync beings (ntp, systemd-timesyncd, etc), we
will restore the saved timestamp to be the system's current time.  We make sure
to store the timestamp in a format which will always have later times be larger
numbers so we can easily compare them and we don't use the normal seconds since
the Unix epoch as there might be interesting issues in about 20 years.  This
makes the restore process slightly more complicated as it's not a normal format
to store a Unix timestamp in but it's much easier for humans to understand when
they look at the timestamp file.

My examples use systemd but you can do something similar with other init
systems, too.  Just be sure to restore the time as early as you can in the boot
sequence and to save the time prior to unmounting your read/write flash memory
during shutdown.

There's two components to this scheme, first is the systemd service file which
will run the script at startup and shutdown (replace with your own mechanism for
non-systemd init).  Key here is that the ExecStart script run may exit with a
non-zero result, such as if the current time is already ahead of the saved
timestamp so we need to allow for this to fail:

```
[Unit]
Description=Poor man's replacement for a battery backed real time clock
After=local-fs.target
Before=basic.target
Conflicts=shutdown.target
DefaultDependencies=false

[Service]
ExecStart=-/usr/sbin/nobbrtc.sh restore
ExecStop=/usr/sbin/nobbrtc.sh save
Type=oneshot
RemainAfterExit=yes

[Install]
WantedBy=basic.target
```

The second part is the script which actually does the saving and restoring of
the time.  Store this as an executable script at /usr/sbin/nobbrtc.sh:


```
#!/bin/sh

# Save/restore the clock to/from a timestamp file.

echo_usage() {
	echo
	echo "Usage: ${0} <save|restore>"
	echo "Save/restore the system clock to/from a file"
	echo
}

# Save the current time to /etc/lasttimestamp
do_save() {
	date -u +%4Y%2m%2d%2H%2M%2S > /etc/lasttimestamp
}

# Restore the time from /etc/lasttimestamp if it's later than the current time
do_restore() {
	if [ -s /etc/lasttimestamp ]; then
		read TIMESTAMP < /etc/lasttimestamp
	else
		exit 0
	fi
	SYSTEMDATE=`date -u +%4Y%2m%2d%2H%2M%2S`
	# If timestamp is newer than now, update the time to it's value
	if [ ${TIMESTAMP} -gt ${SYSTEMDATE} ]; then
		# Format the timestamp as date expects it (2m2d2H2M4Y.2S)
		TS_YR=${TIMESTAMP%??????????}
		TS_SEC=${TIMESTAMP#????????????}
		TS_FIRST12=${TIMESTAMP%??}
		TS_MIDDLE8=${TS_FIRST12#????}
		date -u ${TS_MIDDLE8}${TS_YR}.${TS_SEC}
	else
		exit 2
	fi
}

##########################
# Execution Starts Here! #
##########################
if [ ! ${1} ]; then
	echo_usage
	exit 1
fi
case ${1} in
	save)
		do_save
		;;
	restore)
		do_restore
		;;
	\?)
		echo_usage
		exit 1
		;;
esac
```
