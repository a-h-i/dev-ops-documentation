General server Setup
====================
Information about basic system setup.


## What is SystemD

Systemd is an init replacement, that has a programming API, is python based.
Provides dependency support and actually understands what it's task is. Unlike init which is just a generic script.

That means it has built in support for many advanced functionality and does not require intimate knowledge of BASH which is one of the most complicated non esoteric programming languages in existance.

It manages all processes in a Fedora or RedHat system or any systemd based system. It also manages the boot process, building kernel modules from source when the kernel is updated and features an advanced journaling (loggging mode)

Advantages:


1. systemcall filters
2. user/group ids
3. nice value control
4. OOM score (out of memory killer algorithm applied by linux kernels)
5. IO scheduling class and priority control
6. CPU scheduling policy
7. Processor/core affinity 
8. timer slacks (precision)
9. network access
10. dependency management
11. easy enable and disable
12. easy stopping and starting
13. easy monitoring and restarting on fail
14. Calendar syntax support for timers.
15. Timers woken up exactly on elapsed time due to tight integration with OS, cron wakes up and checks, essentially a scaled up version of busy wait with `sleep()` calls.
16. Timer events can be scheduled relative to finish times
17. Timer/Service status can be checked including when they last ran, when they will run again, etc. cmdline or API
18. Environment variable support.



## Why Timers and not just cron?

Systemd comes with timers, note that cron is still available it is just not favored.

As far as dreidev DevOps is concerned, never use cron.

Timers have the full capabilities of systemd services and it's API.

All systemd services since timers are systemd units, check above list.



## How to view logs

`journalctl -xe -u <unitname>` also `/var/log/messages`, ommit unitname option for full logs 
and `/var/log` directory for specific services such as nginx.





# How Tos

[general dependencies to be installed everywhere base setup and other tid bits.](general.md)