## Setup Machine Learning Development Environment on AWS EC2
*Small scale instance: For inferencing, finetuning and traditional deep learning*  
*Medium scale instance: For small scale model training and finetuning*  
*Large scale instance: For medium scale language & vision models pretraining*  
*Ultra scale instance: For large language & vision models pretraining*  

### (1) [AWS](https://aws.amazon.com/) EC2 Instance Creation
- Region: Your choice
- Instance: Select one from below (my favorite: g6.xlarge)
  - Small scale: `g7e.2xlarge / g7.2xlarge / g6e.xlarge / g6.xlarge / g5.xlarge / g4dn.xlarge`
  - Medium scale: `g7e.12xlarge / g7e.24xlarge / p5.4xlarge / g6e.12xlarge / g6e.48xlarge / p4d.24xlarge / p4de.24xlarge`
  - Large scale: `p5.48xlarge / p5e.48xlarge / p5en.48xlarge / p6e-gb200.36xlarge / p6-b200.48xlarge / p6-b300.48xlarge`
  - Ultra scale: `u-p6e-gb200x36 / u-p6e-gb200x72`
- AMI Image: Deep Learning Base OSS Nvidia Driver GPU AMI (Ubuntu 26.04) [Release Notes](https://docs.aws.amazon.com/dlami/latest/devguide/appendix-ami-release-notes.html)
- Key Pairs: Create your key pairs and save private key file
- EBS Storage: Select one from below
  - Small scale: `Type: gp3, Volume: 100GB, IOPS: 3000, Throughput: 125MB/s`
  - Medium scale: `Type: gp3, Volume: 500GB, IOPS: 3000, Throughput: 125MB/s`
  - Large scale: `Type: gp3, Volume: 2000GB, IOPS: 6000, Throughput: 250MB/s`
  - Ultra scale: `Type: gp3, Volume: 4000GB, IOPS: 10000, Throughput: 500MB/s`
- Security Group: Create one with specs below
  - Inbound rule 1: `Type: All traffic, Source: My IP`
  - Outbound rule 1: `Type: All traffic, Destination: Anywhere-IPv4`
- Note: This AMI Image comes preinstalled with Docker and NVIDIA Container Toolkit

### (2) Connect to Instance
- Run SSH tool ([MobaXterm](https://mobaxterm.mobatek.net/) etc.)
- Create new SSH session with `Instance IP address, username: ubuntu, private key file` to connect to the instance
- Do steps below in this SSH session.

### (3) Remove Unattended-upgrades to Prevent Surprise System Failures
```
sudo systemctl stop unattended-upgrades
sudo apt remove unattended-upgrades
```

### (4) Install and Update Necessary Packages
```
sudo apt update
sudo apt upgrade

# optional
sudo apt install language-pack-ja
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

#### Setup Private and Public SSH Keys
Create .ssh folder, then copy your personal private and public SSH keys to .ssh/ folder, then set access permissions as follow:
```
chmod 600 .ssh
chmod 600 .ssh/private_key
chmod 644 .ssh/public_key.pub
```
If currently do not possess any SSH key, generate a new pair by running the following command:
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
or
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

#### Setup Python Virtual Environment
```
python3 -m venv my_venv3
source my_venv3/bin/activate
```
