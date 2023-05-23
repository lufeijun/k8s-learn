# php docker 镜像搭建



# 搭建思路

## 1、整体作为一个 pod

说明：php-fpm、nginx 两个 container 处在同一个 pod 中

## 2、作为代理层，分开部署

说明：分别部署 nginx、php-fpm，php-fpm 作为 nginx 上游