# Cassandra ![logo](http://cassandra.apache.org/img/cassandra_logo.png)

Banco de dados NoSQL de alto desempenho, altamente escalável e projetado para gerenciar grandes quantidades de dados estruturados. Oferece alta disponibilidade com nenhum ponto único de falha.

## Requisitos
 * Python 2.7
 * Java 8

A instalação do java 8 no Fedora pode ser realizada baixando o pacote RPM http://download.oracle.com/otn-pub/java/jdk/8u101-b13/jdk-8u101-linux-i586.rpm

Após o download executar:
```
$ sudo dnf install jdk-8u101-linux-x64.rpm
```

## Instalação
Baixar o tarball http://www.apache.org/dyn/closer.lua/cassandra/3.7/apache-cassandra-3.7-bin.tar.gz 

Descompactar o tarball:
```shell
$ tar -xvf apache-cassandra-3.7-bin.tar.gz
$ cd apache-cassandra-3.7/
```

Após a extração iniciar a execução do cluster executando:
```shell
$ bin/cassandra
```

O status do processo pode ser verificado executando:
```shell
$ bin/nodetool status
```

O principal arquivo de configuração é o **conf/cassandra.yaml**

### Problema encontrado
No Fedora 24 foi preciso fazer o downgrade do python 2.7.12 para 2.7.11, pois na execução do client ocorria o seguinte erro:
```shell
$ bin/cqlsh localhost
Connection error: ('Unable to connect to any servers', {'localhost': TypeError('ref() does not take keyword arguments',)})
```

O downgrade foi realizado com o seguinte comando no Fedora 24:
```shell
$ sudo dnf downgrade python --allowerasing
```

### Instalação com user específico (recomendado)
Criar usuário e grupo:
```shell
$ groupadd cassandra
$ useradd -g cassandra cassandra
```

Definir uma senha para o usuário(opcional):
```shell
$ passwd cassandra
```

Definir configurações de path e alias específicas para o usuário cassandra:
```shell
$ su - cassandra
$ vi /home/cassandra/.bashrc

Definir as variáves de ambiente e alias de acordo com a necessidade. Ex:
-----------------------
# .bashrc

# User specific aliases and functions
JAVA_HOME=/path/to/jdk1.8.0_101
CASSANDRA_HOME=/path/to/apache-cassandra-3.7

# Aliases
alias python='python2.7'
alias cqlsh=${CASSANDRA_HOME}'/bin/cqlsh'

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# evironment vars
export JAVA_HOME

-----------------------

$ exit
```
Alterar as permissões do diretório do Cassandra para o usuário e grupo criado:
```shell
$ chown -R cassandra:casssandra /path/to/apache-casandra-3.7
```

Executar o Cassandra com o usuário criado a partir do bash do root:
```shell
# runuser -l  cassandra -c '/path/to/apache-cassandra-3.7/bin/cassandra'
```



## Configuração
Arquivo de configuração do Cassandra estalocalizado em **conf/cassandra.yaml**. Este arquivo define as principais configurações e é muito bem comentado.

Segue algumas das principais diretivas:

 * **cluster_name**: Este é o nome do seu cluster. Todos os nós do cluster devem possuir o mesmo nome.
 * **-seeds**: Esta é uma lista delimitada por vírgulas de o endereço IP de cada nó no cluster.
 * **listen_address**: Este é o endereço IP que outros nós do cluster usará para se conectar a este. O padrão é localhost e as necessidades mudaram para o endereço IP do nó.
 * **rpc_address**: Este é o endereço IP para chamadas de procedimento remoto. O padrão é localhost . Se o hostname do servidor está configurado corretamente, deixe este como é. Caso contrário, a mudança para o endereço IP do servidor ou o endereço de auto-retorno ( 127.0.0.1).
 * **endpoint_snitch**: Nome do pomo, que é o que diz a Cassandra sobre o que sua rede se parece. Este padrão é SimpleSnitch , que é usado para as redes em um datacenter. No nosso caso, vamos alterá-lo para GossipingPropertyFileSnitch , que é o preferido para instalações de produção.
 * **auto_bootstrap**: Esta directiva não está no arquivo de configuração, por isso tem de ser adicionado e definido como falso . Isso faz com que novos nós automaticamente usar os dados corretos. É opcional se você estiver adicionando nós a um cluster existente, mas necessária quando você está inicializando um novo cluster, ou seja, um sem dados.

