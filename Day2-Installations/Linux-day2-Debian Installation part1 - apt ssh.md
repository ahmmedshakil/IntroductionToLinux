1. Debian installation
1.1 Create virtual machine
1.2 Download iso image
    (https://cdimage.debian.org/debian-cd/current/i386/iso-cd/debian-9.5.0-i386-netinst.iso)

1.3. Installation with step-by-step description
Select "Install", it is faster than "Graphical install".

On "Software selection:" screen, select only:
* standard system utilities 

Install the GRUB boot loader on a hard disk: Yes

1.4 Если кириллические символы не отображаются
https://mnorin.com/console-cyrillic-i-systemd-v-debian.html

2. Add current user to sudoers
2.1 Login as root
$ su 

2.2 Install sudo package
# apt-get install sudo

2.3 Open sudo config file
# nano /etc/sudoers

2.4 Add line:
debian	ALL=(ALL:ALL) ALL

where "debian" - your not-root user name. Close and save file.

2.5 Check is sudo command works

# exit
$ sudo apt-get update

3. Update apt-get sources settings.
3.1 Open apt sources settings file

$ sudo nano /etc/apt/sources.list

And add following lines, replace existing lines to avoid conflicts.

====
deb http://mirror.yandex.ru/debian/ stretch main contrib non-free
deb-src http://mirror.yandex.ru/debian/ stretch main contrib non-free

deb http://security.debian.org/ stretch/updates main
deb-src http://security.debian.org/ stretch/updates main

deb http://mirror.yandex.ru/debian/ stretch-updates main contrib non-free
deb-src http://mirror.yandex.ru/debian/ stretch-updates main contrib non-free

===

3.2 Update system source-list

$ sudo apt-get update

4. Install Midnight Commander file manager
4.1 Run

$ sudo apt-get install mc

4.2 Check what Midnight Commander allows to do.

5. Install SSH-server
5.1 Run

$ sudo apt-get install ssh

5.2 Hide it from crackers
$ sudo nano /etc/ssh/sshd_config

5.3 Find commented line:
# Port 22

change it to 
Port 2222

5.4 Restart ssh server
$ sudo service ssh restart

5.5 Try to connect to your ssh-server on guest-machine from host-machine.
5.5.1 Determine your guest machine ip

$ ip address

5.5.2 Change guest machine Network adapter setup to "Bridge".
5.5.3 Restart guest vm machine
$ sudo reboot now

5.5.4 Download and run putty ssh-client for Windows (https://the.earth.li/~sgtatham/putty/latest/w32/putty.exe)

5.5.5 Enter vm machine ip addres and ssh port into putty window. Connect.

5.5.6 Try to download and run WinSCP ssh-client for Windows (https://winscp.net/download/WinSCP-5.11.2-Portable.zip)

5.5.7 Enter vm machine ip addres and ssh port into WinSCP window. Connect.

