# Kubernetes_study

Este é um estudo sobre a utilização do Kubernetes.

A Aplicação é um site de notícias da alura, que ao longo do dia apresenta lentidão elevada devido a picos de utilização.

## Conectanto com ssh o Docker-Toolbox
https://stackoverflow.com/questions/30330442/how-to-ssh-into-docker-machine-virtualbox-instance

Rode o comando no DockerToolbox e veja o comando do ssh

- ```docker-machine -D ssh defaul```

O comando para acesso ssh ao docker encontrado foi esse:

- ```ssh.exe -F /dev/null -o ConnectionAttempts=3 -o ConnectTimeout=10 -o ControlMaster=no -o ControlPath=none -o LogLevel=quiet -o PasswordAuthentication=no -o ServerAliveInterval=60 -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null docker@127.0.0.1 -o IdentitiesOnly=yes -i %userprofile%\.docker\machine\machines\default\id_rsa -p 61025```

## Rodando o ambiente

-