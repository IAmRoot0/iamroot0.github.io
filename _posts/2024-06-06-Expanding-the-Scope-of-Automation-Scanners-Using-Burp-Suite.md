---
title: "Expanding the Scope of Automation Scanners Using Burp-Suite"
date: 2024-06-06 07:09:22
categories: [Burp-Suite]
tags: [Burp-Suite, Jython]
mermaid: true
---
&nbsp;

## Limitations of Automation Scanners
The market offers a range of security scanners, including HCL App scan, Acunetix, and Netsparker, among others. However, it is observed
that these types of automated scanners have some disadvantages, basically, these automated security scanners are not smart enough to understand the
requirements of user input fields. sometimes they are not able to reach each and every function while spidering or crawling the applications. Because of
these disadvantages, it is possible that we might have missed the vulnerabilities.

Actually, we can resolve these problems by exploring the entire application manually in automation scanners.

Suppose if we want to scan a single application with multiple tools then, we have to explore the entire application multiple times for each tool.
