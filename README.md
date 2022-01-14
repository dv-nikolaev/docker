# docker

На маке не создаются интерфейсы bridge network, из-за чего трафик между контейнерами не роутится в случае с раздельными network, как в задании. Тем не менее, при корректной работе необходимо изменить адрес upstream в nginx.conf и изменить  network у одного из контейнеров


Вывод проверки работоспособности из консоли:
dmitriy@MacBook-Pro-Dmitry epam % docker-compose up -d
WARNING: Some networks were defined but are not used by any service: apache_net
Recreating epam_nginx_1 ...
Recreating epam_nginx_1 ... done
dmitriy@MacBook-Pro-Dmitry epam % curl localhost:80
Hello, world
dmitriy@MacBook-Pro-Dmitry epam % curl localhost:8080
Hello, world
dmitriy@MacBook-Pro-Dmitry epam % docker ps
CONTAINER ID   IMAGE                              COMMAND                  CREATED          STATUS          PORTS                    NAMES
89ef696102e1   localhost:5000/epam-nginx:latest   "/docker-entrypoint.…"   12 seconds ago   Up 11 seconds   0.0.0.0:80->80/tcp       epam_nginx_1
0a4c3c5dbb0e   localhost:5000/httpd:latest        "httpd-foreground"       3 minutes ago    Up 3 minutes    0.0.0.0:8080->80/tcp     epam_apache_1
ab4a9d27ddeb   registry                           "/entrypoint.sh /etc…"   4 hours ago      Up 4 hours      0.0.0.0:5000->5000/tcp   registry
dmitriy@MacBook-Pro-Dmitry epam % docker image list
REPOSITORY                    TAG       IMAGE ID       CREATED          SIZE
localhost:5000/epam-nginx     1.0.2     cefbee600b0b   46 seconds ago   141MB
localhost:5000/epam-nginx     latest    cefbee600b0b   46 seconds ago   141MB
localhost:5000/epam-nginx     <none>    f403dc5a515f   2 minutes ago    141MB
localhost:5000/epam-nginx     <none>    709fa94c7f02   4 minutes ago    141MB
localhost:5000/epam-nginx     1.0.1     880b8f2a2b0a   2 hours ago      141MB
localhost:5000/epam-nginx     1.0.0     c5a18b95d604   3 hours ago      141MB
nginx                         latest    605c77e624dd   2 weeks ago      141MB
httpd                         latest    dabbfbe0c57b   3 weeks ago      144MB
localhost:5000/httpd          1.0.0     dabbfbe0c57b   3 weeks ago      144MB
localhost:5000/httpd          latest    dabbfbe0c57b   3 weeks ago      144MB
registry                      latest    b8604a3fe854   2 months ago     26.2MB
node                          latest    1016313cda78   4 months ago     907MB
