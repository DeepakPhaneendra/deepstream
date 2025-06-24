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
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | \
  sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg
