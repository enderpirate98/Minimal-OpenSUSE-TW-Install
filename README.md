# Introduction

Have you ever wanted to have the Ultimate Linux setup for your own power hungry Nvidia powered laptop? Well I have the ultimate guide on how to configure your OpenSUSE Tumbleweed system to the best it can be, I myself have been tinkering around with my own setup for the past few months so I have a great system that you can replicate at home!

## What will this guide cover?

- OS installation
- Setting up essential repositories such as packman and Flathub
- Power profile swiching for ultimate battery life when needed and ultimate performance for those gaming sessions
- Gpu switching for when you need battery life or performance
- Disabling zypper's automatic bloat install to have your SSD/HDD nice and empty for more of your files!
- Disclaimer: I HAVE TRIED TO DEBLOAT MY SYSTEM BUT IT JUST HAS AROUND THE SAME AMOUT OF PACKAGES AS NORMAL INSTALL BUT AUDIO ISSUES COME UP!!!!!!


## Getting started

To get started we must of course head over to https://get.opensuse.org/tumbleweed/ and download the iso file from the downloads tab, I am assuming that your semi-modern pc is x86-64 so get the offline image for that.

What about flashing? Use a program called Balena Etcher found here: https://etcher.balena.io and you can just plug in at least and 8GB flash drive and flash it (All data on the drive will be erased during flashing)

Get out the device you want to install it to and boot into your device's boot menu, pick the flash drive and let's move onto the next step!

# Installation!

Go down to ```Installation``` and hit enter

It is recommended for you to connect to WIFI so that we can grab all the latest software 

Setup your language and on the next page hit yes to enabling online repositories

Select the Kde plasma option (last part before we write to disk will have package selection)

Partitioning: go through the guided setup doing these: check ```LLVM``` and ```drive encryption``` after that keep the fs BtrFS (unless dual booting with windows)

Setup your locale correctly (If not correct then you might not get the closest mirrors to you)

Setup your user but make sure that automatic login is unchecked because of security reasons

It will have an install button but don't click that yet

Turn Secure Boot off because we will need Nvidia drivers later

Click on ```Software``` and disable the Kde pim suite and Kde games as well as office from installing and leave the rest as default (my system is kinda broken because of manual selections missing something important)

Click on ```Details``` and select any more packages you want to install

Click on ```Install``` and watch your system install!

## Debloating time!

Open Konsole and edit this file: ```sudo nano /etc/zypp/zypper.conf``` Find this line: ``# installRecomends = yes`` and remove the # while also changing the yes to a no

This will help with zypper not reinstalling bloat every time you update

Before updating we should start debloating

Here is a list of packages that I consider bloat and are safe to remove:
- discover (plus dependencies)
- plasma5-desktop-emojier (Emoji Selector)
- khelpcenter5 (Help)
- kcharselect
- kmag
- kmousetool
- kompare
- konversation
- skanlite
- spectacle
- tigervnc
- xorg-x11-Xvnc (Plus dependency)
- more to come
