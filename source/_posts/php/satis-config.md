title: 利用satis配置私有包
date: 2015-1-12 15:40:25
tags: composer satis
---



Satis 是一个静态的 `composer` 代码库生成器, 可以用来处理私有资源包。  

##install
```
composer.phar create-project composer/satis --stability=dev
```

## 配置
新建配置文件 `satis.json`，设置公共库和私有库
```
{
    "name": "My Repository",
    "homepage": "http://satis.yoursite.org/",
    "repositories": [
        {
            "type": "vcs",
            "url": "ssh://root@yoursite/www/gitdata/test-satis.git"
        },
        { "type": "vcs", "url": "https://github.com/laravel/laravel.git"},
        { "type": "vcs", "url": "https://github.com/padraic/mockery.git"},
    ],
    "require-all": true
}
```
完成配置通过以下命令生产项目 `php bin/satis build <configuration file> <build dir>`.

```
php bin/satis build satis.json web/
```
设置一个虚拟目录指向 web/ 目录, 假设绑定的域名是http://satis.yoursite.org。访问这个域名可以看到已经生成的包列表
> 注：每次更新包文件，都需要重新运行命令更新包列表

资源包介绍
> https://getcomposer.org/doc/05-repositories.md

## 使用

新建`composer.json`, 内容如下：
```
{
    "name": "project/test-satis",
    "type": "project",
    "require": {
        "taoanton/tinyframework": "0.2.0",
        "mockery/mockery": "0.7.*",
        "maxrocky/test-satis": "v0.2.2"
    },
    "minimum-stability": "dev",
    "repositories": [
        {
            "type": "composer",
            "url": "http://satis.yoursite.org/"
        },
        {"packagist": false}
    ]
}

```
运行`composer install` 安装依赖包

更多详细内容
> * https://getcomposer.org/doc/articles/handling-private-packages-with-satis.md
