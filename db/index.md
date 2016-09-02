# MongoDB
Banco de alte desempenho orientado a documentos.

Alguns conceitos são diferentes quando comparados aos tradicionais bancos de dados relacionais. Segue tabela comparativa:

| BD Relacional      | MongoDB       |
| :----------------- |:--------------|
| Tabela             | Collection    |
| Registro da tabela | Documento     |
| Utiliza linguagem SQL | Não utiliza SQL |
| Armazenamento em tabelas relacionadas | Dados relacionados em um único documento(JSON) |

## Console
Acesso ao console client:
```shell
$mongo
```
## Informações
Algumas **estatísticas** como o nome do banco, número de recolha e documentos no banco de dados podem ser obtidos por meio da função **stats**. Ex:
```shell
> db.stats ()
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

## Criar/acessar base
Para acessar uma base deve ser utilizado o comando **use <db_name>**, caso a base n]ao exista o Mongo irá criar automaticamente uma nova. Ex:
```shell
> use base_teste
switched to db base_teste
```

Verificar base selecionada:
```shell
> db
base_teste
```

Para **Listar** todas as bases, utilizaa-se o comando **show dbs**. Ex:
```shell
>show dbs
local  0.000GB
test   0.23012GB
```
Obs: apenas bases que possuem documentos serão listadas.

## Insert
A inserção de um novo documento na base selecionada é realizada com o comando **insert**. Ex:
```
>db.users.insert({"name":"Teste de insert"})
WriteResult({ "nInserted" : 1 })
```
Obs: em mongodb banco de dados padrão é o teste. Se não for criado um banco de dados, as coleções serão armazenados no banco de dados de teste.

## Delete
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
## Show collections
**Listar colecttions**(equivalente a tabelas dos SGDBs):
```
> show collections
users
system.indexes
```
## Drop collection
A remoção de uma collection é realizada com a função drop, **db.<COLLECTION_NAME>.drop()**. Ex:
```shell
> db.users.drop()
true
```

**Listar/buscar**
As buscas e listagens são realizadas com a função **db.<COLLECTION_NAME>.find()**.

Exemplo para listar todos os documentos de uma collection:
```shell
> db.movie.find()
{ "_id" : ObjectId("57c8c570d7a9bc9e973b2c13"), "name" : "Teste de insert" }
{ "_id" : ObjectId("57c8c71ed7a9bc9e973b2c14"), "name" : "Teste de insert 2" }
{ "_id" : ObjectId("57c8c721d7a9bc9e973b2c15"), "name" : "Teste de insert 3" }
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

