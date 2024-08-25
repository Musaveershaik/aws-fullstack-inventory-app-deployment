# Inventory Management

## Overview

This project is a full-stack inventory management application. It includes both a frontend and a backend component. The frontend is built with Next.js and is hosted on AWS Amplify. The backend is a Node.js application hosted on an EC2 instance, with a PostgreSQL database managed via AWS RDS. Images are stored in AWS S3, and the entire application operates within a secure Virtual Private Cloud (VPC) setup.

## AWS Services Used

- **EC2**: Hosts the backend application.
- **RDS**: Hosts the PostgreSQL database.
- **Amplify**: Hosts the frontend application.
- **S3**: Stores images.
- **VPC**: Provides a secure environment for running the applications.
- **Public Subnet**: Allows internet access.
- **Private Subnet**: Does not allow internet access.

## Project Structure

The repository is divided into two main directories:

- **client**: Contains the frontend application.
- **server**: Contains the backend application.

### Client

The client directory contains a Next.js project. Here's a brief overview of its files and folders:

- **public**: Publicly accessible assets.
- **src**: Source code for the application.
- **.eslintrc.json**: ESLint configuration.
- **.gitignore**: Git ignore file.
- **README.md**: Documentation for the frontend application.
- **next.config.mjs**: Configuration file for Next.js.
- **package-lock.json**: Dependency lock file.
- **package.json**: List of dependencies and scripts.
- **postcss.config.mjs**: PostCSS configuration.
- **tailwind.config.ts**: Tailwind CSS configuration.
- **tsconfig.json**: TypeScript configuration.

### Server

The server directory contains the backend application. Here’s what’s inside:

- **assets**: Backend assets.
- **prisma**: Database schema and migration files.
- **src**: Source code for the backend application.
- **.gitignore**: Git ignore file.
- **aws-ec2-instructions.md**: Instructions for deploying on EC2.
- **ecosystem.config.js**: PM2 configuration.
- **package-lock.json**: Dependency lock file.
- **package.json**: List of dependencies and scripts.
- **tsconfig.json**: TypeScript configuration.

## Deployment Instructions

### 1. Setting Up AWS Services

1. **Create an EC2 Instance**:
   - Launch an EC2 instance with the desired configuration (e.g., Ubuntu, t2.micro).
   - Configure security groups to allow HTTP/HTTPS and SSH access.
   - Install Node.js and necessary dependencies on the EC2 instance.

2. **Set Up RDS**:
   - Launch an RDS instance with PostgreSQL.
   - Configure security groups to allow access from the EC2 instance.
   - Note the endpoint, username, and password for connecting to the database.

3. **Configure S3**:
   - Create an S3 bucket for storing images.
   - Set up necessary permissions and policies.

4. **Deploy Frontend with AWS Amplify**:
   - Go to AWS Amplify in the AWS Management Console.
   - Connect your GitHub repository and choose the `client` directory.
   - Configure build settings and deploy.

5. **Set Up VPC**:
   - Create a VPC with both public and private subnets.
   - Ensure the EC2 instance is placed in the private subnet while the RDS instance can be accessed through it.

### 2. Deploy Backend on EC2

1. **SSH into EC2 Instance**:
   ```bash
   ssh -i "your-key.pem" ubuntu@your-ec2-instance-public-dns
   ```

2. **Clone the Repository**:
   ```bash
   git clone https://github.com/Musaveershaik/inventory-management.git
   cd inventory-management/server
   ```

3. **Install Dependencies**:
   ```bash
   npm install
   ```

4. **Configure Environment Variables**:
   - Create a `.env` file with the necessary environment variables (e.g., database connection string).

5. **Start the Application**:
   - Use PM2 to manage the application:
     ```bash
     npm install -g pm2
     pm2 start ecosystem.config.js
     ```

### 3. Connect Frontend and Backend

- Update the frontend application (`client`) with the backend API URL.
- Deploy changes to Amplify.

## Common Issues and Troubleshooting

- **EC2 Connectivity Issues**:
  - Ensure security groups and network ACLs are properly configured.
  
- **Database Connection Issues**:
  - Verify the RDS endpoint and security group settings.

- **Frontend Deployment Issues**:
  - Check Amplify build logs for errors.

## Additional Resources

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/index.html)
- [AWS RDS Documentation](https://docs.aws.amazon.com/rds/index.html)
- [AWS Amplify Documentation](https://docs.amplify.aws/)
- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/index.html)
- [Next.js Documentation](https://nextjs.org/docs)
