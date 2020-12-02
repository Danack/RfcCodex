# Throws declarations 

## General idea

Some languages, notably Java, support declaring which exceptions are thrown by functions. This could be implemented in PHP with something like:

```
function foo() throws SomeException {
   // ...
}
```

In Java, exceptions can be either ['checked' or 'unchecked'](https://www.baeldung.com/java-checked-unchecked-exceptions). 

If a piece of code calls a function that throws any checked exceptions, that code must either catch the exception or declare that it itself can throw that checked exception.

## Hurdles to overcome


### Bad fit for PHP

So it's useful in Java  because it can be used to error out in the compilation stage, and so programs can be forced to handle particular exceptions.

Without a clear compilation phase, it wouldn't be possible to do that in PHP, and instead you would only be able to check the program for correctness through a static analyzer. At which point the value for having it be part of the language/runtime is pretty low.

Someone would need to say a clear reason why this should be part of PHP and not done through psalm/phpstan annotations.

### Bad fit for PHP part 2

It is common for error handlers to convert warnings/errors to exceptions.

This means that it is hard to determine if a function could throw an exception inside it, which means that a lot of the alleged value that comes from how this is used in Java could not be achieved in PHP.

### Java experience was painful  

It's hard to say exactly why, but a significant number of people who experienced checked exceptions in Java did not experience one little bit.

Any proposal for this would first have to understand in depth why this feature was so painful to use, and then figure out a way to make it less painful for PHP.

## Forecast

Unlikely. 

I am personally of the firm opinion that exceptions are useful, particularly for large, layered applications, no matter what the Golang people say.

But they are more useful as things for you can optionally handle. Being forced to handle them makes the api harder to use.

If an exception is very likely to happen, and so _does_ need to be handled most of the time in the layer of code immediately above the one when it occurs, then it sounds like it shouldn't be an exception, but an error code instead.

## Notes

Swift has an interesting [take on this](https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html), but also doesn't seem a good fit for PHP.


> I assume the callback must marked as throwing if it intends to throw, and the caller must also be marked if it wants to throw. But the thing is that Swift makes it easy to translate between different modes: if the callback throws, the caller could choose to panic if that happens, or it could return an optional, or handle the error. likewise the callback could not throw, but the caller could translate it returning an optional into throwing an error.
  
> Swift doesn't support callbacks as strings, they have dedicated function types for that. Closures that throw must also be marked with throws.
 
 ```
struct ExampleError: Error {}

func foo(callback: () throws -> ()) throws {
    try callback()
}

try foo {
    throw ExampleError()
}

```

You even need the try keyword on the function call that throws to make it more explicit that it can throw.
foo could of course also not throw and instead handle the error of callback directly.
