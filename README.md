# Luciphone2

## Installation :

on a raspbian minimal image

- Login as root
```
sudo -i
```
- Install dependencies
```
sudo apt-get install policykit-1, python-pymedia
```
- Install [PhatDac sound card](https://learn.pimoroni.com/tutorial/phat/raspberry-pi-phat-dac-install)
```
curl -sS get.pimoroni.com/phatdac | bash
```
  
- Allow user pi to shutdown
```
nano /etc/polkit-1/localauthority/50-local.d/all_all_users_to_shutdown_reboot.pkla 
```  
copy with the following content:

```
[Allow all users to shutdown and reboot]
Identity=unix-user:*
Action=org.freedesktop.login1.power-off;org.freedesktop.login1.power-off-multiple-sessions;org.freedesktop.login1.reboot;org.freedesktop.login1.reboot-multiple-sessions
ResultAny=yes
```

- Enable multi_gadget
    
edit etc/modules and add at the end

```
dwc2
g_multi
```
    
   create a file /etc/modprobe.d/multigadget.conf (or whatever before .conf) with this

```
options g_multi file=/dev/mmcblk0p4 stall=0 host_addr=36:0b:5c:23:ce:31
```
    

add shared partition in readonly in fstab

```
sudo losetup /dev/loop8 /dev/mmcblk0p4
fdisk -l
...
Disk /dev/loop8: 10.4 GiB, 11195645952 bytes, 21866496 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xc408fa62

Device Boot Start End Sectors Size Id Type
/dev/loop8p1 2048 21862399 21860352 10.4G c W95 FAT32 (LBA)
```

offset = start offset * 512 
2048 * 512 = 1048576
add this line to fstab

```
/dev/mmcblk0p4  /mnt/share      vfat    ro,loop,offset=1048576   0       0
```

- Enable serial for debugging

```
sudo systemctl enable getty@ttyGS0.service
````

- Disable networkink

```
sudo systemctl disable dhcpcd.service
sudo systemctl disable network.service

```
