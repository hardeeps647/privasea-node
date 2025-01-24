
# Privanetix Node Setup Guide 🚀

Welcome to the Privanetix Node setup guide! Follow the steps below to configure and start your node.

---

## 📋 **System Requirements**

Before starting, make sure your system meets the following requirements:

- **Operating System**: Ubuntu (Recommended)
- **CPU**: amd64 architecture
- **Storage**: 100GB available space
- **Memory**: 4GB RAM
- **Processor**: 6 cores, x86 architecture

---

## 🐳 **Step 1: Install Docker**

If Docker is not already installed on your system, follow the instructions below to install it.

### Installation Commands:

```bash
# Install dependencies
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add Docker's official repository
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Update package index
sudo apt update

# Install Docker
sudo apt install -y docker-ce
```

### Verify Docker Installation:

To ensure Docker is installed correctly, run the following command:

```bash
sudo docker --version
```

You should see something like:

```
Docker version 20.10.7, build f0df350
```

### Start Docker Service:

Make sure Docker is running and enabled to start at boot:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

---

## 🚀 **Step 2: Pull Docker Image**

Pull the required Docker image to run the node:

```bash
docker pull privasea/acceleration-node-beta:latest
```

---

## ⚙️ **Step 3: Node Configuration**

To configure your node, follow these steps:

1. **Switch to Root User**:

    ```bash
    sudo su
    ```

2. **Create and Navigate to the Program Directory**:

    ```bash
    mkdir -p /privasea/config && cd /privasea
    ```

3. **Get the Keystore File**:

    Use an existing wallet keystore file or generate a new one:

    ```bash
    docker run -it -v "/privasea/config:/app/config"     privasea/acceleration-node-beta:latest ./node-calc new_keystore
    ```

    You'll be prompted to enter a password for the keystore file.

    Example output:

    ```bash
    Enter password for a new key:      # Enter wallet password  
    Enter password again to verify:   # Re-enter the password for confirmation
    ```

    After successful creation, you’ll see a node address like:

    ```
    node address: 0xf07c3eF23ae7BEb8CD8bA5fF546E35Fd4b332B34
    ```

4. **Rename the Keystore File**:

    ```bash
    mv ./UTC--2025-01-06T06-11-07.485797065Z--f07c3ef23ae7beb8cd8ba5ff546e35fd4b332b34  ./wallet_keystore
    ```

---

## 🔗 **Step 4: Link Node Address and Reward Address**

- Use the generated wallet address and link it with the reward address on the DeepSea dashboard.

---

## 🟢 **Step 5: Start the Node**

Run the following command to start your Privanetix node:

```bash
# Navigate to the program directory
cd /privasea/

# Run the node command:
docker run -d -v "/privasea/config:/app/config" -e KEYSTORE_PASSWORD=your_password_here privasea/acceleration-node-beta:latest
```

Replace `your_password_here` with the actual keystore password.

---

## 🩺 **Step 6: View Node Health**

Check the node's health with this command:

```bash
docker logs -f <container_id>
```

Make sure to replace `<container_id>` with your actual container ID.

---

## 🛑 **Step 7: Stop the Node**

If you need to stop the node, use the following command:

```bash
docker ps -q --filter "ancestor=privasea/acceleration-node-beta:latest" | xargs --no-run-if-empty docker stop
```

If there’s no output, it means the node has been successfully stopped.

---

## ⚠️ **Important Notes**

- **📖 DYOR** (Do Your Own Research) before proceeding.
- **🛡️ Always use a new wallet** to reduce risks. The developers are not responsible for any loss of assets.

---

## 🔗 **Useful Links**

- **📂 GitHub Repository**: [Privanetix Node GitHub](https://github.com/your-repo-link)
- **🌐 DeepSea Dashboard**: [Access DeepSea Dashboard](https://deepsea.example)

---

### 🚀 Start automating your Privanetix Node today and join the decentralized world! 🌍
