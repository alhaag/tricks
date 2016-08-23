# Linux

### Rede
Criar link para acesso a outra rede:
```shell
$ sudo ifconfig eth0:0 10.0.0.5
```
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

### SED
Manipulação de conteúdo de arquivos com sed.

Utilização básica:

```shell
$ sed -i 's/<search>/<replace>/g' <file>
```
Substituição de diretiva de configuração do Nginx:
```shell
$ sed -i 's/location \/atualizador {\nproxy_pass http://web-tomcat;\n}/TESTETESTE/g' nginx.conf
```
Mais exemplos em [Só SED](http://thobias.org/doc/sosed.html)

---

### SSH
Liberar acesso por chave ssh
```shell
$ ssh-copy-id <user>@<ip>
```
---

### Watch
Loop de execução de comando por timer definido. Útil para verificar alterações em tempo real:
```shell
$ watch --interval=0.0 ls -lh
```
---

### TAR
Compactar lista de arquivos:
```shell
$ tar -cvpf /tmp/foo.tar smain/sb1 smain/sb
```
Extrair arquivo compactado em diretório específico:
```shell
$ tar -cvpf /tmp/foo.tar smain/sb1 smain/sb
```
