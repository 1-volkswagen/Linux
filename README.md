# Vcash Install / Update Scripts

## Warning !
Please backup your existing wallet files (~/.Vcash/data/ folder).
I can't be responsible if you break something.

## Requirements

#### GNU/Linux
**GCC/G++ >= 4.8.*** / git / screen / curl. On low-spec hardware, don't forget to increase the swap space (min 1024MB) to avoid 'Virtual memory exhausted: Cannot allocate memory' during the build process.

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

#### Raspbian
Be sure to have enough swap to avoid 'Virtual memory exhausted: Cannot allocate memory'.
Raspbian default swap size is 100MB, please increase the size before building.

Check swap size:
```
free -m
```

Example with 1024MB as swap size:
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

## Install / Update
As user (fresh ssh login as user, not su switch to user from the root account):
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
Ctrl-A Ctrl-D to detach.

## Launch
Be sure there's no vcashd running before !
```
ps x | grep '[v]cashd'
```
To launch:
```
cd ~/vcash/
screen -d -S vcashd -m ./vcashd
```

## Crontab
As user:
Autostart Vcash daemon on reboot with crontab:
```
crontab -e
```
Add this entry (edited with your username):
```
@reboot pgrep vcashd > /dev/null || cd /home/your_username/vcash && screen -d -S vcashd -m ./vcashd
```
Save & check crontab:
```
crontab -l
```
Then do a reboot test.
