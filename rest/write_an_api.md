# 编写一个REST API

**STEP 1:** 建立文件 `class/controller/cgi/hello.php`

由于REST一定是基于HTTP的, 因此并不像其他Controller一样有单独的类别, 而是直接在CGI Controller下进行实现，其默认寻路规则也按照CGI Controller的规定进行。

```php
<?php
namespace Gini\Controller\CGI;

class Hello extends \Controller\REST {

    function getWorld() {
        return \Gini\CGI\Response\JSON(["hello"=>"world"]);
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



