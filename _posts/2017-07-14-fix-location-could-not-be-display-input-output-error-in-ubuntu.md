---
layout: post
title: "Fix: This location could not be displayed Input/Output error in Ubuntu"
tags: [Ubuntu, Linux, Windows, hack]
share-img: https://www.anudit.in/assets/img/io-error.jpg
---

You have a dual boot machine. Sometimes you need to access your Windows partition when you are in Ubuntu OS. However, at times you might come across an error. This error says, "This location could not be displayed" and it seems like an input/output error (I/O). Follow this simple guide to recover from this error and solve it quickly to access your partition.

<center><img src="/assets/img/io-error.jpg" alt="Ubuntu input/output error"></center>

<center><h3>First of all, you need to know why this is happening?</h3></center>
* If you have a dual boot machine with Windows and Ubuntu. You are switching between operating systems (that’s not a problem at all). However, you might not be shutting down Windows properly. There is a power cut while shutting down. You forced it to shut down. In this case, your partition might get corrupted.

* If you have accidentally deleted some important hidden system or configuration files (used by Ubuntu) from inside Windows.

* You have tried to open the ext4 partition (where Ubuntu is installed) from Windows. This will delete the whole partition or either get corrupted or get completely formatted.

* You might be getting the input/output error because of some hardware failure or hardware issues. Then this guide might not help you. It would be best to get the backup of your data by using a data recovery tool and replacing your hard drive.


<h3>Solution:</h3> Now if you are sure that your hardware is working fine then there might be a problem with your GPT partition table. This parition table might be damaged or has a corrupted file system. To repair the partition we will use __chkdsk__. It is a tool to display the file system integrity status of hard disks and can fix logical file system errors.

Now let's get to the solution, follow these steps: 

#### __1. First Log on to your Windows OS.__

#### __2. Open cmd (Command Prompt).__

1. Quickly open the cmd (Command Prompt), press <kbd>Windows</kbd> + <kbd>R</kbd>, type __cmd__ and press <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Enter</kbd> (to __Run as administrator__.)

<center>OR</center>

1. Click __Start__, click __All Programs__, and then click __Accessories__ or type __cmd__ in the Search box.
2. Right-click __Command prompt__, and then click __Run as administrator__.



#### __3. Run chkdsk on cmd.__

* Now on the cmd, you need to __run chkdsk on your affected drive__ to repair the errors. Run the following command (if you want to run check C: Drive)

```bash
chkdsk /f C:
```
This will check the C: drive for errors and fix them if detected.

* Alternatively, you can also type:

```bash
chkdsk /r C:
```
This will check the C: drive for errors, and automatically recover the readable data from the bad sectors that the drive may contain.

I hope this will solve your problem, __"This location could not be displayed" and input/output error__ on Ubuntu, if not then comment below for further discussions.

<h3>Useful Link(s):</h3>

* A complete guide on chkdsk can be found [here.](https://neosmart.net/wiki/chkdsk/)

Thank you for reading.