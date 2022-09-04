# kubernetes-on-pi

### Current Hardware Setup
- Raspberry Pi 4 Model B with WiFi and Bluetooth
- 32Gb SD Card

### Exploration 1: Simple Setup of k3s on Single Node Pi
1. Download Raspberry Pi Imager from https://www.raspberrypi.com/software/
2. Flash Raspberry Pi OS Lite 64-bit SD Card
- Remember to set required additional settings to enable WiFi or SSH access
3.  SSH into pi
- pi name: master
- username: joseph
```
ssh joseph@master.local
```
- Key in either password or automatically login using ssh
4. Install k3s
Update & Upgrade apt-get
Also, installed vim
```
sudo apt-get update
sudo apt-get upgrade -y
sudo apt install vim -y
```
Append cgroups config to /boot/cmdline.txt
```
echo " cgroup_memory=1 cgroup_enable=memory" >> /boot/cmdline.txt
```
Reboot Pi
```
sudo reboot
```
After rebooting, install k3s
```
curl -sfL https://get.k3s.io | sh -
```
Test k3s installation
```
sudo kubectl get nodes
```