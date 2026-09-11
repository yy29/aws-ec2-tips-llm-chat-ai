## Setup CPU Only Python Development Environment on AWS EC2

### (1) [AWS](https://aws.amazon.com/) EC2 Instance Creation
- Region: Your choice
- Instance: m8a.medium / m9g.medium / r9g.medium
- AMI Image: Ubuntu 26.04
- Key Pairs: Create your key pairs and save private key file
- EBS Storage: Type: gp3, Volume: 20GB, IOPS: 3000, Throughput: 125MB/s
- Security Group: Create one with specs below
  - Inbound rule 1: Type: All traffic, Source: My IP
  - Outbound rule 1: Type: All traffic, Destination: Anywhere-IPv4

### (2) Connect to Instance
- Run SSH tool ([MobaXterm](https://mobaxterm.mobatek.net/) etc.)
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
sudo apt upgrade
sudo apt install python3-pip
sudo apt install python3.14-venv

# optional
sudo apt install unzip
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
