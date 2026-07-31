---
title : "Implementation Steps"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2.1. </b> "
---

#### Step 1: User Pool Creation (User Directory Repository)

1. Access the **AWS Management Console**, search for and select the **Amazon Cognito** service.
2. Click **Create user pool** and configure the following properties:
   * **User pool name**: `healthcare`
   * **Sign-in options**: Check the primary sign-in method using **Email**.
   * **Password policy**: Set up a password policy compliant with healthcare data security standards (Minimum 8 characters, required uppercase, lowercase, numbers, and special characters).

![Figure 3](/images/5-Workshop/5.2.1-Step-to-do/Cognito.png)

##### Technical & Security Analysis (JWT & RSA Encryption):

* **Production Infrastructure Verification**: The `Estimated number of users: 9` metric proves that the Auth system is operationally active, successfully receiving test registrations and log-ins.
* **Asymmetric Encryption Standard**: The `Token signing key URL` (**JWKS Endpoint**) link provides Public Keys that allow the NestJS Backend to decrypt JWT Token signatures (RSA) completely automatically. As a result, the Backend does not need to store any user passwords.

#### Step 2: Role-Based Access Control (RBAC)

1. Access the `healthcare` User Pool --> select the **Group management** tab.
2. Create 3 user groups representing the system roles:
   * `Admin`: System Administrators & Receptionists.
   * `Doctor`: Practicing Physicians.
   * `Patient`: Patients booking appointments & viewing medical records.
3. Upon user login, Cognito automatically embeds group information into the `cognito:groups` Claim inside the **JWT Access Token**. The NestJS Backend uses this field to enforce API access authorization via Guards.

![Figure 4](/images/5-Workshop/5.2.1-Step-to-do/Cognito.png)

##### In-Depth Healthcare Data Privacy Analysis:

* **UUID Anonymization**: In the `User name` column, the system assigns a unique identifier string (UUID - e.g., `395ee448...`) instead of using Email or real names. Medical record tables in the Database only store this UUID, ensuring complete patient privacy.
* **Automated Email Verification Flow**: The `Confirmation status` column clearly displays `Confirmed` and `Unconfirmed` statuses, demonstrating that the system successfully integrated automated OTP/Link verification via Email upon new account registration.
* **Centralized Multi-Role Management**: The presence of an admin account (`superadminbkmed@gmail.com`) alongside regular user emails proves the Cognito infrastructure is smoothly coordinating RBAC flows across the entire system.

#### Step 3: Configure App Client (App Client for Next.js)

1. Under **App integration**, select **Create app client**.
2. Name the App Client (e.g., `healthcare-nextjs-web`).
3. Configure OAuth 2.0 parameters:
   * **Grant types**: Select `Authorization code grant` or `Implicit grant`.
   * **Disable Client Secret**: Disabling the **Client Secret** is mandatory. Since the Next.js Frontend runs on the browser (Single Page App - SPA), omitting the Client Secret eliminates the risk of exposing secret keys on the client side.

#### Step 4: Integrate JWT Verification into Backend (NestJS)

1. Extract the **JWKS Endpoint** from the User Pool overview page:  
   ```bash
   https://cognito-idp.<region>[.amazonaws.com/](https://.amazonaws.com/)<user-pool-id>/.well-known/jwks.json
   ```
2. In the NestJS project, configure `JwtStrategy` (using the `jwks-rsa` library):
   ```bash
   // Illustrating JwtStrategy configuration connecting to Cognito JWKS
   passportJwt.Strategy({
       jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
       secretOrKeyProvider: jwksRsa.passportJwtSecret({
           jwksUri: `[https://cognito-idp.ap-southeast-2.amazonaws.com/ap-southeast-2_xxxxxx/.well-known/jwks.json](https://cognito-idp.ap-southeast-2.amazonaws.com/ap-southeast-2_xxxxxx/.well-known/jwks.json)`,
       }),
       algorithms: ['RS256'],
   });
   ```
3. Whenever a User sends a Request with a Bearer Token attached, NestJS automatically downloads the Public Key from Cognito to verify the Token in-memory, avoiding the overhead of making round-trip API calls back to AWS.

#### Summary of Deployment Results

After completing the 4 execution steps for AWS Cognito:
1. **Built an Enterprise-Grade Auth System**: Secure sign-in via Email, automated OTP verification, and password policies meeting healthcare standards.
2. **Implemented Multi-Role-Based Access Control (RBAC)**: User identification via **anonymous UUIDs** and access granting using `cognito:groups` embedded in JWTs.
3. **Optimized Performance & Backend Security**: The NestJS Backend decrypts Tokens using asymmetric RSA algorithms (via JWKS) directly in server memory, boosting request handling speed while guaranteeing maximum security.