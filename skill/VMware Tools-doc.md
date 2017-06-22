## VMwareTools导入

* 1、点击VMware菜单栏的VM选项
* 2、点击下拉菜单中的Install vmware tools
* 3、如果提示不成功，点击右下角的小光盘，点击settings
* 4、进入新页面选择ISO
* 5、找到VMwareTools
* 6、选择linuxISO的路径，进行导入
* 7、进入目录cd /media/linux
* 8、进入目录cd VMware\Tools/
* 9、查看当前目录 ls ,找到tar.gz压缩文件，进行复制：cp VMwareTools-9.2.0-799703.tar.gz ~/
* 10、pwd查看当前用户目录，如果不是在/home/linux下，进入目录cd /home/linux，用ls查看是否复制成功
* 11、tar xvf进行解压
* 12、cd VMware-tools-distrib/
* 13、进行安装：sudo ./vmware-install.pl
