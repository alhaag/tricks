# ![logo](https://datavirtuality.com/wp-content/uploads/sites/2/2016/07/postgresql-logo-e1472859206311.png)

SGBD opensource mais avançado da categoria.

## Instalação

Instar repositório:
```
$ sudo yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-redhat95-9.6-3.noarch.rpm
```

Instalar pacotes:
```
$ sudo yum install postgresql95 postgresql96-devel postgresql96-contrib postgresql95-libs postgresql96-test postgresql96-server postgresql96-docs
```

Habilitar e iniciar serviço:
```
$ sudo systemctl enable postgresql-9.6
$ sudo systemctl restart postgresql-9.6
```

## Administração

A administração deve ser realizada com o usuário postgres:
```
$ su - postgres
```

## Comandos úteis

```
\? Ajuda
\d Definições (depende do escopo)
psql -E Ativa echo das consultas realizadas internamente pelo SGBD a cada query
pgsql$ show all; Exibe configurações carregadas

```
