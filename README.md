# Linux

Linux Vcash Install Script :penguin:

## Warning !
Please backup your existing wallet files (~/.Vcash/data/ folder).
I can't be responsible if you break something.

## Requirements

#### GNU / Linux
GCC version **4.8.***. Don't forget to increase the swap space with a minimum of 1024MB to avoid "Virtual memory exhausted: Cannot allocate memory" during the build process on ARM like developer boards or machines with less then X GB of memory.

Note: GCC version 4.9.2 is confirmed to work on a raspberry pi 2/3 running raspbian jessie.

#### Debian / Ubuntu / Raspbian
```
sudo apt-get install build-essential openssl curl git screen wget
```
#### Arch Linux
```
sudo pacman -S base-devel openssl curl git screen wget
```
#### Gentoo
```
sudo emerge --ask openssl curl git screen wget
```

## Swap

#### Raspbian
Be sure to have enough swap space to avoid "Virtual memory exhausted: Cannot allocate memory".

Check swap size:
```
free -m
```

Set 1024MB as swap size:
```
sudo nano /etc/dphys-swapfile
```
Edit the file:
```
CONF_SWAPSIZE=1024
```
Save & restart dphys-swapfile:
```
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```

#### Arch Linux / Gentoo

Create swap file:
```
sudo fallocate -l 1024M /swapfile
```
Set permissions:
```
sudo chmod 600 /swapfile
```
Format to swap:
```
sudo mkswap /swapfile
```
Activate swap file:
```
sudo swapon /swapfile
```
Open fstab in nano:
```
sudo nano /etc/fstab
```
Add the folowing entry:
```
/swapfile none swap defaults 0 0
```
CTRL+X and press Y.

#### Ubuntu / Debian

Create swap file:
```
dd if=/dev/zero of=/path/filename bs=1M count=1024
```
Set permissions:
```
chmod 600 /path/filename
```
Format to swap:
```
mkswap /path/filename
```
Activate the swap file:
```
swapon /path/filename
```
Add this line to /etc/fstab:
```
/path/filename none swap sw 0 0
```

## Install / Update
Run as user (not root).
```
git clone https://github.com/john-connor/vcash-scripts
cd vcash-scripts
./build-linux.sh
```
The script will auto launch vcashd at the end.
Resume the screen session with:
```
screen -x vcashd
```
Press Ctrl-A + D to detach.

Now you can let the blockchain download and sync up.
