# Install OWFS for use with i2c
This is installaation notes are written as a reminder for my own use. But you are of course free to use my notes at our own risk. There are plenty of tutorials out there but not all of them worked for me.  
The one that I used you can find at: https://www.embeddedpi.com/documentation/isolated-1wire/mypi-industrial-raspberry-pi-1-wire-card-configuration  

### Steps to install and get owfs up and running
Make sure you have i2c sorted out on your device. I used a raspberry pi and acitivated 1-wire and I2C in raspi-config.

#### Install owfs
This installs ofws, owfs-server and the owfs shell commands. The owfs shell is very usefull for debugging.
```
sudo apt install owfs owfs-shell
```

#### Configure owfs  
Open /etc/owfs.conf in editor of your choice.
```
sudo vim /etc/owfs.conf
```
Comment out the line "server: FAKE = DS18S20,DS240"  
Add:
```
server: i2c = ALL:ALL
```
If you want to auto mount the ow filesystem you should uncomment the lines  
"mountpoint = /mnt/1wire"  
"allow_other"
Create the folder:
```
sudo mkdir /mnt/1wire
```

Save the owfs.config file and reboot. Now ofws should be up and runnning. To veryfi this you can use owfs shell commands:  
Use owdir to see your connected 1-wire devices.
```
owdir
```
In my case this is the output:  
/28.97457A060000  
/28.EFAF84050000  
/bus.0  
/uncached  
/settings  
/system  
/statistics  
/structure  
/simultaneous  
/alarm  
  
The temperature sensors I have installed starts with 28. so everything is up and running.  
If you automounted the owfs filessystem you should find the files under /mnt/1wire  


