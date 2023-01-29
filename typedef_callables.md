# Typedef callable signatures

## General idea

Currently PHP has the callable type hint*. This allows you to indicate that a parameter, return value of a function or property of a class will be 'callable'. 

This only indicates that the value can be called either dynamically `$fn();` or through `call_user_function`.
However it does not provide any information about:

* What parameters should be used.

* What type will be returned from that function, if any.

The ability to declare function types would make using callables in PHP be way less dangerous.

The syntax could look something like:

```
// Define the function type
typedef Reducer = callable(int, int): int;

// Use the function type as a paramter type.
function process(array $items, Reducer $rd) {
   $sum = 0;
   foreach ($items as $item) {
       $sum = $rd($sum, $item);
   }
}
```

## Hurdles to overcome

## Implementation needed

Someone needs to sit down do the work of figuring how it should work, and also an implementation would be needed. In particular, co- and contra-variance might be 'non-trivial'.

Additionally, this may need to wait for improvements to the PHP autoloader, which currently only supports classes.

## Forecast

PHP 9

## Notes

A [previous RFC failed](https://wiki.php.net/rfc/functional-interfaces), due more to implementation details rather than the idea being rejected imo.

* Normally, I object to the word 'hint' as for most of the PHP type system, they are not hints but are checked properly at run-time. But callable can't be type-checked for the signature, and so

