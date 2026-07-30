---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# [FCAJ2026] What is AWS Cognito? Why is it an Indispensable Piece of the Smart Healthcare System?

---

### Introduction

During the development of the **Smart Healthcare Platform** (An AI-assisted medical screening and appointment management platform), right after solving the challenges of slot conflict management and AI integration, I was confronted with another "nightmare": **Identity and Access Management (Authentication & Authorization)**.

My system consists of 3 distinct user groups with entirely different roles and permissions:
1. **Patient**: Register/Log in, chat with AI, book appointments.
2. **Doctor**: View daily appointment schedules, read AI-generated medical summary reports, issue prescriptions.
3. **Receptionist**: Manage front-desk operations, check in patients via QR codes, generate invoices, and collect payments.

Initially, my instinct was to build a custom Auth service on the NestJS Backend using JWT, PassportJS, and storing bcrypt-hashed User/Password credentials in a PostgreSQL database. However, when faced with strict medical data security requirements (HIPAA compliance, token encryption, temporary password resets for healthcare personnel, Brute-force protection), I realized that **building an Auth system from scratch was a major trap**.

That was when I turned my attention to exploring and adopting **AWS Cognito**.

---

### Building Your Own Auth System: The Hidden Costs Few Anticipate

When working on small-scale projects, writing a few `/login` and `/register` APIs returning a JWT Token seems trivial. But once the system goes live at scale with thousands of requests, a series of complex challenges emerge:
* **Session & Token Refresh Management**: How do you refresh tokens securely without disrupting the user experience?
* **Multi-Role-Based Access Control (RBAC)**: Ensuring Patients can strictly never access the Doctor Dashboard or Prescription Creation APIs.
* **Internal Account Provisioning**: How does a hospital onboard a new doctor? It requires generating a Temporary Password and forcing the doctor to change their password on the first login.
* **Security & Compliance**: Encrypting user data, mitigating Brute-force/DDoS attacks on authentication APIs, and securely sending password recovery emails.

If I were to custom-code all these features, I would have spent weeks solely tinkering with the Auth layer instead of focusing on developing the project's core business logic.

---

### What is AWS Cognito?

According to official AWS documentation, **Amazon Cognito** is a fully managed user identity management, authentication, and access control service. AWS Cognito lets you quickly add user sign-up, sign-in, and access control to your Web or Mobile applications.

The architecture of AWS Cognito consists of 2 core components:
1. **User Pools**: Stores and manages the User Directory. It handles the entire flow of sign-up, sign-in, MFA authentication, password recovery, and issues **JWT Tokens (ID Token, Access Token, Refresh Token)**.
2. **Identity Pools**: Enables direct authorization of users to grant them legitimate access to other AWS resources (such as S3 Buckets, DynamoDB) based on IAM Roles.

---

### How AWS Cognito Operates in the Healthcare Project

In the **Smart Healthcare Platform**, AWS Cognito completely offloads user management responsibilities from the NestJS Backend:

```text
[ Patient / Doctor / Receptionist ]  
    |  
    v (1. Credentials / Auth Request)  
[ AWS Cognito User Pool ]  
    |  
    v (2. Issue Signed JWT Tokens - RBAC Groups)  
[ Web App / Next.js ]  
    |  
    v (3. Request API + JWT Token)  
[ NestJS Backend Service ] ---> Verified by Cognito Public Key
```
1. **User Group Initialization & Authorization**: Seamless account onboarding.  
   * **Patient**: Registers directly via the Next.js Web App; Cognito automatically assigns the `Patient` role.  
   * **Doctor / Receptionist**: Administrators create accounts via the Cognito API. Cognito automatically dispatches an Email containing a Temporary Password. Upon the initial login to the Doctor Portal, Cognito forces the user to set a new password before issuing official Tokens.  
2. **JWT Token Verification on Backend**: The NestJS Backend does not store any user passwords. For every request accompanied by a Bearer JWT Token, the NestJS Middleware simply verifies the signature of the token against AWS Cognito's Public Key.  
3. **Sensitive Data Protection**: Cognito, combined with a UUID encryption strategy, completely anonymizes the original User ID, guaranteeing medical record privacy compliant with healthcare security standards.  

---

### Why AWS Cognito is the Perfect "Missing Puzzle Piece"?

After successfully integrating Cognito into the project, here are the 3 major value additions I gained:  
1. **Operational Cost & Development Time Savings**: Instead of spending 2-3 weeks setting up an Auth Service, it took me only 1 day to integrate the AWS Cognito SDK into NestJS and Next.js.
2. **Standardized Authorization (RBAC)**: Leveraging the `cognito:groups` attribute embedded within the JWT Token, Guard/Middleware implementations on NestJS to restrict Medical Report views or Prescription Creation became exceptionally lean and precise.
3. **Optimized Cost Efficiency (Generous Free Tier)**: AWS Cognito provides a free tier of up to **50,000 MAU (Monthly Active Users)** per month. This allowed the MVP phase of the project to launch at practically **$0 USD** for authentication infrastructure alone!

---

### Conclusion

Leveraging Cloud-Native services like **AWS Cognito** reflects the core mindset of modern system architecture. Instead of "reinventing the wheel" for classic engineering problems like Authentication, delegate the security and infrastructure overhead to AWS so you can dedicate 100% of your energy toward product optimization and solving business logic for your users!

---

### References

1. AWS. *"Amazon Cognito Developer Guide"*. (<https://docs.aws.amazon.com/cognito/>)
2. NestJS Documentation. *"Authentication with JWT & External Providers"*. (<https://docs.nestjs.com/security/authentication>)

View the article on Facebook [Here](<https://www.facebook.com/groups/awsstudygroupfcj/permalink/2228021697962790/?rdid=MLFJXbxXfs8sMMKH#>)
