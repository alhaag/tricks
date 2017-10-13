# ![logo](https://cdn-images-1.medium.com/max/800/1*dWHAgpfaDhohQ7kTcq9pVA.png)

Banco relacional minimalista baseado em arquivo.

Na maior parte das vezes supre todas as necessidades e em muitos cenários possui tempos de resposta maiores que SGBDs como MySQL e PostgreSQL, Porém não é recomendado para cenários de alta concorrência de escrita.

Tem a limitação de não possuir controle de acesso e usuários e um conjunto de tipos de dados reduzido.

Documentação oficial: https://www.sqlite.org/

## Instalação

Quase todas as distribuições linux possuim o sqlite instalado por padrão

Para verificar a versão:

```
$ sqlite3 --version
3.7.17 2013-05-20 00:56:22 118a3b35693b134d56ebd780123b7fd6f1497668
```

## Administração

O console é acessado por:
```
$ sqlite3
```

### Comandos úteis
```
sqlite> .help # exibe comandos disponíveis
```

## Data Types

| DataType | Descrição         |
| ---------|:------------------|
| NULL     | Valor nulo        |
| INTEGER  | Signed integer, stored in 1, 2, 3, 4, 6, or 8 bytes depending on the magnitude of the value |
| REAL     | Floating point value, stored as an 8-byte IEEE floating point number. | 
| TEXT     | Text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE) |  
| BLOB     | Text string, stored using the database encoding (UTF-8, UTF-16BE or UTF-16LE) |

SQLite não tem uma classe de armazenamento booleana separado. Em vez disso, os valores booleanos são armazenados como inteiros 0 (false) e 1 (true).

## Migrar MySQL -> SQLite
