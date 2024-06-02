---
title: "SMB signing is disabled"
date: 2024-05-27 10:03:38
categories: [Active Directory Basics]
tags: [Active-Directory, Active-Directory-Basic, SMB]
---
&nbsp;

## What is the meaning of SMB signing is disabled ?

When SMB (Server Message Block) signing is disabled, it means that digital signatures are not being used to authenticate and verify the integrity of SMB packets. This can make the network more vulnerable to man-in-the-middle attacks, as an attacker could potentially intercept and modify SMB packets without being detected. It also means that the clients and servers on the network cannot verify the authenticity of the SMB packets they receive, which can lead to security issues. It is generally recommended to keep SMB signing enabled for better security.

Systems are susceptible to an NTLM relay attack because the recipient does not verify the content and origin of the message. The most effective way to remedy this vulnerability is to enable enterprise-wide SMB signing.

SMB signing is a security mechanism in the SMB protocol. When SMB signing is enabled, each SMB message is sent with a signature in the SMB header field. The signature consists of the contents of the SMB message, encrypted with the AES algorithm. This allows the recipient of the SMB message to verify that the content of the message has been changed. It also verifies the identity of the sender. If the content of the message doesn’t match the SMB header, the recipient knows that the message has been tampered with. The recipient then does nothing with this SMB message. This makes it impossible to successfully perform an NTLM relay attack.

## References

- [Finding and Fixing SMB Signing Disabled Vulnerability](https://www.beyondsecurity.com/resources/vulnerabilities/smb-signing-disabled#:~:text=SMB%20Signing%20Disabled%20is%20a,prone%20to%20being%20overlooked%20entirely.)

- [The Basics of SMB Signing (covering both SMB1 and SMB2)](https://itworldjd.wordpress.com/2017/01/04/the-basics-of-smb-signing/)

- [SMB Relay Attacks Explained: Why You MUST Enable SMB Signing Immediately](https://www.youtube.com/watch?v=XtyDwOs2tKA)