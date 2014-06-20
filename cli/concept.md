# Concept

All process started from `\Gini\Core::start()`. It will prepare autoloading mechanism, load config, set timezone, error reporting, etc. Then it will imports all dependent modules configured for your application in `gini.json` and sequentially run bootstrap methods in these modules.

Every module may have their own bootstrap class with same name as the module shortname.
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
