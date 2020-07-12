# Kubernetes_study

Este é um estudo sobre a utilização do Kubernetes.

A Aplicação é um site de notícias da alura, que ao longo do dia apresenta lentidão elevada devido a picos de utilização.

## Conectanto com ssh o Docker-Toolbox
https://stackoverflow.com/questions/30330442/how-to-ssh-into-docker-machine-virtualbox-instance

Rode o comando no DockerToolbox e veja o comando do ssh

- ```docker-machine -D ssh defaul```

O comando para acesso ssh ao docker encontrado foi esse:

- ```ssh.exe -F /dev/null -o ConnectionAttempts=3 -o ConnectTimeout=10 -o ControlMaster=no -o ControlPath=none -o LogLevel=quiet -o PasswordAuthentication=no -o ServerAliveInterval=60 -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null docker@127.0.0.1 -o IdentitiesOnly=yes -i %userprofile%\.docker\machine\machines\default\id_rsa -p 61025```

# Kubernetes


### Inserir o objeto no cluster kubernetes a parir de um arquivo YAML.
Na pasta kubernetes rodar o seguinte comando:

```kubectl create -f aplicacao.yaml```

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
``

### Ver logs
```
kubectl logs <nome-do-pod>
```

## LoadBalancer

### Para identificar o IP da aplicacao, precisa-se perguntar para o minikube e não para o kubectl.

```minikube service <nome-servico> --url```

### Para acessar o container, da mesma forma que o docker.
```
kubectl exec -it <nome-do-pod> bash
```

ou
```
kubectl exec <nome-do-pod> bash
```