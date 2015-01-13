title: Lavavel路由
date: 2014-10-31 15:45:11
tags: 
---



# 路由
- [基础路由](#basic)  
- [路由类型](#type)  
- [匿名函数](#closure)  
- [路由参数](#parameter)  
    - [必填参数](#must)  
    - [可选参数](#notmust)  


<a name="basic"></a>
## 基础路由

URL 地址：
```
http://mydomain.app/my/page
```
对应的路由设置：
```
// app/routes.php
Route::get('my/page', function()
{
    return 'Hello world!';
});
```
<a name="type"></a>
## 路由类型

```
Route::get();
Route::post();
Route::put();
Route::delete();
Route::any();
```

分别对应 GET(查看) POST(新增) PUT(修改) DELETE(删除) 这4种URL请求类型。 
而 `Route::any();` 则是包含了以上4种请求类型。

<a name="closure"></a>
## 匿名函数
```
// app/routes.php
$logic = function()
{
    return 'Hello world!';
}
Route::get('my/page', $logic);
```

<a name="parameter"></a>
## 路由参数

<a name="must"></a>
### 必填参数
```
// app/routes.php
Route::get('/books/{genre}', function($genre)
{
    return "Books in the {$genre} category.";
});
```
以上路由指向 http://mydomain.app/books/crime 并且地址中 $genre 参数必须存在。

<a name="notmust"></a>
### 可选参数
```
// app/routes.php
// routes for the books section
Route::get('/books/{genre?}', function($genre = 'Crime')
{
return "Books in the {$genre} category.";
});
```
此时 http://mydomain.app/books/ 也指向这个路由，并使用默认值 Crime。