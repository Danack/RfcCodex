# Type aliasing 

## General idea

Since PHP 8.0, it has been possible to declare a parameter, property or return as a [union of types](https://wiki.php.net/rfc/union_types_v2), rather than a single type:

```
function foo(int|float $x): 
{
}
```

And since PHP 8.1 it has been possible to declare types in the [Disjunctive Normal Form](https://wiki.php.net/rfc/dnf_types), 
which is a fancy way of saying types can be complicated:

```
// Accepts an object that implements all three of A, B, and D, 
// OR an int, 
// OR null.
(A&B&D)|int|null
```

However, it is somewhat tiresome to have to repeat typing (and reading) all of the elements of a type in every location where it was used.

It would be nice to be able to define a type once and then re-use it elsewhere. For example, being able to define a number:

```

type number = int | float;

// this function accepts either int or float
function add(number $x1, number $x2): number {}
```


### The full power of types 

Although the number example above is useful, it is somewhat simple and may not give a compelling case.

A more advanced example 

```php

type foo_result = [int $value, null $error] | [null $result, ValidationError $error];

function foo(): foo_result {...}

[$result, $error] = foo();

if ($error) {
    // 
}
```


## Hurdles to overcome


### Implementation needed

That's the main hurdle I can think of. It seems like a straightforward reasonable idea.

### People will want typed arrays

e.g. 

```
type foo = array(0 => int, 1 => string)


function bar(foo $foo) {}

foo([4, "hello"]);

```

Which might be more problematic as PHP doesn't currently support typed arrays.


## Forecast

Pretty sure it would be accepted overwhelmingly. 

Unless there was something very horrible about the implementation it would seem to be something that most people who use types would understand and appreciate.

## Notes

An example use-case would be 







