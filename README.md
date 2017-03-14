DevOps Instructions and Guides
==============================


This repository acts as a knowledge repo for any questions regarding the DevOps practices of DreiDev,
A repository of knowledge as well as instructions.

Please not that the instructions here are not guidelines but to be considered law when provisioning servers.




At DreDev we use Fedora for hosting. Always use the latest stable release, as of this writing it is fedora 25.

SELinux should never be disabled and firewalls are always configured.


Many documentation links to manual pages, if you do not read the fucking manual you can not run DevOps.
Take the time to RTFM which is common for Linux users and sysadmins.


# Base Server Setup

For what to do after creating a new server and sshing there for the first time, and how to set it up consult
[this](generic/README.md) document.


# Services


For services that start your applications and auto restart them if failed and standarized logging consult [this](generic/SERVICES.md) document

# Timers


For periodic jobs we use systemd **DO NOT USE CRON** consult [this](generic/TIMERS.md) document for further information.


# Languages and Environments

For setting up language support please check [this](languages/README.md) document.