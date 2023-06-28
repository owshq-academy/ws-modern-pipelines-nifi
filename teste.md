ws-modern-pipelines-nifi

Criando Pipeline de Dados Moderno com Apache Nifi na Prática


![img.png](img.png)


**Instalação Minikube**

https://minikube.sigs.k8s.io/docs/start/


**Requisitos**
2 CPUs or more
2GB of free memory
20GB of free disk space
Internet connection
Container ou virtual machine: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, ou VMware Fusion/Workstation

**Instalação**
macOS
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64
sudo install minikube-darwin-amd64 /usr/local/bin/minikube

Linux
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube


**Iniciar Cluster**
minikube start

kubectl create namespace nifi

kubectl apply -f deployment/workshop.yml 

Verificar se os pods estão com status running
kubectl get pods -n nifi

Inicialize o serviço 
minikube tunnel

acessar o nifi
http://127.0.0.1:9011/nifi/

acessar o nifi-registry
http://127.0.0.1:18080/nifi-registry





