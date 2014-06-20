# Request Lifecycle

All requests into your application are directed through the `web/index.php` script. From here, **Gini** begins the process of handling the requests and returning a response to the client.

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

The static `setup` methods in these class will be called sequentially according the order of module dependencies. After all modules have been set up, your app will be loaded. In a CGI request, Gini will automatically call corresponding CGI controller by parse your request path:

```
/hello/world  =>
    \Gini\Controller\CGI\Hello::actionWorld()
    \Gini\Controller\CGI\Hello::__index($world)
    \Gini\Controller\CGI\Index::actionHello($world)
    \Gini\Controller\CGI\Index::__index($hello, $world)
```

After the action was called, an response will be return and sent back to client. After that, `shutdown` methods in all modules will be called.

