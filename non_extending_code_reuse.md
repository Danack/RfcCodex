# Non-extending class re-use 

## General idea

Re-using code through extending classes is not enough.

There are different models of reusing code that would be really useful, that aren't currently possible in PHP.

## Enums

Imagine you have some enum:

```php
enum ErrorCode {
    case SOMETHING_BROKE;
}
```

And you want to re-use that case in another enum. That isn't currently possible due to enums being final for good reasons - see below.

You can imagine some sort of syntax like:

```php
enum MoreErrorCode {
    
    use ErrorCode;

    case PEBKAC;
}
```

So the set of cases for both `ErrorCode` and `MoreErrorCode` would be a finite set aka sealed. 


## Class Composition

```php
class A {}
    function foo();
}

class B delegate A {
    function __construct(private A $a) {}
}

$b = new B();
$b->foo();
```

without having to wire up a pass through function:

```php
class B {
    function __construct(private A $a) {}

    function foo() {
        $this->a->foo();
    }
}
```


## Hurdles to overcome

### Someone needs to think about this hard

Although some scope of the problem to be solved is known, the exact scope of the problem this general idea could address isn't known.

## Forecast

Far too hard to predict.

## Notes

### Why enums aren't extendable

Classes have contracts on their methods:

```
class A {}
class B {}

function foo(A $a) {}

function bar(B $b) {
    foo($b);
    
}
```

This is safe, as B follows the contract of A, and through the magic of co/contra-variance, any expectation you may have of the methods will be preserved, exceptions excepted.

Enums have contracts on their cases, not methods:

```php
enum ErrorCode {
    case SOMETHING_BROKE;
}

function quux(ErrorCode $errorCode)
{
    // When written, this code appears to cover all cases
    match ($errorCode) {
        ErrorCode::SOMETHING_BROKE => true,
    }
}
```

The match statement in the function quux can be static analyzed to cover all of the cases in ErrorCode.

But imagine it was allowed to extend enums:

```php
// Thought experiment code where enums are not final.
// This won't actually work in PHP. 
enum MoreErrorCode extends ErrorCode {
    case PEBKAC;
}

function fot(MoreErrorCode $errorCode) {
    quux($errorCode);
}

fot(MoreErrorCode::PEBKAC);
```

Under normal inheritance rules, a class that extends another will pass the type check.

The problem would be that the switch statement in `quux()` no longer covers all the cases. Because it doesn't know about MoreErrorCode::PEBKAC the match will throw an exception.

Because of this enums are final and can't be extended.