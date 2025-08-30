## Setup Low Cost CPU Only Python Development Environment in AWS EC2

### (1) [AWS](https://aws.amazon.com/) EC2 Instance Creation
- Region: Your choice
- Instance: m7a.medium or m8g.medium or r8g.medium
- AMI Image: Ubuntu 24.04
- Key Pairs: Create your key pairs and save private key file
- EBS Storage: gp3, Volume: 20GB, IOPS: 3000, Throughput: 125
- Security Group: Create one with specs below
  - Inbound rule 1: SSH, TCP, Port: 22, Source: 0.0.0.0/0
  - Outbound rule 1: All Traffic, All, Port: All, Destination: 0.0.0.0/0

### (2) Connect to Instance
- Run SSH tool (Putty or [MobaXterm](https://mobaxterm.mobatek.net/) etc.)
- Create new SSH session with `Instance IP address, username: ubuntu, private key file` to connect to the instance
- Do steps below in this SSH session.

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
