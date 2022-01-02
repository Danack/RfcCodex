# Array key casting

## General idea

When using arrays, PHP automatically casts numeric-string keys to int if the string is exactly the same as an integer. For example:

```
<?php

$values = [
    '01' => '01',
    '10' => '10',
    '10 ' => '10 ',
];

foreach ($values as $key => $value) {
    echo "key type is: " . gettype($key) . ", key value is [$key] \n";
}
```

The output of that code is:
```
key type is: string, key value is [01]
key type is: integer, key value is [10]
key type is: string, key value is [10 ]
```

i.e. the key '10' has been converted from a string to an int.


This has some implications:

* array_flip(array_flip($a)) !== $a

* array_search('10', $a) is an int when array_search('01', $a) is still a string. Someone using strict types and passing the result to a function expecting a string could end with an unexpected crash.

* general astonishment that this occurs, which leads to people thinking PHP is crap.

## Hurdles to overcome


### BC compatibility

Changing this behaviour would a large and very subtle BC break. If it was to be 'just changed' there would need to be a version that gives a deprecation warning when it occurs.

Alternatively some other mechanism to allow people to opt into a different behaviour for arrays would need to occur.

### Internal engine has a default mode

One of the suggestions to fix this, is to introduce [declare(strict_arrays = 1);](https://news-web.php.net/php.internals/116756).

That might have similar problems to how the engine is [in weak mode by default](https://github.com/Danack/RfcCodex/blob/master/engine_strict_mode_interaction.md), where the behaviour of code in callbacks changes depending on whether the code was called by the engine internally, or from a PHP file that has `declare(strict_arrays = 1);`.

## Forecast

This is certainly a problem that should be solved at some point.

My suspicion is that refactoring arrays completely in a larger piece of work might be more productive. Rather than just poking a single part of arrays, figuring out what to do about ArrayAccess at the same time, might produce a

## Notes



