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
```
```bash
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
```bash
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
```bash
nano .env
```
- Copy this format and paste the required value there, you copied earlier from different websites
```bash
PORT=3001
LOGGER_LEVEL=debug

ORCHESTRATOR_URL=https://orchestrator.chasm.net
SCOUT_NAME=ccon
SCOUT_UID=PASTE UID
WEBHOOK_API_KEY=PASTE API KEY
WEBHOOK_URL=http://your_server_ip:3001/
PROVIDERS=groq
MODEL=gemma2-9b-it
GROQ_API_KEY=PASTE GROK API KEY HERE
```
- Save this file using `Ctrl + X` then `Y` and then press `Enter`

```bash
docker pull chasmtech/chasm-scout:latest
```
```bash
docker run -d --restart=always --env-file ./.env -p 3001:3001 --name scout chasmtech/chasm-scout
```
```bash
docker logs scout
```
```bash
curl localhost:3001
```
```bash
source./ChasmNode/.env
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $WEBHOOK_API_KEY" \
     -d '{"body":"{\"model\":\"gemma2-9b-it\",\"messages\":[{\"role\":\"system\",\"content\":\"You are a helpful assistant.\"}]}"}' \
     $WEBHOOK_URL
```
Monitor the node
```
docker stats scout
```
- Done !!
---
### Node Status

- You can now check your node status here : https://scout.chasm.net/dashboard
- If you see Yellow or Green, it means your node is working properly, also your yellow dot will be turned into green dot after 1 or 2 hrs
