


# Null type 

## General idea

PHP doesn't currently support a stand alone null type, despite that being the default type that all functions that lack an explicit return statement have.

## Hurdles to overcome


### People

PHP programmers don't understand type systems. People have been using void and a lot of them will think that null is a duplicate type

## Forecast

Implemented [in PHP 8.2](https://wiki.php.net/rfc/null-false-standalone-types) along with false as a type.

## Notes

It wasn't included in the [union types](https://wiki.php.net/rfc/union_types_v2) RFC because:

> Allowing it as a standalone type would make both function foo(): void and function foo(): null legal function signatures, with similar but not identical semantics. This would negatively impact teachability for an unclear benefit.