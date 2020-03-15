# Explicit defaults 

## General idea

PHP allows you to define a function that has a default value, and the default value is used when the parameter is not passed to the function.

```
<?php

function echo_repeat(string $string, int $count = 3) {
    for ($i = 0; $i < $count; $i += 1) {
        echo $string . " ";
    }
}

echo_repeat("cells interlinked within");

//output is 'cells interlinked within cells interlinked within cells interlinked within'
```

This works fine by itself. 

But PHP only allows you to use defaults for trailing arguments. It is not possible to skip over an optional parameter if you want to set a later parameter.


```
<?php
  
function echo_repeat_with_glue(string $string, int $count = 3, string $append) {
    for ($i = 0; $i < $count; $i += 1) {
        echo $string . $append;
    }
}

echo_repeat("cells interlinked within", 3, "\n");
```

In this example, when reading the code, it is not possible to tell if the calling code:

* explicitly wanted to pass $count = 3
* wanted to use the default value which happens 3.

Having a way of explicitly saying 'use the default' makes that choice explicit, through something like:

```
echo_repeat("cells interlinked within", default, "\n");
```

This provides benefits for code maintenance.

The code example here is trivial, but for more advanced use-cases where the default value defined changes in one version of the library to another, having the calling code automatically use the new default value would be easier than having to go through every place where that function is called, and figure out if the code should be using the old or new code.  


## Hurdles to overcome


### People prefer the idea of having 'named params' in the language. 

A lot of the discussion was around how the problem could be better solved if [named params](https://github.com/Danack/RfcCodex/blob/master/named_params.md) were added to PHP. 

### People see default params as indicating a bad api design

Functions with multiple default parameters are certainly a little bit icky.

```
CreateWindowEx($foo, default, default, $bar, 0, 0, 100, 100, default, default, default, default); 
```

One of the threads of the issue is that you can avoid needing to use defaults by creating an object to store the params, and passing that object instead. 


Though, this is another example of why having a 'lighter weight' way of defining and using types in PHP compared to full PHP classes might be useful. So see also [structs](https://github.com/Danack/RfcCodex/blob/master/structs.md).


(btw I personally don't think this is a great reason to reject the RFC. There will always be features that are safe to use in some ways, but can be (mis)used to write bad code.)


### Support for internal functions 

Was an issue, but this was covered by the RFC.

> Internal functions that declare parameters as optional but fail to provide proper defaults and rely on ZEND_NUM_ARGS to figure out if to use default or not may be broken. The patch fixes all instances of this in the core extensions, but third-party extensions may need to be fixed too. This applies only to ones that check ZEND_NUM_ARGS() manually in the code instead of using zend_parse_parameters().

Though similar work might need to be done for some extensions.

### Changing defaults

One of the arguments in support of this RFC, is not necessarily a great one.

Having the default value for a parameter change can be a pretty be BC break, and this idea changes that BC break from explicit to implicit. Although 'explicit defaults' would make some aspects of code maintenance easier, this increased chance of BC break is a trade-off.

## Forecast

Really hard to say. I think this is one of those things that people:

* Can see is problem.
* Don't particularly like the proposed solution.
* Don't think the problem is a serious enough one to add this solution to the language.

Any new attempt would probably need to persuade more people that this was a problem that needed to be solved, rather than dramatically improve the proposed solution.

Anyway, I thought the previous RFC was going to pass so what do I know?

# Notes

[Skipparams RFC](https://wiki.php.net/rfc/skipparams) 



