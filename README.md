# Dockervm — Ubuntu 22.04 VM in Docker

A lightweight Ubuntu 22.04 virtual machine running in a Docker container using QEMU/KVM for optimal performance.

Features
- 🐳 Containerized Ubuntu 22.04 VM
- ⚡ KVM-accelerated for near-native performance
- 🌐 Web-based VNC access (port 6080)
- 🔑 SSH access (port 2221)
- 💾 Persistent storage volume

Prerequisites
- Docker installed
- KVM support on host machine
- sudo privileges (for KVM device access)

VM user and pass
- username: root
- password: root

Installation

# Clone the repository
git clone https://github.com/hironull/Dockervm.git
cd Dockervm

# Build the Docker image
docker build -t dockervm .

# Run the container
docker run --privileged -p 6080:6080 -p 2221:2222 -v $PWD/vmdata:/data dockervm

Notes
- The run command uses --privileged for simplicity; alternatively map /dev/kvm and add the necessary capabilities:
  docker run --device /dev/kvm -p 6080:6080 -p 2221:2222 -v $PWD/vmdata:/data dockervm
- Inside the container QEMU is expected to forward guest SSH to container port 2222 so host port 2221 maps to the VM's SSH.

Expose SSH remotely with ssh-tunnel
- To expose or forward the VM SSH port securely, use the companion ssh-tunnel project:
  https://github.com/hironull/ssh-tunnel

Security
- Running containers with KVM access or privileged mode is powerful and dangerous. Only run on trusted hosts.

License
- Add a LICENSE file (MIT / Apache-2.0 recommended).
