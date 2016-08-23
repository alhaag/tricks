# Linux

### File system

Listar dispositivos de armazenamento:
```shell
$ sudo fdisk -l
- ou
$ mount
```

Verificar tamanho do diretorio corrente:
```shell
$ du -sh
```

Contar arquivos recursivamente:
```shell
$ find . -type f | wc -l
```

Formatar pendrive. Para um pendrive montado em /dev/sdb1, executar:
```shell
$ umount /dev/sdb1
$ mkfs.vfat /dev/sdb1
```

Copiar imagem ISO para o pendrive
```shell
$ umount /dev/sdb1
$ sudo dd if=/dev/sdb1 of=file.iso
```

---

### Rede
Criar link para acesso a outra rede.

Exemplo para liberar acesso ao IP 10.0.0.254 por meio da interface de rede **eth0**:
```shell
$ sudo ifconfig eth0:0 10.0.0.5
```
Verificar listen ports
```shell
$ netstat -npa | grep 80
- ou
$ netstat -atunp | grep 80
```
Capturar pacotes de rede para analise no Wireshark:

```shell
$ tcpdump -i any -s0 -w /tmp/dump.cap
```
**-i any** qualquer interface de rede

**-s0** gera capturas ilimitadas

**-port 80** idica a porta que deve ser capturada

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
$ tar xvf /home/file.tgz -C /tmp
```
