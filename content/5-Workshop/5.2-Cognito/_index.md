---
title : "Prerequiste"
date : 2024-01-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

#### Introduction to AWS Cognito

* **Amazon Cognito** is a fully managed, centralized identity, authentication, and authorization service provided by AWS that securely scales to millions of users.
* In healthcare applications, protecting medical records and personal data is mandatory. Cognito ensures compliance with safety standards using **RSA-standard Token encryption (JWKS)**, **Role-Based Access Control (RBAC)**, and **Data Anonymization** at the authentication layer.
  
#### Deployment Overview

In this hands-on lab, you will initialize and integrate an **AWS Cognito User Pool** (`healthcare`) into the system to serve the **Next.js** Frontend and **NestJS** Backend:
* Initialize a **User Pool** featuring high-security password policies and automated email verification flows.
* Set up **User Groups** (`Admin`, `Doctor`, `Patient`) to support **Role-Based Access Control (RBAC)** mechanisms.
* Integrate the **JWKS Endpoint** into the NestJS Backend to verify asymmetric JWT Token signatures without making round-trip calls back to AWS, maximizing performance.
  
#### Implementation Steps Summary

* Step 1: User Pool Creation (User Directory Repository)
* Step 2: Role-Based Access Control (RBAC)
* Step 3: Configure App Client (App Client for Next.js)
* Step 4: Integrate JWT Verification into Backend (NestJS)