# Free TPU OS  
Free TPU OS is linux system running on the zyqn-7000 FPGA.Users can run the Free TPU BIN on the system
# Getting start
## 1. Prepare SD-card
Format the SD-card into two partitions-one for root file system(rootfs), the other one for boot. Skip this step, if you have format the SD-card. Otherwise, do as following(run as a root):  
* check SD-card partition(Mine is /dev/sdc)  
*fdisk -l*   
![](https://github.com/embedeep/Free-TPU-OS/tree/master/images/fdisk_l.png)  
* Partition  
*fdisk /dev/sdc  
![](https://github.com/embedeep/Free-TPU-OS/tree/master/images/fdisk_sdc.png)  



## 2. Copy OS
* Download [rootfs](https://github.com/embedeep/Free-TPU-OS)  
  *git clone https://github.com/embedeep/Free-TPU-OS*    
* mount SD-card, and untar the rootfs to the rootfs partition(/dev/xxx)  
  *mkdir rootfs && mount /dev/xxx rootfs*  
  *cd Ubuntu && cat rootfs_ubuntu16.\* > rootfs_ubuntu16.tar.gz && tar xzf rootfs_ubuntu16.tar.gz -C rootfs*
