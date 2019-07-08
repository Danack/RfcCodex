# Generics

## General idea

Sometimes you want a single class to only accept or return a certain type, but you want various flavours of that class to handle different types.

For example, imagine we want one stack class that stores and returns ints, and another stack that stores and returns objects of type Foo. We could define these classes like:


```php
class IntStack
{
    /** int[] */
    private $items = [];

    function pushItem(int $item) {
        $this->items[] = $item
    }
  
    function getItem(): ?int {
  
        if (count($this->items) === 0) {
            return null;
        }

        $return = $this->items[0];
        $this->items = array_slice($this->items, 1);
         
        return $return;
    } 
}


class FooStack
{
    /** Foo[] */
    private $items = [];

    function pushItem(Foo $item) {
        $this->items[] = $item
    }
  
    function getItem(): ?Foo {
  
        if (count($this->items) === 0) {
            return null;
        }

        $return = $this->items[0];
        $this->items = array_slice($this->items, 1);
         
        return $return;
    } 
}
```

However, this has a downside of having absolutely duplicated code for each of those classes, where the only difference between them is the type declarations.

The idea of generics is to be able to write the class with a 'generic' type and when the class is instantiating, to specify the type at run-time. For example:


```php
class GenericStack<T>
{
    /** T[] */
    private $items = [];

    function pushItem(T $item) {
        $this->items[] = $item
    }
  
    function getItem(): ?T {
        if (count($this->items) === 0) {
            return null;
        }

        $return = $this->items[0];
        $this->items = array_slice($this->items, 1);
         
        return $return;
    } 
}


// Create a stack that accepts ints
$intStack = new GenericStack<int>();

// Create a stack that accepts objects of type Foo.
$fooStack = new GenericStack<Foo>();

$intStack->pushItem(2); // fine
$fooStack->pushItem(new Foo()); // fine

$fooStack->pushItem(2); // Type-error, method expects int
```

## Hurdles to overcome


### Implementation

There is surprisingly little disagreement about the need for generics. The problem is that implementing them in PHP is quite hard.

I don't fully understand the details so can't comment insightfully on them, but my basic understanding is that because PHP doesn't store intermediate represenations of code, there isn't anything to 'hook into' to provide


### Syntax details 

As usual there are some syntax details that people could disagree on. In my opinion, if someone does the work to make an implementation of generics, then they should probably feel free to chose any syntax they feel like, without having to listen to other people.

## Forecast

Likely to happen when one day, when one of the core developers gets bored enough.

## Notes

If people are really desperate for generics, then they should look at using [https://preprocess.io/](https://preprocess.io/) to start using generics through that, rather than waiting for them in PHP.


### Usage as a solution to overloading methods.

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

Or possibly, 

```php
type T = int|string|Bar;

class Foo {
    public function get($name, T $default) : T;
}
```

But this would need to be able to define that the return T has to be of the same type as the parameter T.

