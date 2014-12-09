#php TDD
##测试驱动开发
测试驱动开发（Test-driven development）是极限编程中倡导的程序开发方法，以其倡导先写测试程序，然后编码实现其功能得名。测试驱动开发始于20世纪90年代。测试驱动开发的目的是取得快速反馈并使用“illustrate the main line”方法来构建程序。

测试驱动开发是戴两顶帽子思考的开发方式：先戴上实现功能的帽子，在测试的辅助下，快速实现其功能；再戴上重构的帽子，在测试的保护下，通过去除冗余的代码，提高代码质量。测试驱动着整个开发过程：首先，驱动代码的设计和功能的实现；其后，驱动代码的再设计和重构。

> * 以上内容摘取自维基百科: http://zh.wikipedia.org/wiki/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91
> * 书籍：测试驱动开发 http://book.douban.com/subject/25735501/
> * 练习：https://github.com/daylerees/test-driven-development-example


##什么是测试驱动开发
或许泥瓦匠的例子比较适合， 看一下泥瓦匠如何工作的吧

>工匠一:先拉上一根水平线，砌每一块砖时，都与这根水平线进行比较，使得每一块砖都保持水平。  
>工匠二:先将一排砖都砌完，然后拉上一根水平线，看看哪些砖有问题，再进行调整。  

![泥瓦匠](./images/wall-line.jpg)

##phpunit
PHPUnit是一个轻量级的PHP测试框架， 当前最新版本 PHPUnit 4.4.0
> * https://phpunit.de/

###安装 （linux）
```bash
$ wget https://phar.phpunit.de/phpunit.phar  
$ chmod  +x phpunit.phar  
$ sudo mv phpunit.phar /usr/local/bin/phpunit
```
> * 其他平台安装方式请参考PHPUnit手册第1章

###命令行测试
一些简单的常用命令

测试指定类
```bash
cd your-project-folder/

phpunit --filter AdminLoginTest
PHPUnit 4.4.0 by Sebastian Bergmann.

Time: 2.49 seconds, Memory: 6.75Mb
OK (1 test, 0 assertions)
```

测试指定类的方法
```bash
phpunit --filter AdminLoginTest::testAdminCheckLogin
```

测试指定的文件夹
```bash
phpunit --filter AdminLoginTest::testAdminCheckLogin
```

测试整个项目
```bash
phpunit
```
> *更多命令行选项请参考PHPUnit手册第3章 命令行测试执行器


##laravel testing
laravel的测试扩展自PHPUnit

> * http://laravel.com/docs/4.2/testing
