# 🦊 Cowrie Honeypot Project (Ubuntu VM on macOS)

## 🔒 Project Overview
This project sets up and runs a medium-interaction SSH honeypot using [Cowrie](https://github.com/cowrie/cowrie) inside a secure Ubuntu VM running on macOS. The honeypot simulates a vulnerable Linux system and logs attacker behavior, including login attempts, brute force attacks, and executed commands.

---

## 🧰 Tools & Technologies
- 💻 **macOS** (host)
- 🐧 **Ubuntu Linux VM** (VirtualBox)
- 🐍 **Python 3 & Virtual Environment**
- 📦 **Cowrie Honeypot**
- 📡 **SSH Port Forwarding (Optional Exposure)**

---

## 📌 Project Goals
- Deploy a safe and isolated honeypot environment
- Simulate a vulnerable SSH server
- Capture real-world brute-force and command injection attempts
- Practice Security+ skills: logging, system hardening, network security, and threat analysis

---

## 🛠️ Step-by-Step Setup

### ✅ 1. Install Ubuntu VM on macOS *(Completed)*
- Used VirtualBox or UTM to install Ubuntu

### ✅ 2. Update & Install Dependencies
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3-venv -y

### ✅ 3. Clone & Set Up Cowrie
```bash
git clone https://github.com/cowrie/cowrie.git
cd cowrie
python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
cp etc/cowrie.cfg.dist etc/cowrie.cfg
```

### ✅ 4. Configure Listening Port
```bash
nano etc/cowrie.cfg
```
Then edit this line:
```ini
listen_endpoints = tcp:2222:interface=0.0.0.0
```
This tells Cowrie to listen on TCP port 2222 for all network interfaces.

### ✅ 5. Start Cowrie
```bash
bin/cowrie start
bin/cowrie status
```
You should see output confirming Cowrie is running. If not, check for typos or config issues.

### ✅ 6. Simulate an Attack
```bash
ssh root@localhost -p 2222
```
This simulates an attacker connecting to your honeypot. Try fake usernames/passwords — Cowrie will log them.

### ✅ 7. View Logged Activity
```bash
tail -f var/log/cowrie/cowrie.log
```
Use this to watch real-time logs of failed logins, fake shell commands, and attacker IPs.

---

### 🧪 Next Step: Test It on a Public Network
After confirming that Cowrie works locally, the next step is to expose the honeypot to the internet using router port forwarding or a free-tier cloud VM. This allows real-world attackers and bots to interact with your honeypot, helping you learn how brute force attacks and post-exploitation behavior really happen in the wild.
