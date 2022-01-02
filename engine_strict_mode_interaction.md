# Strict mode and internal engine callbacks

## General idea

The PHP engine is in 'weak' mode by default. This leads to a highly surprising behaviour when using internal functions that call a callback that was defined in a file that had strict mode enabled. For example:

```
<?php

declare(strict_types = 1);

$takesAnIntFn = function (string $x) {
    return $x;
};

$numbers = [1, 2, 3.6, 4];

var_dump(array_map($takesAnIntFn, $numbers));

echo "array_map worked\n";

$results = [];
foreach ($numbers as $number) {
    $results[] = $takesAnIntFn($number);
}

```

The output of that code is:

```
array(4) {
  [0]=>
  string(1) "1"
  [1]=>
  string(1) "2"
  [2]=>
  string(3) "3.6"
  [3]=>
  string(1) "4"
}
array_map worked

Fatal error: Uncaught TypeError: {closure}(): Argument #1 ($x) must be of type string, int given, called in /in/2A1e9 on line 18 and defined in /in/2A1e9:5
Stack trace:
#0 /in/2A1e9(18): {closure}(1)
#1 {main}
  thrown in /in/2A1e9 on line 5
```

What is happening is that when `$takesAnIntFn` is called directly from strict mode, the floats are correctly not cast to string automatically.

When `$takesAnIntFn` is called by the engine inside array_map, then it is called in weak mode, and the floats are cast to string automatically.

Failing to fail, is one of the worst ways that a programming language can fail, as it can lead to data corruption.

## Hurdles to overcome

Someone needs to figure out what the correct behaviour is first, then figure out how to get to that correct behaviour without too huge a BC break.

## Forecast

This needs to be fixed some day. It might be _really_ quite tricky to do.

## Notes

A thread on how surprising it is: https://news-web.php.net/php.internals/116735
