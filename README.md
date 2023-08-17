## AWS EC2 Tips for Setting Up an LLM-based Chat AI with Minimal Cost

### (1) AWS EC2 Instance Creation
- Region: Your choice
- Instance: g4dn.xlarge
- Image: AWS Deep Learning Base GPU AMI (Ubuntu 20.04)
- Key Pairs: Create your key pairs and save private key file
- EBS Storage: gp3, Volume: 200GB, IOPS: 3000, Throughput: 125
- Security Group: Create one with specs below
  - Inbound rule 1: SSH, TCP, Port: 22, Source: YOUR_IP_ADDRESS
  - Inbound rule 2: Custom TCP, TCP, Port: 7860, Source: YOUR_IP_ADDRESS
  - Outbound rule 1: All Traffic, All, Port: All, Destination: 0.0.0.0/0

### (2) Connect to Instance
- Run SSH tool (Putty or MobaXterm etc.)
- Create new SSH session with `Instance IP address, username: ubuntu, private key file` to connect to the instance
- Do step (3)-(5) below in this SSH session.

### (3) Python Environment Setup
```
sudo apt install python3.8-venv
python3 -m venv my_venv3
source my_venv3/bin/activate
```

### (4) Git Clone SimplyRetrieve and Install Requirements
```
git clone https://github.com/RCGAI/SimplyRetrieve.git
cd SimplyRetrieve
pip install -r requirements.txt
```

### (5) Run SimplyRetrieve
```
cd chat
CUDA_VISIBLE_DEVICES=0 python chat.py --config configs/default_release.json
```

### (6) Access SimplyRetrieve
- In browser (Chrome or Edge or etc.), access `<Instance IP address>:7860`
