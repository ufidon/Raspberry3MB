# Raspberry3MB
玩转草莓派3 模型B 1.2版

## 启动
### 经济型配置:
* 草莓派3 模型B 1.2版 板子一块
* 网线及其自带USB线各一根
* 笔记本一台, 系统Ubuntu 16.04
* 路由器一个
* eSecure All-in-One USB读卡器一个

### 烧制Miro SD卡(TF卡):
参考链接:

* http://elinux.org/RPi_Easy_SD_Card_Setup#SD_card_setup
* https://www.raspberrypi.org/documentation/installation/installing-images/linux.md
* https://www.raspberrypi.org/blog/a-security-update-for-raspbian-pixel/

操作步骤:

	1. 从 https://www.raspberrypi.org/downloads/raspbian/ 下载 Raspbian Jessie with PIXEL
	2. 检查文件校验和: $ sha1sum ./2016-11-25-raspbian-jessie.zip 
			6587483c9b90b11185e2ce99175e27fe75af1f61  ./2016-11-25-raspbian-jessie.zip
	3. 解压镜像文件: 7z x 2016-11-25-raspbian-jessie.zip
	4. 运行 df -h 查看当前挂载的块设备
	5. 把带TF卡的读卡器插入电脑, 再次运行df -h, 新增的块设备即属于TF卡(名称可能不一样)
	6. 卸载TF卡分区: sudo umount /dev/sdb
	7. 烧制映像文件: sudo dd bs=4M status=progress if=./2016-11-25-raspbian-jessie.img of=/dev/sdb
	8. 清缓存: sudo sync
	9. 运行df -h 可以看到TF卡被分成了两个区,一个引导区,一个根分区
	10. 在引导分区上增加一个名字为ssh的空白文件以使能ssh服务
	11. 取出 TF 卡插入草莓派3板子
	
### 启动并登录草莓派

参考链接:

* https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md

操作步骤:

	1. 插上USB线给草莓派供电并用网络连接路由器
	2. 运行 sudo nmap -sn 192.168.1.0/24 找到草莓派的IP
	Nmap scan report for 192.168.1.16
	Host is up (0.0011s latency).
	MAC Address: B8:27:EB:A8:45:1C (Raspberry Pi Foundation)
	3. 登录草莓派: ssh -Y pi@192.168.1.16 默认密码: raspberry
