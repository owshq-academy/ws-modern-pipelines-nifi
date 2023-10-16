**ws-modern-pipelines-nifi**



#Instalando NifiKop no GKE

**01 - Criar um novo projeto no Google Cloud Platform (GCP)**

**02 - Criar um Cluster Kubernetes. NÃO É GRATUITO. ANTES DE INICIAR LEIA A POLITICA DE COBRANÇA**

**03 - Clonar o repositório.**
```bash
git clone https://github.com/owshq-academy/ws-modern-pipelines-nifi.git
````

**04 - Navegar para o diretório "ws-modern-pipelines-nifi/kubernetes"**

**05-Criar o namespace**
```bash
kubectl create namespace cert-manager
kubectl create namespace nifi
kubectl create namespace zookeeper
```

**06-Instalar o cert-manager**
```bash
kubectl apply -f \
    https://github.com/jetstack/cert-manager/releases/download/v1.7.2/cert-manager.yaml
````

**07-deploy manually the crds**
```bash
kubectl apply -f https://raw.githubusercontent.com/konpyutaika/nifikop/master/config/crd/bases/nifi.konpyutaika.com_nificlusters.yaml
kubectl apply -f https://raw.githubusercontent.com/konpyutaika/nifikop/master/config/crd/bases/nifi.konpyutaika.com_nifiusers.yaml
kubectl apply -f https://raw.githubusercontent.com/konpyutaika/nifikop/master/config/crd/bases/nifi.konpyutaika.com_nifiusergroups.yaml
kubectl apply -f https://raw.githubusercontent.com/konpyutaika/nifikop/master/config/crd/bases/nifi.konpyutaika.com_nifidataflows.yaml
kubectl apply -f https://raw.githubusercontent.com/konpyutaika/nifikop/master/config/crd/bases/nifi.konpyutaika.com_nifiparametercontexts.yaml
kubectl apply -f https://raw.githubusercontent.com/konpyutaika/nifikop/master/config/crd/bases/nifi.konpyutaika.com_nifiregistryclients.yaml
````

**08-deploy the helm chart**
```bash
helm install nifikop \
    oci://ghcr.io/konpyutaika/helm-charts/nifikop \
    --namespace=nifi \
    --version 1.4.1 \
    --set image.tag=v1.4.1-release \
    --set resources.requests.memory=256Mi \
    --set resources.requests.cpu=250m \
    --set resources.limits.memory=256Mi \
    --set resources.limits.cpu=250m \
    --set namespaces={"nifi"}
```

**09-create custom storageclass**
```bash
kubectl create -n nifi -f storageclass.yml
```

**10-Adicionar o repo bitnami**
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

**11-Como um pré-requisito, o NiFi requer o Zookeeper.**
```bash
helm install zookeeper bitnami/zookeeper \
    --namespace=zookeeper \
    --set resources.requests.memory=256Mi \
    --set resources.requests.cpu=250m \
    --set resources.limits.memory=256Mi \
    --set resources.limits.cpu=250m \
    --set global.storageClass=storage-class-nifi \
    --set networkPolicy.enabled=true \
    --set replicaCount=3 \
    --create-namespace
```

**12-Subir o cluster nifi**
```bash
kubectl create -n nifi -f simplenificluster.yaml
```


#BÔNUS
#Comando Kubernetes
**Iniciar o shell no contêiner**
```bash 
kubectl exec -u 0 -it -n nifi nome_do_pod sh
```
**Verificar erro no contêiner caso não apresente o status running.**
```bash
kubectl describe pod nome_do_pod -n nifi
```
**Exibir o IP para acesso Externo. Utilizar o IP EXterno. (Exemplo: http://34.43.128.10/nifi)**
```bash
kubectl get service -n nifi
```

#Fonte
**https://konpyutaika.github.io/nifikop/**
**https://github.com/konpyutaika/nifikop**