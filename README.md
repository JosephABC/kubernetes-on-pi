# kubernetes-on-pi

### Current Hardware Setup
- Raspberry Pi 4 Model B with WiFi and Bluetooth
- 32Gb SD Card

### SetUp 1: Simple Setup of k3s on Single Node Pi
Reference: https://www.youtube.com/watch?v=rOXkutK8ANc
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

### Exploration 1: Nginx pod, exposed with NodePort Service
To Enter sudo mode:
```
sudo -s
```
1. Run nginx pod
```
kubectl run nginx-pod --image nginx
```
2. Expose with node port
```
kubectl expose pod nginx-pod --port=80 --type=NodePort
```
3. Get Node IP and NodePort
```
kubectl get nodes -o wide
kubectl get svc -o wide
```
4. curl nginx-pod
```
curl <node-IP>:<NodePort>
```

### Exploration 2: KRaft Mode Kafka on kubernetes
References:
- https://github.com/IBM/kraft-mode-kafka-on-kubernetes
- https://developer.ibm.com/tutorials/kafka-in-kubernetes/



