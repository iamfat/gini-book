# JSON-RPC 2.0 over HTTP

**Gini** uses [JSON-RPC 2.0](http://www.jsonrpc.org) over HTTP for communication with other programs.

```php
$rpc = new \Gini\RPC('http://path/to/api');
$ret = $rpc->hello->world(1, "abc");
```
The call will send following json:
```json
{"jsonrpc": "2.0", "method": "hello/world", "params": [1, "abc"], "id": 1}
```

If we assume this call will get a normal response from remote service.
```json
{"jsonrpc": "2.0", "result": "Hello, world!", "id": 1}
```

The result can be easily get by the return value of the call:
```php
$rpc = new \Gini\RPC('http://path/to/api');
$ret = $rpc->hello->world(1, "abc");
// $ret = 'Hello, world!'
```

If an error was happened during the call, an `\Gini\RPC\Exception` will be thrown:
```php
try {
    $rpc = new \Gini\RPC('http://path/to/api');
    $ret = $rpc->hello->world(1, "abc");
} catch (\Gini\RPC\Exception $e) {
    // catch the exception
}
```

### Terms
* **RPC**: _Remote Procedure Call_.
* **JSON**: _JavaScript Object Notation_.
