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
	
8、Linux中有三大类驱动：
	a.字符设备驱动：字符设备最多，I2C、SPI、音频等；
	b.块设备驱动：EMMC、SD、U盘等；
	c.网络设备驱动：网卡、wifi等。
