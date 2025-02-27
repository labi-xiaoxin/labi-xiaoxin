相信有一部分人会有这样的使用场景：
- `人在公司，家里已加班完成了文档、代码，想连接家里的电脑`
- `人在地铁，项目经理打电话要文件，想连接公司的PC`
- `远程桌面帮女朋友解决一下电脑问题、工作问题`
- `给家里不太会用手机的父母解决手机问题`

等等还有各种需要远程的场景，现如今市面上商业远程桌面较为知名的有：`向日葵`、`ToDesk`、`TeamViewer`。

这三家都使用过，在**产品初期**表现均**还不错**，但随着使用人数的上升，以及商业化的布局，逐渐变得越来越**难以使用**，各式各样的问题让我对这三款产品都逐渐失望。

后来在网上搜索此类软件的平替，了解到了`RustDesk`这个软件，并且发现该软件为***开源项目***，在接触使用后，发现能满足我的使用需求，并且简单、易操作，故作此文以分享。

### 极简使用教程

1. 客户端下载

首先下载官方提供的客户端：[rustdesk官网](https://rustdesk.com/download) 

![官网提供的客户端版本](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502181456803.png)

目前官方提供了近乎全平台的客户端，常见的`Windows、Linux、Mac、Android、iOS`。根据大家的使用需求，下载自己的客户端（**被控端、控制端均需下载**）。

> 请从官方下载客户端！！！避免被植入未知程序
> 
> 提示：iOS可以直接从应用商店下载。Android部分厂商识别为ZP软件，安装时断开网络即可。
>
> 提示：iOS只能作为控制端，无法作为被控制端。

2. 被控制端操作

被控制端需要开启相应的权限，这里我以Android示例，其他平台可以参照官方文档进行。

[Mac平台](https://rustdesk.com/docs/zh-cn/client/mac/)
[Windows平台](https://rustdesk.com/docs/zh-cn/client/windows/)
[Android平台](https://rustdesk.com/docs/zh-cn/client/android/)

进入`共享屏幕`页面，默认`服务未运行`，点击**启动服务**

![共享屏幕](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502191014498.png)

由于该软件是ZP高风险软件，官方会进行防诈提示

![FZ提示](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502191014433.png)

接着会跳到系统页面，勾选`在其他应用上层显示`权限

![权限设置](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502191014793.png)

接着同意系统弹出的权限框，返回应用后，出现如下界面

![设备ID与密码](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502191015610.png)

若允许其他软件控制，则需要`无障碍`->`已安装的服务`->`勾选RustDesk Input`权限

此时，控制端可通过ID+密码进行远程控制

3. 控制端操作

控制端输入被控制端ID+密码，即可建立连接。

![控制端页面](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502181613425.png)

> 由于ZP团伙的猖獗，目前官方公共服务器已屏蔽国内IP。因而国内环境无法直接连接。
>
> 为此，可以使用自建中继服务器，以解决该问题，并且相对公共服务器而已，有较高的**安全性**以及**流畅性**。

### 自建中继服务器

自建中继服务器目的就是**替代原有默认的公共服务器**，控制端与被控制端的数据均通过**中继服务器**进行数据交互。根据官方文档，RustDesk对云服务器的配置要求很低，我使用的是2C2G的云服务器，大家也可以选择更低配置。

> 目前官方提供免费版以及专业版（付费版）,个人使用的话，我觉得免费版就够用了。

目前支持直接通过两种安装方式：`代码包安装`和`Docker安装`，这里介绍`代码包安装`。

1. 下载代码包

[代码包地址](https://github.com/rustdesk/rustdesk-server/releases)

根据中继服务器的系统、硬件情况，下载适用的包。

2. 代码包解压

将下载的代码包解压后，能够发现其中有`hbbr`和`hbbs`两个可执行的文件。

3. pm2运行hbbr和hbbs

pm2是一款进程管理工具，有`进程管理`、`负载均衡`、`日志管理`等功能。只需通过如下两行命令即可实现中继服务器的服务运行：
```
pm2 start hbbs 
pm2 start hbbr 
```

接着可以通过查看日志确认RustDesk的服务是否正常运行
```
pm2 logs hbbs 
pm2 logs hbbr
```

![hbbs运行日志](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502181703747.png)

4. 端口开放

服务成功启动后，需要开放相应的端口以对外提供服务。
官方默认端口如下，21118,21119为网页客户端，不需要可以不开：

- TCP(21115, 21116, 21117, 21118, 21119)
- UDP(21116)

> 云服务器需要开放服务器厂商的防火墙，以及服务器内的防火墙

5. 客户端连接

在客户端的`设置->网络->ID/中继服务器`选项下，有相关中继服务器的配置：

- ID服务器：hbbs所在服务器IP:端口，若无修改端口等情况，无需填写端口
- 中继服务器：hbbr所在服务器IP:端口，若无修改端口等情况，无需填写，RustDesk自动推导
- API服务器：无特殊需求，无需填写
- Key：启动日志内已标红的文本，或是hbbr/hbbs执行目录下，查看id_ed25519.pub获取

 ![Mac客户端连接](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502181709971.png)
 ![Android客户端连接](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502181738101.png)

### 闲谈

由于Mac的分辨率与我Windows的分辨率不同，导致RustDesk的分辨率无论如何调整，都非常模糊。

去看了下RustDesk的工作文档，RustDesk采用的是RFB（Remote Framebuffer）协议实现远程桌面访问的。**RFB协议是一种基于帧缓冲区的远程桌面协议，它允许客户端获取服务器的屏幕内容并进行操作**。下面是官方所绘的图：

![工作流](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502190912559.png)

通俗话讲，RustDesk的实现是通过**截屏**实现，因此不同分辨率下，截屏就会导致模糊等情况。似乎这个模糊已经无法通过RustDesk的设置解决了，但是可以通过XXX（留个悬念）实现。

下面是对比图：

![RFB截图](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502190956886.png)

![RDP截图](https://cdn.jsdelivr.net/gh/labi-xiaoxin/img/202502191011494.png)
