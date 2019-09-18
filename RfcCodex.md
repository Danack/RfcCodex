# RfcCodex

There are some notes on PHP RFCs, why some were declined, and what others might need for them to be implemented.

The purpose of these documents is to avoid information from being lost and to try to avoid conversations needing to be repeated multiple times on PHP internals.

## Things still being discussed 

[Annotations](https://github.com/Danack/RfcCodex/blob/master/annotations.md)

[Class scoping improvements](https://github.com/Danack/RfcCodex/blob/master/class_scoping_improvements.md)

[Consistent callables](https://github.com/Danack/RfcCodex/blob/master/consistent_callables.md)

[Enums](https://github.com/Danack/RfcCodex/blob/master/enums.md)

[Generics](https://github.com/Danack/RfcCodex/blob/master/generics.md)

[Method overloading](https://github.com/Danack/RfcCodex/blob/master/method_overloading.md)

[Standardise core library](https://github.com/Danack/RfcCodex/blob/master/standardise_core_library.md)

[Ternary right associative](https://github.com/Danack/RfcCodex/blob/master/ternary_operator_right_associative.md)

[Union types](https://github.com/Danack/RfcCodex/blob/master/union_types.md)

## TODO

Async

Structs

Explicit defaults

Tuple returns

Null short-circuiting - https://wiki.php.net/rfc/nullsafe_calls

Type declarations `type number = float | int;`

Strong typing 

```
class RetryLimit extends int {

}


function foo(RetryLimit $rl) {
    
    for ($i = 0; $i < $rl ; $i += 1) {
        if(bar()) {
            break;        
        }
    } 
}


```


# Ideas that overcame their challenges

[Co- and contra-variance](https://github.com/Danack/RfcCodex/blob/master/co_and_contra_variance.md)

[Briefer closure syntax](https://github.com/Danack/RfcCodex/blob/master/briefer_closure_syntax.md)


## Contributing

Please read the [contributing](https://github.com/Danack/RfcCodex/blob/master/CONTRIBUTING.md) guidelines before writing your 4,000 word novelella on why some RFC really should pass.

## Disclaimer

I reserve the right to be as opinionated as I feel like when commenting on RFCs; I'm not going to attempt to stay 100% neutral when talking about RFCs that I consider to be either dumb or bad for PHP.
