# Install proprietary NVIDIA driver on Debian 11
## Shoutout
Go follow these legends, they helped making this guide what it is today

[ichirodev](https://github.com/ichirodev)

[HangedScratcher](https://github.com/HangedScratcher)

## Run nvbase.sh
```
 
```
## The steps (part 1)
Set root password
```
sudo -i
passwd
```
It will ask you to type a new sudo password.

Use root account
```
su
```
OR
```
sudo -i

```
Next use nvidia-detect to find your gpu
```
nvidia-detect
```
First install these packages and build linux depemdecies.
```

sudo dpkg --configure -a
sudo apt install build-essential linux-headers-amd64
sudo apt build-dep linux
```

Download driver from https://www.nvidia.com/object/unix.html
Those who need the legacy driver look for Latest Legacy GPU version.

Disable Nouveau and other drivers that might have conflicts with the installation.
```
echo 'blacklist amd76x_edac' | sudo tee -a /etc/modprobe.d/blacklist.conf
echo 'blacklist vga16fb' | sudo tee -a /etc/modprobe.d/blacklist.conf
echo 'blacklist rivafb' | sudo tee -a /etc/modprobe.d/blacklist.conf
echo 'blacklist rivatv' | sudo tee -a /etc/modprobe.d/blacklist.conf
echo 'blacklist nvidiafb' | sudo tee -a /etc/modprobe.d/blacklist.conf
echo 'blacklist nouveau' | sudo tee -a /etc/modprobe.d/blacklist.conf

```
sudo apt install initramfs-tools
sudo systemctl set-default multi-user.target
```

**NOTE: If it says that it will remove dracut its fine let it remove it**

Use this command next
```
sudo update-initramfs -u
```
if it fails run these commands
```
sudo apt-get autoclean
sudo apt-get clean
sudo apt-get update 
sudo apt-get upgrade
sudo apt-get -f install
sudo dpkg --configure -a
sudo update-initramfs -u
```
Next reboot
```
sudo systemctl reboot
```
## The steps (part 2)
Log in as root with the password we have set up earlier.

Next go to Downloads forlder
```
cd Downloads
```

* Lastly run the installer
```
sudo bash NVIDIA-....run
```

Next select Install and overwrite existing filesort installation.

It should ask you to generate X-org configuration. Accept that too.

If not, run nvidia-xconfig after the installer finishes.

Reenable GUI
```
sudo systemctl set-default graphical.target
``` 
Then reboot.
```
sudo reboot
```
And that's it. You should have succesfully installed the proprietary NVIDIA driver.
