# 🚀 DeepStream Docker Setup

This repository provides instructions to set up Docker and the NVIDIA Container Toolkit required to run NVIDIA DeepStream applications in containers.

---

## 📋 Prerequisites

1. **Install Docker CE**  
   Follow the official installation guide for your OS:  
   🔗 [Docker Installation Guide](https://docs.docker.com/engine/install)

2. **Post-install steps (optional but recommended)**  
   Enable running Docker without `sudo`:  
   🔗 [Docker Linux Post-install Guide](https://docs.docker.com/engine/install/linux-postinstall)

---

## 🧰 Install NVIDIA Container Toolkit

Required to enable GPU access inside Docker for DeepStream.

1. **Add the NVIDIA GPG key and repository**
   ```bash
   curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
     && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
       sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
       sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
   ```
   Optionally, configure the repository to use experimental packages:
   ```bash
   sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-toolkit.list
   ```
2. **Update the packages list from the repository**
   ```bash
   sudo apt-get update
   ```
3. **Install the NVIDIA Container Toolkit packages**
   ```bash
   export NVIDIA_CONTAINER_TOOLKIT_VERSION=1.17.8-1
   sudo apt-get install -y \
         nvidia-container-toolkit=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
         nvidia-container-toolkit-base=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
         libnvidia-container-tools=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
         libnvidia-container1=${NVIDIA_CONTAINER_TOOLKIT_VERSION}
   ```

Configuring Docker
1. **Configure the container runtime by using the <span style="color: green; font-weight: bold;">nvidia-ctk command</span>**
   ```bash
   sudo nvidia-ctk runtime configure --runtime=docker
   ```
2. **Restart the Docker daemon**
   ```bash
   sudo systemctl restart docker
   ```
