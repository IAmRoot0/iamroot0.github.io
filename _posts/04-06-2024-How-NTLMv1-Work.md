---
title: "How NTLMv1 Work?"
date: 04-06-2024 07:09:22
categories: [Active Directory Basics]
tags: [Active-Directory, Active-Directory-Basic]
---

[![](https://mermaid.ink/img/pako:eNqFVMFu2zAM_RVCl21YUmCXHYwhQJa0XQ8thibFgCIXxaZtYbbkUVKKrOi_j5JiJ16zLkAAiSYf3yMpPovcFCgyYfGXR53jUsmKZLvRwL9OklO56qR28GCRXltXSLtz9uUi2ULUdDZLblm8wo_g4AzIPEdrwdU4gvkrZE1S21YlAlq2mLzujEMgVdUOTMnpMrgyBNIzmmYW0imjQeoimgyp39HyZUsz6Dx1xqKdcBi0UmnHfwt36-XqYnmzhlI1CMHzSbk6Ub7RpaH2CPpN2hq-S2ufDBX24oSSYdLQc79GjSTZes9BpoVPn2HLSuYWJCxq2TSoq4OeFDJl4SFhxndOs-bSDH6wNidNiMkaLKP8FBJh79F2RlucxLr6QJ7bSvvO2Sg-WPMBMiqUUAc5jMMfFXEfk67g__4yBQfh3ipdwfJyBbKpuKSubj-cbVnkHhL1ZAL10xa_rtTgeUVcp1jzj0PH-Ri5H3mPajabhfY_cDwQ5qh2gWZIT30tQnQw2BjAqpuGz0xSxUEMn3gUghe3GdhFlf0Ibfcgi6JHDC7-wGpyxI8zkY8bOh7QgJ_BlHU6UjuMYEHeOzueJfi6f3PQe5xDWyLOYtxOn2D7Lkb8t6BupctrmFfhETjWFAmeyBlk_keXJx3pWCedt2DSbSutssGTUXzjEsZyMT0dlxQwhXlaCNe8H7D4x7M46ysmokV-n6rgTfYcIjeCk3MJRcbHQtLPjdjoF_bjdWBWe52LzJHHiSDjq1pkpWy4j8J3BT_Xww4crLzRHo053rFQztBtWpxxf778AUJUzD0?type=png)](https://mermaid.live/edit#pako:eNqFVMFu2zAM_RVCl21YUmCXHYwhQJa0XQ8thibFgCIXxaZtYbbkUVKKrOi_j5JiJ16zLkAAiSYf3yMpPovcFCgyYfGXR53jUsmKZLvRwL9OklO56qR28GCRXltXSLtz9uUi2ULUdDZLblm8wo_g4AzIPEdrwdU4gvkrZE1S21YlAlq2mLzujEMgVdUOTMnpMrgyBNIzmmYW0imjQeoimgyp39HyZUsz6Dx1xqKdcBi0UmnHfwt36-XqYnmzhlI1CMHzSbk6Ub7RpaH2CPpN2hq-S2ufDBX24oSSYdLQc79GjSTZes9BpoVPn2HLSuYWJCxq2TSoq4OeFDJl4SFhxndOs-bSDH6wNidNiMkaLKP8FBJh79F2RlucxLr6QJ7bSvvO2Sg-WPMBMiqUUAc5jMMfFXEfk67g__4yBQfh3ipdwfJyBbKpuKSubj-cbVnkHhL1ZAL10xa_rtTgeUVcp1jzj0PH-Ri5H3mPajabhfY_cDwQ5qh2gWZIT30tQnQw2BjAqpuGz0xSxUEMn3gUghe3GdhFlf0Ibfcgi6JHDC7-wGpyxI8zkY8bOh7QgJ_BlHU6UjuMYEHeOzueJfi6f3PQe5xDWyLOYtxOn2D7Lkb8t6BupctrmFfhETjWFAmeyBlk_keXJx3pWCedt2DSbSutssGTUXzjEsZyMT0dlxQwhXlaCNe8H7D4x7M46ysmokV-n6rgTfYcIjeCk3MJRcbHQtLPjdjoF_bjdWBWe52LzJHHiSDjq1pkpWy4j8J3BT_Xww4crLzRHo053rFQztBtWpxxf778AUJUzD0)

{% mermaid %}
sequenceDiagram
    participant User
    participant Server
    participant DC
    User->>Server: User Want to access the Server
    User->>Server: Transmit Username
    Note right of DC: For authentication and authorization<br> purposes, DC maintains NTDS.DIT file <br>with User Information and Hash Passwords.
    Note over Server: Generate Random 16 bit As a Challenge
    Server-->>User: Send The Challenge To User
    Note left of User: As a Response, the user encrypts<br> the challenge with a hash of their password<br>(Encryption using DES algorithm)
    User->>Server: Send the Response To Server
    Note over Server: Response From User + Username + <br> challenge 
    Server->>DC: Upon receiving the response,<br>the server will send it to the DC <br>for verification by adding the <br>username, response, and challenge
    Note right of  DC : - Retrive the User's Hash Password By Username
    Note right of  DC : - Encrypt the Challenge with user's password Hash
    Note right of  DC : - Match Against retrived challenge response
    Note right of  DC : - Return the status on the basis of result
    DC-->>Server: Status - Access Ganted
    Server-->>User: Status - Access Ganted
{% endmermaid %}