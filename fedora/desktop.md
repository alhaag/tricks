# Fedora 26 Desktop

Instalação do ambiente dedesenvolvimento com Fedora 26 e interface gráfica i3.

## Distribuição

Utilizada versão mais leve do fedora com interface XFCE:

https://spins.fedoraproject.org/xfce/download/index.html

## Atualização do sistema

```
# dnf update
```

## Instalação Fedy (opcional)

Instalador de de pacotes
```
# sh -c 'curl https://www.folkswithhats.org/installer | bash'
```

## Instalação do i3wm

Interface gráfica i3 mais pacotes extras:

```
# dnf install i3 i3status i3lock
```

## Removendo o XFCE4(Opcional)
```
# dnf groups remove "Xfce Desktop"
```

## Inicialização do i3
criar ~/.xinitrc para uso do startx:
```
$ echo "exec i3" > ~/.xinitrc
```
Reboot e após o login execute o seguinte comando para iniciar o i3wm:
```
$ startx
```

