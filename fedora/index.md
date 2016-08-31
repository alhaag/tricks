# Fedora
Procedimentos particulares para instalação e configuração do ambiente de desenvolvimento no Fedora 24.

### MongoDB
Instalação do MongoDB 3.2 desenvolvido pela comunidade.

Criar o arquivo para indicar ao dnf o repositório:
```shell
/etc/yum.repos.d/mongodb-org-3.2.repo
```

Inserir o seguinte conteúdo no arquivo de repositório:
```
$[mongodb-org-3.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/7/mongodb-org/3.2/x86_64/
gpgcheck=0
enabled=1
```

Instalar com o comando:
```shell
$ sudo dnf install mongodb-org
```
