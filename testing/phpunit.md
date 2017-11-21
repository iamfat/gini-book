# PHPUnit

你可以使用 `gini ci phpunit init` 命令初始化你的 PHPUnit 环境

```bash
gini ci phpunit init
# 这会生成ci/test目录
```

然后你可以使用 `gini ci phpunit create` 命令来建立指定名称的测试

```bash
gini ci phpunit create Hello/World
# 这会生成 ci/test/Hello/World.php 文件
```

测试的示例:

```php
<?php

namespace Gini\PHPUnit\Hello;

class World extends \Gini\PHPUnit\TestCase\CLI {

    public function testHello() {
        $this->assertTrue(false, "PLEASE IMPLEMENT THIS!");
    }

}
```



