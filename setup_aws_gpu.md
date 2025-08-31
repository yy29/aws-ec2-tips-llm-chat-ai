## Setup Machine Learning Development Environment on AWS EC2

### (1) [AWS](https://aws.amazon.com/) EC2 Instance Creation
- Region: Your choice
- Instance: g6.xlarge or g5.xlarge or g6e.xlarge or g4dn.xlarge
- AMI Image: Deep Learning Base OSS Nvidia Driver GPU AMI (Ubuntu 24.04)
- AMI Image Release Notes: https://docs.aws.amazon.com/dlami/latest/devguide/X86-base-dlami.html
- Key Pairs: Create your key pairs and save private key file
- EBS Storage: gp3, Volume: 100GB, IOPS: 3000, Throughput: 125
- Security Group: Create one with specs below
  - Inbound rule 1: Type: All traffic, Source: My IP
  - Outbound rule 1: Type: All traffic, Destination: Anywhere-IPv4

### (2) Connect to Instance
- Run SSH tool (Putty or [MobaXterm](https://mobaxterm.mobatek.net/) etc.)
- Create new SSH session with `Instance IP address, username: ubuntu, private key file` to connect to the instance
- Do step (3)-(6) below in this SSH session.

### (3) Remove Unattended-upgrades to Prevent Surprise System Failures
```
sudo systemctl stop unattended-upgrades
sudo apt remove unattended-upgrades
```

### (4) Python Environment Setup
```
sudo apt update
sudo apt install python3.12-venv
python3 -m venv my_venv3
source my_venv3/bin/activate
```
