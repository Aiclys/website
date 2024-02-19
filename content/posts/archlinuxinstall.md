+++
title = 'Arch linux installation and setup guide'
author = 'Nyr'
date = 2024-01-13T21:37:03+01:00
tags = ["linux", "arch"]
+++

# CURRENTLY STILL WORKING ON THIS ARTICLE, IT ISN'T FINISHED YET!

# Why use Arch Linux?

GNU/Linux and BSD, more than any operating system, give you the freedom of choice.Why use Arch linux and not another distribution like Ubuntu, which is more beginner friendly or Fedora? Well, here are five reasons for using Arch.

## Arch is minimalist
The base Arch Linux installation contains only the minimum necessary packages to boot into a terminal on a working system. It without desktop environment, printer, bluetooth, or audio drivers, no network connectivity packages, very few utilities, and no typical user applications like firefox. It makes zero assumptions as to what any particular user might need, allowing them to build exactly the system they want, with nothing they don't. This way the user has near infinite freedom for what they want to do with their device.

## Arch isn't "easy" to install 
Because of its minimalism, Arch demands that you become a competent system administrator. Arch does almost nothing for you. You have to roll up your sleeves, install and set up the base system from the command line(or used an install script like archinstall or [ArchTitus](https://github.com/ChrisTitusTech/ArchTitus)), and install and configure every detail of the entire system to your liking. To develop enough skill to do that takes a lot of time and effort. You will learn a lot building an Arch system. And when you're done, you will not only understand your system far more deeply, you will feel much more connected to it.

## Arch is a rolling-release distro
With Arch, there is no "version". You are always running the latest packages. Many distros have stable, slow release cycles, which makes an update something you perform every year or two. An update can be a big event--a scary one, even, since so much changes in one fell swoop. With Arch, updates are available every single day, and as long as you stay current, if something does break, it's pretty easy to identify the problem and fix it. And if you really want to be on the bleeding edge you can enable the testing and unstable repos.

## Arch has the largest repositories
Arch has an excellent, well regarded package management system, along with some of the largest, most up-to-date repositories. I have yet to find anything I needed that wasn't available in either the official Arch repos, or the AUR. And when a new package version is released by a developer, it's usually added to the Arch repositories very quickly. 

&nbsp;
&nbsp;
&nbsp;

# DISCLAIMER
### This is only me documenting my way of installing Arch Linux. I am not responsible for any breakage that might happen during the installation. For help in case of issues visit the [ArchWiki](https://wiki.archlinux.org/)
&nbsp;
&nbsp;
&nbsp;

# Foreword
In the following I will describe and document my preferred way of installing Arch Linux, it being without(I mostly use a desktop which is why I don't really need it. If you use a latptop I would recommend it though) LUKS disk encription, UEFI BIOS instead of Legacy BIOS and with my personal dotfiles.

# Preparation
Before installing Arch Linux or any other distributions you need to tweak some settings in your BIOS and download the ISO. 

### Installation media
To download the Arch ISO visit https://archlinux.org/download. To boot from a drive you first need to flash the ISO onto a bootable USB-stick. For this you can use a tool like [Balena Etcher](https://etcher.balena.io/). 

### BIOS configuration
To enter the BIOS you need to press F12, F10, F2 or DEL (this may vary depending on your motherboard and device). After you booted into the BIOS, make sure you set the following things up:
- **Make sure UEFI is on.** This is probably already the case but make sure this is true. If you don't know how to do it you can watch a video on youtube

- **Disable Fast Startup Mode.** This can cause serious problems if you are dual booting with Windows. Fast Startup Mode puts Windows into hibernation when your power off. Because some processes might still be active during hibernation, this might cause problems when booting into Linux.

- **Disable Secure Boot.** Secure boot verifies the digital signature of a bootloader and since Linux bootloaders typically don't have one, it might cause problems.

### Booting into Arch Linux
The next step is to boot into the Arch installation medium. To do so you need to go into your BIOS on startup and choose to boot from your USB-drive.

&nbsp;
&nbsp;
&nbsp;

# Installation

&nbsp;

### Choosing the right keyboard layout 
First, you want to choose the right keyboard layout as the default console keymap is the US layout. To see a list of available layouts do:
```
$  localectl list-keymaps
```
To set the keyboard layout you want, you need to pass it's name to the [loadkeys](https://man.archlinux.org/man/loadkeys.1) command:
```
$  loadkeys de-latin1
```
In this example the keyboard layout is set to german

&nbsp;

### Set terminal font size
If you are using a high resolution monitor, the chances are very high that the terminal font is too small. To fix this problem you need to install terminus fonts.
First step is to update the pacman databases:
```
$ pacman -Sy
```
Then you need to install the fonts:
```
pacman -S terminus-font
```
Update the font cache:
```
fc-cache -fv
```
 And the last step is too set the font to the desired size, 32 in this case:
 ```
 setfont ter-v32b
 ```

&nbsp;

### Setting up an internet connection
To begin note that it will be easiest to be connected via Ethernet. To check wether you are online, you can ping your favorite website. Let's ping Luke Smith's website for example:
```
$  ping 8.8.8.8
```
#### Wlan and WWan setup
If you don't have an Ethernet connnection and want to create an internet connection through wlan, you first need to make sure your wifi card is unblocked. To do this use the [rfkill](https://wiki.archlinux.org/title/Network_configuration/Wireless#Rfkill_caveat) command:
```
$ rfkill
```
If your network card is hard-blocked, this means that your card as a physical button you can press to unblock it. If it is soft-blocked, you need to run the following command to unblock it:
```
$  rfkill unblock wlan
```
After unblocking your network card, you can setup Wifi with one command:
```
$ wifi-menu
```
If it failed or another issue related to wifi occured, visit the [Archwiki](https://wiki.archlinux.org/title/Network_configuration/Wireless) for more information.

&nbsp;

###  

&nbsp;
&nbsp;
&nbsp;

## [Go back](/posts/postsintro)
