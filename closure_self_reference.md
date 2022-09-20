# Closure self reference 


## General idea

Currently, the main way used to call a closure from within that closure, is to bind a variable by reference into the closure, when the closure is created.

However this can lead to shenanigans:

```
$fibonacci = function (int $n) use (&$fibonacci) {
    if ($n === 0) return 0;
    if ($n === 1) return 1;
    return $fibonacci($n-1) + $fibonacci($n-2);
};
```

```
echo $fibonacci(10). "\n";
$this_is_the_original_fibonacci = $fibonacci;
// ... many lines of code here
$fibonacci = function (int $n) { return rand(0, $n); };
// ... many lines of code here

echo $this_is_the_original_fibonacci(10). "\n";
```

i.e. a change to the variable outside the closure has modified the behaviour of the closure. That a closure can change behaviour like this violates the Principle of least astonishment


```
function (... $args) as $lambda: returnType use ($captures...) {}
function (... $args): returnType as $lambda use ($captures...) {}
function (... $args): returnType use ($captures...) as $lambda {}
```

## Hurdles to overcome

### Patch is required

Someone needs to write a patch for it and that involves touching the parser, which is an annoyingly tricky bit of internals.

### Avoiding return type clash

Currently PHP is limited to a single return type:

```
function foo(): int {}
```

At some point, PHP might be able to return tuples:

```
function foo(): [int, bool] {}
```

The syntax chosen for closure self-references musn't get in the way of that.

## Forecast

Apart from the inevitable bickering over syntax it should pass reasonably easily.

## Notes

Or just see https://wiki.php.net/rfc/closure_self_reference


