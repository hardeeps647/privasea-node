# 🌐 Privanetix Node Setup Guide

Welcome to the Privanetix Node setup guide! Follow these instructions to set up and run the Privanetix (Acceleration) Node effortlessly. 🚀

---

## 🖥️ Minimum System Requirements

- **OS**: Ubuntu (Recommended)
- **CPU**: amd64 architecture
- **Storage**: 100GB available storage
- **Memory**: 4GB RAM
- **Processor**: 6-core processor (x86 architecture)

---

## 🛠️ Complete Setup Commands  

Copy and paste the following commands into your terminal to set up the Privanetix Node:  

```bash
# Update system and install necessary dependencies
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add Docker's official repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Update package index and install Docker
sudo apt update && sudo apt install -y docker-ce

# Verify Docker installation
sudo docker --version

# Start and enable Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Pull the Privanetix node Docker image
docker pull privasea/acceleration-node-beta:latest

# Switch to root user
sudo su

# Create program directory
mkdir -p /privasea/config && cd /privasea

# Generate a new keystore file
docker run -it -v "/privasea/config:/app/config" privasea/acceleration-node-beta:latest ./node-calc new_keystore

# Enter password for a new key when prompted (e.g., 123456)
# Save the node address displayed after key creation

# Rename the keystore file
cd /privasea/config && ls
# Replace 'UTC--...' with the exact file name displayed in the previous step
mv ./UTC--2025-01-06T06-11-07.485797065Z--f07c3ef23ae7beb8cd8ba5ff546e35fd4b332b34 ./wallet_keystore
ls

# Start the Privanetix node
docker run -d -v "/privasea/config:/app/config" -e KEYSTORE_PASSWORD=123456 privasea/acceleration-node-beta:latest

# Verify node health
docker ps
docker logs -f $(docker ps -q --filter "ancestor=privasea/acceleration-node-beta:latest")
