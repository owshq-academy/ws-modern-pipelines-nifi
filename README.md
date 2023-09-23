**ws-modern-pipelines-nifi**



#Criando Pipeline de Dados Moderno com Apache Nifi na Prática

<div style="display: inline_block"><br>
  <img align="center" height="800" width="800" src="./image/roadmap.png">
</div>
![img.png](img.png)

**Requisitos**
- 2 CPUs or more
- 2GB of free memory
- 20GB of free disk space
- Internet connection
- Container ou virtual machine: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, ou VMware Fusion/Workstation


# Como executar o Projeto
Escolha instalar no Docker ou Minikube


**1- Clonar repositório**
```bash
xxxxxxxxxxxxxxxxx
````

**2- Instalar Docker**

https://docs.docker.com/desktop

**3- Iniciar os serviços**
```bash
#(.../ws-modern-pipelines-nifi/docker)
docker-compose up -d
````
# Ou 

**2- Instalar Minikube**

https://minikube.sigs.k8s.io/docs/start/

**3- Iniciar os serviços**
```bash
# Iniciar Cluster
minikube start

# Criar novo namespace
kubectl create namespace nifi

# Criar os pods
kubectl apply -f deployment/workshop.yml 

# Verificar se os pods estão com status running
kubectl get pods -n nifi

# Iniciar os serviços 
minikube tunnel
````
#
**4- Acessar o Nifi:**

http://127.0.0.1:8080/nifi
#
**5- Acessar o Nifi-Registry:**

http://127.0.0.1:18080/nifi-registry
#
**6- Configurar o Nifi-Registry**

- Clique no menu de ferramentas.

![img.png](image/menu_ferramentas.png)
#
- Clique em Novo Bucket e adicione um nome.

![img_1.png](image/novo_bucket.png)
#
- Abra o Nifi >> Menu Sandwich >> Controller Settings

![img_2.png](image/controller_settings.png)
#
- Na guia Registry Clients, adicione um nome para o registry

![img.png](image/regystri.png)
#
- Edite as propriedades do novo registry com os parâmetros abaixo.

- http://nifi-registry:18080/
- Clique Update

![img.png](image/nifi-registry.png)
#

7- Configurar a conexãom com Postgres

- Configure o Controller Service: DBCPConnectionPool
- jdbc:postgresql://postgres:5432/postgres
- org.postgresql.Driver
- /opt/jdbc/postgresql-42.5.2.jar
- usr: postgres
- pws: postgres123

CREATE TABLE device (
    id INTEGER,
    uid UUID,
    build_number INTEGER,
    manufacturer VARCHAR(255),
    model VARCHAR(255),
    platform VARCHAR(255),
    serial_number VARCHAR(255),
    version INTEGER,
    user_id INTEGER,
    dt_current_timestamp BIGINT
);

![img.png](image/configure_controller_service_postgres.png)

<div style="display: inline_block"><br>
<img align="center" alt="docker" height="50" width="50" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original-wordmark.svg" />
<img align="center" alt="kubernetes" height="50" width="50" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/kubernetes/kubernetes-plain-wordmark.svg" />
<img align="center" alt="AWS" height="60" width="60" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" />
<img align="center" alt="GCP" height="70" width="70" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/googlecloud/googlecloud-original-wordmark.svg" />
<img align="center" alt="AZURE" height="70" width="70" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/azure/azure-original-wordmark.svg" />
                    
</div>
  
  ##
<div> 
  <a href="https://www.youtube.com/@engenhariadedadosacademy" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" target="_blank"></a>
  <a href="https://www.instagram.com/engenhariadedados/" target="_blank"><img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-badge&logo=instagram&logoColor=white" target="_blank"></a>
  <a href = "mailto:leonardo.souza@owshq.com"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
  <a href="https://www.linkedin.com/in/leonardo-c%C3%B4co-9863712a/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a> 
  
</div>







