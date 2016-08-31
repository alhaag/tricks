# Fedora
Procedimentos particulares para instalação e configuração do ambiente de desenvolvimento no Fedora 24.

## DNF
Comandos uteis do gerenciador de pacotes DNF.

Pesquisar pacotes:
```shell
$ sudo dnf search <package>
```

Instalar pacote:
```shell
$ sudo dnf install <package>
```

Remover pacote:
```shell
$ sudo dnf remove <package>
```

Verificar atualizações:
```shell
$ sudo dnf clean all
$ sudo dnf check-update
```

Atualizar pacotes instalados:
```shell
$ sudo dnf update
```

Documentação completa em http://dnf.readthedocs.io/en/latest/command_ref.html


## MongoDB
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

### Resolução de problemas de inicialização
Criar o diretório **/data/db** caso não exista:
```shell
$ sudo mkdir -p /data/db
```

Obter user-id e group-id do mongo:
```shell
$ grep mongo /etc/passwd
mongod:x:498:496:mongod:/var/lib/mongo:/bin/false
```
Alterar as permissões do diretório para o usuário e grupo do mongo com os respectivos IDs:
```shell
sudo chmod 0755 /data/db
sudo chown -R 498:496 /data/db    # usando o user-id e group-id
```



