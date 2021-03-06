title: Lavavel响应
date: 2014-10-31 15:45:11
tags: 
---


# 响应

## 视图响应

模板文件：

```
<html lang="en">
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Views!</title>
</head>
<body>
    <p>Oh yeah! VIEWS!</p>
</body>
</html>
```

路由定义：
```
// app/routes.php
Route::get('/', function()
{
    return View::make('simple');
});
```

### 向视图中传递数据

```
Route::get('/{squirrel}', function($squirrel)
{
    $data['squirrel'] = $squirrel;
    return View::make('simple', $data);
});

<!-- app/views/simple.php -->
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Squirrels</title>
</head>
<body>
    <p>I wish I were a <?php echo $squirrel; ?> squirrel!</p>
</body>
</html>
```

重定向
```
// app/routes.php
Route::get('first', function()
{
    return Redirect::to('second');
});
Route::get('second', function()
{
    return 'Second route.';
});
```
重定向在用户认证中的应用

```
// app/routes.php
Route::get('books', function()
{
    if (Auth::guest()) return Redirect::to('login');
    // Show books to only logged in users.
});
```
可定制的服务器响应

定制响应的“头信息”

```
// app/routes.php
Route::get('markdown/response', function()
{
    $response = Response::make('***some bold text***', 200);
    $response->headers->set('Content-Type', 'text/x-markdown');
    return $response;
});
```
定制响应的“存活时间”

存活时间 Time-to-live 这个时间以秒为单位，它是数据包可以生存的时间。在传输中，如果超过了这个时间，这个数据报就被认为丢失了，或在一个循环内并且被废弃。

```
// app/routes.php
Route::get('our/response', function()
{
    $response = Response::make('Bond, James Bond.', 200);
    $response->setTtl(60);
    return $response;
});
```
Response 的 API
> [TheSymfonyResponseObject](http://api.symfony.com/2.2/Symfony/Component/HttpFoundation/Response.html)

Respanse 的快捷方法

JSON 响应

```
// app/routes.php
Route::get('markdown/response', function()
{
    $data = array('iron', 'man', 'rocks');
    return Response::json($data);
});
```
浏览器将输出 `["iron","man","rocks"]`

下载 响应

```
// app/routes.php
Route::get('file/download', function()
{
    $file = 'path_to_my_file.pdf';
    return Response::download($file);
});
```
可定制 HTTP 状态码、头信息

```
// app/routes.php
Route::get('file/download', function()
{
    $file = 'path_to_my_file.pdf';
    return Response::download($file, 418, array('iron', 'man'));
});
```