---
title: "Common Terminologies of Kerberos"
date: 2024-06-03 10:29:52
categories: [Active Directory Basics]
tags: [Active-Directory, Active-Directory-Basic, Kerberos]
---
&nbsp;

## Common Terminologies of Kerberos Authentication 

Kerberos authentication is a robust protocol used for network security, particularly in Active Directory (AD) environments. Here’s a list of common terminology associated with Kerberos authentication in AD:

### Key Terms in Kerberos Authentication

- **KDC (Key Distribution Center)**: The service that issues Kerberos tickets. It consists of two parts: the Authentication Server (AS) and the Ticket Granting Server (TGS).
    
- **AS (Authentication Server)**: Part of the KDC, it authenticates users and provides the initial ticket called the Ticket Granting Ticket (TGT).
    
- **TGS (Ticket Granting Server)**: Part of the KDC, it issues service tickets based on the TGT provided by the AS.
    
- **TGT (Ticket Granting Ticket)**: A special ticket obtained after initial authentication that allows the user to request service tickets from the TGS.
    
- **Service Ticket**: A ticket obtained from the TGS, used to authenticate a user to a specific service.
    
- **Principal**: An identity to which Kerberos can assign tickets. In AD, this can be a user, a service, or a machine.
    
- **Realm**: The Kerberos administrative domain. In AD, the realm is typically the domain name.
      
- **krbtgt (Kerberos Service Account)**: Special account used by the KDC to encrypt TGTs for secure transmission.
    
- **Ticket**: A time-stamped, encrypted block of data that serves as a user's credentials.
    
- **Session Key**: A temporary encryption key used between the client and a server during a single session.
    
- **KRB_AP_REQ**: The request sent by a client to a server to authenticate using a service ticket.
    
- **KRB_AP_REP**: The response from the server to the client, confirming authentication.
    

### Additional Terms Related to Kerberos in AD

- **SPN (Service Principal Name)**: A unique identifier for a service instance used in Kerberos authentication.
    
- **PAC (Privilege Attribute Certificate)**: A data structure used by Kerberos that contains authorization information for a user.
    
- **Kerberos Policy**: The set of rules governing ticket lifetime, renewal, and related security settings within a realm.
    
- **KRB_TGS_REQ**: The request sent by a client to the TGS to obtain a service ticket.
    
- **KRB_TGS_REP**: The response from the TGS to the client, containing the requested service ticket.
    
- **Pre-authentication**: An additional step in the Kerberos protocol that helps prevent certain types of attacks, requiring the client to prove its identity before receiving a TGT.
    
- **Forwardable Tickets**: Tickets that can be used to obtain new tickets on behalf of the user, allowing for single sign-on across multiple services.
    
- **Renewable Tickets**: Tickets that can be renewed without re-authenticating the user, extending their validity period.
    
- **Transited Field**: A part of the ticket that indicates the intermediate realms a ticket has passed through.
