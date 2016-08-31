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

db.COLLECTION_NAME.drop()

**Criar collection**(equivalente a tabela dos SGDBs):
```
>db.createCollection(<name>, options)
```

Detalhamento de opções:

| Opção         | Tipo     | Descrição  |
| ------------- |:--------:| :-----|
| capped        | Boolean  | (Opcional) Se verdadeiro, permite uma coleção tampado. Coleção tampado é uma coleção collecction tamanho fixo que substitui automaticamente suas entradas mais antigas quando atinge seu tamanho máximo. Se você especificar true, você precisa especificar parâmetro de tamanho também. |
| autoIndexID   | Boolean  | (Opcional) Se for verdade, criar automaticamente índice em _id field.s O valor padrão é falso. |
| size          | number   | (Opcional) Especifica um tamanho máximo em bytes para uma coleção tampado. Se se tampado é verdade, então você precisa especificar neste campo também. |
| max           | number   | (Opcional) Especifica o número máximo de documentos permitidos na coleção tampado. |

Exemplo:
```
>db.createCollection("users", { capped : true, autoIndexID : true, size : 6142800, max : 10000 } )
{ "ok" : 1 }
```

Em mongodb você não precisa criar coleção. MongoDB cria coleção automaticamente, quando um documento é inserido. Ex:
```
>db.users.insert({"name" : "Nome do usuario"})
>show collections
mycol
mycollection
system.indexes
users
```

**Listar colecttions**(equivalente a tabelas dos SGDBs):
```
>show collections
users
system.indexes
```

**Remover collection**:
```
>db.COLLECTION_NAME.drop()
true
```

## Tipos de dados
 * **String**: Tipo mais comum para armazenamento de dados. Strings em mongodb devem ser UTF-8 válidos.
 * **Integer**: Este tipo é usado para armazenar um valor numérico. Integer pode ser de 32 bits ou 64 bits, dependendo do servidor.
 * **Boolean**: Este tipo é usado para armazenar um valor booleano (true / false).
 * **Double**: Este tipo é usado para armazenar valores de ponto flutuante.
 * **Min/ Max keys**: Este tipo é usado para comparar um valor contra os elementos mínimos e máximos BSON.
 * **Arrays**: Este tipo é usado para armazenar matrizes ou lista ou vários valores em uma chave.
 * **Timestamp**: ctimestamp. Isto pode ser útil para a gravação quando um documento foi modificado ou adicionado.
 * **Object** : Este tipo de dados é usado para documentos incorporados(aninhados).
 * **Null**: Este tipo é usado para armazenar um valor nulo.
 * **Simbol**: Este tipo de dados é utilizada de forma idêntica a uma corda no entanto, é geralmente reservado para as línguas que usam um tipo de símbolo específico.
 * **Data**: Este tipo de dados é usado para armazenar a data ou a hora atual no formato de UNIX. Você pode especificar o seu próprio tempo de data através da criação de objeto de Data e passar o dia, mês, ano para ele.
 * **Object ID**: Este tipo de dados é usado para armazenar o ID do documento.
 * **Binary data**: Este tipo de dados é usado para armazenar dados binarios.
 * **Code**: Este tipo de dados é usado para armazenar o código javascript em documento.
 * **Regular expression**: Este tipo de dados é usado para armazenar expressão regular.

# Postgres

# Redis
