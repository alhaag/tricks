
# SVN

### SVN2GIT
Migrar repositório SVN para o GIT

Instalar a ferramenta python SVN2GIT:
```shell
$ sudo apt-get install git-core git-svn ruby
$ sudo gem install svn2git
```
Gerar projeto GIT a partir de um repositório SVN:
```shell
$ mkdir /local/path/project
$ cd /local/path/project
$ svn2git http://svn.digitro.com.br/path/to/project
```

Adicionar origem de um projeto GIT vazio para que seja possível comitar para o repositório:
```shell
$ git remote add origin git@gitlab.digitro.com.br:<group>/<project>.git
$ git push -u origin master
```
