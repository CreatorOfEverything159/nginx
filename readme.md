# Lab-3
## Задание
Реализовать два приложения, располагающиеся на файловой системе в */var/www/html/app1/index.html* и  */var/www/html/app2/index.html*, доступные по адресам http://ip/ и http://ip:7777/docs/ соответственно с помощью конфигурирования NGINX.

## Ход работы

### Конфигурация файла default в sites-enabled
**Настройка сервера:**
```
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html/app1;

        index index.html index.htm index.nginx-debian.html;

        server_name borewsha.ninja;

        location / {
                try_files $uri $uri/ =404;
        }
}

server {
        listen 7777 default_server;
        listen [::]:7777 default_server;

        root /var/www/html/app2;

        index index.html index.htm index.nginx-debian.html;

        server_name borewsha.ninja;

        location / {
                return 404;
        }

        location /docs {
                try_files $uri /index.html =404;
        }
}
```
