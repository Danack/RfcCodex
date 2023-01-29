# Class method callable

## General idea

Since the [First-class callable syntax](https://wiki.php.net/rfc/first_class_callable_syntax) was passed, it has been able to create a closure directly from any function, static class method, or instance class method when also provided an instance.

This is useful as:

* It allows you to avoid 'string based programming'.
* Creating the closure will error if you have a typo in your code. This means that typo errors will happen in the bootstrap part of your application, rather than in the middle of your app. That makes them easier to handle.

However it is not currently possible to create a closure to a class instance method, without also providing an instance.


## Hurdles to overcome


### Distaste

```
class Foo {
    function bar(string $name): string {
        echo "Hello $name";
    } 
}

$fn = Foo::bar(...);


$fn = fn (Foo $foo, string $name): string => $foo->bar($name);

$fn("John");
```

## Forecast

It's one of the missing pieces in the language.

## Notes



