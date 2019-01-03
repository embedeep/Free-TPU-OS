# Free TPU OS  
Free TPU OS is linux system running on the zyqn-7000 FPGA.Users can run the Free TPU BIN on the system  
* [Getting start](#Getting)
* [Copy OS](#Copy)
* [Run the system](#Run)
# Getting start
## 1. Prepare SD-card
Format the SD-card into two partitions-one for root file system(rootfs), the other one for boot. Skip this step, if you have format the SD-card. Otherwise, do as following(run as a root):  
* check SD-card partition(Mine is /dev/sdc)  
*fdisk -l*   
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_l.png)  
* Start to partition  
*fdisk /dev/sdc*  
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_sdc.png)  
* Create boot partition  
*Enter "n" -> "p" -> default -> +200M(size of boot partition)*  
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_bootn.png)
* Enable boot partition bootable  
*Enter "a"*    
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_boota.png) 
* Create root partition  
*Enter "n" -> all default*  
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_rootfsn.png) 
* Finish the partition  
*Enter "w"*  
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_f.png)
* Format the partition  
*mkfs.vfat -F 32 -n boot /dev/sdc1*  
*mkfs.ext4 -L root /dev/sdc2*

## 2. Copy OS
* Download [boot](https://github.com/embedeep/Free-TPU)  
*git clone https://github.com/embedeep/Free-TPU  
* Download [rootfs](https://github.com/embedeep/Free-TPU-OS)  
*git clone https://github.com/embedeep/Free-TPU-OS*    
* mount SD-card, then untar the rootfs to the rootfs partition(/dev/sdc2), and cp boot files to boot patition.  
  *mkdir rootfs && mount /dev/sdc2 rootfs*  
  *cd Ubuntu && cat rootfs_ubuntu16.\* > rootfs_ubuntu16.tar.gz && tar xzf rootfs_ubuntu16.tar.gz -C rootfs*  
  *mkdir boot && mount /dev/sdc1 boot*  
  *cp bootfiles boot*  
  *umount boot rootfs*
* (optional) Copy free-TPU bin to rootfs  
*cp binfiles rootfs/home/linaro*
## 3. Run the system
Prepare The development board, and set board boot from SD-card. Then insert the SD-card, start the system.  
### 3.1 Connect UART
Connect the UART to your PC, and open the serial Terminal([putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html "Download putty"), or the other serial terminals). Set the baudrate to 115200, then power-on the board.
### 3.2 Configure network
Make sure the network cable inserted. Based on step 3.1, on the serial terminal Enter:
*ifconfig eth0 xxx.xxx.xxx.xxx*
*ifconfig eth0 up*
### 3.3 Connect ssh and upload bin