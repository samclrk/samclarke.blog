---
layout: post
image:
  feature: nas-setup.jpg
title: Attempting to Set Up FreeNAS
comments: true
---

Backups have always been a double edged sword for me.  I either didn't back up frequently enough, or poorly planned my redundancy. Several times I've ended up losing data all together, through my own bad backup habits. A few years ago I'd pretty much resigned myself to pulling a full hard drive backup every couple of weeks, splitting it across a couple of drives (just in case) and repeating the process for each of my machines. That was until, I started using Dropbox.

With Dropbox loaded up on all my machines, a 1TB storage limit and unlimited bandwidth, I pretty much ran my entire life from the `/Dropbox` folder of each of my computers.

This was great, it saved me a lot of pain, time, and regret when my ill-planned backup schedule failed and I was left with 500GB of nothing on my Western Digital Elements drive. One thing it wasn't great for though, was backing up the other computers in the house and our ever-growing media collection. To make sure everything was covered, I decided to invest in a NAS.

After a fair amount of research and poking around, I ultimately decided I really wasn't willing to part with the best part of £500 if the only benefit I gained from the likes of a Synology/Drobo style box was storage space. I wanted the ability to control backup schedules, manage my own RAID arays of drives as I continued to add them, and future-proof the machine to the extent that I could justify the hefty cost. With that in mind, I ended up switching gears slightly and began researching the idea of building a home server.

I had a number of spare parts lying around from my most recent PC upgrade so immediately I was on to a winner with building my own server. After double-checking the requirements for a decent home server and some reading in to FreeNAS (at the recommendation of [Tested.com](http://www.tested.com)) I decided to get to work.

## Build Specs

The rationale behind the build I put together for this home server is fairly straightforward. I needed a clean build with decent airflow, low noise, and I needed an easy way to add/change storage further down the line.

| **Case**| Fractal Design - Define R5 |
| **Power Supply**| Corsair CX 500W Modular |
| **Motherboard**| Gigabyte GA-H97M-D3H |
| **CPU**| Intel Core i5-4590 3.30GHz |
| **Memory**| Kingston 8GB |
| **Storage**| Western Digital Green - 2TB |

## The Build

Putting this machine together was really easy compared to my gaming PC rig. Once the new CPU arrived, I harvested the motherboard from my older, shelved, gaming PC, I had my current rig donate 8GB of it's RAM, attached the stock CPU cooler (It would do to start me off) and carefully loaded it in to my brand new Fractal Define R5. 

*At the time of writing this, I only have one hard drive to load in to the machine, so it seems a little overkill right now, but I know it's going to save me a ton of time later. Plus, it looks sexy as hell.*

After I'd loaded the parts in to the machine (I didn't test run before putting the machine together, I was a little eager to see the finished product), I dropped in my 2TB drive, plugged in all the peripherals and booted it up to see it was all OK. 

**Thank fuck for that**.

## Installing FreeNAS

Everything I'd read about FreeNAS lead me to believe it was to be a fairly simple process. I have a ton of USB drives lying around so quickly formatted a couple of those. Loaded one up with the install files, left the other blank and booted straight to the install menu.

### Initial Install

The install went well, three fairly easy to navigate menus, a couple of on-screen prompts and I was golden. Once I was in to the GUI, I followed the set up wizard, secured the box, created my users, and began setting up several volumes to split among the computers in the house.

*This is where things started to get a little interesting.*

For some reason, I wasn't able to create any volumes or jails (a FreeNAS specific way of partitioning a drive for a set use), larger than 11GB. I knew there was something wrong as there was plenty more space than that available, for sure. I went back, deleted my volumes, booted in to a copy of Ubuntu I have on another USB drive and checked the partitions were all set up correctly.

*Something was definitely wrong.*

After some searching and eventually running back through the initial install sequence, I discovered that I had actually installed FreeNAS on to my 2TB hard drive, rather than the seconday USB drive I had prepared earlier.

### Re-install

I went back to square one. I formatted all the drives, downloaded a fresh copy of FreeNAS, loaded it's install files to a USB drive and followed the install process from the beginning. At this point the system runs a reboot to load you in to the OS, rather than the install files themselves.

*Problem.*

After the reboot (and every subsequent reboot), I was left with an error message, and forced in to the shell.

~~~~~~~~
SMP: AP CPU #1 Launched!  
SMP: AP CPU #2 Launched!  
SMP: AP CPU #3 Launched!  
Timecounter "TSC-Low" frequency 1650033691 Hz quality 1000  
Trying to mount root from zfs:freenas-boot/ROOT/default []...  
init: not found in path /sbin/init:/sbin/oinit:/sbin/init.bak:rescue/init:/stand/sysinstall  
panic: no init  
cpuid = 2  
KDB: stack backtrace:  
db_trace_self_wrapper() at db_trace_self_wrapper+0x2a/frame 0xffffff8000258850  
kdb_backtrace() at kdb_backtrace+0x37/frame 0xffffff8000258910  
panic() at panic+0x1ce/frame 0xffffff8000258a10  
start_init() at start_init+0x27a/frame 0xffffff8000258aa0   
fork_exit at fork_exit+0x11f/frame 0xffffff8000258af0  
fork_trampoline() at fork_trampoline+0xe/frame 0xffffff8000258af0  
--- trap -, rip = 0, rsp = 0xffffff8000258bb0, rbp = 0 ---  
KDB: enter: panic  
[ thread pid 1 tid 100002 ]  
Stopped at     kdb_enter+0x3b: mov1    $0,0xd04732(%rip)
~~~~~~~~

This bring me up to now. I've spent the entire day researching this error with the limited knowledge I have on FreeBSD. My machine meets the minimum required spec, as do the USB drives I'm using to install FreeNAS. I can't find any similar errors online and currently have no idea how to fix this. I'm somewhat hoping someone will see this and scream at their screen for how simple an issue this is to fix, but until then, I'll keep plugging away.

> Side note: If you do know how to resolve this, I'd love to hear how!

## Update

It looks as though there was an issue with FreeNAS 9.3 (Actually released the day I was having these problems). I downgraded my instal files to FreeNAS 9.2.1.8 and it worked immediately!

I'm now in the process of creating my volumes, setting up our new Plex Server and this afternoon I'll be getting our computers all backing up automatically!

## Update #2

I finally have my FreeNAS instance running on the most up to date version of 9.3. I'm yet to ascertain exactly which files were missing from the initial install or what may have caused it to fail. Technically speaking FreeNAS doesn't support my set up, since I'm not running on ECC memory and am using a desktop grade motherboard/CPU combination. I'll continue to work on finding out what the issue was, should anyone come across it in future this post may prove to be useful.

In the meantime however, I'll continue working with 9.3 and see how I get on over the next few weeks. I've now got all our backups running smoothly across all devices, shared drives up and running and Plex is running fantastically (Although it would probably benefit from 12GB of RAM instead of just the 8GB it's currently working with). Next on my list is to build in extra redundancy, move to a RAID array of multiple drives and try to get rsync set up to replicate individual, important files!