title: Lavavel过滤器
date: 2014-10-31 15:45:11
tags: 
---



# 过滤器

## 基础过滤器

定义过滤器：

```
// app/filters.php
Route::filter('birthday', function()
{
    if (date('d/m') == '12/12')
    {
        return View::make('birthday');
    }
});
```

路由中的调用方法：
```
// app/routes.php
Route::get('/', array(
    'before' => 'birthday',
    function()
    {
        return View::make('hello');
    }
));
```

## 多重过滤

采用“|”分隔，或数组定义
```
// app/routes.php
Route::get('/', array(
    'before' => 'birthday|christmas',
    function()
    {
        return View::make('hello');
    }
));
 
// app/routes.php
Route::get('/', array(
    'before' => array('birthday', 'christmas'),
    function()
    {
        return View::make('hello');
    }
));
```

## 过滤器参数

```
// app/filters.php
// before 前置过滤器
Route::filter('test', function($route, $request)
{
});
// after 后置过滤器
Route::filter('test', function($route, $request, $response)
{
});
```

向过滤器中传递额外的参数

```
// app/routes.php
Route::get('/', array(
    'before' => 'birthday:foo,bar,baz',
    function()
    {
        return View::make('hello');
    }
));
 
// app/filters.php
Route::filter('birthday', function($route, $request, $first, $second, $third)
{
    return "{$first} - {$second} - {$third}";
});
```

## 使用类文件来作为过滤器

首先确保已经 注册 laravel 的类加载目录

```
// app/start/global.php
ClassLoader::addDirectories(array(
    ...
    app_path().'/filters',  //  如需使用过滤器类，请添加
    ...
));
```
接着定义过滤器类文件

```
// app/filters/Birthday.php
class BirthdayFilter {
    ...
    public function filter($route, $request, $date)
    {
        if (date('d/m') == $date)
        {
            return View::make('birthday');
        }
    }
    ...
}

// app/routes.php
Route::filter('birthday', 'BirthdayFilter');
```
注意： 最终执行的是类中的 filter() 方法，并且新定义的类需要执行一次 php artisan dump-autoload 指令以帮助其载入。

## 全局过滤器

```
// app/filters.php
App::before(function($request)
{
    //
});
App::after(function($request, $response)
{
    //
});
```
## 模式过滤器

```
// app/routes.php
Route::when('profile/*', 'birthday');
```

以上代码将匹配所有 profile/ 开头的路由，来使用 birthday 作为前置过滤器。 
还可以针对 HTTP 请求类型 限定模式过滤器：

```
Route::when('admin/*', 'admin', array('post'));
```