# Write an API

**STEP 1:** Create file `class/controller/api/hello.php`

```php
<?php
namespace Gini\Controller\API;

class Hello extends \Controller\API {

    function world() {
        return "Hello, world!\n";
    }

}
```

**STEP 2:** Run a test server

```bash
$ gini cache
$ gini config update
$ gini web update
$ gini web preview <host:port>    # default is localhost:3000
```

**STEP3:** Call it from another program

```php
<?php
$rpc = new \Gini\RPC('http://localhost:3000/api');
$response = $rpc->hello->world();
echo $response; // "Hello, world!";
```



