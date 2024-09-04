---

# Fullstack Inventory Management Application Deployment

## Overview

Welcome to the Inventory Management project, a full-stack application designed for efficient inventory tracking and management. This project includes both a frontend and backend component and utilizes various AWS services for deployment and management.

This repository contains the full-stack application created and developed by the YouTuber [ED Roh](https://www.youtube.com/@EdRohDev). I have forked this repository to share it with others who may find it useful.

![image](https://github.com/user-attachments/assets/1d46456a-9610-4536-aa24-dd751adc6182)



## AWS Services Used

- **EC2**: Hosts the backend application.
- **RDS**: Hosts the PostgreSQL database.
- **Amplify**: Hosts the frontend application.
- **S3**: Stores images.
- **VPC**: Provides a secure environment for running the applications.
- **Public Subnet**: Allows internet access.
- **Private Subnet**: Does not allow internet access.
- **API Gateway**: Manages and routes API requests to the backend application.

## Project Structure

The repository is divided into two main directories:

- **client**: Contains the frontend application.
- **server**: Contains the backend application.

### Client

The `client` directory contains a Next.js project. Here's a brief overview of its files and folders:

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

The `server` directory contains the backend application. Here’s what’s inside:

- **assets**: Backend assets.
- **prisma**: Database schema and migration files.
- **src**: Source code for the backend application.
- **.gitignore**: Git ignore file.
- **aws-ec2-instructions.md**: Instructions for deploying on EC2.
- **ecosystem.config.js**: PM2 configuration.
- **package-lock.json**: Dependency lock file.
- **package.json**: List of dependencies and scripts.
- **tsconfig.json**: TypeScript configuration.

The `server/src/index.ts` file includes the following routes:

- **Dashboard**: `./routes/dashboardRoutes`
- **Product**: `./routes/productRoutes`
- **User**: `./routes/userRoutes`
- **Expense**: `./routes/expenseRoutes`

Make sure to configure these routes in the API Gateway to ensure that requests are properly routed to your backend application.

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

6. **Set Up API Gateway**:
   - Go to the API Gateway in the AWS Management Console.
   - Create a new API.
   - Define your API routes and methods (GET, POST, etc.) and link them to your EC2 backend endpoints.
     - Ensure that routes correspond to the endpoints defined in `server/src/index.ts`:
       - **Dashboard**: `/api/dashboard`
       - **Product**: `/api/product`
       - **User**: `/api/user`
       - **Expense**: `/api/expense`
   - Deploy the API and note the endpoint URL to be used in your frontend application.

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

- Update the frontend application (`client`) with the API Gateway endpoint URL.
- Deploy changes to Amplify.

## Common Issues and Troubleshooting

- **EC2 Connectivity Issues**:
  - Ensure security groups and network ACLs are properly configured.
  
- **Database Connection Issues**:
  - Verify the RDS endpoint and security group settings.

- **Frontend Deployment Issues**:
  - Check Amplify build logs for errors.

- **API Gateway Issues**:
  - Ensure that API Gateway is properly configured and linked to the EC2 backend.

## Additional Resources

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/index.html)
- [AWS RDS Documentation](https://docs.aws.amazon.com/rds/index.html)
- [AWS Amplify Documentation](https://docs.amplify.aws/)
- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/index.html)
- [AWS API Gateway Documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [Next.js Documentation](https://nextjs.org/docs)

## Acknowledgments

Special thanks to [ED Roh](https://www.youtube.com/@EdRohDev) for creating and developing this full-stack project. This repository is a direct fork of his original work.

---

🎉🚀 **Thank you for checking out the Inventory Management project!** 🚀🎉

Feel free to clone, deploy, and customize it to fit your needs. Happy coding!

---
