---
layout: post
title: Vulnversity - Writeup
author: V0ID7
date: 2023-03-14
icon: https://i.postimg.cc/T29Q8LRY/screenshot-144.jpg
categories: [TryHackMe,Linux]
tags: [thm-vulnversity]
pin: false
image:
  path: https://i.postimg.cc/T29Q8LRY/screenshot-144.jpg
  width: 1280   # in pixels
  height: 720   # in pixels
  alt: 
---


This is a free room from TryHackMe, created by tryhackme.
> Disclaimer 
No flags (user/root) are shown in this writeup, so follow the procedures to grab the flags! Enjoy! 
{: .prompt-warning}


## Setting-up the Environment
Make connection with VPN or use the attackbox on Tryhackme site to connect to the Tryhackme lab environment.

## Reconnaissance

###### Task 1

Deploy the machine attached to the task and press complete

###### Task 2

Start `nmap` scan of the machine by typing in the following command:-

```shell
nmap -Pn -n -p- -sC -sV -O -T4 -vvv -oN nmap_vulnversity <machine_ip>
```

