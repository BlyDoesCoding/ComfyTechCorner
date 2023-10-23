---
title: Single GPU Passthrough Setup
description: Unlock Multi-OS Flexibility with Single GPU Passthrough
slug: vmgpupass
date: 2023-10-23 00:00:00+0000
image: cover.jpg
categories:
    - Guide
tags:
    - Guide
    - VMs
    - Linux
    - GPU
    - Single
    - AMD
    - Nvidia
weight: 1
---
The Problem
============

Most people are used to running a single operating system on their PC—it's the way it's meant to be, and it usually works like a charm. But what if you need to test something on a different OS or want to use software only available on another one? The traditional approach would be to dual-boot or even triple-boot, but let's be honest, that can be a bit of a headache.

The problem with multiboot setups is that a Bootloader (often Windows) can mess with other bootloaders and leave you with an unbootable system. Managing your drives can also become a hassle since some operating systems use filesystems not supported by others.

A more convenient solution for testing and using different operating systems is to turn to virtual machines. With VMs, you sidestep the issues associated with multiboot setups. However, there's often a trade-off in terms of performance, with your CPU taking a hit, and GPU performance suffering. But what if I told you there's a way to pass a GPU to your virtual machine, unlocking 100% graphics performance?

This concept is known as GPU passthrough, and it works by unbinding GPU drivers from your base OS and rebinding the GPU to your virtual machine. The catch is that most guides on the internet require at least two GPUs, which can be a problem for those who can't afford multiple graphics cards.

Installation
============

Step 1: Install Ubuntu
----------------------

Start with the latest version of Ubuntu Desktop as your base OS.

Step 2: Clone Repository
------------------------

Clone the following GitHub repository using the terminal:

    git clone https://github.com/wabulu/Single-GPU-passthrough-amd-nvidia.git

Step 3: Execute Setup Script
----------------------------

Navigate into the cloned folder and execute the `setup.sh` file provided:

    sudo bash ./setup.sh

Step 4: Download OS ISO
-----------------------

Download the latest ISO of the OS you want to virtualize. For this example, let's use Windows 10 from [here](URL).

Step 5: Create Virtual Machine
------------------------------

Open your virtual machine manager and create a new virtual machine. Choose the downloaded ISO, follow the setup steps, and before finishing, check "Customize configuration." Configure the following options:

*   Boot: `/usr/share/OVMF/OVMF_CODE_4M.fd`
*   Chipset: "Q35"
*   CPU: 1 socket, X number of cores, 2 threads
*   Allocate 2 GB less RAM than you have
*   Set your virtual disk's cache mode to writeback

Step 6 (Windows only)
---------------------

Download Virtio drivers and add them as a disk to your virtual setup. These drivers are necessary for Windows; most other OSs have them built-in.

Step 7: Install OS
------------------

Install the OS, then shut down the virtual machine.

Step 8: Retrieve GPU BIOS
-------------------------

Retrieve your GPU's BIOS. You can conveniently download it [here](URL), or use various programs to dump your GPU BIOS:

*   Nvidia: NVIDIA NVFlash
*   AMD: ATI ATIFlash

Step 9: Add GPU ROM
-------------------

Place the GPU ROM in the following directory:

    
            sudo mkdir /usr/share/vgabios
            cp ./patched.rom /usr/share/vgabios/
            cd /usr/share/vgabios
            sudo chmod -R 644 patched.rom
            sudo chown yourusername:yourusername patched.rom
        

Replace "yourusername" with your actual username.

Step 10: Configure Virtual Machine
----------------------------------

Remove any spice/qxl components in your virtual machine setup and add your GPU to the PCI section. You should have two devices for your GPU, so add both.

Step 11: Edit GPU XML
---------------------

Enable XML editing in the settings of your virtual machine manager and insert `<rom file='/var/lib/libvirt/vgabios/patched.rom'/>` into both of your GPU devices' XMLs, between "source" and "address."

Step 12: Add Devices
--------------------

Add your PCI host controller, audio controller, and any other devices you want to include.

Step 13: Modify QEMU File
-------------------------

Check the `/etc/libvirt/hooks/qemu` file and edit the name of the placeholder "win10" to match your virtual machine's name. You can also add new sections by copying the existing one below it and editing the name.

Conclusion
============

If everything worked as expected, you now have an awesome setup that can run virtually any OS. You can enjoy gaming on Windows, code on your favorite Linux distribution, and maybe even tinker with BSD somehow. It's all at your fingertips now.