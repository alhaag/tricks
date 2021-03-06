# Nginx

## Autoindex
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

## Hack para multiplas condições
```
    if ($request_uri = /) { 
      set $test  A; 
    } 
  
    if ($host ~* teambox.com) { 
      set $test  "${test}B"; 
    } 
  
    if ($http_cookie !~* "auth_token") { 
      set $test  "${test}C"; 
    } 
    
    if ($test = ABC) { 
      proxy_pass http://teambox-cms.heroku.com; 
      break; 
    }
```

## Extras
Remover http para // como sulução de problemas relacionados quando atuando como proxy reverso:
```
server {
    ...
    proxy_redirect http://$host/ /;
    ...
```
