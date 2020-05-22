# Briefer closure syntax 

Implemented in PHP 7.4, though only as single expressions, not multiple expressions.

## General idea

Closures in PHP are quite verbose compared to those in other languages.


```php
$add1 = function ($x) {
    return $x + 1;
};

```

This is similar to how closures were originally implemented in Javascript.

```php

var add1 = function (x) {
    return x + 1;
}

```

Since then however, as Javascript developers thought they were too long, they introduced arrow functions.

```php
var add1 = x => x + 1;
```

It would be nice to have a similar short syntax in PHP.


## Hurdles to overcome

### Some people don't see the need 

Although they are very useful where they are needed, it is not every PHP program that needs closures, and it's only in some cases where short closures provide that much benefit over the current closures.

For people who haven't been exposed to those use-cases, it can appear that there isn't much need for shorter closures.

Convincing these people (possibly by getting to read or write some modern Javascript) would be a big step in getting them to see the need.

### Exact details seem to provoke 

The exact implementation that is most appropriate still needs to be decided.

In Javascript, both the original closures and arrow functions will automatically inherit parameters from the scope they are defined in. 

```php
function getAddFunction(x) {
    return y => y + x;
}

var fn = getAddFunction(1);

var result = fn(2); 

// result is 3 

```

For the current closure syntax in PHP, you must explicitly pull in variables from the scope the closure is defined in.

```php
function getAddFunction($x) {
    return function($y) use ($x) {
        return $x + $y;
    };
}

$fn = getAddFunction(1);

$result = fn(2); 

// result is 3

```

Exactly what the syntax should be for using variables seems to need to be settled.


Also, should people be able to set return types for short closures, and what the syntax for that should be.


## Forecast

Reasonably likely to happen when someone has the time and energy to make another push for it.

Particularly if more people are exposed to the equivalent in Javascript.

## Notes


https://wiki.php.net/rfc/arrow_functions

https://wiki.php.net/rfc/short-closures





