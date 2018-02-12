# Virtual Box

Redimensionar disco:

1. Criar um novo disco e clonar o antigo
```
$ VBoxManage createhd --filename NewDisk.vdi --size 20480000000 
$ VBoxManage clonehd OldDisk.vmdk NewDisk.vdi --existing 
```

2. Na interface de configurações da VM (VirtualBox) trocar o disco.

3. Dentro da máquina virtual expandir a partição para ocupar o novo espaço não alocado.
