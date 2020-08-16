# Kubernetes_study

Este é um estudo sobre a utilização do Kubernetes.

A Aplicação é um site de notícias da alura, que ao longo do dia apresenta lentidão elevada devido a picos de utilização.

Estudo: https://docs.google.com/document/d/1UgcEUKV_AVBkC6HVXloQe7ZcZxDI7RadScxuElBwfQU/edit#heading=h.cr9h198n50sx


## Conectanto com ssh o Docker-Toolbox
https://stackoverflow.com/questions/30330442/how-to-ssh-into-docker-machine-virtualbox-instance

Rode o comando no DockerToolbox e veja o comando do ssh

- ```docker-machine -D ssh defaul```

O comando para acesso ssh ao docker encontrado foi esse:

- ```ssh.exe -F /dev/null -o ConnectionAttempts=3 -o ConnectTimeout=10 -o ControlMaster=no -o ControlPath=none -o LogLevel=quiet -o PasswordAuthentication=no -o ServerAliveInterval=60 -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null docker@127.0.0.1 -o IdentitiesOnly=yes -i %userprofile%\.docker\machine\machines\default\id_rsa -p 61025```

## Conectando com WSL2

Rode o comando `wsl --list --verbose` ou `wsl -l -v` para visualziar as distribuicoes linux instalada, estado e versao (WLS).

Em seguida selecione a distro padrao: `wsl -s <nome_distro>`


Rode o comando no prompt para entrar no linux: ```wsl```

Suba o ambiente com o docker-compose ```docker-compose up -d```

## Instalação do Minikube e kubectl

Primeiro passo é instalar o Kubernetes. Localmente necessita-se instalar o minikube e o kubectl. Existe um passo a passo para cada plataforma (windows, linus, ios).
- https://kubernetes.io/docs/tasks/tools/install-kubectl/
- https://kubernetes.io/docs/tasks/tools/install-minikube/


# Kubernetes


## Kubernetes tipos:
- POD:
    - Menor unidade de deploy no Kubernetes.
    - Um Pod normalmente tem apenas um container associado, mas existe a possibilidade de definir outros containers no mesmo Pod, desde que varia a porta de rede entre os containers isso funciona.
    - Um Pod tem um IP.
    - Objeto do Kubernetes descrito por um arquivo YML.
    - Quando se deleta um POD de uma aplicação no Kubernetes o mesmo é removido. Diferentemente de um deployment, quando se deleta um POD o Kubernetes já sobe outro POD no lugar.

- Deployment:
    - É responsável por definir a quantidade de réplicas do Pod. Podemos definir através dashboard, pelo kubectl ou na arquivo yml a quantidade de réplicas. 
    - É  responsável por garantir que o Pod está disponível (rodando). Um Pod criado SEM deployment não garante disponibilidade.
    - Funciona como controlador do POD, define a quantidade de replcias e a disponibilidade do POD.
    - o Deployment é um controller **stateless**, ou seja, nao compartilha nenhuma informacao entre PODS.

- Service LoadBalancer
    - É um servico do Kubernetes que dá acesso ao deployment.
    - O serviço fica associado ao deployment ou PODs através do *Selector*.
    - o comando `minikube service <nome-servico> --url` devolve a url para testar o serviço.

- StatefulSet
    - permite o compartilhamento de informações entre PODs.
    - tambem usa um POD por debaixo dos panos.
    - garante que atraves dos volumes, os dados serão mantidos mesmo se o POD for reiniciado.
    - necessario definir:
        - *volumeMounts*: define a pasta concreta de montagem e da um nome para o volume.
        - *volumes*: associa nome do volume com uma permissão.
        - *PersistentVolumeClaim*: define as permissões e o tamanho do recurso.

# Kubectl
Kubectl é a interface de linha de comando para gerenciar Kubernetes.

## Comandos

### Inserir o objeto no cluster kubernetes a parir de um arquivo YAML.
Na pasta kubernetes rodar o seguinte comando: 

```kubectl create -f aplicacao.yaml```

-f significa file.

### Remover a objeto do cluster kubernetes a partir de um arquivo YAML.

```kubectl delete -f aplicacao.yaml```

### visualizar os objetos do cluster kubernetes

```
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get nodes
```
e
```
kubectl get pod <nome-do-pod>
kubectl get deployment <nome-do-deployment>
kubectl get service <nome-do-service>
```
Obter mais informaçoes usar o flag ```-o wide```.
```
kubectl get pods -o wide
```

### Entender melhor um recurso
```
kubectl explain nodes
kubectl explain pod
```

### Obter informaçoes detalhadas

É possivel identificar o IP da aplicação.

```
kubectl describe pods
kubectl describe pods <nome-do-pod>
```

### remover objeto

```
kubectl delete pods <nome-do-pod>
kubectl delete deployment <nome-deployment>
kubectl delete service <nome-service>
```

### Ver logs
```
kubectl logs <nome-do-pod>
```

### Editar o YAML pelo kubectl

```
kubectl edit deployment <nome-deployment>
```

### Para acessar o container, da mesma forma que o docker.

`kubectl exec -it <nome-do-pod> bash` ou  `kubectl exec <nome-do-pod> bash`

# Minikube
Minikube é uma implementação do Kubernetes. O minikube é uma implementação de simples uso do Kubernetes. Existem outras como Google GKE, Amazon EKS ou Azure Kubernetes Service.

## Comandos

### Inciar o minikube

Rode o comando ```minikube start```. Isso iniciará o minikube no Oracle Virtual Box dentro do windows ou um docker no linux.

### Check do minikube

Verificar se o minikube esta em funcionamento: `minikube status`

### Dashboard do minikube

Dashboard é uma pagina web para acompanhar as configuracoes do kubernetes. 

`minikube dashboard`

### Identificação do IP da aplicacao

Para identificar o IP da aplicacao, precisa-se perguntar para o minikube e não para o kubectl.

`minikube service <nome-servico> --url`

### Rodar Kubectl dentro do minikube

`minikube kubectl -- get pods`
