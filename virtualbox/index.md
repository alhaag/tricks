# Virtual Box

Redimensionar disco:

1. Criar um novo disco e clonar o antigo
```
$ VBoxManage createhd --filename NewDisk.vdi --size 20480000000 
$ VBoxManage clonehd OldDisk.vmdk NewDisk.vdi --existing 
```

2. Alterar o disco da VM.

3. Dentro da maquina virtual expandir a partição para ocupar o novo espaço não alocado.
