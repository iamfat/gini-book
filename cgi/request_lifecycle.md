# 请求的声明周期

所有进入应用的请求都会经过 `web/index.php` 脚本进行分发. 从这个点, **Gini** 开始对请求的相应并把回应返回给客户端。

每一个请求的开始函数是 `\Gini\Core::start()`. 这个内核加载函数会准备自动加载机制, 加载配置, 设置时区, 设置错误处理等工作。接着他会按照`gini.json`定义的各个Gini模块的依赖顺序加载。

每一个模块都可以在各自的`class/Gini/Module/<MODULE_NAME>.php`配置自己的模块入口相关代码。

```php
// 如果模块目录叫 my-module, 或者在 gini.json 定义的 id: my-module
// 入口会是是 class/Gini/Module/MyModule.php

namespace Gini\Module;

class MyModule extends Prototype {

    public static function setup() {
        // run when each request started
    }

    public static function shutdown() {
        // run when each request finished
    }

}
```

这些入口类里面的静态方法 `setup` 会按照模块依赖顺序依次被执行。所有入口`setup`代码被执行完毕后 ，应用完成初始化，进入正式的请求主程序。

在CGI请求中，Gini会自动根据HTTP请求情况定位CGI controller。在一般的PHP框架中, 会首先根据HTTP请求进行routing操作，然后再分发，这部分请阅读[请求路由](/cgi/routing.md)。Gini框架自动设置了一套类似Kohana的路由分发标准，将路径与PHP自动加载路径完全对应，不损失性能的直接定位到函数入口:

```
/hello/world  =>
    \Gini\Controller\CGI\Hello::actionWorld()
    \Gini\Controller\CGI\Hello::__index($world)
    \Gini\Controller\CGI\Index::actionHello($world)
    \Gini\Controller\CGI\Index::__index($hello, $world)
```

相应的请求被触发之后，回应会返回到客户端。之后系统会按照依赖次序反序依次调用所有模块入口的`shutdown`方法。至此完成所有请求。

