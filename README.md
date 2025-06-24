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

```bash
# 1. Add the NVIDIA GPG key and repository
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | \
  sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg

curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
  sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
  sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

# 2. (Optional) Enable experimental features
sudo sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-toolkit.list

# 3. Update package index
sudo apt-get update

# 4. Install the toolkit
export NVIDIA_CONTAINER_TOOLKIT_VERSION=1.17.8-1
sudo apt-get install -y \
  nvidia-container-toolkit=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
  nvidia-container-toolkit-base=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
  libnvidia-container-tools=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
  libnvidia-container1=${NVIDIA_CONTAINER_TOOLKIT_VERSION}
