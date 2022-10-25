# RfcCodex

There are some notes on PHP RFCs, why some were declined, and what others might need for them to be implemented.

The purpose of these documents is to avoid information from being lost and to try to avoid conversations needing to be repeated multiple times on PHP internals.

## Things still being discussed 

[Array key casting](https://github.com/Danack/RfcCodex/blob/master/array_key_casting.md)

[Better web sapi](https://github.com/Danack/RfcCodex/blob/master/better_web_sapi.md)

[Call site error or exception control](https://github.com/Danack/RfcCodex/blob/master/call_site_error_exception_control.md)

[Class scoping improvements](https://github.com/Danack/RfcCodex/blob/master/class_scoping_improvements.md)

[Chained comparison operators](https://github.com/Danack/RfcCodex/blob/master/chained_comparison_operators.md)

[Generics](https://github.com/Danack/RfcCodex/blob/master/generics.md)

[Method overloading](https://github.com/Danack/RfcCodex/blob/master/method_overloading.md)

[Out parameters](https://github.com/Danack/RfcCodex/blob/master/out_parameters.md)

[Standardise core library](https://github.com/Danack/RfcCodex/blob/master/standardise_core_library.md)

[Strict mode and internal engine callbacks](https://github.com/Danack/RfcCodex/blob/master/engine_strict_mode_interaction.md)

[Strings/encoding is terrible](https://github.com/Danack/RfcCodex/blob/master/strings_and_encoding.md)

[Strong typing](https://github.com/Danack/RfcCodex/blob/master/strong_typing.md)

[Structs](https://github.com/Danack/RfcCodex/blob/master/structs.md)

[Template string literals](https://github.com/Danack/RfcCodex/blob/master/template_literals.md)

[Throws declarations](https://github.com/Danack/RfcCodex/blob/master/throws_declaration.md)

[Type aliasing](https://github.com/Danack/RfcCodex/blob/master/type_aliasing.md)

[Type callable signatures](https://github.com/Danack/RfcCodex/blob/master/typedef_callables.md)

## TODO

These need to be summarised.

Pipe-operator - https://wiki.php.net/rfc/pipe-operator

Tuple returns - though these would be moot if we had [out parameters](https://github.com/Danack/RfcCodex/blob/master/out_parameters.md).

Type declarations `type number = float | int;`

## Ideas that overcame their challenges

PHP is actually getting better. These are all things that used to be pipe-dreams, but are now in PHP core. 

[Annotations](https://github.com/Danack/RfcCodex/blob/master/annotations.md)

[Briefer closure syntax](https://github.com/Danack/RfcCodex/blob/master/briefer_closure_syntax.md)

[Co- and contra-variance](https://github.com/Danack/RfcCodex/blob/master/co_and_contra_variance.md)

[Enums](https://github.com/Danack/RfcCodex/blob/master/enums.md) implemented by [Enumerations](https://wiki.php.net/rfc/enumerations).

[Immutables](https://github.com/Danack/RfcCodex/blob/master/immutable.md) - this is done through the [Readonly properties](https://wiki.php.net/rfc/readonly_properties_v2). There is still some work to do here, as currently it is slightly annoying to clone an object and during the clone change some of it's properties.

[Named params](https://github.com/Danack/RfcCodex/blob/master/named_params.md)

Null short-circuiting - https://wiki.php.net/rfc/nullsafe_operator

[Referencing functions](https://github.com/Danack/RfcCodex/blob/master/referencing_functions.md) - implemented by [First-class callable syntax](https://wiki.php.net/rfc/first_class_callable_syntax)

[Ternary right associative](https://github.com/Danack/RfcCodex/blob/master/ternary_operator_right_associative.md)

[Union types](https://github.com/Danack/RfcCodex/blob/master/union_types.md)

## Things that are probably moot

PHP is actually getting better, but that means that some solutions to problems have become pretty moot, as they seek to solve problems that are now less of a problem.

[Consistent callables](https://github.com/Danack/RfcCodex/blob/master/consistent_callables.md)

[Explicit defaults](https://github.com/Danack/RfcCodex/blob/master/explicit_defaults.md)

# Misc notes

[SPL notes](https://github.com/Danack/RfcCodex/blob/master/spl_summary.md)

## Contributing

Please read the [contributing](https://github.com/Danack/RfcCodex/blob/master/CONTRIBUTING.md) guidelines before writing your 4,000 word novelella on why some RFC really should pass.

## Disclaimer

I reserve the right to be as opinionated as I feel like when commenting on RFCs; I'm not going to attempt to stay 100% neutral when talking about RFCs that I consider to be either dumb or bad for PHP.
