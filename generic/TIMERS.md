Systemd Timers
==============

To list timers run `systemctl list-timers`.

Timers can be run relative to many things, or absolute times, or weekly. They can define what happens when they miss an activation time due to for example being offline. This page is an introduction and links to manuals and wiki pages but is not a one stop reference. If you are too lazy to read the manual you are not qualified to run DevOps.


## Example timer

```bash
# /etc/systemd/system/foo.timer
[Unit]
Description=Run foo weekly

[Timer]
OnBootSec=15min
OnCalendar=weekly
Persistent=true
# Persistent means it should run if it missed a target, due for example system being offline.
ExecStart=/usr/local/bin/systemd-email address %i

[Install]
WantedBy=timers.target
```

Note that best practice is to configure a service unit and then use a timer to run it periodically via `Unit=` in the timer.


To enable a timer, which means it will start after boot run `systemctl enable <name>.timer` same as services.
Starting a timer is identical to starting a service as well


## Documentation
[Here](https://wiki.archlinux.org/index.php/Systemd/Timers) and [here](https://www.freedesktop.org/software/systemd/man/systemd.timer.html)

There are many ways to define when the timer can be started and many configuration option, take the time to read the manual. 