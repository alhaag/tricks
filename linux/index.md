# Linux

### watch
Loop de execução de comando por timer definido
```shell
$ watch --interval=0.0 ls -lh
```

### Rede (debug)
Verificar listen ports
```
$ netstat -npa | grep 80
- ou
$ netstat -atunp | grep 80
```

### SSH
Liberar acesso por chave ssh
```
$ ssh-copy-id <user>@<ip>
```
