# ![logo](https://cdn-images-1.medium.com/max/800/1*dWHAgpfaDhohQ7kTcq9pVA.png)

Banco relacional minimalista baseado em arquivo.

Na maior parte das vezes supre todas as necessidades e em muitos cenários possui tempos de resposta maiores que SGBDs como MySQL e PostgreSQL, Porém não é recomendado para cenários de alta concorrência de escrita.

Tem a limitação de não possuir controle de acesso e usuários.

Documentação oficial: https://www.sqlite.org/

## Instalação

Quase todas as distribuições linux possuim o sqlite instalado por padrão

Para verificar a versão:

```
$ sqlite3 --version
3.7.17 2013-05-20 00:56:22 118a3b35693b134d56ebd780123b7fd6f1497668
```

## Migrar MySQL -> SQLite
