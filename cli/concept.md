# 概念

所有的进程都是从 `\Gini\Core::start()` 开始. 系统会准备自动加载机制，加载配置文件，设置时区，设置默认错误报警等等。然后会按照`gini.json`定义的依赖关系，依次加载模块。

每一个模块都可以有一个和模块同名的类, 用于实现模块的基本方法.
```php
// path/to/mymodule/class/Gini/Module/MyModule.php

namespace Gini\Module;

class MyModule {

    static function setup() {
        // run when each request started
    }

    static function shutdown() {
        // run when each request finished
    }
    
    static function diagnose() {
        // run to check all things required for module
        // will be called by `gini doctor`
    }

}
```

The static `setup` methods in these class will be called sequentially according the order of module dependencies. After all modules have been set up, your app will be loaded and corresponding action will be called.

```
gini hello world  =>
    \Gini\Controller\CLI\Hello::actionWorld()
    \Gini\Controller\CLI\Hello::__index($world)
    \Gini\Controller\CLI\Index::actionHello($world)
    \Gini\Controller\CLI\Index::__index($hello, $world)
```

After the action was called, an response will be return and sent back to client. After that, `shutdown` methods in all modules will be called.
