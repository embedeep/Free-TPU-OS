# Free TPU OS  
Free TPU OS is linux system running on the zyqn-7000 FPGA.Users can run the Free TPU BIN on the system
# Getting start
## 1. Prepare SD-card
Format the SD-card into two partitions-one for root file system(rootfs), the other one for boot. How to format SD-card, user can refer to [Xilinx-wiki](https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842385/How+to+format+SD+card+for+SD+boot "How+to+format+SD+card+for+SD+boot"). 
## 2. Copy OS
* Download [rootfs](https://github.com/embedeep/Free-TPU-OS/tree/master/Ubuntu)  
  *git clone https://github.com/embedeep/Free-TPU-OS/tree/master/Ubuntu*    
* mount SD-card, and untar the rootfs to the rootfs partition(/dev/xxx)  
  *mkdir rootfs && mount /dev/xxx rootfs*  
  *cd Ubuntu && cat rootfs_ubuntu.\* | args -n tar xzf -C rootfs*
