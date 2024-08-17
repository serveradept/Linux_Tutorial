### How To Add Swap Space on Ubuntu 20.04

- To Get Access via SSH
```sh
Syntax:- ssh -p PORT USERNAME@HOSTIP
Example:- ssh -p 22 serveradept@198.128.0.1
```
- Step 1 – Checking the System for Swap Information
```sh
sudo swapon --show
free -h
```
- Step 2 – Checking Available Space on the Hard Drive Partition
```sh
df -h
```
- Step 3 – Creating a Swap File
```sh
sudo fallocate -l 2G /swapfile
```
- We can verify that the correct amount of space was reserved by typing:
```sh
ls -lh /swapfile
```
- Step 4 – Enabling the Swap File
```sh
sudo chmod 600 /swapfile
```
- Verify the permissions change by typing:
```sh
ls -lh /swapfile
```
- We can now mark the file as swap space by typing:
```sh
sudo swapon /swapfile
sudo swapon --show
free -h
```
- Step 5 – Making the Swap File Permanent
```sh
Back up the /etc/fstab file in case anything goes wrong:
sudo cp /etc/fstab /etc/fstab.bak
Add the swap file information to the end of your /etc/fstab file by typing:
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```
- Step 6 – Tuning your Swap Settings
```sh
We can see the current swappiness value by typing:
cat /proc/sys/vm/swappiness
Output: 60
We can set the swappiness to a different value by using the sysctl command.
For instance, to set the swappiness to 10, we could type:
sudo sysctl vm.swappiness=10
Output: vm.swappiness = 10
This setting will persist until the next reboot. We can set this value automatically at restart by adding the line to our /etc/sysctl.conf file:
sudo nano /etc/sysctl.conf
At the bottom, you can add:
vm.swappiness=10
```
- Adjusting the Cache Pressure Setting
```sh
cat /proc/sys/vm/vfs_cache_pressure
Output: 100
We can set this to a more conservative setting like 50 by typing:
sudo sysctl vm.vfs_cache_pressure=50
Output: vm.vfs_cache_pressure = 50
We can change that by adding it to our configuration file like we did with our swappiness setting:
sudo nano /etc/sysctl.conf
At the bottom, add the line that specifies your new value:
vm.vfs_cache_pressure=50
```
### Save and close the file when you are finished.
