6.1 Open user settings file
$ nano ~/.bashrc

6.2 Add line to .bashrc file

echo Hello, $USER!

6.3 Check how it works
$ bash

6.4 Exit from this session
$ exit

6* How to resize your virtual hard disk?

7. Create and mount new hard drive. Set auto-mounting in fstab.
7.1 Power down the VM. (Do not close it by saving the state—it must be powered down).
$ sudo shutdown now

7.2 In the VirtualBox Settings window, click the Storage section.
7.3 Under the Storage tree click Controller: SATA and then, near the bottom click the Add Disk button (the green plus sign over the floppy icon),
and select Add Hard Disk.
7.4 In the popup window, click Create New Disk and walk through the Create Virtual Hard Disk wizard: Select VDI,
either Dynamically Allocated or Fixed Size, Name, and (if dynamic) size of the disk, and click Create.
You should have a new, unformatted drive attached to your VM
7.5 Click OK to close out the Settings window and fire up your VM.

7.6 Check which hard drives you have
$ sudo fdisk -l

7.7 Partion the new disk using the following command:
$ sudo cfdisk /dev/sdb

Select gpt option.
New >
Enter (Size) >
Write > yes > Quit

7.8 Format the new disk using the ext4 filessystem
$ sudo mkfs.ext4 /dev/sdb1

7.9 Mounting drive to a new folder
$ sudo mkdir /disk2
$ sudo mount -t ext4 /dev/sdb1 /disk2

7.10 Add the new drive to fstab so that it will automatically mount when we reboot the machine.
Add the following line to your fstab file
$ sudo nano /etc/fstab

/dev/sdb1 /disk2 ext4 defaults,errors=remount-ro 0 2

7.11 Reboot and check is it works.
$ sudo reboot now
$ df -h

7* Change fstab to mount /dev/sdb1 with write permissions, not with read-only.
