# Tuple returns 

fyi - A tuple (pronounced TUH-pul) is an ordered set of values. It isn't a set number of values, even though it kind of sounds like 'triple'. 

## General idea

Since 7.0, PHP has had the ability to specify the [return type of functions](https://wiki.php.net/rfc/return_types). 

This is useful for many reasons including program correctness, the ability to reason about the code, and static analysis tools.

However you can only define a single return type. Some functions should have multiple return values.


```php

function foo($bar_data, $quux_data)
{
    $bar_errors = bar($bar_data);
    
    if (count($bar_errors)) {
        return ["Bar data was invalid", null];
    }
    $quux_errors = bar($quux_data);
    
    if (count($bar_errors)) {
        return ["Quux data was invalid", null];
    }
    
    return [null, new BarQuux($bar_data, $quux_data)]
}

// Used as 
[$error, $barQuux] = foo($bar_data, $quux_data);

```

Here, the function returns two values:

* if there are errors, the first value is a string, and the second value is null.
* if there are no errors, the first value is null, and the second is an object of type BarQuux


### Similarity to structs problem

Classes in PHP are quite 'heavy' to use, in the sense that they take a lot of letters to type, and are non-trivial to read, particularly compared to TypeScript:

```tsx
interface Foo {
    description: string;
    value: number;
}
```

Even after the improvement of constructor promotion, the equivalent in PHP is more words: 

```php
class Foo {
    function __construct(
        readonly string $description,
        readonly int|float $number;
    )
}
```

It would be really nice if there was a lighter way of defining data structures, which has some words written at 
[Type Aliasing RFC](https://github.com/Danack/RfcCodex/blob/master/structs.md).



## Hurdles to overcome


### Syntax not obvious

What would be the appropriate syntax for tuple returns is 'not obvious'. Even for a simple example:

```
function foo(): [string, int] {
  ...
}
```

It is kind of fugly, but it is even worse for functions of the pattern like the `foo()` one above, where the return type would be documented in Psalm as:


```php
array{0: null, 1: BarQuux}|array{0: string, 1: null}
```

I don't think it will be tenable to cram that into where we currently have return types.


## Forecast

Adding this feature would make writing certain types of code a lot easier, and is a feature that is widely accepted in other languages, but it's hard to see it happening soon.

The way forward for this idea is quite likely to be a lot clearer if/when a [Type Aliasing RFC](https://github.com/Danack/RfcCodex/blob/master/type_aliasing.md) is passed.

## Notes

