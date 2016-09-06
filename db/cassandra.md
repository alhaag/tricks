# Casandra

Banco de dados NoSQL altamente escalável e flexível. Trabalha nativamente com o conceito de clusters.

## Requisitos
 * Python 2.7
 * Java 8

A instalação do java 8 no fedora pode ser realizada baixando o RPM http://download.oracle.com/otn-pub/java/jdk/8u101-b13/jdk-8u101-linux-i586.rpm

Após o download executar:
```
$ sudo dnf install jdk-8u101-linux-x64.rpm
```

## Instalação
Baixar o tarball http://www.apache.org/dyn/closer.lua/cassandra/3.7/apache-cassandra-3.7-bin.tar.gz 

Descompactar o tarball:
```shell
$ tar -xvf apache-cassandra-3.7-bin.tar.gz
```

Após a extração subir o cluster executando:
```shell
$ bin/cassandra
```

No Fedora 24 foi preciso fazer o downgrade do python 2.7.12 para 2.7.11, pois na execução do client ocorria o seguinte erro:
```shell
$ bin/cqlsh localhost
Connection error: ('Unable to connect to any servers', {'localhost': TypeError('ref() does not take keyword arguments',)})
```

O downgrade foi realizado com o seguinte comando:
```shell
$ sudo dnf downgrade python --allowerasing
```


