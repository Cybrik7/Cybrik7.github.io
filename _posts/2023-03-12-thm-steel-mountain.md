---
layout: post
title: Steel Mountain - Writeup
author: V0ID7
date: 2023-03-18
categories: [TryHackMe,Windows]
icon: https://i.postimg.cc/WpHJTvwP/screenshot-155.jpg
tags: [thm-kenobi]
pin: false
image:
  path: https://i.postimg.cc/WpHJTvwP/screenshot-155.jpg
  width: 1280   # in pixels
  height: 720   # in pixels
  alt: 
---

### Welcome Folks!!

This is a free room from TryHackMe, created by tryhackme.

[https://tryhackme.com/room/steelmountain](https://tryhackme.com/room/steelmountain)

This article outlines my approach to solving the “Basic Pentesting” room available on the TryHackMe platform.

> Disclaimer 
No flags (user/root) are shown in this writeup, so follow the procedures to grab the flags! Enjoy! 
{: .prompt-warning}

## Task 1 - Web App Testing and Privilege Escalation

###### Setting-up the Environment

> 1. Deploy the machine attached to the task and press complete

Make connection with VPN or use the attackbox on Tryhackme site to connect to the Tryhackme lab environment.


###### Reconnaissance

> 2. Find the services exposed by the machine

As usual I started by connecting to and scanning the target machine for any open ports and services using the `NMAP`.

```shell
sudo nmap -sS -A -p- 10.10.251.116 -vvv -oN nmap_basic_pentesting 
```

The `nmap` command can be broken down as follows:

```shell
-sS: Stealth Scan / Half-open scan or SYN scan - only SYN packets sent. Responses same as full
 -A: Enable OS detection, version detection, script scanning, and traceroute
     or use below switches instead of -A
-sV: Probe open ports to determine service/version info  .
-sC: Performs a script scan using default scripts available in NMAP.
 -O: Performs OS Detection
-p-: Scan all ports
-vv: Increase verbosity level about the nmap scan.
-oN: Outputs scan results to a file.
```
Nmap found following open `ports` & `services`

![img](https://i.postimg.cc/k4RX1zb5/screenshot-146.jpg){: width="1280" height="720"}


port 22 (SSH)
port 80 (Apache)
port 139 & 445 (SMB)
port 8009 (Apache Jserv)
port 8080 (Apache Tomcat)

Then I decided visit the web page hosted on port 80.

![img](https://i.postimg.cc/c4XJNmk7/screenshot-147.jpg)

> 3. What is the name of the hidden directory on the web server(enter name without /)?

I decided to use GoBuster, a tool which can be used to find hidden directories.

```shell
gobuster dir -u http://[MACHINE_IP] -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,aspx,js,html
```
Using a tool called gobuster, we can find hidden directories on the web server:

![img](https://i.postimg.cc/V6fCR6Jm/screenshot-148.jpg)

Looking at the “dev.txt” file, some interesting development notes were left behind.

## Task 2 - Vijay Rand