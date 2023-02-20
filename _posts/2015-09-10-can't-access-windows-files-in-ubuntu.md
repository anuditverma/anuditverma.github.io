---
layout: post
title: "Why I'm unable to access my Windows' drives in Ubuntu?"
tags: [linux, windows, dual boot, hack]
thumbnail-img: https://www.anudit.in/assets/img/WinVsUb.jpg
share-img: https://www.anudit.in/assets/img/io-error.jpg
---

__The scenario:__ You have just installed a freshly brewed Linux image alongside your Windows OS. Everything works fine then you realise that you are unable to mount/access your Windows partitions.

__So why is this happening?__ If you have Windows 8 or a later version then you might face this problem because of the fast-startup (aka fast-boot) feature, which must be turned off, what it does is it allows your computer to go into a partial sleep state or hibernation state. This helps Windows to boot up quickly. In technical terms, Windows’ kernel still possesses control of your hardware even if you shut down/restart your computer and boot into a different OS.

__What should you do then?__ I will tell you 3 ways to fix this, quick steps, no fuss! FYI, a little over with more experimentation with the bootloader and MBR records displayed in the BIOS settings. I found a new easy way to make Windows files accessible. So now there are __4 ways!__

Let’s check them out, but before actually going with one of the ways make sure to read all the steps and choose the one according to the situation you are in.

__Useful Link:__ [Here](http://www.disk-image.com/faq-bootmenu.htm) is a list of PC brands with their corresponding hot keys for accessing the Boot Menu or BIOS settings.

#### __1. Using Terminal (Use this when you are currently logged in to Ubuntu)__:

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

Run this command (if the previous one didn't work)

```bash
sudo ntfsfix /dev/<YOUR-Partition-name>
```

It only repairs some fundamental NTFS inconsistencies and resets the NTFS journal file. It’s a quick way to access your drives if you need them urgently __BUT__ there is a little caveat. It schedules an NTFS consistency check for the first boot into Windows.


#### __2. Disabling Fast Startup (Permanent fix but at the cost of increased bootup time)__:

2.1 Navigate to __Control Panel__ then __Power Options__ of your Windows OS.

2.2 Click __“Choose what the power buttons do.”__

2.3 Then Click “__Change settings that are currently unavailable__” to make the Fast Startup option available for configuration.

2.4 Look for the "__Turn on fast-startup (recommended)__" option and uncheck this box.

Reboot your computer into Ubuntu. You should be able to access your drives now.

__NOTE:__ Remember, doing such a permanent method could hamper some of your Windows bootup time. You might not consider this method if you use Windows frequently.

#### __3. (Re)boot Way (Use this when you are about to Power up your system)__:

Nothing technical, the easiest way but might take some time, depending on your machine configuration and bootup timings. Just sit back, relax and watch your computer booting up (meanwhile check your phone or try recollecting what you will be doing after the bootup or clean the dust off your laptop, (first-world problems, I know, right?) so let’s dive in.

3.1 __Restart/Turn on__ your computer and __boot up Windows OS first__ (with GRUB or any other bootloader you use to switch OS ), till the login screen.

3.2 __Don't__ enter your credentials to log in, just don't log in, instead __restart again.__ 

3.3 Now only this time, boot up into Ubuntu, log in and check if you can access your drives or not. (if not select method 2 or 3)

#### __4. Reboot Shutdown Reboot (RSR, a quick way, requires Ninja Skills)__:

According to me, this seems a more efficient way (less time-consuming) to make the Windows files system accessible but there is a catch. Here you cannot just sit back and watch your computer booting up (like in Method 3), you need to be swift in using your hotkeys to trigger the boot menu or BIOS.

4.1 __Start/Restart__ your computer to the __boot menu.__

4.2 __Don't make any selections.__ Just press the power button to __turn off your computer.__

4.3 __Boot again to the boot menu__ and __select Ubuntu__, you should be able to access your Windows file system.

### __Conclusion__:
Choose any method depending on your needs, follow method 2, if you use Ubuntu more frequently (or your primary OS is Ubuntu) it’s a permanent solution. Use methods 1 or 3 which are temporary solutions if you use Windows equally. Try method 4 if you need something in between permanent and temporary.

Comment below if you know another method or didn’t understand any of the methods above.

Thank you for reading.