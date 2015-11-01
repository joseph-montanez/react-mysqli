# AsyncMysql

Asynchronous & non-blocking MySQL driver for [React.PHP](https://github.com/reactphp/react).

## Usage

Create instance of AsyncMysql and call method `query`.
It returns [Promise](https://github.com/reactphp/promise) of [mysqli_result](http://cz2.php.net/manual/en/class.mysqli-result.php) that will be resolved imediately after query completes.

```php
<?php

$loop = React\EventLoop\Factory::create();

$makeConnection = function () {
  return mysqli_connect('localhost', 'user', 'pass', 'dbname');
};

$mysql = new \KHR\React\Mysql\Client($loop, new \KHR\React\Mysql\Pool(function(){
    return mysqli_connect('127.0.0.1', 'root', '', 'test');
}, 10));
$mysql->query('select * from ponies_and_unicorns')->then(
  function ($result) { writeHttpResponse(json_encode($result->all())); },
  function ($error)  { writeHeader500(); }
);
```
