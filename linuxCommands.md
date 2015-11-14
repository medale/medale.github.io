---
layout: page
title: Linux Command Goodies
tagline: Useful Linux commands
---

# Exploring Hardware Environment

## Determine 32 vs. 64-bit OS
    >file /sbin/init
    /sbin/init: ELF 64-bit LSB shared object, x86-64,...
    
## Determine Ubuntu Version and Version Name
    >lsb_release -a
    Description:	Ubuntu 13.10
    Release:	13.10
    Codename:	saucy
    > cat /etc/*-release
    DISTRIB_ID=Ubuntu
    DISTRIB_RELEASE=13.10
    DISTRIB_CODENAME=saucy
    DISTRIB_DESCRIPTION="Ubuntu 13.10"
    NAME="Ubuntu"
    VERSION="13.10, Saucy Salamander"
    ...
    
# Network

## Determine other machines on same local subnet

    >/sbin/ifconfig - shows Bcast address, e.g. 192.168.1.255
    >ping -b 192.168.1.255 - shows other machines on local subnet

