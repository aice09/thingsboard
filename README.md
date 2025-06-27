# Dream IoT Lab with ThingsBoard

This guide helps you set up your own local IoT lab using **ThingsBoard Community Edition (CE)** with Docker Compose on a Linux host (e.g., Ubuntu).

---

## 🛠️ Prerequisites

- 🖥️ A laptop or desktop with **Ubuntu** (or your preferred Linux distro) installed.
- 🌐 Internet access.

---

## ⚡ Step 1: Update Your System

First, make sure your packages are up to date:

```bash
sudo apt update && sudo apt upgrade -y
```
## 🐳 Step 2: Install Docker Using EasyTool
Use this [docker-easytool script](https://github.com/aice09/docker-easytool) to install Docker and Docker Compose quickly:

```bash
cd /tmp
wget https://raw.githubusercontent.com/aice09/docker-easytool/main/install_docker.sh
chmod +x install_docker.sh
./install_docker.sh
```

### ✅ Verify installation:

```bash
docker --version
docker compose version
```

## 🔗 Step 3: Connect to Your Host
If working remotely, SSH into your host:

```bash
ssh username@ptc-lt-dream
```
> 📝 Replace username and ptc-lt-dream with your actual SSH user and hostname/IP.

## 📂 Step 4: Create Your Working Directory
Choose any path you like. Example:

```bash
mkdir -p /home/dream/dream/thingsboard
cd /home/dream/dream/thingsboard
```

## 📥 Step 5: Download the Docker Compose File
Get the official compose file:

```bash
wget https://raw.githubusercontent.com/aice09/thingsboard/refs/heads/main/docker-compose.yaml
```

## 🏗️ Step 6: Initialize the ThingsBoard Database Schema
Run this command once to set up the database schema and load demo data:

```bash
docker compose run --rm -e INSTALL_TB=true -e LOAD_DEMO=true thingsboard-ce
```

## ▶️ Step 7: Start All Services
Spin up all services in detached mode:

```bash
docker compose up -d
```

## ✅ Step 8: Verify Your Services
### 📦 a. PostgreSQL
Open pgAdmin (or any DB GUI):

```text
http://{your-host-ip}:5050
```
#### 📝 Add a new server in pgAdmin:

Name: thingsboard
Host/Address: postgres
Database: thingsboard
Username: postgres
Password: postgres

### 🌐 b. ThingsBoard UI
Access ThingsBoard in your browser:

```text
http://{your-host-ip}:8080
```
Example for local access:

```text
http://localhost:8080
```
#### 🔑 Default Login Credentials
- System Administrator 
  - Username: sysadmin@thingsboard.org
  - Password: sysadmin

- Tenant Administrator
  - Username: tenant@thingsboard.org
  - Password: tenant
    
- Customer User
  - Username: customer@thingsboard.org
  - Password: customer
    
### 📡 Step 9: Connect Your Host to the Access Point
We use a Globe modem as the access point.
### 🌐 Globe Modem Info
- WIFI SSID: PTC-WIFI
- Frequency: 2.4 GHz
- Password: PTC@2.0!
- Default IP: 192.168.254.254

#### 🗺️ Example Static IP Configuration
Set your device to the same subnet:

- IP: 192.168.254.10
- Subnet Mask: 255.255.255.0
- Gateway: 192.168.254.1

### ✅ Test connectivity to confirm everything works.
