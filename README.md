![Alt text](/Host_a_Static_Website_on_AWS(2).png)


# Host a Static Website on AWS

## Project Overview

This project demonstrates how to host a static HTML web application on AWS using an EC2 instance. It utilizes various AWS resources to ensure a scalable and secure deployment.

## Technologies & Resources Used

1. **Virtual Private Cloud (VPC)** – Configured with public and private subnets across two Availability Zones.
2. **Internet Gateway** – Facilitates connectivity between VPC instances and the Internet.
3. **Security Groups** – Acts as a network firewall mechanism.
4. **Multi-AZ Deployment** – Enhances system reliability and fault tolerance.
5. **Public Subnets** – Used for infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint** – Enables secure connections to assets within both public and private subnets.
7. **Private Subnets** – Hosts web servers (EC2 instances) for enhanced security.
8. **NAT Gateway** – Allows private application and data subnets to access the Internet.
9. **EC2 Instances** – Hosts the website.
10. **Application Load Balancer & Target Group** – Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
11. **Auto Scaling Group** – Automatically manages EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.
12. **GitHub** – Stores web files for version control and collaboration.
13. **AWS Certificate Manager** – Secures application communications.
14. **Simple Notification Service (SNS)** – Alerts about activities within the Auto Scaling Group.
15. **Route 53** – Registers the domain name and manages DNS records.

## Architecture Diagram

The reference architecture diagram illustrating the deployment setup is available in the repository.

## Project Repository

The full project, including setup scripts and documentation, is available on GitHub: [GitHub Repository](https://github.com/dhatboyjay/Host-A-Static-Website-on-AWS-2)

## Deployment Steps

### 1. Clone the Repository

```bash
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
cd host-a-static-website-on-aws
```

### 2. Launch an EC2 Instance

- Select an **Amazon Linux 2** or **Ubuntu** AMI.
- Choose an appropriate instance type (e.g., **t2.micro** for free-tier eligibility).
- Configure security groups to allow **HTTP (port 80) and SSH (port 22)** traffic.
- Attach an IAM role if required.

### 3. Connect to the Instance

```bash
ssh -i your-key.pem ec2-user@your-ec2-public-ip
```

### 4. Install Web Server & Deploy Application

Run the provided setup script to install and configure the web server:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/dhatboyjay/Host-A-Static-Website-on-AWS-2.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd  
# Start the Apache HTTP Server to serve web content
systemctl start httpd  
```

This script will:

- Install Apache.
- Copy website files to the web root (`/var/www/html`).
- Start the web server.

### 5. Access the Website

Once the setup is complete, open your browser and enter the **public IP address** of your EC2 instance:

```
http://your-ec2-public-ip
```

If configured correctly, your static website should be live!

## Future Enhancements

- Automate deployment with **Terraform** or **CloudFormation**.
- Use **Amazon S3 + CloudFront** for better scalability.
- Implement **SSL/TLS** with **Let’s Encrypt** for HTTPS.

## Author

This project was created by Joshua Agyapong as part of a DevOps learning experience.

## License

This project is open-source and available under the [MIT License](LICENSE).

