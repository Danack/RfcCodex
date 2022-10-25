# Multiple return type aka tuples

## General idea

Since the dawn of time, PHP has returning single variables from functions. e.g. strpos

```
$result = strpos($haystack, $needle);

if ($result === false) {
  // failed to find needle
}
else {
  // Found result and $result contains an integer
}
```

This is sub-optimal for a few reasons:

* The possible return types need to be encoded separately from the normal return type info. e.g. docblocks for userland code, or stub files for internals.
* The return types are not checked at run-time.
* The return types are not inspectable by reflection.


Other languages, notably Go, use multiple return values (aka tuples) to return multiple independent values from a function.

This is possible in PHP, so we could make our own version of strpos that did return multiple values:

```
function strpos_multiple_return(string $haystack, string $needle)
{
  $result = strpos($haystack, $needle);
  if ($result === false) {
    return [false, null];
  }
  else {
    return [true, $result];
  }
}
```

The problem is we can't currently write the return type for those functions as anything other than array in PHP. It's 
possible to write the return type as a dockblock:

```
/**
 * @param string $haystack
 * @param string $needle
 *
 * @psalm-return array{0: false, 1: null}|array{0: true, 1: int} 
 */
function strpos_multiple_return(string $haystack, string $needle): array
{
    $result = strpos($haystack, $needle);
    if ($result === false) {
        return [false, null];
    }
    else {
        return [true, $result];
    }
}
```

It might be nicer to be able to write it as a mutliple return type without the docblock




```
function strpos_multiple_return(string $haystack, string $needle): array{0: false, 1: null}|array{0: true, 1: int}
{
    $result = strpos($haystack, $needle);
    if ($result === false) {
        return [false, null];
    }
    else {
        return [true, $result];
    }
}
```

or with type-aliases:


```
type strpos_not_found_result = array{0: false, 1: null};
type strpos_found_result = array{0: true, 1: int};

function strpos_multiple_return(string $haystack, string $needle): strpos_not_found_result|strpos_found_result
{
    $result = strpos($haystack, $needle);
    if ($result === false) {
        return [false, null];
    }
    else {
        return [true, $result];
    }
}
```

## Hurdles to overcome

### Needs an implementation

### Syntax is kind of hinkey


## Forecast

I honestly don't know. 

Many developers are getting very used to using PHPStan/Psalm and other static code analysis tools. Moving more of the type information 
from docblock to actual type information seems a good idea, but the verbosity of the information seems off-putting.

## Notes

It is not a good idea to try to change the current standard library.

I'll say that again so everyone can hear it: IT IS NOT A GOOD IDEA TO TRY TO CHANGE THE CURRENT STANDARD LIBRARY.

Instead this is a capability that should be added to PHP, then let people evolve to a new standard library 
over time. Trying to change the current uses of the the standard library would be such a huge BC break
it would probably kill PHP as a language.
