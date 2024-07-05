Here's your script converted to Markdown format with explanations:

```markdown
# Setup Script for Master Node

This script sets up Docker, Kubernetes components (`kubelet`, `kubeadm`, `kubectl`), and initializes the Kubernetes master node. It also configures the environment for `kubectl`.

## Script

```sh
#!/bin/bash

# Set hostname for master node
sudo hostnamectl set-hostname master-node

# Update package lists
sudo apt update

# Install necessary packages for Docker
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add Docker repository to apt sources
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update package lists again
sudo apt update

# Install Docker CE
sudo apt install -y docker-ce

# Check Docker service status
sudo systemctl status docker

# Add current user to the docker group (optional, for non-root Docker usage)
sudo usermod -aG docker ${USER}

# Update package lists for Kubernetes components
sudo apt-get update

# Install Kubernetes components (kubelet, kubeadm, kubectl)
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl

# Prevent Kubernetes packages from being automatically updated
sudo apt-mark hold kubelet kubeadm kubectl

# Enable and start kubelet service
sudo systemctl enable --now kubelet

# Install cri-dockerd (if required)
wget https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.14/cri-dockerd_0.3.14.3-0.ubuntu-jammy_amd64.deb
sudo dpkg -i cri-dockerd_0.3.14.3-0.ubuntu-jammy_amd64.deb

# Optionally switch to root user
sudo -i

# Initialize Kubernetes using cri-dockerd socket
kubeadm init --cri-socket unix:///var/run/cri-dockerd.sock

# Configure KUBECONFIG environment variable
echo 'export KUBECONFIG=/etc/kubernetes/admin.conf' >> ~/.bashrc
source ~/.bashrc
```

## Explanation

1. **Set hostname**: Sets the hostname of the master node to `master-node`.
2. **Update package lists**: Refreshes the list of available packages.
3. **Install Docker prerequisites**: Installs packages required to install Docker.
4. **Add Docker's official GPG key**: Adds Docker's GPG key for package verification.
5. **Add Docker repository**: Adds the Docker repository to the system's package sources.
6. **Install Docker CE**: Installs the Docker Community Edition.
7. **Check Docker service status**: Verifies if the Docker service is running.
8. **Add user to Docker group**: Adds the current user to the Docker group for non-root Docker usage (optional).
9. **Install Kubernetes prerequisites**: Installs packages required to install Kubernetes.
10. **Add Kubernetes GPG key**: Adds Kubernetes' GPG key for package verification.
11. **Add Kubernetes repository**: Adds the Kubernetes repository to the system's package sources.
12. **Install Kubernetes components**: Installs `kubelet`, `kubeadm`, and `kubectl`.
13. **Prevent auto-update of Kubernetes packages**: Marks the installed Kubernetes packages to prevent them from being automatically updated.
14. **Enable and start kubelet**: Enables and starts the `kubelet` service.
15. **Install cri-dockerd**: Downloads and installs the `cri-dockerd` package (if required).
16. **Switch to root user**: Optionally switches to the root user.
17. **Initialize Kubernetes**: Initializes the Kubernetes cluster using the `cri-dockerd` socket.
18. **Configure KUBECONFIG**: Sets the `KUBECONFIG` environment variable to point to the admin configuration file.

## Usage

1. Save the script to a file, for example `setup-master-node.sh`.
2. Make the script executable:
   ```sh
   chmod +x setup-master-node.sh
   ```
3. Run the script:
   ```sh
   ./setup-master-node.sh
   ```
```