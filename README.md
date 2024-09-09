# Chasm-scout Incentivised Node

## Project Information

- Twitter : https://x.com/ChasmNetwork
- Website : https://chasm.net

## Node Info

- Need VPS
- This node is Incentivised

### Min Requirements

| **Requirement**        | **Details**              |
|------------------------|--------------------------|
| **Operating System**   | Linux (linux/amd64, linux/arm64) |
| **vCPU**               | 1                        |
| **RAM**                | 1GB                       |
| **Disk Space**         | 20GB                     |
| **IP Address**         | Static IP                |


### Prerequisites

- Visit : https://console.groq.com/keys
- Copy the API key after signing in
- Save it somewhere for now

- Now visit : https://scout.chasm.net/private-mint
- Mint this with 0.025 $MNT Gas fee
- Bring MNT from Bybit (Cost free - No gas fee)

- After minting, click on `_mint(scout)` button
- Copy the value of `SCOUT_UID` and `WEBHOOK_API_KEY`
- Save it a notepad

- Now, Go to : https://dashboard.ngrok.com/signup
- Go to `Your Authtoken` section
- Click on `Show Authtoken` button in the corner, then copy the command and save it somewhere in a notepad

---
### Installation

```bash
sudo apt update && sudo apt upgrade -y
```
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
```bash
sudo apt-get update
```
```bash
sudo apt-get install ca-certificates curl
```
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```
```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```bash
sudo apt-get update
```
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```
mkdir ChasmNode && cd ChasmNode
```
## Run Multiple Scouts

```bash
nano .env
```
- Copy this format and paste the required value there, you copied earlier from different websites

```bash
services:
  scout1:
    image: chasmtech/chasm-scout:0.0.5
    container_name: scout1
    restart: always
    ports:
      - "3001:3001"
    environment:
      PORT: 3001
      LOGGER_LEVEL: debug
      ORCHESTRATOR_URL: https://orchestrator.chasm.net
      SCOUT_NAME: ""
      SCOUT_UID: 
      WEBHOOK_API_KEY: 
      WEBHOOK_URL: http://<YOUR_PUBLIC_IP>:3001
      MODEL: gemma2-9b-it
      PROVIDERS: groq
      GROQ_API_KEY: 

  scout2:
    image: chasmtech/chasm-scout:0.0.5
    container_name: scout1
    restart: always
    ports:
      - "3002:3002"
    environment:
      PORT: 3002
      LOGGER_LEVEL: debug
      ORCHESTRATOR_URL: https://orchestrator.chasm.net
      SCOUT_NAME: ""
      SCOUT_UID: 
      WEBHOOK_API_KEY: 
      WEBHOOK_URL: http://<YOUR_PUBLIC_IP>:3002
      PROVIDERS: groq
      MODEL: gemma2-9b-it
      GROQ_API_KEY: 
```
**Start Node**
```
docker compose up -d
```
**Check Logs**
```
docker logs scout1 -f
```
**Health Check**

```bash
curl localhost:3001
```

Monitor the node
```
docker stats scout1
```
- Done !!
---
### Node Status

- You can now check your node status here : https://scout.chasm.net/dashboard
- If you see Yellow or Green, it means your node is working properly, also your yellow dot will be turned into green dot after 1 or 2 hrs
