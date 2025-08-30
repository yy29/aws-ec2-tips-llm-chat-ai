## AWS EC2 Tips for Setting Up an LLM-based Chat AI with Minimal Cost

### (1) [AWS](https://aws.amazon.com/) EC2 Instance Creation
- Region: Your choice
- Instance: g6.xlarge or g5.xlarge or g6e.xlarge or g4dn.xlarge
- AMI Image: Deep Learning Base OSS Nvidia Driver GPU AMI (Ubuntu 20.04)
- AMI Image Release Notes: https://docs.aws.amazon.com/dlami/latest/devguide/X86-base-dlami.html
- Key Pairs: Create your key pairs and save private key file
- EBS Storage: gp3, Volume: 100GB, IOPS: 3000, Throughput: 125
- Security Group: Create one with specs below
  - Inbound rule 1: SSH, TCP, Port: 22, Source: YOUR_IP_ADDRESS
  - Inbound rule 2: Custom TCP, TCP, Port: 7860, Source: YOUR_IP_ADDRESS
  - Outbound rule 1: All Traffic, All, Port: All, Destination: 0.0.0.0/0

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
sudo apt install python3.9-venv
python3 -m venv my_venv3
source my_venv3/bin/activate
```

### (5) Git Clone [SimplyRetrieve](https://github.com/RCGAI/SimplyRetrieve.git) and Install Requirements
```
git clone https://github.com/RCGAI/SimplyRetrieve.git
cd SimplyRetrieve
pip install -r requirements.txt
```

### (6) Run SimplyRetrieve
```
cd chat
CUDA_VISIBLE_DEVICES=0 python chat.py --config configs/default_release.json
```

### (7) Access SimplyRetrieve
- In browser (Chrome or Edge or etc.), access `<Instance IP address>:7860`
- You are done! Should be able to see a Chat AI interface by now
