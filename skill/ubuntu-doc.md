# ubuntu在VMware下的安装及使用
## ubuntu的下载
### 步骤：
1. 下载ubuntu的镜像到本地,这里给出ubuntu16.04的地址: [下载地址](https://www.ubuntu.com/download/desktop/thank-you?country=CN&version=16.04.2&architecture=amd64)。  
2. 也可以在地址栏输入地址：ubuntu.com,然后点击图片如下：
![](./pic/ubuntu/ubuntu03.png)
选择需要的ubuntu下载即可。  
## ubuntu的安装
1.打开VMware开始安装，点击create a new virtual mechine新建一个虚拟机。  
![](./pic/ubuntu/ubuntu01.png)  
然后在下图的红框里面选择要安装的系统的镜像，即上面下载的ubuntu的镜像。  
![](./pic/ubuntu/ubuntu02.png)    

在安装的时候会问你账户和密码，这里我设置账户为linux，密码为1,，如下图  
![](./pic/ubuntu/ubuntu04.png)     

然后选择需要安装的系统盘即可等待安装完成。  
## ubuntu的使用  
ubuntu属于liunx系统下的一种，所以使用方法与linux系统类似。  
在这里我只例举几个基本的操作：
### 1. 常用指令
* ls　　        显示文件或目录  
     -l           列出文件详细信息l(list)  
     -a          列出当前目录下所有文件及目录，包括隐藏的a(all)  
* mkdir        创建目录  
     -p           创建目录，若无父目录，则创建p(parent)  
* cd               切换目录  
* touch          创建空文件  
* echo            创建带有内容的文件。  
* cat              查看文件内容  
* cp                拷贝  
* mv               移动或重命名  
* rm               删除文件  
     -r            递归删除，可删除子目录及文件  
     -f            强制删除  
* find              在文件系统中搜索某文件  
* wc                统计文本中行数、字数、字符数  
* grep             在文本文件中查找某个字符串  
* rmdir           删除空目录  
* tree             树形结构显示目录，需要安装tree包  
* pwd              显示当前目录  
* ln                  创建链接文件  
* more、less  分页显示文本文件内容  
* head、tail    显示文件头、尾内容  
* ctrl+alt+F1  命令行全屏模式  

### 2.系统管理命令  
* stat              显示指定文件的详细信息，比ls更详细  
* who               显示在线登陆用户  
* whoami          显示当前操作用户  
* hostname      显示主机名  
* uname           显示系统信息  
* top                动态显示当前耗费资源最多进程信息  
* ps                  显示瞬间进程状态 ps -aux  
* du                  查看目录大小 du -h /home带有单位显示目录信息  
* df                  查看磁盘大小 df -h 带有单位显示磁盘信息  
* ifconfig          查看网络情况  
* ping                测试网络连通  
* netstat          显示网络状态信息  
* clear              清屏  
* alias               对命令重命名 如：alias showmeit="ps -aux" ，另外解除使用unaliax showmeit  
* kill                 杀死进程，可以先用ps 或 top命令查看进程的id，然后再用kill命令杀死进程。  

### 3.打包压缩相关命令
* gzip：  
* bzip2：  
* tar:                打包压缩  
     -c              归档文件  
     -x              压缩文件  
     -z              gzip压缩文件  
     -j              bzip2压缩文件  
     -v              显示压缩或解压缩过程 v(view)  
     -f              使用档名  
例：  
> tar -cvf /home/abc.tar /home/abc            只打包，不压缩  
> tar -zcvf /home/abc.tar.gz /home/abc        打包，并用gzip压缩  
> tar -jcvf /home/abc.tar.bz2 /home/abc      打包，并用bzip2压缩  

当然，如果想解压缩，就直接替换上面的命令  tar -cvf  / tar -zcvf  / tar -jcvf 中的“c” 换成“x” 就可以了。  

### 4.关机/重启机器
* shutdown  
     -r             关机重启  
     -h             关机不重启  
     now          立刻关机  
* halt               关机  
* reboot          重启  

 





