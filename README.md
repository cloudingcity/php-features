# PHP Features

## PHP 7.1

### Spaceships

- `$a <=> $b`
    - if `$a == $b` return 0
    - if `$a < $b`  return -1
    - if `$a > $b`  return 1

```php
usort($array, function ($a, $b) {
    if ($a == $b) {
        return 0;
    }

    return ($a < $b) ? -1 : 1;
});

// same as
usort($array, function ($a, $b) {
    return $a <=> $b;
});
```

### Null Coalesce Operator

```php
$foo = (isset($bar)) ? $bar : 'default';

// same as
$foo = $bar ?? 'default';
```

### Anonymous Classes

```php
interface Logger
{
    public function log($message);
}

class App
{
    protected $logger;

    public function __construct(Logger $logger)
    {
        $this->logger = $logger;
    }

    public function log($message)
    {
        $this->logger->log($message);
    }
}
```

Use `new class` create a anonymous class:

```php
$logger = new class implements Logger
{
    public function log($message)
    {
        var_dump($message);
    }
};

$foo = new App($logger);
$foo->log('Hello World');

// string(11) "Hello World"
```

## PHP 7.2

### Symmetric Array Destructuring

```php

```

