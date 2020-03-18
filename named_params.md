# Named params

## General idea

Named arguments are a way to pass arguments to a function, which makes use of the parameter names rather than the position of the parameters:

```
// Using positional arguments:
array_fill(0, 100, 42);


// Using named arguments:
array_fill(start_index => 0, num => 100, value => 42);
```

The order in which the named arguments are passed does not matter. The above example passes them in the same order as they are declared in the function signature, but any other order is possible too:

```
array_fill(value => 42, num => 100, start_index => 0);
```

It is possible to combine named arguments with normal, positional arguments and it is also possible to specify only some of the optional arguments of a function, irregardless of their order:

```
htmlspecialchars($string, double_encode => false);
// Same as
htmlspecialchars($string, ENT_COMPAT | ENT_HTML401, 'UTF-8', false);
```

## Hurdles to overcome


### Syntax 

There is still no consensus on the syntax.


### Inheritance and signature checking.

From the RFC: "Parameter names during inheritance will not be enforced by our LSP checks. It was decided that this would be too large of a BC break."


### Internal functions and extensions consistency

If all functions are going to be callable with both positional and named parameters, then the name of the parameter becomes part of the API for that code.

There would be some work to do for each extension to make sure that the args defined in the C code for the extension e.g.:

```
ZEND_BEGIN_ARG_INFO_EX(imagickpixel_sethsl_args, 0, 0, 3)
		ZEND_ARG_INFO(0, hue)
		ZEND_ARG_INFO(0, saturation)
		ZEND_ARG_INFO(0, luminosity)
	ZEND_END_ARG_INFO()
```

has appropriate spelling of parameter names, as changing the name will become a BC break once named params are added.  


## Forecast

This idea keeps coming up during discussions of other RFCs.

* [Default / skip params](https://wiki.php.net/rfc/skipparams) - a lot of the discussion was about how named parameters would be allow 'cleaner' code. 

* [Compact Object Property Assignment](https://wiki.php.net/rfc/compact-object-property-assignment) - this idea appears to be one special case of named params. 


## Notes

The dormant RFC: https://wiki.php.net/rfc/named_params

It's been wanted for a 'while' - [Posted 14 years ago](https://externals.io/message/16009#16019)

> As far as I remember this was brought to the list first by Thies and later by me, back in the days when PHP 5 was still on the design table.

