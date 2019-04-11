# Standardise core library functions

## General idea

PHP is not as consistent as other languages are. Two areas in particular make people quite sad.

### Standard library function naming

Some functions have underscores....other do not.

```
 str_ireplace
 str_pad
 str_repeat
 str_replace
 str_shuffle
 str_split
 str_word_count
 strcasecmp
 strchr
 strcmp
 strcoll
 strcspn
```

Some functions use abbreviations...others do not.

```
function usleep(int $micro_seconds) : void; 
function microtime([bool $get_as_float]): mixed;
```

This is not a complete list of the diversification in naming. 


### Standard library parameter order

'Haystack -> needle' vs 'needle -> haystack'. 

```
function strpos(string $haystack, mixed $needle [, int $offset = 0]): int;

function stristr(string $haystack, mixed $needle [, bool $before_needle = false ] ): string;

function in_array(mixed $needle, array $haystack [, bool $strict] ):bool;

function array_search(mixed $needle, array $haystack [, bool $strict]): mixed;

```

## Hurdles to overcome

### Not all of the inconsistencies are inconsistencies   

> It should also be noted that many of the function names that people
> don't think are consistent are actually quite consistent when you
> consider that PHP is just a thin wrapper on top of underlying libraries.
> Functions from libc like tempnam() and strlen() are perfectly fine. The
> fact that you can go to your Linux command line and type: "man tempnam"
> to get a good idea of what is happening behind the scenes of the PHP
> function of the same name is a good thing.


### No path to a solution 

Even for people who think addressing this problem is important, there is no clear plan (that would be acceptable) to get to a solution. Every proposal so far has some major downsides.


#### Break a large amount of existing code

Renaming the functions or re-ordering parameters would break all code until it was migrated.

That is quite a problem.

#### Duplicate/alias a large number of functions 

At least for renaming functions, some proposals have suggested having both the old current names, and the new names in PHP for a while, so that people using PHP can migrate all of their code from the old version names, to the new version names inside a single version of PHP. 

This has a downside in that internals people don't appear to be too enthusiastic about having a large number of function aliases around for any amount of time.


## Forecast

Not likely to ever happen without someone coming up with a cunning plan.

The consensus seems to be that the barrier to making these changes is too high make the change worth doing.

It's much more likely that an alternative approach, such as improving PHP with [scalar objects](https://github.com/nikic/scalar_objects) would take the language to a place where most of the major 'inconsistencies' could be removed. 

## Notes

I personally think that one reason why some people think this is a big deal while other people don't consider it a big problem depends on how often people use PHP.

For people who use frequently use PHP, this problem seems small as those people develop a good set of 'muscle memory' around the function names/parameter order, or use an IDE dedicated to PHP.  


For people who only infrequently use PHP, and use other more standardised programming languages most of the time, having to lookup the correct function name or parameter order in the manual would be quite annoying. 


### Links

https://wiki.php.net/rfc/consistent_function_names

http://phpsadness.com/sad/9