## Configurar cluster
Este é exemplo simples para configuração de um cluster com vários nós, e deve ser executado em cada nó do cluster.

 1. **Parar o processo** cassandra, isso pode ser feito de várias formas dependendo de como o processo foi instalado.
 2. **Exclusão de dados padrão**:
 
 ```shell
 sudo rm -rf /path/to/cassandra/data/data/system/*
 ```
 3. **Configurar cluster**, configurar as seguintes diretivas do arquivo **cassandra.yaml**:

 ```shell
 . . .
cluster_name: 'CassandraDOCluster'
. . .
seed_provider:
  - class_name: org.apache.cassandra.locator.SimpleSeedProvider
    parameters:
         - seeds: "your_server_ip,your_server_ip_2,...your_server_ip_n"
. . .
listen_address: your_server_ip
. . .
rpc_address: your_server_ip
. . .
endpoint_snitch: GossipingPropertyFileSnitch
. . .
# incluir no fim do arquivo caso não exista:
auto_bootstrap: false
 ```
 4. **Firewall**, liberar as portas 7000(TCP para comandos e dados) e 9042 (TCP para o servidor de transporte nativo. cqlsh). Ex:
 
 ```shell
 -A INPUT -p tcp -s your_other_server_ip -m multiport --dports 7000,9042 -m state --state NEW,ESTABLISHED -j ACCEPT
 ```
 5. **Iniciar o processo**

## Client
O acesso ao terminal client é realizado executando binario **cqlsh** seguido do node do cluster:
```
$ bin/cqlsh localhost
```

```shell
cqlsh> SELECT cluster_name, listen_address FROM system.local;

 cluster_name | listen_address
--------------+----------------
 Test Cluster |      127.0.0.1

(1 rows)
```

# Comandos básicos

## Keyspaces:
Listar keyspaces:
```
cqlsh> describe keyspaces;
```

Criar keyspace:
```
cqlsh> CREATE KEYSPACE new_cluster WITH replication = {'class':'SimpleStrategy', 'replication_factor' : 1};
```

Alterar keyspace:
```
cqlsh> ALTER KEYSPACE dgt_cluster WITH REPLICATION = {'class' : 'SimpleStrategy', 'replication_factor' : 3};
```

## Tables
Criar tabela:
```
cqlsh> CREATE TABLE new_cluster.user (name text PRIMARY KEY, age int);
```

Insert:
```
cqlsh> INSERT INTO new_cluster.user (name, age) VALUES ('Andre Luiz Haag', 30);
```

Select:
```
cqlsh> SELECT * FROM new_cluster.user;
```

Obs: O Cassandra não suporta JOINS, transações e relacionamentos de tableas.

## User-Defined Types
O CQL(Cassandra Query Language), permite a criação de tipos de dados definidos pelo usuário.

A criação de um novo tipo é definida por **CREATE TYPE**. Ex:
```
create_type_statement ::=  CREATE TYPE [ IF NOT EXISTS ] udt_name
                               '(' field_definition ( ',' field_definition )* ')'
field_definition      ::=  identifier cql_type
```

```
CREATE TYPE phone (
    country_code int,
    number text,
)

CREATE TYPE address (
    street text,
    city text,
    zip int,
    phones map<text, phone>
)

CREATE TABLE user (
    name text PRIMARY KEY,
    addresses map<text, frozen<address>>
)
```

## Insert
Com os tipos definidos proviamente definidos q inserção pode ser realizada conforme exemplo a seguir:
```
INSERT INTO user (name, addresses)
 VALUES ('z3 Pr3z1den7', {
     'home' : {
         street: '1600 Pennsylvania Ave NW',
         city: 'Washington',
         zip: '20500',
         phones: { 'cell' : { country_code: 1, number: '202 456-1111' },
                   'landline' : { country_code: 1, number: '...' } }
     }
     'work' : {
         street: '1600 Pennsylvania Ave NW',
         city: 'Washington',
         zip: '20500',
         phones: { 'fax' : { country_code: 1, number: '...' } }
     }
 })
```

## Drivers

 * NodeJs
  * [Express driver](http://expressjs.com/pt-br/guide/database-integration.html#cassandra) 
  * [DataStax](https://github.com/datastax/nodejs-driver)
  

## Referências
 * http://cassandra.apache.org/doc
 * http://www.tutorialspoint.com/cassandra/
 * https://www.digitalocean.com/community/tutorials/how-to-run-a-multi-node-cluster-database-with-cassandra-on-ubuntu-14-04

