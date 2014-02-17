---
layout: post
title: "Android Emulator Acceleration"
description: "Using Intel Android Emulator Acceleration under Ubuntu"
category: "general"
tags: [android, linux, setup]
---
{% include JB/setup %}

# Resource Site
* [Intel Hardware Accelerator Site](http://software.intel.com/en-us/android/articles/speeding-up-the-android-emulator-on-intel-architecture)

# Commands Actually Run

    # determine 32 vs. 64 bit OS
    >file /sbin/init

    # ensure all repos are up-to-date
    >sudo apt-get update

    # should be greater than 0 to support hardware virtualization (BIOS must enable virtualization!)
    >egrep -c '(vmx|svm)' /proc/cpuinfo
    
    # installs kvm-ok program used to check whether CPU supports kvm virt
    >sudo apt-get install cpu-checker
    
    >kvm-ok
    INFO: /dev/kvm exists
    KVM acceleration can be used
    
    >sudo apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils
    
    # my user was already a member of libvirtd so I just needed to add to kvm group
    >sudo adduser your_user_name kvm

    # test installation after logging out/in
    sudo virsh -c qemu:///system list
    
# Installing x86 Intel Atom 

Only Intel Atom-based emulated phones benefit from the accelerator. But when setting up a new emulator,
Intel Atom wasn't one of my CPU/ABI choices. So I needed to install that via the Android SDK manager (the
half Android/half download arrow icon next to the Android Virtual Device Manager icon).

* For whatever version, select Intel x86 Atom System Image and install

