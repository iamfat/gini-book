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

## 有名变量自适应

使用请求路由后有一个优点是，如果在路由中使用了`{var}`形式的变量, 系统在调用Controller相应action的时候，会通过反射机制自动解析代码中的变量名称，对变量进行赋值，而不受顺序影响。

```php
$router->get('user/{uid}/comment/{comment}', 'REST\\Hello@postComment');

class Hello extends REST {
    public function postComment($comment, $uid) {
        // 在这样的参数顺序中, 系统扔能确保传入数据正常
    }
}
```



