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

Desligar a máquina:
```shell
$ vagrant suspend         # congela e mantem o estado
$ vagrant halt            # desliga e mantem o estado
$ vagrant destroy --force # destroi as alterações realizadas
```

## Listar VMs
Obter informações de VMs, estado, etc:
```shell
$ vagrant global-status
```

## Manipulação de box
Listar box baixas(disponiveis localmente):
```shell
$ vagrant box list
```

## Referências
 * https://www.vagrantup.com/docs/
 * https://gist.github.com/dergachev/3866825

