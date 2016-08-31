# Casandra

# DB2

# MySQL

# MongoDB
Banco de alte desempenho orientado a documentos.

Acesso ao **client**:
```shell
$mongo
```

Verificar **estatísticas**, isto irá mostrar o nome do banco, número de recolha e documentos no banco de dados.
```shell
>db.stats ()
{
	"db" : "test",
	"collections" : 0,
	"objects" : 0,
	"avgObjSize" : 0,
	"dataSize" : 0,
	"storageSize" : 0,
	"numExtents" : 0,
	"indexes" : 0,
	"indexSize" : 0,
	"fileSize" : 0,
	"ok" : 1
}
```
Acessar base ou criar caso não exista:
```shell
>use <db_name>
switched to db db_name
```

Verificar base selecionada:
```shell
>db
db_name
```

**Listar** todas as bases(apenas bases que possuem documentos serão listadas):
```shell
>show dbs
local  0.000GB
test   0.23012GB
```

**Inserir** documento na base selecionada:
```
>db.movie.insert({"name":"Teste de insert"})
WriteResult({ "nInserted" : 1 })
```
Em mongodb banco de dados padrão é o teste. Se não for criado um banco de dados, as coleções serão armazenados no banco de dados de teste.

**Remover** base selecionada (caso nenhuma esteja selecionada a base teste será removida):
```
>db.dropDatabase()
{ "dropped" : "db_name", "ok" : 1 }
```

**Criar collection**(equivalente a tabela dos SGDBs):
```
>db.createCollection(<name>, options)
```
Detalhamento de opções:
Opção | Tipo | Descrição
--- | --- | ---
capped | Boolean | (Opcional).
autoIndexID | Boolean | xxx
size | number | xxx
max | number | xxx

Exemplo:
```
>db.createCollection("users", { capped : true, autoIndexID : true, size : 6142800, max : 10000 } )
{ "ok" : 1 }
```

# Postgres

# Redis
