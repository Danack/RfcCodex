# Method overloading

## General idea

Other languages allow multiple versions of the same method with the same name but with different parameter types.

The exact method dispatched is chosen when the program runs depending on the parameter types passed in.

```php
class Foo {

    function sum(int $a, int $b): int
    {
        echo "int version was called\n";
        return $a + $b;
    }
    
    function sum(float $a, float $b): float
    {
        echo "float version was called\n";
        return $a + $b;
    }
}

$foo = new Foo();
$foo->sum(1, 2); // echos 'int version was called' 
$foo->sum(1.1, 2.2); // echos 'float version was called'

```



## Hurdles to overcome


### PHP type juggling

The main problem is that unlike other more statically typed languages, PHP does a lot of type-juggling at run-time. This means that the exact behaviour is hard to define. For example:

Which function would `$foo->sum(17.4, 42)` call? 

Other languages that have method overloading (e.g. Java) tend not to have type-juggling so they avoid quite a few problems with dynamic types.

Also other languages that have method overloading (e.g. Java again) compile all the code in a program before running it. PHP doesn't and so has to make some decisions at run-time, which makes the behaviour of method overloading harder to define.

Any RFC would need to address all of the different type conversion edge-cases that could occur


### Performance hit

When the idea for method overloading was raised before some responses were concerned that it would have a performance impact on all applications.

This is due to needing to add extra information about what types a method will accept, even if the class itself doesn't use method overloading, as the child classes could implement another method with the same name.

```php
class Foo {
    function sum(int $a, int $b): int
    {
        echo "int version was called\n";
        return $a + $b;
    }
}

class FooBar extends Foo {
    function sum(float $a, float $b): float
    {
        echo "float version was called\n";
        return $a + $b;
    }
}

$foobar = new FooBar();
$foobar->sum($x1, $x2);
```

The exact behaviour of that code for different types of $x1 and $x2 are also unclear. 

### People have strong feelings for method overloading


Although some people like method overloading, my impression is that most people who have experienced method overloading / dynamic dispatch have come to hate it. 

### Lacking a strong reason

A really strong argument for why method overloading is a good thing needs to be made as well, particularly as
the equivalent behaviour can be done in userland.

None of the RFCs seem to have made a really clear case of why method overloading _needs_ to be included, rather than just be a 'nice to have'.


## Forecast

Not likely to ever happen.


## Notes

### Alternative solution to the same problem 

One suggested used for method overloading was for a use-case along these lines:

```php
class Foo {
    public function get($name, string $default) : string;
    public function get($name, int $default) : int;
    public function get($name, Bar $default) : Bar;
}
```

where the difference between the methods is that the return type is the same type as the `$default` parameter.

This could be solved with some solution that touched generics and union types.

```php
class Foo {
    public function get<T : int|string|Bar>($name, T $default) : T;
}
```


### Userland implementation

Method overloading is trivially implementable in userland.

```php
/**
 * @method sum(int $a, int $b): int;
 * @method sum(float $b, float $b): float;
 */
class Foo
{
    public function __call($name, $arguments)
    {
        if ($name === 'sum' && is_int($arguments[0]) && is_int($arguments[1])) {
            return $this->sumInts($arguments[0], $arguments[1]);
        }
        if ($name === 'sum' && is_float($arguments[0]) &&
is_float($arguments[1])) {
            return $this->sumFloats($arguments[0], $arguments[1]);
        }
        throw new \InvalidArgumentException("Don't know how to call this");
    }

    private function sumInts(int $a, int $b): int
    {
        // echo "sumInts was called.\n";
        return $a + $b;
    }

    private function sumFloats(float $a, float $b): float
    {
        // echo "sumFloats was called.\n";
        return $a + $b;
    }
}

```
