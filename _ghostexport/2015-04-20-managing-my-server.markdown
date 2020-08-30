---
layout: post
title: Managing my Server
date: '2015-04-20 23:00:00'
tags:
- writing
---

It’s been a couple of weeks now since I first got FreeNAS up and running on my home server. It wasn’t quite as easy as advertised, I came across a couple of issues (one of which is still unsolved) but for the most part things are now running smoothly. You can read about the build and getting FreeNAS running, here and now, I’m looking at how I can improve the current set up, getting the most out of it.

## Plex

There were two main goals of having my own server, the first of which was moving my somewhat huge1media library off my personal rig to free up space and make all the movies/TV shows I have more available throughout the house.

The way FreeNAS handles Plex made the transition really simple. I install the Plex Media Server plugin to my instance of FreeNAS, created a jail which allowed me to set a disk quota (I’m currently only running with 1TB of space so don’t want it run in to any issues), created a user/group combination for security purposes and was away!

To make things slightly easier for myself, I also enabled a Windows Share to the designated media folder which my Plex Jail was pointing to, meaning I could mount the Plex Server as a network drive and simply dump all my content straight in! In future, I’ll be adding a Bluray Writer to my server, allowing me to rip films directly, but for now I’ll still need to use my desktop as a go-between.

All set — I’d freed up a huge amount of space on my personal rig and had the new Plex server running on all clients in the house! Next, I needed to get my backups running. Having learned many mistakes from not properly managing my backups in the past, I felt it was only right that I had all the machines in the house backing up to the new server, as well as an off-site backup2. Charleigh and I both have Macbooks and so setting up Time Machine was the first task on my backup list.

## Time Machine

Setting up Time Machine on the server was only a little more complicated than Plex. There’s no plugin as such since the server isn’t actually required to do anything, other than store data. The first thing I did was create a new jail specifically for Time Machine. I’d decided beforehand that I’d have all Macs in the house backup to one location, rather than giving each user their own “drive”. It’s important to note that Time Machine will over time, basically use up however much space you give to it and as a result I needed an easy way to manage disk space and user access.

Hell, it’s only the two of us.

Once I’d created the jail and given it 500GB to work with, I needed to designate an AFP3in order for our Macs to pick up the new shared drive for Time Machine to use. I then loaded up both laptops, ignored a few folders from the sync and ran the first full backup on each machine. This has to be the only time in my life that I’d wished my Macbook Air had an ethernet port.

In total I think it took about 11 hours to fully backup both machines to the server, in the process, I came across an interesting issue that I’ve not yet resovled. For some reason the Macbooks occasionally lose connection with the server and I have to refresh their network lease in order to reconnect the server and continue the backup. I have both machines connecting to and mapping the network drive on boot, which seems to work, most of the time… But I need to work on a permanent solution to this.

## Windows Backup

Once Time Machine was running (somewhat successfully), I moved on to getting my Windows PC backed up as well. This presented quite a challenge for me. The last time I ran any major backups on a PC, outside of manually copying files/folders to some external hard drives, windows had it’s own backup protocol and tools. Those have seemingly vanish in Windows 8.1, or rather, changed to the point that they don’t function quite like I was expecting.

Anyway, I decided for the short term to use File Restore and Windows Scheduler to automate the process of backing up some of the more important files on my PC whilst I looked in to alternative methods of backing up the entire machine. On the FreeNAS side of things, all I needed to do was create another jail to manage access and disk space, then create a Windows CIFS4Share so that I could map the jail as a network drive.

One final task whilst creating all the jails and shares on FreeNAS was to create something of a media server. Not really to serve content, more as long-term storage for my growing catalog of photos. I had however, come up against a slight issue with the amount of remaining space on my 1TB drive and was forced to put this on hold for a short while.  
My media library is currently stored on my personal rig, tied in to Dropbox (not ideal I realise, but a legacy of moving away from my Macbook Pro and needing somewhere quick to drop a couple of hundred gigabytes of images). Once my new set of hard drives arrives, I’ll be moving away from Dropbox as a storage medium and then start looking towards off-site backup solutions.

## Upgrades

The first couple of weeks of living with my new server, moving all our backups and content to it and trying to get over the initial hurdles I faced during it’s setup, have left me with a short list of upgrades to work on in the near future.

## Storage

I absolutely need more storage. I bought the Fractal R5 case specifically because it allows me to house 12 hard drives, I need to take advantage of the physical storage space and make sure I move to a neat RAID array for drive redundancy.

## Memory

The server is currently running on 8GB of Kingston Hyper X DDR3 (Non ECC) RAM. It’s a disaster waiting to happen given that FreeNAS essentially runs from the system memory. But it’s also causing a slight issue with Plex content. Whilst 8GB does meet the minimum requirements, it’s not quite enough to stream 1080p content over the network, flawlessly. Ideally I’d like at least 16GB of ECC RAM, but that is fairly costly and if I was going that route this early, I’d probably have gone for a server grade motherboard and XEON processor to match.  
In all, I’m really pleased with how the server has been running so far. I’ve a few changes to make to it in the short term and I’ve already learned a number of lessons in how to best manage my storage and systems locally. Hopefully I can continue to improve on it’s performance and begin pushing more it’s way!

