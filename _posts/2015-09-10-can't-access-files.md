---
layout: post
title: "Why I'm unable to access my Windows' drives in Ubuntu ?"
tags: [linux, windows, dual boot, hack]
---

__The scenario:__ You have just installed a freshly brewed linux image along side with your Windows OS, everything works fine but then you realise you are not able to mount/access your Windows' partitions. 

__So why is this happening ?__ If you have Windows 8 or later version then you might face this problem because of the fast-startup (aka fast-boot) feature, which must be turned off, what it does is it allows your computer to go in a partial sleep state or hibernation state which helps Windows to boot up quickly, in technical terms Windows' kernel still possess the control of your hardware even if you shutdown/restart your computer and boot into a different OS.

__What should you do then ?__:
I will tell you 3 ways to fix this, quick steps no fuss !

#### __1. Using Terminal__:

1.1 Quickly open the terminal or press <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>T</kbd>

1.2 First you need to find out the partition's name which you want to access, run the following command:

```bash
sudo fdisk -l 
```
1.3 Then run this command in your terminal, to access your drive in read/write mode.

```bash
mount -t ntfs-3g -o rw /dev/sda1 /media/<YOUR-Partition-name>
```

<center>OR</center>

Run this command (if the previous didn't work)

```bash
sudo ntfsfix /dev/<YOUR-Partition-name>
```
It only repairs some fundamental NTFS inconsistencies and resets the NTFS journal file, its a very quick way to access your drives if you need them urgently __BUT__ it schedules an NTFS consistency check for the first boot into Windows.


#### __2. Disabling Fast Startup__:

2.1 Navigate to __Control Panel__ then __Power Options__ of your Windows OS.

2.2 Click __“Choose what the power buttons do.”__

2.3 Then Click “__Change settings that are currently unavailable__” to make the Fast Startup option available for configuration.

2.4 Look for "__Turn on fast-startup(recommended)__" option and uncheck this box.

Reboot your computer into Ubuntu, you should be able to access your drives now.

__NOTE:__ Remember doing such a permanent method could hamper some of your Windows bootup time, you might not consider this method if you use Windows frequently.


#### __3. (Re)boot Way__:

Nothing technical, the most easiest way but might take some time, depending upon your machine configuration and bootup timings. Just sit back, relax and watch your computer booting up (meanwhile check your phone or try recollecting what you will be doing after the boot up or clean the dust off your laptop, first world problems, I know right) so let's dive in,

3.1 __Restart/Turn on__ your computer and __boot up Windows OS first__ (with GRUB or any other bootloader you use to switch OS ), till login screen.

3.2 __Don't__ enter your credentials to login, just don't login, instead __restart again.__ 

3.3 Now this time bootup into Ubuntu, login and check if you can access your drives or not. (if not select method 2 or 3)

### __Conclusion__:
Choose any method depending upon your needs, follow method 2, if you use Ubuntu more frequently (or your primary OS is Ubuntu) its a permanent solution. Use method 1 or 3 which are temporary solutions if you use Windows equally.

Thanks for reading, comment below if you know another method or didn't understand any of the methods above.