# Linux

### Compactação de arquivos (tar)
Compactar lista de arquivos:
```shell
$ tar -cvpf /tmp/foo.tar smain/sb1 smain/sb
```
Extrair arquivo compactado em diretório específico:
```shell
$ tar -cvpf /tmp/foo.tar smain/sb1 smain/sb
```
---

### Rede (debug)
Verificar listen ports
```shell
$ netstat -npa | grep 80
- ou
$ netstat -atunp | grep 80
```

Capturar pacotes de rede para analise no Wireshark

-i any =  qualquer interface de rede

-s0 =  gera capturas ilimitadas
```shell
$ tcpdump -i any -s0 -w /tmp/dump.cap
```
---

### SSH
Liberar acesso por chave ssh
```shell
$ ssh-copy-id <user>@<ip>
```
---

### watch
Loop de execução de comando por timer definido
```shell
$ watch --interval=0.0 ls -lh
```
