# kubentes install
## Docker installation [Referhere](https://get.docker.com/)
### step 1: Installing Docker runtime

```
sudo apt-get update 
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh 
sudo usermod -aG docker $user
``` 
### (OR) Add repo and Install packages
```
sudo apt update
sudo apt install -y curl gnupg2 software-properties-common apt-transport-https ca-certificates
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y containerd.io docker-ce docker-ce-cli

```

### step 2: Create required directories
```
sudo mkdir -p /etc/systemd/system/docker.service.d
```
### step3: Create daemon json config file
```
sudo tee /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
```

### step 4: Start and enable Services
```
sudo systemctl daemon-reload 
sudo systemctl restart docker
sudo systemctl enable docker
```

## Docker Engine latest:
```
sudo apt-get update
```
```
sudo apt-get install \
ca-certificates \
curl \
gnupg \
lsb-release
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

```

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

```
apt-cache madison docker-ce
```

```
sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```
## Kubeadm [Refer_here](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

### steps
#### Update the apt package index and install packages:
```
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl 
```
#### Download the Google Cloud public signing key:
```
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
```
#### Add the Kubernetes apt repository:
```
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
#### Update apt package index, install kubelet, kubeadm and kubectl:
```
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

## kubeadm cluster setup:
```
sudo -i
kubeadm init --pod-network-cidr=10.244.0.0/16
```
## Make a note of the instructions given which appear as shown above comand 

#### To start using your cluster, you need to run the following as a regular user:
```
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## sample for node join become root and execute below cmd 
```
kubeadm join 172.31.37.90:6443 --token q331we.xj6o2j07sy066v1r \
        --discovery-token-ca-cert-hash sha256:e281cbdb4c7de0c621e78d42d88b2bfb7d64d454afc56d3090dca3966be76ae3
```

## network plugin install kubeadm:

```
kubectl apply -f https://github.com/coreos/flannel/raw/master/Documentation/kube-flannel.yml
```

