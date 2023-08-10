# Introduction

Have you ever wanted to have the Ultimate Linux setup for your own power hungry Nvidia powered laptop? Well I have the ultimate guide on how to configure your OpenSUSE Tumbleweed system to the best it can be, I myself have been tinkering around with my own setup for the past few months so I have a great system that you can replicate at home!

## What will this guide cover?

- OS installation
- Setting up essential repositories such as packman and Flathub
- Power profile swiching for ultimate battery life when needed and ultimate performance for those gaming sessions
- Gpu switching for when you need battery life or performance
- Disabling zypper's automatic bloat install to have your SSD/HDD nice and empty for more of your files!

## Getting started

To get started we must of course head over to https://get.opensuse.org/tumbleweed/ and download the iso file from the downloads tab, I am assuming that your semi-modern pc is x86-64 so get the offline image for that.

What about flashing? Use a program called Balena Etcher found here: https://etcher.balena.io and you can just plug in at least and 8GB flash drive and flash it (All data on the drive will be erased during flashing)

Get out the device you want to install it to and boot into your device's boot menu, pick the flash drive and let's move onto the next step!

# Installation!

Go down to "Installation" and hit enter

It is recommended for you to connect to WIFI so that we can grab all the latest software 

Setup your language and on the next page hit yes to enabling online repositories

Select the minimal X mode (last part before we write to disk will have package selection

For partitioning just go through the guided setup and keep the fs BtrFS (unless you are dual booting)

Setup your locale correctly (If not correct then you might not get the closest mirrors to you)

Setup your user but make sure that automatic login is unchecked because of security reasons

jegierjhgeighheiuheihgeriugh (will be included with more stuff later)
