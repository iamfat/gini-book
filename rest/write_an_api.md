# 编写一个REST API

**STEP 1:** 建立文件 `class/controller/cgi/hello.php`

由于REST一定是基于HTTP的, 因此并不像其他Controller一样有单独的类别, 而是直接在CGI Controller下进行实现，其默认寻路规则也按照CGI Controller的规定进行。

```php
<?php
namespace Gini\Controller\CGI\REST;

use \Gini\Controller\REST;

class Hello extends REST {

    // @rest(GET /hello/article/{id})
    public function getArticle($id) {
        return \Gini\CGI\Response\JSON(["hello"=>"world"]);
    }

    // @rest(POST /hello/article)
    public function postArticle($author, $title, $body) {
        return \Gini\CGI\Response\JSON(["hello"=>"world"]);
    }

}
```

**STEP 2:** 运行测试服务器

```bash
$ gini cache
$ gini web update
$ gini web preview <host:port>    # default is localhost:3000
```

**STEP3:** 从另外的Gini模块进行调用

```php
<?php
$rest = new \Gini\REST('http://localhost:3000/rest');
$response = $rest->get('hello/article/1');
echo $response; // "Hello, world!";

$response = $rest->post('hello/article', ['author'=>'libai', 'title'=>'jiangjinjiu', 'body'=>'balabala']);
```



