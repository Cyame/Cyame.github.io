# 字幕组文件服务系统搭建指南

*开幕感谢技术支持无敌小火龙晨轩° 救Nginx苦手的菜菜我于水火之中*

> ## 前言
>
> 本指南将尽可能详细地指导小白进行文件服务系统的搭建，并最终可以实现/学会以下内容：
>
> - 基于[OLAINDEX](https://olaindex.js.org/)的下载盘
> - 基于[Cloudreve](https://cloudreve.org/)的开源自建共享网盘
> - 基于[OneInStack](https://oneinstack.com/)的快速网站搭建
> - 基于[YouTube-DL](https://github.com/ytdl-org/youtube-dl)与[OneDriveUploader](https://github.com/MoeClub/OneList)的服务器扒源流程
>
> 在阅读本指南之前，你需要具备以下基础：
>
> - Linux系统基础操作
>   - 基础文件指令
>   - VIM文本编辑
>   - APT包管理(推荐使用Ubuntu16.04+)
> - 一颗肯折腾、愿意不断学习和修复错误的心
>
> 这些服务虽然是免费开源的，但服务器却不是。因此你还需要具备以下资源：
>
> - 一台海外网络服务器
>
>   - 价格：$20-100不等/年
>   - 推荐服务提供商：[搬瓦工](https://bandwagonhost.com/)
>
> - 一个域名
>
>   - 价格：¥10-100不等/年
>   - 推荐服务提供商：[GoDaddy](godaddy.com)
>
> - 一个OneDrive(Microsoft Office 365)账号
>
>   *强烈推荐世纪互联版，在大陆地区下行可以跑满，其他亚洲区也可以稳定使用*
>
>   - 价格：¥500左右/永久
>   - 推荐购买渠道：某宝
>
>   *一定要问清楚卖家是否支持OneIndex等使用API的服务，买错了可能会导致无法正常配置而吃瘪*
>
>   *（不要贪便宜去买低价黑卡，产品介绍里可能写不支持，最好能和客服提前交流）*
>
> 
>
> ​		**如果你不使用世纪互联版，一是可以使用学生信息去注册(似乎会获得5T免费空间)，二是也可以直接去购买国际版账号。**
>
> ​		**当然个人版也是极好的！**（但是本文中许多操作都是为了使用世纪互联而去做的，如果使用国际版的话，可以使用被更广泛使用的OneIndex来替代OLAINDEX，部署方法/步骤更简单（可以参见其他教程）。
>
> - *<del>一个梯子</del>*
> - <del>一台网速尚可的个人电脑</del>
> - 一个SSH链接工具
>   - 价格：免费/<del>有一些付费的但没必要</del>
>   - 推荐软件：MobaXTerm(Windows)/Terminus(Mac)
>
> 当然，你可以先阅读本指南了解全部流程后再决定是否购入。关于VPS服务器等一系列资源，网上都有各类充分详尽的教程，因此如何配置DNS解析，如何做CDN，如何购买服务器刷系统、备份镜像等内容不会再本指南中过度展开。
>
> 上述推荐服务商仅为本教程所使用的服务商，目前已稳定运行半年以上，**本身不存在推广**<del>没有恰饭</del>。如果不想对比其他教程使用其他服务商，想阅读本指南一步到位，那还请使用相似的系统方便操作。
>
> ## 敬告
>
> 由于网络服务商/域名提供商/(尤其是)网盘存储提供商可能存在跑路情况(泥给路达哟.gif) 本指南不会对所推荐网络服务的稳定性进行任何承诺和担保！如出现任何情况，请自行妥善处理！<del>域名过期了换个域名和SSL证书，服务器跑路了推倒重来一遍，网盘跑路了...wdnmd文件都没了，那还是看情况找个NAS或者稳定的云服务器服务就好；当然有能力维权的话也请维护自己正当权利！</del>
>
> 本指南所涉及内容均为爱好者自建行为，未参考地方法律相关条款。请不要使用本服务进行违法犯罪活动（商业行为请自行确认并依法备案），所产生的法律风险本文作者概不负责。
>
> 本指南遵循MIT License，保留署名权。禁止一切未标明出处和作者的转载，对于侵权行为保留一切法律追责权利。请周知！

# 环境配置

*请确认您已具备前文中所需条件方可开始操作*

## 配置DNS解析

与其他的教程不同，我推荐先进行DNS解析的配置（主要原因在于解析的生效需要一段时间。虽然GoDaddy生效较快，基本2-5分钟就可以，但不同的域名服务商生效时间不同，可能需要30分钟甚至更长时间）。

#### 购买域名

- 注册一个账户（记得配置一个有效邮箱方便找回）

- 点击**域名注册**

  ![image-20200825143008462](https://i.loli.net/2020/08/25/kmqMTXZ4jsghSwI.png)

- 搜索想要的域名（无需后缀）

  例如搜索**myddsite**，得到以下结果：![image-20200825143138087](https://i.loli.net/2020/08/25/VrU3M4P6fpAOzNm.png)一般选择最便宜的即可（`.xyz`的域名通常最便宜，如果没有什么刚需建议找价格合适的就可，解析速度体感上区别不大）

- 付款（支持支付宝）

  之后加入购物车进行购买即可，选择一年即可。

  ![image-20200825143534573](https://i.loli.net/2020/08/25/Ci6Jme4kEQotuxn.png)

  *注意：可能会有绑定一些安全服务或者建站服务，这里完全不需要，可以直接取消掉...一般来说只要域名够长，最多30块钱以内就可以搞定。*

  ![image-20200825143631577](https://i.loli.net/2020/08/25/BUnToR13eVhgabI.png)

  确认无误后点击**结账**即可，支持支付宝！

  *（当然这个我没买，所以之后的域名会部分打码，请理解！）*

#### 打开DNS解析配置页

登录后点击右上角的用户名，从下拉菜单中打开**我的产品**。

![image-20200825143850580](https://i.loli.net/2020/08/25/ovtKRirWPCxMZAc.png)

可以看到自己所购买的域名：

![image-20200825144019224](https://i.loli.net/2020/08/25/zYZuVkWBI5RtL8e.png)

点击**DNS**，进入DNS配置界面：

![image-20200825144244812](https://i.loli.net/2020/08/25/XwQKxcb87WOYVL5.png)

#### 配置A域名解析

DNS解析记录我们需要了解两种即可：CNAME和A。

- A是名访问，即给服务器的IP地址**命名**。图中@即是指，如果直接在浏览器中输入**myddpoint.xyz**的话，会请求**值**中的IP。

- CNAME有点类似于重定向，是使用一个域名指向另一个域名的方法。图中的www指的是，访问**www.myddpoint.xyz**与**myddpoint.xyz**是等价的（会指向**myddpoint.xyz**）。

因此我们可以点击右下角的添加，添加一个A类型的解析：

![image-20200825145410566](https://i.loli.net/2020/08/25/147ioSKGzfsQqdH.png)

主机即为**名称**，或者可以成为**次级域名**；**指向**即为服务主机(的IP)。

例：假设这里主机填写be，指向填写2.3.4.5。那么当我们在浏览器中访问**be.myddpoint.xyz**时，会访问2.3.4.5的80端口(HTTP)或者443端口(HTTPS)，具体取决于后文中是否配置了SSL证书以及NGINX配置。这里我们可以模糊地理解为*给2.3.4.5起名为**be.myddpoint.xyz**。*

在这里，你需要申请两个次级域名，分别对应上述**OLAINDEX**和**Cloudreve**的服务。

## 初始化服务器环境

### 购买服务器

### 重建系统

### 使用SSH连接

### 更新APT镜像

在控制台中运行

```shell
apt update
```

### 运行一键安装脚本

*请按顺序进行运行，有部分软件依赖由前一步携带安装*

- 安装YouTube-DL和OneDriveUploader

  ```shell
apt install curl
  ```
  
  ```shell
curl https://raw.githubusercontent.com/lovezzzxxx/liverecord/master/install.sh | bash
  ```
  
  ```shell
source ~/.bashrc
  ```
  
- 下载Cloudreve服务

  请下载到非/root/(~)目录下，并在下载解压后使用`chmod +777 <解压可执行文件>`进行授权。

  ```
  
  ```

- 下载OLAINDEX服务

  请下载到非/root/(~)目录下，并在下载解压后使用`chmod +777 <解压文件夹>`进行授权。

  ```
  
  ```

- 一键NGINX+PHP脚本（来自ONEINSTACK）

  ```shell
  wget -c http://mirrors.linuxeye.com/oneinstack-full.tar.gz && tar xzf oneinstack-full.tar.gz && ./oneinstack/install.sh --nginx_option 1 --php_option 8 --phpcache_option 1 --reboot 
  ```

  运行后会自动断开SSH连接并重启，请稍后

### 安装配置环境&检测

## OneDrive服务搭建

## 启动WEB服务

### 申请SSL证书

使用运行脚本时下载的Oneinstack进行一键SSL申请+配置（默认应该在`~/oneinstack/`）

运行其中的`vhost.sh`

```shell
/root/oneinstack/vhost.sh
```

### 配置NGINX

但是vhost配置的服务是给静态网站使用的，本次需要配置的网站一个为本地服务，另一个为伪静态网站，需要另行配置。

因此在分别添加vhost服务后，需要对`/usr/local/nginx/conf/vhost/`中网站对应服务的配置文件作出修改，在此给出范例：

- OLAINDEX

  ```nginx
  
  ```

- Cloudreve

  ```nginx
  
  ```

### 重启NGINX服务

```shell
service nginx restart
```

## 初始化文件系统

### YouTube-DL + OneDriveUploader

### OLAINDEX

### Cloudreve

## 用户使用指南

