# Free TPU OS  
Free TPU OS is linux system running on the zyqn-7000 FPGA.Users can run the Free TPU BIN on the system  
* [Getting start](#start)
* [Copy OS](#OS)
* [Run the system](#system)
* [Appendix-PS configuration](#appendix)

<a name="start"></a>

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
* Change a partition's system id   
*Enter "t" -> "c"*  
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_boott.png) 
* Create root partition  
*Enter "n" -> all default*  
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_rootfsn.png) 
* Finish the partition  
*Enter "w"*  
![](https://github.com/embedeep/Free-TPU-OS/blob/master/images/fdisk_f.png)
* Format the partition  
*mkfs.vfat -F 32 -s 2 -n boot /dev/sdc1*  
*mkfs.ext4 -L root /dev/sdc2*  

<a name="OS"></a>

## 2. Copy OS

* Download [boot](https://github.com/embedeep/Free-TPU)  
*git clone https://github.com/embedeep/Free-TPU  
* Download [rootfs](https://github.com/embedeep/Free-TPU-OS)  
*git clone https://github.com/embedeep/Free-TPU-OS*  
*User can open URL in the rootfs/baidu_disk.txt, and download the root file system from Baidu Drive. Otherwise, download the rootfs from Google Drive by open URL in the rootfs/google_drive.txt.*  
* mount SD-card, then untar the rootfs to the rootfs partition(/dev/sdc2), and cp boot files to boot patition.  
  *mkdir rootfs && mount /dev/sdc2 rootfs*  
  *cd Ubuntu && cat xxxxx.gz\* > xxxxx.tar.gz && tar xzf xxxxx.tar.gz -C rootfs*  
  *mkdir boot && mount /dev/sdc1 boot*  
  *cp bootfiles boot*  
  *umount boot rootfs*
* (optional) Copy free-TPU bin to rootfs  
*cp binfiles rootfs/home/linaro*

<a name="system"></a>

## 3. Run the system

Prepare The development board, and set board boot from SD-card. Then insert the SD-card, start the system.  

### 3.1 Connect UART
Connect the UART to your PC, and open the serial Terminal([putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html "Download putty"), or the other serial terminals). Set the baudrate to 115200, then power-on the board.
### 3.2 Configure network
Make sure the network cable inserted. Based on step 3.1, on the serial terminal Enter:  
*ifconfig #check the network*  
or configure the network:  
*ifconfig eth0 xxx.xxx.xxx.xxx*  
*ifconfig eth0 up*

### 3.3 Connect SSH and upload bin  
As above, user can copy execution bins to rootfs, and run the EEP-program on the serial terminal. Alternative, user can connect the system running on the board with SSH:  
*ssh username@xxx.xxx.xxx.xxx(ipaddr)*  
Login in SSH, user can upload the bin and execute it on the SSH terminal.  

<a name="appendix"></a>

# Appendix-PS configuration     

Board|ZC702|Zedboard
:---:|:---:|:---:
FPGA|XC7Z020-CLG484-1|XC7Z020-CLG484-1
PS-FREQ|666.66MHz|666.66MHz
PS-SPI 0|No|No
PS-SPI 0|No|No
PS-I2C 0|Yes|No
PS-I2C 1|No|No
PS-CAN 0|Yes|No
PS-CAN 1|No|No
PS-UART 0|No|No
PS-UART 1|Yes|Yes
PS-GPIO|Yes|Yes
PS-SD 0|Yes|No
PS-SD 1|No|No
PS-USB 0|Yes|Yes
PS-USB 1|No|No
PS-ENET 0|Yes|Yes
PS-ENET 1|No|No
PS-SRAM/NOR|No|No
PS-NAND|No|No
PS-QSPI|Yes|Yes
Memory Part|MT41J256M8 HX-15E|MT41J128M16 HA-15E  

**Note**: Yes indicates APU configured with the peripheral; No indicates APU configured without the peripheral.