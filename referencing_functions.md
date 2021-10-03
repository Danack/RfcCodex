# Referencing functions 

## General idea


Not being able to reference functions by name directly, and instead have to use strings e.g.


```
$fn = 'strlen';
var_dump($fn('test')); 

// int(4)
```

is bad is not good, as typos can occur, and are hard for either humans or static analyzers to pickup on.

```
$fn = 'stlren';
$fn('test');
//  Call to undefined function stlren()
```


What's needed is some way to refer to a function that is unambiguously intended to be a reference to a function, or method of a class.

A new piece of syntax could allow this:

```
$fn = $(strlen);
var_dump($fn('test')); 
```

or maybe refactor how 


## Hurdles to overcome



### Explain the problem more clearly

Currently if you try to use a raw string, it is assumed to be a define:

```
$fn = strlen;
$fn('test');
```

We can't we change that to do the right thing?

### Figure out all of the requirements

Someone needs to figure out what the correct behaviour is around:

* non-existent functions. Does autoloading occur?
* referencing class methods e.g. and can you reference private methods?

## Forecast

PHP 8.2

## Implemented!

First-class callable syntax [implemented in PHP 8.1](https://wiki.php.net/rfc/first_class_callable_syntax).

## Notes



