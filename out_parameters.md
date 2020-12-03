# Out parameters 

## General idea

Any function that needs to return multiple values is currently a little bit hard to use.

Although it's possible to define functions that returns a 'tuple', enforcing type correctness and even just having your IDE understand what the code is doing is harder e.g. 

```php
<?php

function calculateDimensions($inputValue) {
    // do some maths.
    return [$width, $height];
}


[$width, $height] = calculateDimensions($inputValue);

```

Although that works, you have to go off and read the comment for the function to see what it is returning, and that it actually matches what you are expecting.


It would be possible to add multiple return types to PHP, but they would be quite hard to read and reason about. For example, if we allowed two ints to be returned:

```
function calculateDimensions($inputValue): [int, int] {
    // do some maths.
    return [$width, $height];
}

```

You still need to look inside the documentation for the function, to see that the parameters are 'width' and 'height' in that order, rather than 'height', 'width'.


Instead of using multiple return values, 'out parameters' would allow to programmers to write functions that return multiple values, in a way that is easier to reason about:

```php
<?php

function calculateDimensions(int $inputValue, out int $width, out int $height) {
    // do some maths.
    
    $width = 5;
    $height = 10;
}

calculateDimensions($inputValue, $width, $height);

// If code reaches here, then width and height are set and guaranteed to be ints.

```

Wikipedia [definition](https://en.wikipedia.org/wiki/Parameter_(computer_programming)#Output_parameters):

"An output parameter, also known as an out parameter or return parameter, is a parameter used for output, rather than the more usual use for input." 

## Hurdles to overcome

Someone needs to sit down and do the work to think through how it should work, and think through what is an appropriate syntax.

### Syntax 

Random list of possibilities:

* `in`/`out` keywords
* Copying the TypeScript idea of having a separator in the parameter list
* In place of the return type.

I have no idea which would be better.

### Type juggling

Probably some horrible edge-cases around type juggling and calling weak mode code from strict, string from weak, and internals calling a callable that was defined in a strict file. 

### Compatibility with named params

## Forecast

Quite likely to happen one day. Mostly needs someone to spend the time on it.

## Notes

This is a precusor idea to having better error handling in PHP.