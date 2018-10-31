### 基于VNCServer+noVNC构建Docker桌面系统
>  资料说明 http://www.voidcn.com/article/p-prehfrox-nz.html
#### VNC (VirtualNetwork Computer)
VNC(Virtual Network Computer)是虚拟网络计算机的缩写。VNC 是一款优秀的远程控制工具软件，由著名的 AT&T的欧洲研究实验室开发的。VNC 是在基于 UNIX和 Linux 操作系统的免费的开源软件，远程控制能力强大，高效实用，其性能可以和 Windows和 MAC 中的任何远程控制软件媲美。 在 Linux 中，VNC 包括以下四个命令：vncserver，vncviewer，vncpasswd，和 vncconnect。大多数情况下用户只需要其中的两个命令：vncserver 和 vncviewer。

VNC基本上是由两部分组成：一部分是客户端的应用程序(vncviewer)；另外一部分是服务器端的应用程序(vncserver)。VNC的基本运行原理和一些Windows下的远程控制软件很相像。VNC的服务器端应用程序在UNIX和Linux操作系统中适应性很强，图形用户界面十分友好，看上去和Windows下的软件界面也很类似。在任何安装了客户端的应用程序(vncviewer)的Linux平台的计算机都能十分方便地和安装了服务器端的应用程序(vncserver)的计算机相互连接。另外，服务器端 (vncserver)还内建了JavaWeb接口，这样用户通过服务器端对其他计算机的操作就能通过Netscape显示出来了，这样的操作过程和显示方式比较直观方便。

同样可能远程连入UNIX、Linux进行图形化操作的还有流行的Xmanager，VNC与之相比——两者工作原理不一样，前者（VNC）是远程连入操作系统，所有操作在UNIX、Linux主机服务端进行，即使操作过程中“本地电脑与操作主机网络断开”，也不影响操作的顺利进行；而后者（Xmanager）是通过端口将主机服务器的UI界面引导到本地电脑进行展现，如操作过程出现“本地电脑与操 作主机网络断开”，操作将中断失败！如果操作中进行的工作任务非常重要，不能中断，如ORACLE RAC实施，结果是灾难性的！

#### noVNC
noVNC提供一种在网页上通过html5的Canvas，访问机器上vncserver提供的vnc服务，需要做tcp到websocket的转化，才能在html5中显示出来。网页就是一个客户端，类似win下面的vncviewer，只是此时填的不是裸露的vnc服务的ip+port，而是由noVNC提供的websockets的代理，在noVNC代理服务器上要配置每个vnc服务，noVNC提供一个标识，去反向代理所配置的vnc服务。

#### 使用过程
> 目前使用的是ubuntu16.04+lxde桌面，直接使用github已经打包好的镜像

容器的使用安按照readme进行，目前发现谷歌浏览器不能使用，只有火狐浏览器可以用，估计是谷歌浏览器需要利用开启声频的启动方式才可以使用

* 安装vscode
```
下载deb包安装失败，提示
Can't run the archiver executable:
Failed to execute child process "ar" (No such file or directory)

# 利用dpkg安装
dpkg -i code_1.28.2-1539735992_amd64-1.deb
```

* 安装搜狗拼音
