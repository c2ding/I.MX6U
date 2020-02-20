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
11、交叉编译命令
	arm-linux-gnueabihf-gcc -v
12、编译内核
		a. make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean
		make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- imx_alientek_emmc_defconfig
		make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-
13、压缩文件（使用tar创建，使用bz2压缩）
	tar -vcjf *.tar.bz2 *.* 
	-c 创建新的压缩文件。
	-C< 目的目录> 切换到指定的目录。
	-f< 备份文件> 指定压缩文件。
	-j 用 tar 生成压缩文件，然后用 bzip2 进行压缩。
	-k 解开备份文件时，不覆盖已有的文件。
	-m 还原文件时，不变更文件的更改时间。
	-r 新增文件到已存在的备份文件的结尾部分。
	-t 列出备份文件内容。
	-v 显示指令执行过程。
	-w 遭遇问题时先询问用户。
	-x 从备份文件中释放文件，也就是解压缩文件。
	-z 用 tar 生成压缩文件，用 gzip 压缩。
	-Z 用 tar 生成压缩文件，用 compress 压缩。
	
14、解压缩文件 
	tar -vxjf *.tar.bz2
15、nano中启用行号
	sudo nano /etc/naorc
	将#set constantshow中的#去掉即可；
	或者linenumber
16、nano 查找文字 ctrl+w
17、安装ssh
		sudo apt-get install openssh-server
18、配置ssh
		/etc/ssh/sshd_config
19、nano 复制粘贴
    ctrl+6 起始
	Alt+6 结尾
	Ctrl+u 粘贴
20、命令行下载
        wget -c https://supernote.com.cn/update/SN100.B000.299_release/update.zip
	Wget -c 下载地址（-c 断点续传）
21、当apt install 提示无法获得锁 /var/lib/dpkg/lock-frontend 和 无法获取dpkg前端锁
       sudo rm /var/lib/dpkg/lock-frontend
22、Ubuntu 中文目录名称如何快速更改为英文
	export LANG=en_US
	xdg-user-dirs-gtk-update
23、swap交换分区通常作为内存不够时使用，一般不超过2GB；
24、给虚拟机扩容后，需要调整Ubuntu的硬盘空间
		a. 安装gparted : sudo apt install gparted
		b. 运行gparted : sudo gparted
		c. 选择并拖动可用空间
		
25、调整开发板的开机启动顺序
		

						
26、压摆率
	    IO 电平跳变所需要的时间,比如从 0 到 1 需要多少时间,时间越小波形就越陡,说明压摆率越高;反之,时间越多波形就越缓,压摆率就越低。如果你的产品要过 EMC 的话那就可以使用小的压摆率,因为波形缓和,如果你当前所使用的 IO做高速通信的话就可以使用高压摆率。

27、IOMUXC_SW_MUX_CTL_PAD_XX_XX 和 IOMUXC_SW_PAD_CTL_PAD_XX_XX
    使用这两组寄存器对IO口进行配置
		IOMUXC_SW_MUX_CTL_PAD_XX_XX 配置当前IO口的复用功能
		IOMUXC_SW_PAD_CTL_PAD_XX_XX 配置当前IO口的速度、上拉、下拉等功能

28、寄存器
	 DR数据寄存器：当配置IO为输出模式时，DR中的32位配置相应IO口为0低电平、1高电平；
	               当配置IO为输入模式时，DR保存对应IO的电平值；
	 GDIR方向寄存器：32个位，对应IO位 0输入、1输出；
	  PSR寄存器与DR输入功能相同，读取相应IO口的高低电平；
	
	
29、IMX6U的每个外设都有时钟，可以关掉相应外设时钟达到省电的目的。
30、安装Linux时交换分区通常是内存的二倍即可。
40、Ubuntu的分区设计
			i. efi分区100mb左右即可；
			ii. swap分区为内存的二倍；
			iii. /根分区安装操作系统，通常最多30GB，此处安装了50GB；
			iv. /home为用户分区，存储用户自己的文档、程序等。
	如上分区方法为了确保数据存储安全，重装系统只需对/根分区重装即可。
	
41、当使用ssh连接Linux时提示has changed 时的解决方法 
	
	Windows:          C:\Users\wbx\.ssh\known_hosts 文件删除指定ip的密钥，然后重新连接
	出现这个问题是因为192.168.0.106之前是开发板的ip，现在是ubuntu PC的ip，所以使用win ssh登录Ubuntu失败；
	
42、安装交叉编译器
	sudo apt install gcc-arm-linux-gnueabihf
	
43、BSP目录结构存储项目文件的Makefile内容讲解在350页里。
	

44、使用Windows通过FTp向Ubuntu发送文件，传到Ubuntu后的中文变成乱码可以采用如下方法解决
		
	强制使用UTF-8编码，即可读出Ubuntu中的中文，也可以传过去中文目录、文件等内容。
	
45、解决Ubuntu无法关机（关机时卡在Logo界面）
    
