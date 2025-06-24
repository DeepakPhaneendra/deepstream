✅ Final README.md
# 🚀 DeepStream Docker Setup

This guide walks you through setting up Docker and the NVIDIA Container Toolkit to run NVIDIA DeepStream applications in containers.

---

## 📋 Prerequisites

- Install `docker-ce` by following the [official instructions](https://docs.docker.com/engine/install).
- After installation, follow the [post-installation steps](https://docs.docker.com/engine/install/linux-postinstall/) to allow running Docker without `sudo`.

---



### 1. Update your system:
```bash
sudo apt update
2. Install required packages:
sudo apt install \
  ca-certificates \
  curl \
  gnupg \
  lsb-release -y
3. Add Docker’s official GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
4. Add the Docker repository:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
5. Install Docker Engine:
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io -y
6. Verify Docker installation:
docker --version
🔧 Installing the NVIDIA Container Toolkit

1. Configure the production repository:
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | \
  sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg

curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
  sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
2. (Optional) Enable experimental packages:
sudo sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-toolkit.list
3. Update package list:
sudo apt-get update
4. Install the NVIDIA Container Toolkit:
export NVIDIA_CONTAINER_TOOLKIT_VERSION=1.17.8-1
sudo apt-get install -y \
  nvidia-container-toolkit=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
  nvidia-container-toolkit-base=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
  libnvidia-container-tools=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
  libnvidia-container1=${NVIDIA_CONTAINER_TOOLKIT_VERSION}
⚙️ Configure Docker to Use the NVIDIA Runtime

1. Configure the runtime:
sudo nvidia-ctk runtime configure --runtime=docker
This updates /etc/docker/daemon.json to use the NVIDIA Container Runtime.

2. Restart Docker:
sudo systemctl restart docker
