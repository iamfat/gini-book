# CGI请求路由

请求路由是一个比较方便的方式来决定相应的访问路径应该定位到哪个Controller去。每个模块都可以根据需要在模块入口配置自定义的请求路由。

```php
namespace Gini\Module;

class Hello {
    public static function cgiRoute($router) {
        $router->get('hello/world', 'Real\\Hello@actionWorld');
        $router
            ->get('user/{id}', 'REST\\Hello@getUser')
            ->put('user/{id}/comment/{comment}', 'REST\\Hello@postComment');
    }
}
```

请求路由是能够嵌套的

```php
$router->get('nested/to', function($router) {
    $router->get('some-place/action', 'Real\\Place@someAction');
});
```



