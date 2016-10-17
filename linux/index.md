# Linux

## Basico

Listar variaveis de ambiente:
```shell
$ printenv
```

Ver nome e versão do SO:
```shell
$ cat /etc/*-release
CentOS release 5 (Final)
```
ou
```
$ lsb_release -a
LSB Version:	:core-3.1-ia32:core-3.1-noarch:graphics-3.1-ia32:graphics-3.1-noarch
Distributor ID:	CentOS
Description:	CentOS release 5 (Final)
Release:	5
Codename:	Final
```

Obter informações do kernel e arquitetura:
```shell
$ uname -a
Linux alhaag-Vostro-3560 4.2.0-42-generic #49-Ubuntu SMP Tue Jun 28 21:26:26 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
```
## curl
Exemplos de utilização:
```shell
## GET
$ curl http://host/resource

## POST
$ curl -d "paramn1=value&paramn2=value" http://host/resource
```

## File system

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

Contar linhas de um arquivo:
```shell
$ wc -l file.txt
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

Verificar codificação de arquivo:
```shell
$ file -i file.txt
file.txt: text/plain; charset=utf-8
```

Alterar codificação do arquivo:
```shell
$ iconv -f ISO-8859-1 -t UTF-8 file.old > file.new
```

Alterar codificação de arquivos recursivamente:
```shell
#!/bin/bash
find ./ -name "*.php" -o -name "*.html" -o -name "*.css" -o -name "*.js"  -type f |
while read file
do
  echo " $file"
  mv $file $file.icv
  iconv -f ISO-8859-1 -t UTF-8 $file.icv > $file
  rm -f $file.icv
done
```

---

## ISO

Visualizar conteúdo do arquivo:
```shell
$ isoinfo -f -i foo.iso 
```

Copiar imagem ISO para o pendrive:
```shell
$ umount /dev/sdb1
$ sudo dd if=/dev/sdb1 of=file.iso
```

---

## Rede
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

Capturar pacotes para analise no terminal:
```shell
$ tcpdump -nnnpi eth0 host 192.168.10.1 and proto UDP
```

**-i** interface de rede

**-s0** gera capturas ilimitadas

**-port 80** idica a porta que deve ser capturada

------

### NMAP
A aplicação **nmap** permite escanear portas abertas de um determinado host. 

Nomalmente não vem instalada por padrão, porém a maior parte dos sistemas operacionais possui esta pacote nos gerenciadores padrão, apt-get, yum, dnf, etc.

Escanear portas TCP (3 segundos):
```shell
# nmap -p0- IP
```

Escanear portas UDP (pode levar horas...):
```shell
# nmap -sU -F IP
```

### t50 - Testes de blindagem a DDos
O t50 é uma ferramenta desenvolvida por um brasileiro para testes de ataque DDos.

Para instalação deve ser baixado o tarball do endereço https://sourceforge.net/projects/t50 e executar os seguintes comandos:
```shell
$ tar xvf t50-5.6.6.tar.gz
$ cd t50-5.6.6/
$ ./configure
$ make
$ sudo make install
```

Para executar um teste de indisponibilidade executar o seguinte comando:
```shell
$ sudo t50 IP --flood --turbo -S --dport PORTA
```

---

## SED
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

## SSH
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

## TAR
Compactar lista de arquivos:
```shell
$ tar -cvpf /tmp/foo.tar smain/sb1 smain/sb
```
Extrair arquivo compactado em diretório específico:
```shell
$ tar xvf /home/file.tgz -C /tmp
```

Extrair um arquivo específico do tarball:
```shell
$ tar xvf /home/file.tgz /path/file.txt
```

## ZIP
Vizualizar conteúdo:
```shell
$ zipinfo foo.zip
```

Extrair arquivo ZIP:
```shell
$ unzip foo.zip
```
