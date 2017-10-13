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

## Atualização

Procedimentos de atualização de acordo com o salto de versão.

### Minor version (ex: 9.5.8 -> 9.5.9)
 * Instalar repositório da nova versão;
 * Instalar nova versão;
 * Reiniciar serviço;
 
### Major version (ex: 9.5.9 -> 9.6.5)
* Backup dos dados;
* Backup de arquivos de configuração: formas de conexão (pg_hba.conf) e parâmetros para o diretório da nova versão (postgresql.conf).
* Instalar a versão nova, sem remover a versão anterior;
* Parar e desabilitar a versão anterior;
* Habilitar e iniciar a versão nova;
* Restaurar os dados na versão nova.

**Observações**
Upgrade Major Version exigirá 3x o tamanho da base:

 1. espaço da base antiga;
 2. dump da base antiga;
 3. espaço para a base na nova versão.

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
