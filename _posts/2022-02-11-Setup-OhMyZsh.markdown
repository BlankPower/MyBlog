---
layout: post
title:  "Setup Oh-My-Zsh"
date:   2022-02-11 13:59:00 +0800
category: Linux, Setup
prevPart: _posts/2021-09-20-setup-your-wsl.markdown
nextPart: _posts/2022-02-12-github-proxy-settings.markdown
---
这篇介绍如何在一台新的机器上设置Oh-My-Zsh，默认操作系统为Linux，并且有sudo权限。

以我在node6为例, 原本已经安装了zsh，如果没有安装则需要通过如下命令安装:
{% highlight bash %}
sudo apt-get update
sudo apt-get install zsh
{% endhighlight %}
之后再安装oh-my-zsh:
{% highlight bash %}
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
{% endhighlight %}

node6由于没有设置代理，在从github下载时出现连接超时的情况，如何解决代理问题将在下一篇blog进行介绍。
下载完成之后，可以根据自己的喜好配置主题，在`~/.zshrc`中找到ZSH_THEME进行修改即可。
{% highlight bash %}
ZSH_THEME="robbyrussell"
{% endhighlight %}
更多的主题可以参见[Themes](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)

另外可以根据自己的需要添加插件，这里推荐以下的几款插件：
* [zsh-history-substring-search](https://github.com/zsh-users/zsh-history-substring-search): 自动匹配历史输入指令
* [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions): 在输入命令的过程中根据你的历史记录显示你可能想要
输入的命令
* [colored-man-pages](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/colored-man-pages): 带颜色的man指令
* [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting): shell命令代码高亮
{% highlight bash %}
plugins=(
        git
        zsh-history-substring-search
        zsh-autosuggestions
        colored-man-pages
        zsh-syntax-highlighting
)
{% endhighlight %}

那么到此为止，oh-my-zsh就设置完成了，主题和插件可以根据个人喜好进行调整~
