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

Ver demais opções:
```shell
$ vagrant

Common commands:
     box             manages boxes: installation, removal, etc.
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           log in to HashiCorp's Atlas
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     version         prints current and latest Vagrant version
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
Criar um arquivo .box para reuso a partir do estado atual da VM:
```shell
$ vagrant package
```

Ver demais opções:
```shell
$ vagrant box

Available subcommands:
     add
     list
     outdated
     remove
     repackage
     update

```

Repositório público de boxes:
https://atlas.hashicorp.com/boxes/search

## Referências
 * https://www.vagrantup.com/docs/
 * https://gist.github.com/dergachev/3866825

