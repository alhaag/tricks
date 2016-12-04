# Docker

## Instalação

```shell
curl -sSL https://get.docker.com | sh
```
### Obter informações

Obter status dos containers
```shell
sudo docker ps
```

Listar imagens disponíveis na máquina
```shell
sudo docker images
```

Ver modificações realizadas em um container
```shell
sudo docker diff <container_id>
```

Ver informações detalhadas de um container
```shell
sudo docker inspect <container_id>
```

Verificar consumo de recuros do docker
```shell
sudo docker stats
```

### Criar containers

Criar um novo container
```shell
sudo docker run -it <nome_imagem> /bin/bash
```

Para mapear a porta pode ser usado o parâmetro -p
```shell
sudo docker run -it -p 8080:80 <nome_imagem> /bin/bash
```

Criar container que se comunica com outro container
```shell
sudo docker run -it --name <host_name_1> --link [nome_container]:<host_name_2> <nome_novo_container>
```

Criar container a partir de um arquivo Dockerfile. Só pode existir um arquivo por diretório
```shell
docker build -t <nome_container> .
```

### Sair, finalizar e excluir containers e imagens

Sair de um container sem encerrar a execução
```shell
[ctrl] + [p] + [q]
```

Encerrar um container
```shell
sudo docker stop <container_id>
```

Remover um container
```shell
sudo docker rm <container_id>
```

Remover uma imagem
```shell
sudo docker rmi <imagem_id>
```

### Comitar containers

Comitar estado atual de um container (isso cria uma copia do container)
```shell
sudo docker commit <container_id> <nome_novo_container>
```

# Docker compose
É uma extenção do docker que permite criar composições de containers de forma declarativa.

## Instalação

```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.9.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
