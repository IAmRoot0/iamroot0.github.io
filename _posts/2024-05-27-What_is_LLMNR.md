---
title: "What is LLMNR ?"
date: 2024-05-27 10:03:38
categories: [Active Directory Basics]
tags: [Active-Directory, Active-Directory-Basic]
---
&nbsp;

&nbsp;
## What is LLMNR?

Link-Local Multicast Name Resolution (LLMNR) is a protocol that allows computers on a local network to resolve the names of other computers to their IP addresses. It is similar to the NetBIOS Name Service (NBNS) protocol, which is used to resolve NetBIOS names to IP addresses in Microsoft Windows operating systems.

LLMNR is based on the Client/Server model, in which one computer, called the server, provides a service to other computers, called clients, on the network. When a client computer wants to communicate with another computer on the network using its hostname, it sends a request to the LLMNR server on the network. If the server has the IP address of the target computer in its database, it responds with the IP address. The requesting computer can then use this IP address to establish a connection with the target computer and communicate with it.

Devices in a network use IP addresses to communicate with each other. However, for human simplicity, we use the name of the device (//xy.com/d$) instead, which is resolved to IP address on a local network, and that’s known as name resolution. The Windows system has three main methods for handling name resolution: Domain Name System (DNS), Link-Local Multicast Name Resolution (LLMNR), and NetBIOS.

LLMNR is designed to be used in networks where a Domain Name System (DNS) server is not available. It allows computers on a local network to communicate using hostnames, even if they are not connected to the Internet.

LLMNR can work over IPv4 and IPv6.


## Here's how LLMNR works:

1.  A client computer wants to communicate with another computer on the network using its hostname.
    
2.  The client computer sends a request to the LLMNR server on the network, asking for the IP address of the target computer.
    
3.  If the LLMNR server has the IP address of the target computer in its database, it responds with the IP address.
    
4.  The requesting computer can then use this IP address to establish a connection with the target computer and communicate with it.
    

If the LLMNR server does not have the IP address of the target computer in its database, it will send a multicast request to all computers on the network, asking if any of them know the IP address of the target computer. If a computer on the network knows the IP address, it will respond with the IP address. The requesting computer can then use this IP address to communicate with the target computer.

LLMNR is designed to be used in networks where a Domain Name System (DNS) server is not available. It allows computers on a local network to communicate using hostnames, even if they are not connected to the Internet.\
