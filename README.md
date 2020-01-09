# I.MX6U
这是我学习正点原子I.MX6U开发板的过程记录、学习笔记等内容。


如果使用putty登录linux命令行，如下命令如果放入脚本则需要在一行内完成，否则报错。
1、Linux主机间传递文件、文件夹
	文件夹： scp -r dog root@192.168.2.21:/home/root
	文  件： scp main.c root@192.168.2.21:/home/root
	
2、Linux终端连接远程主机ssh
	ssh -l 用户名 192.168.2.21
	ssh  用户名@192.268.2.21
	
3、交叉编译
	/usr/bin/arm-linux-gnueabihf-gcc-7 -o main main.c
	
4、加入启动
      /etc/rc.local

5、使用usb摄像头录制视频
	gst-launch-1.0 -vvv -e v4l2src num-buffers=1000 device=/dev/video2 ! image/jpeg,width=640,heigh=480,framerate=30/1,rate=30 ! matroskamux ! filesink location=video.mkv
	
6、使用usb摄像头拍照
	gst-launch-1.0 imxv4l2src num-buffers=1 device=/dev/video2 ! jpegenc ! filesink location=picture.jpg
	gst-launch-1.0 imxv4l2src num-buffers=1 device=/dev/video2 ! jpegenc ! filesink location=pn.jpg
	
7、i.MxLL Arm开发板的开发结构
	1、裸机开发：将该核心板当作一个高级单片机，无任何操作系统，采用寄存器控制技术，利用“汇编语言”、“C语言”、“SDK”等方式对该核心板进行编程，编译并链接成功后，将文件烧录至核心板内，启动加电后，该核心板只运行这一种程序。
	2、Linux操作系统编程：在上位机上采用“C语言”编写相应的程序，然后采用交叉编译器，将源文件“编译”并“链接”成ARM下的可执行文件，然后使用Putty等支持SSH协议的软件将该文件传入Linux开发板内，采用“./文件名”在Linux操作系统下运行。
8、使用USB WIFI模块上网
        a、搜索wifi 
               wpa_cli -I wlan0 scan_result  
        b、加入指定wifi
               source ./alientek_usb_wifi_setup.sh -m station -i SSID -p PASSWORD -d wlan0
        c、获取dhcp ip（如果已经有了ip可忽略）
		udhcpc -I wlan0
9、终端解压缩
	.tar.gz     格式解压为          tar   -zxvf   xx.tar.gz
	.tar.bz2   格式解压为          tar   -jxvf    xx.tar.bz2

10、编译ARM Linux驱动
		a. 先取得arm-linux-gnueabihf-gcc (交叉编译器)
		创建/usr/local/arm （标准arm交叉编译目录）
		通常 sudo tar -vxf gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf.tar.xz 解压到/usr/local/arm中
		b. 修改环境变量
		sudo nano /etc/profile
		最后加入：
		export PATH=$PATH:/usr/local/arm/gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf/bin
		c. 重新启动Ubuntu。
		d. arm-linux-gnueabihf-gcc -v （查看编译器版本信息）
		e. 在/home/wbx/linux/IMX6ULL/linux/temp下放置linux-imx-rel_imx_4.1.15_2.1.0_ga_alientek.tar.bz2并解压
		
		f. 在程序里使用make进行编译
		
