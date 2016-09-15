# Vagrant

## Instalação

### Ubuntu
```shell
$ sudo apt-get install vagrant
```

### Centos
...

## Comandos básicos
Adicionar uma imagem no vagrant:
```shell
$ vagrant box add IMAGE_NAME http://imgserver.com.br/vagrant/img.box
```

Iniciar um ambiente à partir de uma imagem previamente adicionada (esta ação gera um arquivo Vagrantfile com as configurações iniciais):
```shell
$ cd /path/to/env # entrar no diretório onde será instalada a imagem
$ vagrant init IMAGE_NAME
```

Inicializa a máquina virtual com as configurações presentes no Vagrantfile:
```shell
$ vagrant up
```

Acessa a máquina por ssh:
```shell
$ vagrant ssh
```

Reinicia a máquina para o últimno estado:
```shell
$ vagrant reload
```

Desliga a máquina e destroi o estado:
```shell
$ vagrant destroy --force
```

## Referências
 * https://www.vagrantup.com/docs/
 * https://gist.github.com/dergachev/3866825

