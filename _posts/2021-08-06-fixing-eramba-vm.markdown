---
layout: post
title:  Fixing Eramba's Virtual Machine
date:   2021-08-06 08:30:00 +0530
image:  eramba.jpg
tags:   [How-to,Infosec]
---

Recently I was introduced to Eramba during my Information Security & Governance course at my University. Eramba is an Open GRC tool that helps with compliance, risk management, control testing, exception management, etc. We then set up a VM using the Virtual machine builds provided by the official website to act as a server, enabling it to be easily accessible.

After instaliing the Virtual Machine, I noticed that it wasn't able to assign itself an proper IP address and defaulted to using localhost.
This is validated by the fact that ifconfig only shows a loopback address, meaning that no IP has been assigned.

Here are the steps that I took to get it to run properly.

![output](../img/eramba1.png)

### Fixing the Issue

We need to firstly import the VM and make sure that the network adapter is set to briged mode.

* Identify your connected network adapters
{% highlight sh%}
$ ip a
{% endhighlight %}

![output](../img/eramba2.png)

Take note of the network adapter name, in my case it turned out to be enp0s3.

* Set the network adapter to up
{% highlight sh%}
$ sudo ip link set enp0s3 up
{% endhighlight %}
* Find out your IP and netmask

Before proceeding further you need to find out what is the IP and subnet mask of the network you are currently on.

On Linux you can use

{% highlight sh%}
$ ifconfig
{% endhighlight %}

On Windows you can use

{% highlight sh%}
$ ipconfig
{% endhighlight %}

note the IP address, subnet mask and the defaut gateway.

* Assign an ip/mask to the network adapter. Use an available IP in your network and keep the subnet mask same.
{% highlight sh%}
$ sudo ip addr add 192.168.1.7/24 dev enp0s3
{% endhighlight %}
* Set your router as the default gateway. The router is usually the first address in your IP range.
{% highlight sh%}
$ sudo route add default gw 192.168.1.1 enp0s3
{% endhighlight %}
* Configure DNS resolver by opening resolv.conf and setting it as follows.
{% highlight sh%}
$ sudo nano /etc/resolv.conf
{% endhighlight %}
![output](../img/eramba3.png)

### Testing the Fix

The VM should now be accessible from your network devices and have internet connection available.

You can test this by pinging your router from the VM and then ping amazon.com to check that dns is also properly configured.

You will now be able to acess the eramba login page by navigationg to the ip set from any web browser in the network.
