# docker-symfony-lemp-macosx

### Hakkında

Symfony tabanlı uygulamaların Docker containerları üzerinden çalıştırılmasını sağlar. 
Macosx performans iyileştirmeleri yapıldı.

### Yapı

- Webserver
-- Ubuntu 16.04 üzerinde Php 7.3 fpm + Nginx
- Database
-- Mysql 8.0
- Queue
-- Rabbitmq 3.7
- Phpmyadmin

### Kullanım

Kullanılan Domainler :
```sh
* phpmyadmin.test -> phpmyadmine erişim için kullanılır
* symfony.test -> app_dev.php üzerinden symfony appinize erişim için kullanılır. (web debug toolbar ile kullanım)
* symfony.prod -> app.php üzerinden symfony appinize erişim için kullanılır.
```

