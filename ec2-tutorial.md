# Amazon EC2 Tutorial

## What is it?
Amazon Elastic Compute Cloud (**EC2**) is a cloud computing service provided by Amazon Web Services (AWS) that allows users to rent virtual servers (called **instances**) on demand. These instances can run applications, host websites, process data, or perform any computational task, with the ability to scale resources up or down as needed.

## Why does it exist? What problem does it solve?
EC2 exists to eliminate the need for physical hardware investments and management in data centers. It solves problems like:

- High upfront capital costs for servers
- Slow provisioning times (weeks or months for physical hardware vs. minutes in the cloud)
- Lack of scalability during demand spikes
- Overprovisioning (buying more hardware than needed)

By offering pay-as-you-go virtual servers, it enables rapid deployment, global reach, and cost efficiency for businesses of all sizes.

## Key Terms & Components You Must Understand First

| Term/Component              | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| **Instance**                | A virtual server in the AWS cloud, configurable with CPU, memory, storage, and networking. |
| **AMI (Amazon Machine Image)** | A pre-configured template that includes an operating system (e.g., Amazon Linux, Ubuntu, Windows) and optional software. It's the "blueprint" for launching instances. |
| **Instance Type**           | Defines the hardware specs of an instance (e.g., t2.micro for general-purpose, low-cost use). Families include general-purpose (t/m/a), compute-optimized (c), memory-optimized (r/x/z), etc. |
| **Security Group**          | A virtual firewall that controls inbound and outbound traffic to instances (e.g., allow SSH on port 22). |
| **Key Pair**                | Security credentials for secure login: AWS stores the public key; you keep the private key (.pem file). |
| **VPC (Virtual Private Cloud)** | A logically isolated network where you launch instances, controlling subnets, IP ranges, and routing. |
| **EBS (Elastic Block Store)** | Persistent block-level storage volumes attached to instances (like virtual hard drives). |
| **Region**                  | A geographic area (e.g., US East (Ohio)) where AWS data centers are located. |
| **Availability Zone (AZ)**  | Isolated locations within a Region for fault tolerance (e.g., us-east-2a). |
| **Elastic IP**              | A static public IP address that can be reassigned between instances. |

## Prior Knowledge Assumed
- Basic familiarity with computers and operating systems (Linux commands like SSH or Windows RDP)
- Networking basics (IP addresses, ports, firewalls)
- General understanding of what a virtual machine is
- An active AWS account (free to sign up, with Free Tier options)

No advanced programming is required for the basics.

## How Does It Work? Step-by-Step (Launching Your First Instance)

1. Sign in to the AWS Management Console and navigate to EC2.
2. Click **Launch instance**.
3. Give your instance a name (e.g., "MyFirstInstance").
4. Choose an **AMI** (e.g., Amazon Linux 2 – Free Tier eligible).
5. Select an **instance type** (e.g., t2.micro or t3.micro – Free Tier eligible).
6. Create or select a **key pair** (download the .pem file securely).
7. Configure **network settings** – use default VPC, but edit security group to allow SSH (port 22) from your IP only.
8. Add storage (default 8–30 GB EBS volume is fine for beginners).
9. Review and click **Launch instance**.
10. Wait for the instance status to become **running**.
11. Connect to your instance:
    - Linux/macOS: `ssh -i "your-key.pem" ec2-user@public-dns`
    - Windows: Use RDP with decrypted password
12. Use the instance (install software, run commands, deploy apps).
13. When finished → select instance → **Instance state** → **Terminate instance** (to stop charges).

**Important:** Always terminate instances you're not using to avoid unexpected costs.

## Main Parts & Variables Involved
- Instance (the VM itself)
- AMI ID
- Instance type/family
- Key pair name
- Security group rules (ports, source IPs)
- EBS volume size/type
- Region / Availability Zone
- User data (optional startup script)

## Inputs & Outputs
**Inputs:**
- Chosen AMI, instance type, key pair, security rules
- Applications/code/data you upload or install

**Outputs:**
- Running instance with public/private IP and DNS name
- Console output / logs
- Hosted services (website, API, processed data, etc.)

## Underlying Principles
- Virtualization (using hypervisors like AWS Nitro)
- Pay-as-you-go pricing (billed per second after first 60 seconds)
- Scalability & elasticity
- Shared responsibility model (AWS secures the hardware; you secure the OS & data)
- High availability via multiple Availability Zones

## Real-Life Use Cases & Examples
- Hosting websites and web applications
- Running backend APIs and microservices
- Data processing and batch jobs
- Machine learning model training (GPU instances)
- Game servers
- Development & testing environments

**Examples:**
- Hosting a WordPress blog
- Running a Minecraft server
- Training deep learning models
- Serving static websites with Nginx/Apache

## When to Use EC2 (and When Not To)
**Use EC2 when:**
- You need full control over the operating system
- Running custom or legacy software
- Long-running workloads
- Need specific hardware configurations (GPU, high memory, etc.)

**Avoid EC2 when:**
- You want zero server management → use AWS Lambda (serverless)
- Running containerized apps → prefer ECS / EKS
- Very simple websites → consider Amazon Lightsail or S3 + CloudFront

## Common Beginner Mistakes
- Forgetting to terminate instances → surprise bills
- Opening security groups to 0.0.0.0/0 (insecure)
- Choosing oversized instance types
- Losing the key pair file (can't connect)
- Not enabling MFA on AWS account
- Using root user instead of IAM users/roles
- Not backing up important data before termination

## EC2 vs. Alternatives
- **Google Compute Engine** — often cheaper sustained use, better Kubernetes integration
- **Azure Virtual Machines** — strong Windows & hybrid cloud support
- **DigitalOcean Droplets** — simpler, developer-friendly, flat pricing
- **AWS Lightsail** — easier, cheaper for simple apps
- **Lambda / Fargate** — serverless alternatives for event-driven or container workloads

## Advantages & Limitations

**Advantages:**
- Extremely flexible & scalable
- Thousands of instance types
- Global infrastructure
- Deep integration with other AWS services
- Spot & Reserved Instances for cost savings

**Limitations:**
- Requires server management (patching, monitoring, scaling)
- Can become expensive if not monitored
- Steeper learning curve than managed services
- Risk of data loss on termination (unless using persistent storage)

## 5-Minute Teaching Version
"EC2 is like renting a computer from Amazon's huge data centers. You pick the operating system, choose how powerful it should be, set up a secure login, and launch it in minutes. You connect to it like any remote server, install what you need, and shut it down when you're done to save money. It's way faster and more flexible than buying your own hardware."

## The 20% That Gives 80% of the Results
1. Launching, connecting to, and terminating an instance
2. Configuring security groups properly
3. Staying within the AWS Free Tier limits
4. Monitoring your billing dashboard

## Next Steps / Deeper Topics
- Auto Scaling Groups & Elastic Load Balancing
- EBS snapshots and backups
- Advanced VPC networking
- IAM roles and instance profiles
- Spot Instances & Savings Plans
- CloudWatch monitoring & alarms
- AWS Systems Manager for management
- Integrating EC2 with S3, RDS, Lambda, etc.
