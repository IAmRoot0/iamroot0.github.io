---
title: "Expanding the Scope of Automation Scanners Using Burp-Suite"
date: 2024-06-06 07:09:22
categories: [Burp-Suite]
tags: [Burp-Suite, Jython]
mermaid: true
---

---
## Limitations of Automation Scanners
---
The market offers a range of security scanners, including HCL App scan, Acunetix, and Netsparker, among others. However, it is observed
that these types of automated scanners have some disadvantages, basically, these automated security scanners are not smart enough to understand the
requirements of user input fields. sometimes they are not able to reach each and every function while spidering or crawling the applications. Because of
these disadvantages, it is possible that we might have missed the vulnerabilities.

Actually, we can resolve these problems by exploring the entire application manually in automation scanners.

Suppose if we want to scan a single application with multiple tools then, we have to explore the entire application multiple times for each tool.

---
## About Burp-Suite
---
Burp-Suite is very popular in the hacking community because of the flexibility and high-level customization capabilities of the burp-suite. It allows users to modify and craft requests, intercept and modify responses, and perform in-depth manual testing.

The burp-suite proxy tool connects to the browser, so whatever we explore or trigger the functionality of target application in the browser, it will be captured by the burp-suite tool. Burp-Suite can store the request and response with proper user inputs and application flow.

Since our goal is to explore the entire application once manually and capture the traffic in burp-suite and then transfer the captured traffic from burp suite to HCL App scan or other proxy tools, we will use Burp-Suite Upstream Functionality here.

### Burp-Suite Upstream Tool
Upstream Functionality is used to route the traffic form Burp-suite to other proxy tools or machine. The Burp Suite Upstream Setting refers to a feature within the Burp Suite tool that allows users to configure upstream proxies. Upstream proxies act as intermediaries between the client and the server, forwarding requests from the client to the server and vice versa.

### Burp-Suite Repeater Tool
Repeater allows you to modify any part of an HTTP request, such as headers, parameters, cookies, or the request body. You can then resend the modified request to the target server and observe the response. This functionality is helpful for testing different input values, parameters, or headers to identify vulnerabilities or to understand how the application responds to specific inputs.

---
## Setup 
---
The scenario for the setup is as follows.

- Burp-suite will be the sender, so we will setup the "Upstream Proxy Server" in Burp-suite and
- HCL App Scan will be the receiver, so we will need to setup a Proxy Listener in HCL App to record the traffic.

#### Step 1:
Explore the entire application in burp suite. trigger the each and every function of application with proper user inputs and flow.
In the following image, you can see that we have already explored the entire application https://demo.testfire.net

![](assets/images/burp-suite1/expand-scope-1.png)

