# Auto capture closure and/or multiline short closures

## General idea

PHP currently has two ways to write closures.

* Traditional anonymous functions which are quite verbose and require explicit use`ing of variables.
* Arrow functions which are short to write, have implicit use`ing of variables

## Hurdles to overcome

### Smoother RFC process 

A future RFC on the same topic needs to be introduced with less chaos. There were multiple pieces of confusion, including an RFC going to vote when it had severe technical problems identified, and the latest RFC also (imo) technical inaccuracies that prevented a smooth discussion.

Even just the title of "Short Closures 2.0" 

### Little gain

One of the arguments for the RFC is that 'fn' has fewer letters than 'function'.

For many people, this does not seem a convincing argument.

### Introducing a 3rd syntax for closures seems 'ungood'

PHP already has long form:

```
$message = 'Hello there %s!';
$fn = function ($name) use ($message) {
    return sprintf($message, $name);
};
```

And arrow functions:

```
$fn = fn($name) => sprintf($message, $name);
```

Adding a third separate syntax, seems bad.

Instead making multi-line blocks be 'a thing' would allow them to be used both here, and for use in `match`. 

### RFC felt incomplete part 1

The RFC only addressed auto-capturing for short closures, and did not address the older, long form closures. For myself at least, this made me feel that the RFC was incomplete, as if PHP is going to add auto-capturing of variables for things other than arrow functions, it should do so for both.

For the older anonymous functions, one proposal is to require doing `use(*)` to make it clear the anonymous function is capturing variables:

```
$message = 'Hello there %s!';

$fn = function ($name) use (*) {
    return sprintf($message, $name);
};

$fn('John');
```

### RFC felt incomplete part 2

The RFC did not say how variables could be use`d by reference with the fn() syntax. 

### People like the explicit scope in PHP

The RFC said "Most languages get along fine without that extra step". That is not the view of everyone. In particular scoping rules in JavaScript appear to be a shitshow.

## Forecast

Might be added when the RFC is drama free, and more complete. And gives a solution that can be used in multiline blocks.

## Notes

Previous RFC - https://wiki.php.net/rfc/auto-capture-closure

