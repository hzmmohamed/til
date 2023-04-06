---
date: 11-03-2022
title: Finally Grokking UEFI and GRUB
tags: ['jupyter', 'python', 'notebook']
---

## Introduction
UEFI is, without a doubt, a term that has become quite familiar over the years, yet equally elusive, especially during my phase of naive Hackintosh tinkering without knowing why kernel panics even happened. I've learned at some point that UEFI enabled richer UIs and mouse interactions without loading an operating system.

I finally got to it, I read the manual. I was basically forced to, when I had to troubleshoot an issue when my Arch installation bootloader kept abruptly disappearing from the BIOS boot options.

Thanks to the amazing [Arch Wiki](https://wiki.archlinux.org/), I've acquired the knowledge of the fleeting world between bare-metal valley and kernel land.

## EFI
EFI entries are just entries stored on the computer's NVRAM. Each entry has an ID and points to an EFI "application"/image stored on some disk. Along with these entries, some variables like `BootCurrent`, `BootNext`, `Timeout`, and the `BootOrder` are stored in NVRAM. Their names are self-explanatory.

EFI entries are independent of the images they point to. They are completely static, unlike for example boot options in GRUB which scans for bootable disks at runtime. More about GRUB in a later section. That's when an old operating system's disk is wiped on your system, the EFI entry that it originally added upon installation stays around.

`efibootmgr` is a linux program that can list and manipulate the EFI entries on your system. It requires root access. `efibootmgr` makes managing EFI so easy. You can create, edit or remove EFI entries. 

This is how EFI entries look like:

```bash
$ sudo efibootmgr
BootCurrent: 000C
Timeout: 0 seconds
BootOrder: 000C,2001,2002,2003
Boot0006* EFI USB Device (SanDisk)	PciRoot(0x0)/Pci(0x14,0x0)/USB(14,0)/HD(1,MBR,0x208e0b,0x800,0x1ca3592)RC
Boot0007* EFI Network 0 for IPv4 (54-E1-AD-C9-1E-AB) 	PciRoot(0x0)/Pci(0x1c,0x4)/Pci(0x0,0x0)/MAC(54e1adc91eab,0)/IPv4(0.0.0.00.0.0.0,0,0)RC
Boot0008* EFI Network 0 for IPv6 (54-E1-AD-C9-1E-AB) 	PciRoot(0x0)/Pci(0x1c,0x4)/Pci(0x0,0x0)/MAC(54e1adc91eab,0)/IPv6([::]:<->[::]:,0,0)RC
Boot0009* EFI Network 0 for IPv6 (54-E1-AD-C9-1E-AB) 	PciRoot(0x0)/Pci(0x1c,0x4)/Pci(0x0,0x0)/MAC(54e1adc91eab,0)/IPv6([::]:<->[::]:,0,0)RC
Boot000A* EFI Network 0 for IPv6 (54-E1-AD-C9-1E-AB) 	PciRoot(0x0)/Pci(0x1c,0x4)/Pci(0x0,0x0)/MAC(54e1adc91eab,0)/IPv6([::]:<->[::]:,0,0)RC
Boot000B* EFI Network 0 for IPv4 (54-E1-AD-C9-1E-AB) 	PciRoot(0x0)/Pci(0x1c,0x4)/Pci(0x0,0x0)/MAC(54e1adc91eab,0)/IPv4(0.0.0.00.0.0.0,0,0)RC
Boot000C* GRUB	HD(1,GPT,e00b1f28-8a59-475c-959f-901d15069e91,0x30,0x100000)/File(\EFI\GRUB\grubx64.efi)
Boot2001* EFI USB Device	RC
Boot2002* EFI DVD/CDROM	RC
Boot2003* EFI Network	RC
```

EFI implementations across manufacturers are not perfect. Some firmwares have bugs. For example, on my Lenovo laptop, I used efibootmgr to remove some entries and rebooted to find that they were still there. 

>If efibootmgr cannot successfully create an entry, you can use the bcfg command in UEFI Shell v2 (i.e., from the Arch Linux live iso).

The Arch Linux Live iso has an embedded UEFI Shell. (https://wiki.archlinux.org/title/EFISTUB#bcfg)



## EFISTUB
EFISTUB is a feature in the Linux kernel. It is enabled in the Arch Linux kernel builds. It allows the kernel to be loaded as an EFI application. So the system can boot the kernel directly without using a bootloader like GRUB.

## GRUB
I learned more about GRUB today. I read through much of the GNU Manual for it. 

The key highlights that are useful to me:
- GRUB can load pretty much any operating system I would be using (Linux, Windows)
- GRUB can be installed as an EFI application.
- To allow grub-mkconfig to drives for bootable images, install os-prober and mount the drives that have bootable operating systems. The mount point is not important, since os-prober will scan mtab rather than fstab.

- GRUB customization:
    - Themes
      - Catpuccin themes
      - Minegrub
    - Play a tune before showing the bootloader (Caution: will only play at full volume hehe)

- modules for loading keyboard layouts for ecample before the kernel
- has many modules
- can read luks encrypted drives
    - not sure how it finds the kernel executable on the encrypted drive though
    - i dont actually understand how my current luks + grub setup works. how does grub find the executable?
    - What does the generated grub.cfg mean? Since GRUB prompts me to decrypt the disk, I believe, how does it load the linux kernel file after that?
    - Probably it is the arch microcode that runs and decrypts the drive. mkinitcpio.conf has the decrypt and keyboard modules added.
- correct a mistake. grub does scan for bootable images at runtime. it does so when grub-mkconfig is ran. os-prober makes it scan for other types of OSs.
- https://wiki.archlinux.org/title/GRUB#Configuration
- https://wiki.archlinux.org/title/GRUB/Tips_and_tricks#Recall_previous_entry
- https://www.gnu.org/software/grub/manual/grub/html_node/Simple-configuration.html#Simple-configuration


Other interesting details that I picked up:
- The current GRUB version is called GRUB2, which was a re-implementation of "GRUB Legacy".
- GRUB implements the Multiboot specification.
- GRUB loads Windows using a process called chain-loading. This process is used for loading kernels that do not support the Multiboot specification.



## EFI System Partition 
https://wiki.archlinux.org/title/EFI_system_partition