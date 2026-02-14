# Secure Web Application Deployment on AWS using Ansible & ALB

Secure access via Bastion (no public IPs on web servers)

Automated NGINX + HTML deploy via Ansible

High availability via ALB across 2 public subnets (2 AZs)

## Overview
This project demonstrates a secure, highly available web application deployment on AWS using:
- EC2 (Bastion + 2 private web servers)
- Application Load Balancer (ALB)
- VPC with public/private subnets
- Security Groups (least privilege)
- Ansible automation (NGINX + HTML deployment)

## Architecture
![Architecture Diagram](architecture/architecture.png)

## Security Design
- Web servers have **no public IP**
- SSH access is only through the **Bastion Host**
- Web servers allow **HTTP (80) only from the ALB security group**
- Bastion allows **SSH (22) only from my IP**

## Automation (Ansible)
Playbooks are in `ansible/`.

Run (example):
```bash
ansible -i ansible/inventory.ini webservers -m ping
ansible-playbook -i ansible/inventory.ini ansible/site.yml

##How to Reproduce
Create VPC/subnets/route tables
Create SGs (Bastion, ALB, Web)
Launch instances
Run Ansible playbook
Create target group + ALB

## Write-up
- Medium/Hashnode: https://medium.com/@jaymacsberg/secure-web-application-deployment-on-aws-using-ansible-and-application-load-balancer-888fc41c2570https://medium.com/@jaymacsberg/secure-web-application-deployment-on-aws-using-ansible-and-application-load-balancer-888fc41c2570
