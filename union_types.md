# Union types

Implemented in PHP 8.0

## General idea

The function strpos approximately has the following signature:

```
strpos(string $haystack, string $needle [, int $offset = 0 ] ) : mixed
```

The result of the function will be either an int or false if the needle wasn't found in the haystack string.

Because we can't currently express 'int or false' in the PHP type system, we use the type 'mixed' in the documentation, and [possibly soon in the code](https://wiki.php.net/rfc/mixed-typehint).

The idea of union types is to allow people to express types as unions of other types. In the case for strpos the return value will either be int or false, which could be represented by int|bool, or more closely by int|false, if true and false are allowed as 'types'.

So strpos would now have the signature:

```
strpos(string $haystack, string $needle [, int $offset = 0 ] ) : int|false
```

This means that static analysis tools like PHPStan or Psalm can much more easily understand what the code says it's going to be doing, and the PHP engine enforces that the code will behave as it is documented, or otherwise generate an error.

## Hurdles to overcome

### Inertia

Scalar types were only 'recently' introduced to PHP, and it takes time for people to get used to using more types. It's entirely possible that some people think that there has been too much change too rapidly, and that any further changes to PHP's type system should wait a bit.


### Lack of exposure to type systems

A significant number of programmers in the PHP community haven't been exposed that much to an effective type system. 

Although C, C++, Java and now PHP have type systems, they aren't particularly great type systems. 

Until people have experienced projects where the majority of the code is fully typed, and can be fully analysed by a static analysis tool it can be hard to see the benefit.


## Forecast

Likely to happen....but a lot later than a large chunk of the community would like.

This is one of the few RFCs that would benefit from a 'write in' campaign or some letter to internals 


## Notes

https://wiki.php.net/rfc/union_types


Union types in Flow:

https://flow.org/en/docs/types/unions/


Which also has intersection types:

https://flow.org/en/docs/types/intersections/
