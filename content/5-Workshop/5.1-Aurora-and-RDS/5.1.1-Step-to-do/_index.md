---
title : "Implementation Steps"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1.1. </b> "
---

#### Step 1: Database Cluster Creation (Database Creation)

1. Access the **AWS Management Console**, search for and select the **Aurora and RDS** service.
2. Select **Databases** --> click **Create database**:
   * **Creation method**: Choose **Standard create**.
   * **Engine options**: Select **PostgreSQL** (Ensures consistency with the initial architecture and guarantees full compatibility with Prisma ORM on the NestJS Backend).
   * **Settings**:
     + DB instance identifier: `healthcare-db`
     + Master username / password: Set up system administrator credentials.
   * **Instance configuration**: Select the `db.t4g.micro` configuration.

##### Technical Analysis (Cost Optimization):

The `db.t4g.micro` instance family utilizes ARM-based processors (**AWS Graviton2**). This is a significant advantage in terms of Cloud operational strategy: ARM architecture offers higher processing performance at a substantially lower running cost compared to traditional x86 architecture, making it ideal for the project's Dev/Test environments.

![Figure 1](/images/5-Workshop/5.1.1-Step-to-do/Aurora-and-RDS.png)

#### Step 2: Network & Security Configuration (Network & Security)

1. Route the database into a specific **Virtual Private Cloud (VPC)** within the system.
2. **Configure Security Group (VPC Firewall)**:
   * Open the default PostgreSQL port `5432` to accept incoming connections from the Backend.
3. **Encryption in Transit**: Download the AWS-provided SSL Certificate file (`global-bundle.pem`) to prepare for secure connections.

![Figure 2](/images/5-Workshop/5.1.1-Step-to-do/Aurora-and-RDS(2).png)

##### Security Review & Critique:

* **Current State in Screenshot**: The *Security group rules* section under the `CIDR/IP - Inbound` rule is currently set to `0.0.0.0/0` (open to the entire Internet).
* **Dev/Test Purpose**: This configuration allows team members to query data effortlessly from local machines using tools such as DBeaver, TablePlus, or Prisma Studio.
* **Remediation for Production**: For a healthcare system carrying sensitive patient records, exposing the Database port directly to the Internet poses an extreme security risk. When moving to production, it is mandatory to remove the `0.0.0.0/0` rule and restrict access strictly to the Backend Server (EC2) IP or Bastion Host via port `5432`.

#### Step 3: Extract Connection String

1. After the database status changes to **Available**, navigate to the **Connectivity & security** tab.
2. Retrieve the host address (**Endpoint**): `healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com`
3. Download the SSL certificate file for connection encryption using the command:  
   `curl -o global-bundle.pem https://truststore.pki.rds.amazonaws.com/global/global-bundle.pem`
4. Combine details (*Endpoint, Port 5432, Username, Password*) to construct the `DATABASE_URL` string compliant with healthcare encryption standards (`sslmode=verify-full`):  
   ```bash
   postgresql://<username>:<password>@[healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com:5432/postgres?sslmode=verify-full&sslrootcert=global-bundle.pem](https://healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com:5432/postgres?sslmode=verify-full&sslrootcert=global-bundle.pem)
   ```

#### Step 4: Synchronize Schema from NestJS to AWS RDS

1. Update the `DATABASE_URL` environment variable inside the `.env` file at the root directory of the NestJS Backend source code:  
   ```bash
   DATABASE_URL="postgresql://<username>:<password>@[healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com:5432/postgres?sslmode=verify-full&sslrootcert=global-bundle.pem](https://healthcare-db.cdu4ym0ac08t.ap-southeast-2.rds.amazonaws.com:5432/postgres?sslmode=verify-full&sslrootcert=global-bundle.pem)"
   ```
2. Open Terminal and execute Prisma CLI commands to automatically initialize the database schema on AWS RDS:  
   ```bash
   npx prisma db push
   # Or for production use:
   npx prisma migrate deploy
   ```
3. The Prisma tool will automatically connect over an encrypted SSL channel and generate all table schemas (`User`, `Appointment`, `DoctorProfile`, etc.) on the Cloud without requiring manual SQL DDL operations.

#### Summary of Deployment Results

Through 4 execution steps, the team successfully built the core data foundation for the healthcare application:
1. **Solid Infrastructure Setup**: Guaranteed compatibility between **PostgreSQL** and **Prisma ORM**, while optimizing budget using the **ARM Graviton2** instance class (`db.t4g.micro`).
2. **Compliant Data Security**: Enforced encryption in transit using **SSL Certificate** (`global-bundle.pem`).
3. **Automated Synchronization**: Executed Prisma CLI to push the complete NestJS project schema to AWS RDS, leaving it ready for operational read/write traffic.