# Write "Hello, world!"

**STEP 1:** Create file `class/Gini/Controller/CLI/Hello.php`
```php
<?php

namespace Gini\Controller\CLI;

class Hello extends \Gini\Controller\CLI {

    function actionWorld() {
        echo "Hello, world!\n";
    }

}

```

**STEP 2:** Run it from command line!
```bash
$ gini cache
$ gini hello world
Hello, world!
```
