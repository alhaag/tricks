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
Para acessar uma base deve ser utilizado o comando **use DB_NAME**, caso a base n]ao exista o Mongo irá criar automaticamente uma nova. Ex:
```shell
> use base_teste
switched to db base_teste
```

Verificar base selecionada:
```shell
> db
base_teste
```
## Listar bases
A listagem de todas as bases pode ser obtida por meio do comando **show dbs**. Ex:
```shell
>show dbs
local  0.000GB
test   0.23012GB
```
Obs: apenas bases que possuem documentos serão listadas.

## Drop database
A remoção da base selecionada é realizada por meio do comando **db.dropDatabase()**. Ex:
```
>db.dropDatabase()
{ "dropped" : "db_name", "ok" : 1 }
```
Obs: caso nenhuma base esteja selecionada, a base teste será removida;

## Criar collection
A criação de uma nova collection é realizada por meio do comando **db.createCollection(NAME, options)**. Ex:
```
> db.createCollection("users", {capped : true, autoIndexID : true, size : 6142800, max : 10000})
```
Opções disponíveis:

| Opção         | Tipo     | Descrição  |
| ------------- |:--------:| :-----|
| capped        | Boolean  | (Opcional) Se verdadeiro, permite uma coleção tampado. Coleção tampado é uma coleção collecction tamanho fixo que substitui automaticamente suas entradas mais antigas quando atinge seu tamanho máximo. Se você especificar true, você precisa especificar parâmetro de tamanho também. |
| autoIndexID   | Boolean  | (Opcional) Se for verdade, criar automaticamente índice em _id field.s O valor padrão é falso. |
| size          | number   | (Opcional) Especifica um tamanho máximo em bytes para uma coleção tampado. Se se tampado é verdade, então você precisa especificar neste campo também. |
| max           | number   | (Opcional) Especifica o número máximo de documentos permitidos na coleção tampado. |

Obs: em mongodb você não precisa criar coleção. MongoDB cria coleção automaticamente, quando um documento é inserido.

## Show collections
A listagem colecttions de uma base selecionada é realizada por meio do comando **show collections**. Ex:
```
> show collections
users
system.indexes
```

## Drop collection
A remoção de uma collection específica é realizada com o comando **db.COLLECTION.drop()**. Ex:
```
> db.users.drop()
{ "dropped" : "db_name", "ok" : 1 }
```

## Insert
A inserção de um novo documento na base selecionada é realizada por meio do comando **db.COLLECTION.insert(DOCUMENT)**. Ex:
```
> db.users.insert({"name":"Teste de insert"})
WriteResult({ "nInserted" : 1 })
```
Obs: em mongodb banco de dados padrão é o teste. Se não for criado um banco de dados, as coleções serão armazenados no banco de dados de teste.

Exemplo de inserção de coleção de documentos:
```
>db.post.insert([
   {
      title: 'MongoDB Overview', 
      description: 'MongoDB is no sql database',
      by: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 100
   },

   {
      title: 'NoSQL Database', 
      description: "NoSQL database doesn't have tables",
      by: 'tutorials point',
      url: 'http://www.tutorialspoint.com',
      tags: ['mongodb', 'database', 'NoSQL'],
      likes: 20, 
      comments: [ 
         {
            user:'user1',
            message: 'My first comment',
            dateCreated: new Date(2013,11,10,2,35),
            like: 0 
         }
      ]
   }
])
```

## Update
Para inserir o documento que você pode usar **db.COLLECTION.save(DOCUMENT)**. Se você não especificar _id no documento, o **save** irá funcionar como o **insert**. Porém o **_id** for especificado, ele irá substituir os dados do documento que contém _id informado. Ex:
```
> db.COLLECTION.save({_id:ObjectId(),NEW_DATA})
```

Para atualização de multiplos documentos por um criterio de busca é necessário utilizar o método **update()**, onde a sintaxe básica é:
```
> db.COLLECTION.update(SELECTIOIN_CRITERIA, UPDATED_DATA)
```
Por padrão o MongoDB irá atualizar apenas um único documento, para atualizar múltiplos, é necessário definir um parâmetro, "multi" para true. Ex:
```
> db.mycol.update({'title':'MongoDB Overview'},
   {$set:{'title':'New MongoDB Tutorial'}},{multi:true})
```

Detalhes sobre os criterios de busca serão apresentados na seção select.

## Select (find)
As buscas e listagens são realizadas com a função **db.COLLECTION.find()**.

Listar todos os documentos de uma collection:
```shell
> db.users.find()
{ "_id" : ObjectId("57c8c570d7a9bc9e973b2c13"), "name" : "Teste de insert" }
{ "_id" : ObjectId("57c8c71ed7a9bc9e973b2c14"), "name" : "Teste de insert 2" }
{ "_id" : ObjectId("57c8c721d7a9bc9e973b2c15"), "name" : "Teste de insert 3" }
```

A adição da função **pretty()** faz com que a lista seja apresentada com indentamento. Ex:
```shell
> db.users.find().pretty()
{ 
    "_id" : ObjectId("57c8c570d7a9bc9e973b2c13"),  
    "name" : "Teste de insert" 
}
...
```
A consulta de um único documento é realizada por meio da função **findOne()**. Ex:
```shell
> db.users.findOne()
{ "_id" : ObjectId("57c8c570d7a9bc9e973b2c13"), "name" : "Teste de insert" }
```
No MongoBD existe uyma equivalência ao **WHERE** dos RDMBS, onde as seguintes condições podem ser utilizadas em uma busca passando-se por parâmetro no método **find()** ou **findOne()**:

| Operação       | Sintaxe do parâmetro | Exemplo                        | Equivalente em RDBMS         |
| :--------------|:---------------------|:-------------------------------|:-----------------------------|
| Igualdade      | {key:value}          | find({"by":"tutorials point"}) | where by = 'tutorials point' |
| Menor que      | {key:{$lt:value}}    | find({"likes":{$lt:50}})       | where likes < 50             |
| Menor ou igual | {key:{$lte:value}}   | find({"likes":{$lte:50}})      | where likes <= 50            |
| Maior que      | {key:{$gt:value}}    | find({"likes":{$gt:50}})       | where likes > 50             |
| Maior ou igual | {key:{$gte:value}}   | find({"likes":{$gte:50}})      | where likes >= 50            |
| Diferente de   | {key:{$ne:value}}    | find({"likes":{$ne:50}})       | where likes != 50            |

No método find() é possível passar várias chaves separadas  por ',', assim o MongoDB trata como uma condição **AND**. Sintaxe básica é mostrada no exemplo a seguir:
```
> db.users.find({key1:value1, key2:value2})
```
A equivalência da clausula **OR** é obtida com a palavra chave **$or**. Ex:
```
> db.users.find({$or: [{key1: value1}, {key2:value2}]})
```

Exemplo de utilização de **AND** e **OR** em uma mesma busca:
```
>db.mycol.find({"likes": {$gt:10}, $or: [{"by": "tutorials point"}, {"title": "MongoDB Overview"}]}).pretty()
{
   "_id": ObjectId(7df78ad8902c),
   "title": "MongoDB Overview", 
   "description": "MongoDB is no sql database",
   "by": "tutorials point",
   "url": "http://www.tutorialspoint.com",
   "tags": ["mongodb", "database", "NoSQL"],
   "likes": "100"
}
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

