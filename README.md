# Secure Web Application Deployment on AWS using Ansible and ALB

This project demonstrates a secure web application deployment on AWS using EC2, private web servers, a bastion host, Ansible automation, and an Application Load Balancer.
The deployment follows a basic cloud infrastructure pattern where public access is handled through a load balancer, while web servers remain private and are managed through controlled SSH access via a bastion host.

This is a hands-on cloud infrastructure project, not a live production system.
---
## Key Features

* Secure access through a bastion host
* Web servers deployed without public IP addresses
* Automated Nginx and HTML deployment using Ansible
* Application Load Balancer routing traffic to two private web servers
* Public/private subnet separation within a custom VPC
* Security group rules following least-privilege access principles
* Deployment validation using SSH, Ansible, target health checks, browser testing, and `curl`
---
## Technologies Used
* AWS EC2
* AWS VPC
* Public and private subnets
* Security Groups
* Application Load Balancer
* Target Groups
* Linux Ubuntu
* Ansible
* Nginx
* SSH / ProxyJump
* Bash
---
## Architecture Overview

The infrastructure includes:

* A bastion host deployed in a public subnet
* Two private web servers deployed without public IP addresses
* An Application Load Balancer deployed across public subnets
* A target group containing the private web servers
* Security groups controlling traffic between the ALB, bastion host, and web servers
* Ansible playbooks for automated Nginx installation and HTML deployment

The web servers are not directly accessible from the public internet. External users access the application through the ALB, while administrative access to the private instances is handled through the bastion host.
---
## Security Design
* Web servers have no public IP addresses
* SSH access to private web servers is only available through the bastion host
* Web servers allow HTTP traffic only from the ALB security group
* Web servers allow SSH traffic only from the bastion security group
* The bastion host allows SSH only from an authorised operator IP
* Application traffic and administrative access are separated
---

## Automation with Ansible
Ansible playbooks are stored in the `ansible/` directory.

Example validation command:

```bash
ansible -i ansible/inventory.ini webservers -m ping
```

Example deployment command:

```bash
ansible-playbook -i ansible/inventory.ini ansible/site.yml
```

The playbook installs and configures Nginx, deploys the application HTML content, and supports repeatable server configuration across the private web servers.

---

## How to Reproduce
1. Create a VPC with public and private subnets.
2. Configure route tables for public and private subnet access.
3. Create security groups for the bastion host, ALB, and private web servers.
4. Launch the bastion host in a public subnet.
5. Launch two private web servers without public IP addresses.
6. Configure SSH access using ProxyJump through the bastion host.
7. Run the Ansible playbooks to install Nginx and deploy the HTML application.
8. Create a target group and register the private web servers.
9. Create an Application Load Balancer across public subnets.
10. Forward ALB traffic to the target group.
11. Validate that the target group is healthy.
12. Confirm that the ALB DNS endpoint serves the web application.
---
## Validation and Troubleshooting
Validation activities included:
* Testing SSH access through the bastion host
* Running Ansible ping checks against private web servers
* Verifying Nginx installation and service status
* Testing HTTP responses with `curl`
* Checking Application Load Balancer target health
* Confirming that web servers were reachable only through approved access paths
* Reviewing security group rules for SSH and HTTP traffic
* Testing the ALB DNS endpoint from a browser

---

## Repository Structure

```text
secure-web-application-aws-ansible/
├── ansible/        # Inventory and Ansible playbooks
├── docs/           # Architecture diagram, screenshots, and validation evidence
├── README.md       # Project documentation
└── ...
```

---

## Write-up
A detailed project write-up is available here:
[Secure Web Application Deployment on AWS using Ansible and Application Load Balancer](https://medium.com/@jaymacsberg/secure-web-application-deployment-on-aws-using-ansible-and-application-load-balancer-888fc41c2570)
---
## Status
Completed hands-on AWS infrastructure and automation project.
The infrastructure may not currently be running, and any previously generated public endpoints may no longer be active.
---
## Career Relevance
This project demonstrates practical skills relevant to cloud support, infrastructure support, junior cloud engineering, DevOps, and systems operations roles, including:
* AWS infrastructure deployment
* Linux server administration
* Ansible automation
* Bastion-host access patterns
* Load balancer configuration and validation
* Security group design
* Network troubleshooting
* Technical documentation
