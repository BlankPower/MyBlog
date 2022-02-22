---
layout: post
title:  "Setup your WSL"
date:   2021-09-20 21:10:00 +0800
category: Linux
---

首先参照微软的[WSL2安装教程](https://docs.microsoft.com/en-us/windows/wsl/install-win10)进行安装，具体的步骤就不细说了。

WSL2与WSL1最大的不同之处在于它是一个独立运行在Hyper-V上的操作系统，可以视作是与Windows同级的在同一个局域网上的另外一台机器。但是这种设计导致WSL2在目前的版本还存在着一些网络连接方面的问题：比如一个部署在WSL上的网页，想要从windows端访问的话是无法直接使用localhost来访问的，需要使用WSL在局域网上的地址才可以访问。

同时如果想要从WSL端使用windows端的代理，可以设置如下的代理：

{% highlight bash %}
function proxy_set() {
    export hostip=$(cat /etc/resolv.conf |grep -m1 -oP '(?<=nameserver\ ).*');
    export http_proxy="http://${hostip}:7890";
    export https_proxy="http://${hostip}:7890";
    export all_proxy="http://${hostip}:7891";
    curl myip.ipip.net;
    echo "proxy set.";
}
{% endhighlight %}

这里假定windows端的clash已开启局域网代理（LAN）并且转发端口为7890。首先使用 `cat /etc/resolv.conf` 获取windows端(host)的IP地址，然后设置`http`、`https`等转发。其他具体的一些网络上的操作比如从windows端访问WSL的网络应用可以参照[微软WSL2的文档](https://docs.microsoft.com/en-us/windows/wsl/compare-versions)。

另外推荐使用 `Windows Terminal` 作为WSL2的终端，界面和字体都比较好看，可以选择在WSL、powershell、cmd之间切换。接下来的一篇会介绍 `zsh` 和 `oh-my-zsh`以及`vim`的一些设置。

2022-2-22 更新：
wsl在电脑上运行有vpn或者游戏加速器等软件时可能会报错：“参考的对象类型不支持尝试的操作。（The attempted operation is not supported for the type of object referenced.）”。解决方法可以参考[使用NoLsp](https://github.com/microsoft/WSL/issues/4177#issuecomment-597736482)。下载NoLsp后使用管理员权限运行NoLsp.exe，并指定wsl的绝对路径即可解决问题。

> 如果Winsock LSP DLL被加载到其进程中，则wsl.exe将显示此错误。最简单的解决方案是对wsl.exe使用WSCSetApplicationCategory WinAPI调用来防止这种情况。在后台，该调用在HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WinSock2\Parameters\AppId_Catalog中为wsl.exe创建一个条目。这将告诉Windows不要将LSP DLL加载到wsl.exe进程中。

wsl的绝对路径可以通过命令`Get-Command wsl.exe`

> NoLsp.exe C:\Windows\System32\wsl.exe
