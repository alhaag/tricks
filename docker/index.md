# Docker

## Instalação

```shell
$ curl -sSL https://get.docker.com | sh
```
### Operações gerais
Obter status dos containers
```shell
$ docker ps
```

Listar imagens disponíveis na máquina
```shell
$ docker images
```

Ver modificações realizadas em um container
```shell
$ docker diff <container_id>
```

Ver informações detalhadas de um container
```shell
$ docker inspect <container_id>
```

Verificar consumo de recuros do docker
```shell
$ docker stats
```

Remover uma imagem:
```shell
$ docker rmi <imagem_id>
```

Remover todas as imagens:
```shell
$ docker rmi $(docker images -q)
```

### Operações sobre containers

**Criar** um novo container:
```shell
$ docker run -it <nome_imagem> /bin/bash
```

**Criar** container mapeando porta com o host hospedeiro com o parâmetro -p:
```shell
$ docker run -it -p 8080:80 <nome_imagem> /bin/bash
```

**Criar** container que se comunica com outro container
```shell
$ docker run -it --name <host_name_1> --link [nome_container]:<host_name_2> <nome_novo_container>
```

**Criar** container a partir de um arquivo **Dockerfile**(só pode existir um arquivo por diretório e o comando deve ser executado no diretório onde o Docker file está localizado):
```shell
$ docker build -t <nome_container> .
```

**Acessar o bash** de um container em execução com o exec (esta opção pode ser utilizada para executar diversos outros comando sobre o container):
```
$ docker exec -it <container_id> /bin/bash
```

**Sair** de um container sem encerrar a execução:
```shell
<ctrl> + <p> + <q>
ou
<ctrl> + <d>
```

**Encerrar(desligar)** um container:
```shell
$ docker stop <container_id>
```

**Remover** um container:
```shell
$ docker rm <container_id>
```

**Remover todos** os containers:
```shell
$ docker rm $(docker ps -a -q)
```

### Comitar containers

Comitar estado atual de um container (isso cria uma copia do container)
```shell
$ docker commit <container_id> <nome_novo_container>
```

# Docker compose
É uma extenção do docker que permite criar composições de containers de forma declarativa.

## Instalação

```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.9.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

## Utilização

Exemplo de arquivo descritor de containers **docker-compose.yml**:
```yml
web: 
  image: nginx:latest
  ports:
   - "80:80"
  volumes:
   - /home/alhaag/Projects:/var/www/html
   - /home/alhaag/env/dsc-conf-dev/nginx.d:/etc/nginx/conf.d
  links:
   - php-fpm

php-fpm:
  image: php:7-fpm
  ports:
   - "9000:9000"
  volumes:
   #- /home/alhaag/env/dsc-conf-dev/php-fpm.d:/etc/php/7.0/fpm/pool.d
   - /home/alhaag/Projects:/var/www/html

mysql:
  image: mysql
  ports:
    - "3306:3306"
  environment:
    MYSQL_ROOT_PASSWORD: 123456
```

Para inicializar a estrutura de containers, executar o seguinte comando no diretório onde está o arquivo descritor:

```shell
$ sudo docker-compose up
```

## Docker HUB

Repositório de imagens:

https://hub.docker.com/explore/
