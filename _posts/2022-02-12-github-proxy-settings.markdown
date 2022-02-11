---
layout: post
title: "Setup Github Proxy"
date: 2022-02-12 00:13:00 +0800
catagory: Linux, Setup
---
{% highlight bash %}
Host github.com
    HostName github.com
    User git
    ProxyCommand nc -X connect -x {Proxy Host}:{Proxy Port} %h %p
{% endhighlight %}

{% highlight bash %}
# only github
git config --global http.https://github.com.proxy http://{Proxy Host}:{Proxy Port}
# unset proxy
git config --global --unset http.https://github.com.proxy
{% endhighlight %}