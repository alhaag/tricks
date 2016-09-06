# Casandra

Banco de dados NoSQL altamente escalável e flexível. Trabalha nativamente com o conceito de cluster.

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

### Problema enncontrado
No Fedora 24 foi preciso fazer o downgrade do python 2.7.12 para 2.7.11, pois na execução do client ocorria o seguinte erro:
```shell
$ bin/cqlsh localhost
Connection error: ('Unable to connect to any servers', {'localhost': TypeError('ref() does not take keyword arguments',)})
```

O downgrade foi realizado com o seguinte comando:
```shell
$ sudo dnf downgrade python --allowerasing
```
## Client
O acesso ao terminal client é realizado executando binario **cqlsh** seguido do node do cluster:
```shell
$ bin/cqlsh localhost
```
```shell
cqlsh> SELECT cluster_name, listen_address FROM system.local;

 cluster_name | listen_address
--------------+----------------
 Test Cluster |      127.0.0.1

(1 rows)
```

## User-Defined Types (Create table)
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
  * [DataStax](https://github.com/datastax/nodejs-driver)

## Referências
 * http://cassandra.apache.org/doc
 * http://www.tutorialspoint.com/cassandra/

