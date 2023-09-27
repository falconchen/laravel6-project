# Travellist - Laravel Demo App


相关教程

- [How to Install and Configure Laravel with LEMP on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-laravel-with-lemp-on-ubuntu-18-04)



- [构建Laravel Docker环境](https://www.digitalocean.com/community/tutorials/how-to-install-and-set-up-laravel-with-docker-compose-on-ubuntu-22-04)

- [MySQL镜像参考文档](https://hub.docker.com/_/mysql)


## 笔记：

### php-fpm

可以往Dockerfile里加入一些自定义的配置, 比如安装php redis扩展。使用pecl时注意clash需要开全局增强。
`RUN pecl install redis && docker-php-ext-enable redis`

docker-compose.yml中可以定义在构建时指定参数，用特定用户来运行php-fpm、composer 和 laravel 的 cli
        
使用 root 访问容器（当前为build时指定的user和uid)

```docker compose exec -u root -it app /bin/bash```

### docker compose

构建
```docker-compose build app```

运行
```docker-compose up -d```

查看进程
```docker compose top```

查看当前运行容器
```docker compose ps```

挂起
```docker compose pause```

恢复
```docker compose unpause```

查看日志
```docker-compose logs nginx```


### laravel

生成密码，用于加密会话
```docker-compose exec app php artisan key:generate```

安装依赖

``` 
docker-compose exec app rm -rf vendor composer.lock
docker-compose exec app composer install
```

### MySQL

- 指定目录存储MySQL数据目录，即使用目录映射
`-v /my/own/datadir:/var/lib/mysql`

- [MySQL镜像参考文档](https://hub.docker.com/_/mysql)

- 使用变量 `MYSQL_ROOT_PASSWORD` 指定root密码





