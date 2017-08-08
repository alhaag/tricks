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

---

## AWK
A linguagem awk é muito conhecida por sua eficácia em criar filtros de conteúdos de arquivos.

Exemple de filtragem por coluna PID de resposta de um comando ps:
```shell
$ ps aux | grep ngix | awk '{ print $2 }'
```

mais exemplos em: https://www.vivaolinux.com.br/dica/Awk-Uma-poderosa-ferramenta-de-analise

---

## curl
Exemplos de utilização:
```shell
## GET
$ curl http://host/resource

## POST
$ curl -d "paramn1=value&paramn2=value" http://host/resource
```

---

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

Verificar tamanho do diretório corrente detalahndo arquivos e diretórios:
```shell
$ du -sk * | sort -h
```

Contar linhas de um arquivo:
```shell
$ wc -l file.txt
```

Contar arquivos recursivamente:
```shell
$ find . -type f | wc -l
```

Alterar permisões recursivamente e por tipo:
```
$ find /diretorio -type d -exec chmod 0755 {} \;
$ find /diretorio -type f -exec chmod 0644 {} \;
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

## Processos
Ver arvore de processos na ordem de subida:
```
$ pstree -np | less
```

Ver data e hora da subida de um processo:
```shell
$ ps axo comm,lstart|grep XXXXXX
```

Verificar consumo de memória de um processo:
```
$ pmap -x $pid
```
ou

```
$ ps -eo size,pid,user,command --sort -size | awk '{ hr=$1/1024 ; printf("%13.2f Mb ",hr) } { for ( x=4 ; x<=NF ; x++ ) { printf("%s ",$x) } print "" }'
```

top filtros:
```
## ordenar por consumo de ram
ps aux --sort -rss
```

---

## Rede
Criar link para acesso a outra rede.

Exemplo para liberar acesso ao IP 10.0.0.254 por meio da interface de rede **eth0**:
```shell
$ sudo ifconfig eth0:0 10.0.0.5
## PAra remover:
$ sudo ifconfig eth0:0 down
```

Para adicionar uma rota:
```
$ sudo route add -net <IP_REDE>/24 gw <IP_GATEWAY>
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

Realizar testes com limite de velociade de download e upload:
```
$ sudo apt-get install trickle
$ sudo trickle -vvv -d 10 -u 5 firefox
```
Obs: velocidade em Kbytes

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

## TELNET

Protocolo de comunicação para execução de comandos sobre um determinado host.

Estabelecer conexão:
```
$ telnet <ip_ou_host> <porta>
telnet>
```
Mais detalhes em: http://www.computerhope.com/unix/utelnet.htm

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
Gerar uma chave RSA local:
```shell
$ ssh-keygen
$ ls ~/.ssh
authorized_keys2  id_dsa  known_hosts   config  id_dsa.pub

$cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDILg/SCzmm29Nd4F/8q4M+imp3tw6c7sd47tgreOappkdhCsZa4uz3Qetc4rejwbLOrIDRlgCoGkROsahzpGIE7DaWvNsfjh1HV2zo175T5o+covHGDie7zPTfZjRuQy6cVnatu8DZWCDbujaqKaYSE2zoZ9hEb+9W138wdCKZSuery87aw+z3llkWyji+P4F9c/Z7ep4SgMuNi8xFJvFTnVr4I1ShYlmzTJqFrIZWXIcD46IM4uht6d3+n5CYGtMpIU3gnGLHZjlRobvhMzvLdC5lit4OUqs4QJoe+p3WOSN+BmQGjnUNKsQBTnfqpthfuroe874hgd9rtyuGg+AiEr user@hostname
```

Depuração de problemas relacionados ao SSH:
```shell
$ ssh <user>@<ip> -vvv
```
Realizar SSH informando uma chave de um path específico:
```shell
$ ssh <user>@<ip> -i /path/to/key
```

Liberar acesso por chave ssh
```shell
$ ssh-copy-id <user>@<ip>
```
---

## SystemD
Listar Unit files:
```
systemctl list-unit-files
```

Ordem de precedência dos units:
```
1. /etc/systemd/system
2. /run/systemd/system
3. /usr/lib/systemd/system
```

Recarrega o systemd, scaneando por units novas e modificadas:
```
$ systemctl daemon-reload
```

Niveis de execução:
```
$ ls -ltr /lib/systemd/system/runlevel*
lrwxrwxrwx. 1 root root 13 Jun  4 20:49 /lib/systemd/system/runlevel1.target -> rescue.target
lrwxrwxrwx. 1 root root 15 Jun  4 20:49 /lib/systemd/system/runlevel0.target -> poweroff.target
lrwxrwxrwx. 1 root root 17 Jun  4 20:49 /lib/systemd/system/runlevel2.target -> multi-user.target
lrwxrwxrwx. 1 root root 17 Jun  4 20:49 /lib/systemd/system/runlevel3.target -> multi-user.target
lrwxrwxrwx. 1 root root 17 Jun  4 20:49 /lib/systemd/system/runlevel4.target -> multi-user.target
lrwxrwxrwx. 1 root root 16 Jun  4 20:49 /lib/systemd/system/runlevel5.target -> graphical.target
lrwxrwxrwx. 1 root root 13 Jun  4 20:49 /lib/systemd/system/runlevel6.target -> reboot.target
```

Obter nível de execução atual:
```
$ systemctl get-default
graphical.target
```

Explanação sobre níveis de execução:
```
0	poweroff.target
1	rescue.target
2	multi-user.target
3	multi-user.target
4	multi-user.target
5	graphical.target
6	reboot.target
```

Ações sobre serviços:
```
systemctl start name.service
systemctl stop name.service
systemctl restart name.service
...
```

Ver logs:
```
$ journalctl  (todos)
$ journalctl -u nginx.service (por serviço)
$ journalctl -u nginx.service --since today (dia atual)
$ journalctl -k (logs do kernel)
$ journalctl -f (Following Logs)
```

Referencias:
https://fedoramagazine.org/systemd-getting-a-grip-on-units/

https://wiki.archlinux.org/index.php/Systemd_(Português)

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

---

## Users e Groups

Para possibilitar operações de root sem inserir senha, incluir no arquivo **/etc/sudoers**:

```shell
## Permition 'user' sudo less password
user  ALL=(ALL) NOPASSWD: ALL
```

---

## ZIP
Vizualizar conteúdo:
```shell
$ zipinfo foo.zip
```

Extrair arquivo ZIP:
```shell
$ unzip foo.zip
```
