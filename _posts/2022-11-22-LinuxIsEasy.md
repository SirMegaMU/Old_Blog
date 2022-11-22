---
layout: post
title: A Week With Ubuntu 
date: 2022 11-22
tag: 杂项
---

I installed the latest Ubuntu LTS as dual system in the election public holiday , And till now I have been using it for a week and experienced nearly, 

I can say, almost all aspects of Ubuntu.

### First tiral

I have used ubuntu for a nearly a year after I started to learn Python in the summer holiday after Gaokao.

But in that period, I was using Vm Workstation and WSL, and I only used them to write and compile some code,
thus i didn't care about the OS itself very much, i just copied my code and paste it and let it run. I stay with Windows in the most of the time.

**But now, I have new needs.**

Unlike the life in SZU, the life in UM is quite different. In china, we have textbooks for nearly every courses, and we just write notes on the textbooks. 
But UM is different, there is no text books, I have to take my notes either on my laptop or on a notebook.

I tried to take notes and do my home work on paper in the first few weeks in UM, and that was truely a mass. 
The pieces of paper went missing quickly and the remained paper is quite unneat due to my bad nite habit. 

So I decided to take my notes on laptop.

Unfortunately, I did't consider the need of taking notes when I brought the gaming laptop, 
it's good when you don't have to carry around and it's good when you can find power suply easily. 
The battery of my laptop is poor, it cano only work for nearly 2 hours with some 'lite' work. 

So I turn to Ubuntu .

### Install the System

Install the System itself is quite easy, and there a lot of guides on the internet, 
But i still met some problems.

- the latest ubuntu don't support boot from `\boot`, so you need to install it to a new efi partition, it don't need to be too big, 500MB is enough.
  the efi partition should be in the same hard disk where Windows's efi partition locates, or you will not find it in the BIOS later.
- Since I installed Windows as the first OS oif the laptop, SO I can't find Ubuntu in the boot options. That don't means the installation failed.
  There should be also a uefi option in the BIOS, you can choose ubuntu in it.

### Softwares and PLugs

I'm quite a big fan of Typora, I use typora to take notes Windows , i still need it on Ubuntu.

also other softwares like WPS, chrome are installed , I am planning to use ubuntu on the classes, so I still need them.

But for Plugs I installed a lot, plus for gnome, plugs for vim... having a good look always makes me feel happy. haha

Also I installed Waydroid to use android apps , I tried WSA, but that didn't solve my problem, maybe Waydroid can meet my need ? I don't know

### The tools I used

- [Graet anime GRUB Theme](github.com/13atmo1/GRUB-Theme)
- [Waydroid](doc.waydro.id)
- [Waydroid Script](github.com/casualsnek/Waydroid_script)
- [Vim Plug](github.com/junegunn/vim-plug)
- [Gnome tweaks](github.com/GNOME/gnome-tweaks)
- [Gnome extensions](extensions.gnome.org)

### brief feelings

Now my laptop can survive the 2 hour lecture without turing the performance mode off and limiting the refresh rate, 
I don't need to kept the screen dark along the class , god save my eyes

also, using Vim plugins on GUN/Linux is quite easier than using it on windows, it's the same to those applications, all I need is simply copy the install code, good

> By the way, this blog is fully written in Vim, yeah

![I love Vim](megamu.icu/images/posts/2022-11-22/pic.png)




