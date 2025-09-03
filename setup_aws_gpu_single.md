## Setup Small Scale Machine Learning Development Environment on AWS EC2

### (1) [AWS](https://aws.amazon.com/) EC2 Instance Creation
- Region: Your choice
- Instance: `g6e.xlarge / g6.xlarge / g5.xlarge / g4dn.xlarge`
- AMI Image: Deep Learning Base OSS Nvidia Driver GPU AMI (Ubuntu 24.04)
- AMI Image Release Notes: https://docs.aws.amazon.com/dlami/latest/devguide/X86-base-dlami.html
- Key Pairs: Create your key pairs and save private key file
- EBS Storage: gp3, Volume: 50GB, IOPS: 3000, Throughput: 125
- Security Group: Create one with specs below
  - Inbound rule 1: Type: All traffic, Source: My IP
  - Outbound rule 1: Type: All traffic, Destination: Anywhere-IPv4
- Note: This AMI Image comes preinstalled with Docker and Nvidia-docker2

### (2) Connect to Instance
- Run SSH tool (Putty or [MobaXterm](https://mobaxterm.mobatek.net/) etc.)
- Create new SSH session with `Instance IP address, username: ubuntu, private key file` to connect to the instance
- Do steps below in this SSH session.

### (3) Remove Unattended-upgrades to Prevent Surprise System Failures
```
sudo systemctl stop unattended-upgrades
sudo apt remove unattended-upgrades
```

### (4) Install Necessary Packages
```
sudo apt update
sudo apt install python3.12-venv
```

### (5) Create Non-root User with Password
```
sudo useradd -m -s /bin/bash <username>
echo "username:newpassword123" | sudo chpasswd
```

### (6) Setup Non-root User Environment
Run the following in non-root user's SSH terminal.

#### Inhibit Long Welcome Screen in SSH Terminal
```
touch ~/.hushlogin
```

#### Setup Python Virtual Environment
```
python3 -m venv my_venv3
source my_venv3/bin/activate
```
