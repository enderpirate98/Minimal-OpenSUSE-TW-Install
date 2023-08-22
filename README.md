# Introduction

Have you ever wanted to have the Ultimate Linux setup for your own power hungry Nvidia powered laptop? Well I have the ultimate guide on how to configure your OpenSUSE Tumbleweed system to the best it can be. I myself have been tinkering around with my own setup for the past few months so I have a great system that you can replicate at home!

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

## Optional: Remove unwanted packages

Open Konsole and edit this file: ```sudo nano /etc/zypp/zypper.conf``` Find this line: ``# installRecomends = yes`` and remove the # while also changing the yes to a no

This will help with zypper not reinstalling unneeded packages every time you update

Before updating we remove any packages that we don't want (this may be different for you so do your own research into each package)

Here is a list of packages that I don't want and are safe to remove without breaking the system as a whole:
- discover (plus dependencies)
- plasma5-desktop-emojier (Emoji Selector)
- khelpcenter5 (Help)
- kcharselect
- kmag
- kmousetool
- kompare
- konversation
- skanlite
- spectacle (I prefer flameshot)
- tigervnc
- xorg-x11-Xvnc (Plus dependency)
- xterm


It is recommended to use YaST Software for this step since dependencies might not show themselves in terminal

What about the remaining packages in the start menu?

The remaining packages cannot be removed without the underlying system also being removed so we will have to do a different method...

#### Optional: Declutter start menu

~~Right click on the start menu button and hit ``Edit Applications...``~~

~~We can then use the menu editor to remove the shortcuts by hitting ``Delete``&``Save`` (we can pretend the bloat is gone!)~~

~~Again we will remove what we don't need:~~
- ~~Ark~~
- ~~Crashed Proccess Viewer~~
- ~~File Manager - Super User Mode~~
- ~~Gwenview~~
- ~~Info Center~~
- ~~Kate~~
- ~~KWalletManager~~
- ~~Menu Editor~~
- ~~Okular~~
- ~~Terminal - Super User Mode~~
- ~~Wacome Tablet Finder~~
- ~~XScreenSaver~~
- ~~XScreenSaver Settings~~


## Repo setup

After all that debloating you are now good to update your system with ``sudo zypper dup`` and reboot if it tells you to with ``sudo reboot``

We now need to get a communtiy maintained repo such as Packman to get access to additional software such as codecs and other unoffical software that you might want
```
sudo zypper ar -cfp 90 https://ftp.fau.de/packman/suse/openSUSE_Tumbleweed/ packman && sudo zypper dup --from packman --allow-vendor-change
```
My laptop the Dell XPS 15 9510 and it came with an RTX 3050 Mobile so I need drivers
```
sudo zypper addrepo --refresh https://download.nvidia.com/opensuse/tumbleweed NVIDIA && sudo zypper in nvidia-driver-G06-kmp-default
```
For best video playback we of course need codecs
```
sudo zypper in opi && opi codecs
```
Rather than using the default Bash shell there is one called Fish that auto suggests commands when based on my command history

```
sudo zypper addrepo https://download.opensuse.org/repositories/shells:fish:release:3/openSUSE_Tumbleweed/shells:fish:release:3.repo && sudo zypper ref && sudo zypper in fish
```
For gaming I use flatpak because of its advantages over traditional packages
```
sudo zypper in flatpak && flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```
Reboot after all those installs and now the gaming software!
```
flatpak install yuzu atlauncher com.valvesoftware.Steam && sudo zypper in steam devices && sudo zypper rm steam
```
With all that installed it is time to optimize the system for togglable battery/performance!

## Ultimate Performance and Battery life!

There are two packages that we will install that can make your laptop either have the best performance or the best battery life denpending on which mode you prefer
```
sudo zypper in git && cd Downloads/ && git clone https://github.com/bayasdev/envycontrol && cd envycontrol/ && sudo pip install . --break-system-packages
```

After that reboot and we will install the widget to go along with it

Right click start menu button > ``Add Widgets`` > ``Get New Widgets`` > ``Download New Plasma Widgets`` and search for optimus gpu switcher and install the one from enlroma

We will reboot and install the 2nd package

```
sudo zypper in power-profiles-daemon && sudo systemctl enable power-profiles-daemon
```

If you have the problem of a 4k screen on your laptop we can also gain battery life by going into the system settings and lowering the resolution to 2560x1600 in my case but yours could very, the important thing here is making sure to select one that is the same aspect ratio and not go down to low because your image won't be as sharp as you want it

Reboot and when you click on the battery icon you will notice a new slider full of different power profiles as well as the other widget where you can control which gpu to use

## Installing custom Kde Plasma theme and grub theme

Go into Appearance>Global Theme>``Get New Global Theme`` and pick one that is right for you

I love this one made by the CachyOS team and I have written a guide on it: https://github.com/enderpirate98/Cachyos-look-and-feel/

As for Grub themeing go to https://store.kde.org/browse?cat=109 Instructions for theme install should hopefully be provided by creator of said theme

I like the Tela theme by vinceliuice

```
cd Downloads/ && git clone https://github.com/vinceliuice/grub2-themes && cd grub2-themes && sudo ./install.sh -t tela -s 2k
```

Those are the options but your device and preferences will be different so please check

Also go into YaST and change grub to be the same resolution that you picked

During your reboot you should see a good looking theme and hopefully HIDPI scaling is corect, if not run the script again but tinker around and see what works

## Web Browser

Which Web Browser do I use?

I prefer Vivaldi due to it's privacy and Customization but feel free to go with any other options.

Vivaldi
```
sudo zypper ar https://repo.vivaldi.com/archive/vivaldi-suse.repo && sudo zypper in vivaldi-stable
```
Chrome
```
flatpak install com.google.Chrome
```
Firefox is already preinstalled but if you want to switch it out for the flatpak version here you go
```
sudo zypper rm mozillafirefox mozillafirefox-branding-opensuse && flatpak install org.mozilla.firefox
```
Any other Web Browser you could want should also be avalible in flatpak format but if not then feel free to look up how to install those on OpenSUSE Tumbleweed

There are 4 extensions that I use myself that you can get through the Chrome web store or Firefox addons but feel free to use what you like

Plasma Browser Integration: It gives you media control options in one of the taskbar widgets

Bitwarden Password Manager: Rather than using the same password for everything you now can have randomly generated ones stored in a secure database only you have access to for better personal security

Ublock Origin: A content blocker that protects you from harmful websites and annoying ads

Dark Reader: This forces every website you visit to be in dark mode so that your eyes won't burn at certain times of the day (or night)

## Additional things

For screenshots I use Flameshot which works pretty well
```
flatpak install org.flameshot.Flameshot
```
I have not tried it out myself but someone on reddit suggested additional sudo configuration

https://en.opensuse.org/SDB:Administer_with_sudo

This Guide is still in development so please be patient with me :)
