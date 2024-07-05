Here's the content in Markdown format:

```markdown
# Setting up Master Node

## Set hostname for master node
```sh
sudo hostnamectl set-hostname master-node
```

## Update package lists
```sh
sudo apt update
```

## Install necessary packages for Docker
```sh
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

## Add Docker's official GPG key
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

## Add Docker repository to apt sources
```sh
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Update package lists again
```sh
sudo apt update
```

## Install Docker CE
```sh
sudo apt install -y docker-ce
```

## Check Docker service status
```sh
sudo systemctl status docker
```

## Add current user to the docker group (optional, for non-root Docker usage)
```sh
sudo usermod -aG docker ${USER}
```

## Update package lists for Kubernetes components
```sh
sudo apt-get update
```

## Install Kubernetes components (kubelet, kubeadm, kubectl)
```sh
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
```

## Prevent Kubernetes packages from being automatically updated
```sh
sudo apt-mark hold kubelet kubeadm kubectl
```

## Enable and start kubelet service
```sh
sudo systemctl enable --now kubelet
```

## Install cri-dockerd (if required)
```sh
wget https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.14/cri-dockerd_0.3.14.3-0.ubuntu-jammy_amd64.deb
sudo dpkg -i cri-dockerd_0.3.14.3-0.ubuntu-jammy_amd64.deb
```

## Optionally switch to root user
```sh
sudo -i
```

## Initialize Kubernetes using cri-dockerd socket
```sh
kubeadm init --cri-socket unix:///var/run/cri-dockerd.sock
```

## Configure KUBECONFIG environment variable
```sh
echo 'export KUBECONFIG=/etc/kubernetes/admin.conf' >> ~/.bashrc
source ~/.bashrc
```

# Setting up Worker Node (Slave Node)

## Set hostname for worker node
```sh
sudo hostnamectl set-hostname slave-node
```

## Update package lists
```sh
sudo apt update
```

## Install necessary packages for Docker
```sh
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

## Add Docker's official GPG key
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

## Add Docker repository to apt sources
```sh
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Update package lists again
```sh
sudo apt update
```

## Install Docker CE
```sh
sudo apt install -y docker-ce
```

## Check Docker service status
```sh
sudo systemctl status docker
```

## Add current user to the docker group (optional, for non-root Docker usage)
```sh
sudo usermod -aG docker ${USER}
```

## Update package lists for Kubernetes components
```sh
sudo apt-get update
```

## Install Kubernetes components (kubelet, kubeadm, kubectl)
```sh
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
```

## Prevent Kubernetes packages from being automatically updated
```sh
sudo apt-mark hold kubelet kubeadm kubectl
```

## Enable and start kubelet service
```sh
sudo systemctl enable --now kubelet
```

## Install cri-dockerd (if required)
```sh
wget https://github.com/Mirantis/cri-dockerd/releases/download/v0.3.14/cri-dockerd_0.3.14.3-0.ubuntu-jammy_amd64.deb
sudo dpkg -i cri-dockerd_0.3.14.3-0.ubuntu-jammy_amd64.deb
```

## Optionally switch to root user
```sh
sudo -i
```
```