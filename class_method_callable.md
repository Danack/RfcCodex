# Class method callable

## General idea

Since the [First-class callable syntax](https://wiki.php.net/rfc/first_class_callable_syntax) was passed, it has been able to create a closure directly from any function, static class method, or instance class method when also provided an instance.

This is useful as:

* It allows you to avoid 'string based programming'.
* Creating the closure will error if you have a typo in your code. This means that typo errors will happen in the bootstrap part of your application, rather than in the middle of your app. That makes them easier to handle.

However it is not currently possible to create a closure to a class instance method, without also providing an instance.


## Hurdles to overcome


### Distaste

It would be possible to 'just' allow the same syntax for static methods as instance methods, except the callable generated would have a parameter typed to the object type at the start, and the dispatch to the method happens internally:

```
class Foo {
    function bar(string $name): string {
        echo "Hello $name";
    } 
}

$fn = Foo::bar(...);

// $fn is equivalent to:
$fn = fn (Foo $foo, string $name): string => $foo->bar($name);

```

This seems to meet all of the required goals, except that it is novel and not immediately aesthetically pleasing.

## Forecast

It's one of the tiny but important missing pieces in the language. Particularly for things like routers, you want to be able to specify instance methods of a class as a thing, without having to resort to string based programming.

## Notes

Java uses the same syntax as I'm currently suggesting.

Hard to read documentation [here](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html).

Easier to read [blog post](https://www.baeldung.com/java-method-references).


Given this code:
```java
class Integer {
    ...
    public int compareTo(Integer anotherInteger) {...}
}

List<Integer> numbers = Arrays.asList(5, 3, 50, 24, 40, 2, 9, 18);

```
Then you can use a "Reference to an instance method of an arbitrary object of a particular type" 
```java
numbers.stream()
.sorted(Integer::compareTo);
```

Is equivalent to creating a lambda:

```java
numbers.stream()
  .sorted((a, b) -> a.compareTo(b));
```

i.e. the instance needs to be the first parameter.
