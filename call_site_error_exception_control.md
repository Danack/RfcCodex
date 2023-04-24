# Call side choice of return error or exception

## General idea

Error handling is one of the gnarliest problems in programming. 

Some people take the position that exceptions should never be used (e.g. Golang) and instead errors should always be passed back as return values.

Other people take the position that exceptions are fine (e.g. most sane programming langauges) and where used appropriately (i.e. not for normal control flow) exception provide a lot of value to a programming langauge.

Instead of continuing the debate of errors vs exceptions, why don't we just allow users to control whether they want to handle errors themselves, or if they want an exception to be thrown? 

```php
function foo($input, out ValidationException $exceptionOutParameter): ?int {

    $validationProblems = validateInput($input);
    
    // No problems, process data
    if (count($validationProblems) === 0) {
       return bar($input);
    }
    
    $exception = new ValidationException($validationProblems);
    
    // Check if out parameter was used
    if (is_void($exceptionOutParameter) === true) {
        //it was not passed in, so throw exception
        throw $exception; 
    }

    // out parameter was used, so don't throw exception
    // as calling user wants to handle the error with 
    // normal code flow.
    $exceptionOutParameter = $error;
}  
```

Calling that code with an explicit out parameter passed in does not result in an exception:

```php
$value = foo('someinvaliddata', $validationError);
```

Calling that code without an explicit out parameter passed in, results in an exception :

```php
$value = foo('someinvaliddata');
```


## Hurdles to overcome

### Out parameter support needed 
This idea depends on having 'out parameters' similar to [C#'s implementation](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/out-parameter-modifier).

### Reasoning is slightly annoying

For the above example, it would not be trivial to reason that either foo return a useful value, or returns an error in the out parameter, but not both.

If we had named types, this would be much easier to reason about:

```php
type foo_result = [int $value, null $error] | [null $result | ValidationError $error];

function foo($input): foo_result {
   //
}
```

Psalm, PHPStan and other static analyzers can inspect this code and see that value is not checked for being null:
```
$fooResult = foo('bar');

bar($fooResult->value);
```


And Psalm, PHPStan and other static analyzers would be able to reason about this code and see that it is more correct:
```
$fooResult = foo('bar');

if ($fooResult->error) {
    // there was an error, do something different.
}
else {
    bar($fooResult->value);
}
```

## Forecast

Depends on out parameters, and maybe isn't the best option.

## Notes



