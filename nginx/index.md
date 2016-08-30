# Nginx

### Autoindex
Listagen de diretórios/arquivos com autenticação:
```
location / {
    auth_basic "Restricted";                  
    auth_basic_user_file /etc/nginx/.htpasswd;
    autoindex_exact_size off;
    autoindex_localtime on;
    autoindex on;
    allow all;
  }
```

Procedimento para geração de senha:
```shell
$ sudo htpasswd -c /etc/nginx/.htpasswd exampleuser
```
Referencias [Tutorial Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-http-authentication-with-nginx-on-ubuntu-12-10)
