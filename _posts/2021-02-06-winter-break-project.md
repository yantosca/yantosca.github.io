---
title: 'What I did on my Christmas holiday break 2020'
date: 2021-02-06
permalink: /posts/2021/02/06/
tags:
  - linux
  - ubuntu
---

I have a HP Inspiron desktop that I originally bought in 2016.  It has 4GB RAM, an Intel Core i3 CPU w/ 4 cores (basically a Broadwell chip), an Intel Graphics GPU, and a Broadcom 43132 wireless card.  This used to run Windows 7 fine, but with the end of support announced for early 2020, I upgraded it to Windows 10.

On Windows 10 this machine crawled.  Don't get me wrong, I like the look and feel of Windows 10, but the 4GB of RAM and Core i3 PC were clearly overtaxing this machine.  But I wanted to hold on to this laptop because it has a HD screen and a HDMI port, which makes it easy to project to a monitor at my office (ahem, in the good old pre-COVID days when we could, you know, go to the office).

Harvard gives us staff the week off between Christmas & New Year's Day (actually this week they gave us the 2 weeks, which was much appreciated.  So I decided to take a chance and install Ubuntu 20.04 LTS "Focal Fossa" on my laptop.  I originally kept it as dual-boot with Windows, but then after a catastrophic disk error caused by "sudo apt update-release", I reformatted the disk totally for Ubuntu and got rid of the windows.  Specs are below.

![All glory to the Hypnotoad!](/images/neofetch.png)

I named the laptop "Hypnotoad" after the hypnotic toad from the Futurama animated series.  (Also one of my favorite shows.)  ![All glory to the Hypnotoad!](/images/the_hypnotoad.jpg){:style="float:right" margin-top:10px; margin-left:10px"}

I now have a dual partition with Ubuntu 20.04 and Ubuntu 20.10, but I am sticking with the 20.04 for now.  When the next LTS (Ubuntu 22.04) comes out, I will probably upgrade to that.

One thing I noted is that the Ubuntu has much less bloat than Windows 10.  Running the Stacer app, you can see that the machine is using half of the available RAM!

![Stacer](/images/stacer.png)

This means that CPU-intensive applications like Zoom are much less apt to hang.  I've also set the swappiness down from 60 to 10 (sysctl -w vm.swappiness=10) so that it will not swap to disk as frequently (as it has plenty of RAM).

One thing that I still need to work out is the Wifi card.  The Broadcom 43142 card needs to use the proprietary driver from bcmwl-kernel-source.  It generally works OK but sometimes the signal strength varies.  I've looked into an number of solutions (setting REGDOMAIN=US seems to have made it more stable) but the problem still happens intermittently.  The solution may have to wait for the next driver update from Broadcom.

All in all, I am glad I switched over my laptop to Linux.  I've learned a lot about Linux desktop management in only a few weeks.  There are plenty of internet sites like [Ask Ubuntu](https://askubuntu.com) and [OMG Ubuntu](https://www.omgubuntu.co.uk/) that have useful tips and tricks for desktop management.
