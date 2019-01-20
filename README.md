# PHP Features
## PHP 5.6

### Variable-length argument lists

Instead `func_get_arg()`

```php
function dd(...$args)
{
    var_dump($args);
    exit;
}

dd(1, 2, 3);

/*
array(3) {
  [0] => int(1)
  [1] => int(2)
  [2] => int(3)
}
*/
```

```php
function animals($cat, $dog)
{
    echo $cat, PHP_EOL;
    echo $dog, PHP_EOL;
}

animals(...['Cat', 'Dog']);
```
---

## PHP 7

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

## PHP 7.1

### Symmetric Array Destructuring

```php
$fruits = ['Apple', 'Banana'];

list($apple, $banana) = $fruits;

// same as
[$apple, $banana] = $fruits;
```

```php
$books = [
    ['title' => 'Title 1', 'description' => 'Body 1'],
    ['title' => 'Title 2', 'description' => 'Body 2'],
];

['title' => $head, 'description' => $body] = $books[0];

var_dump($head, $body);
// string(7) "Title 1"  string(6) "Body 1"


foreach ($books as ['title' => $title, 'description' => $description]) {
    var_dump($title, $description);
}
// string(7) "Title 1"  string(6) "Body 1"
// string(7) "Title 2"  string(6) "Body 2"
```

### Multi-Catch Exception Handling
```php
class FooException extends Exception {}
class BarException extends Exception {}

try {
    // do some stuff
} catch (FooException $exception) {
    echo $exception->getMessage();
} catch (BarException $exception) {
    echo $exception->getMessage();
}

// same as
try {
    // do some stuff
} catch (FooException | BarException $exception) {
    echo $exception->getMessage();
}
```

### Class constant visibility
```php
class ConstDemo
{
    const PUBLIC_CONST_A = 1;
    public const PUBLIC_CONST_B = 2;
    protected const PROTECTED_CONST = 3;
    private const PRIVATE_CONST = 4;
}
```
