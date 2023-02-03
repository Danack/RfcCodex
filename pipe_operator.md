# Pipe operator 

## General idea

When you have code that is a lot of function calls in a row, the need to always name the return variable, and pass it onto the next function makes some people unhappy e.g. this:

```
$config = loadConfig();
$dic = buildDic($config);
$app = getApp($dic);
$router = getRouter($app);
$dispatcher = getDispatcher($router, $request);
$logic = dispatchBusinessLogic($dispatcher, $request, new Response());
$render = renderResponse($logic);
$psr7 = buildPsr7Response($render);
$response = emit($psr7);
```

With a pipe-operator in the language could be re-written as:

```
$response = loadConfig()
|> buildDic($$)
|> getApp($$)
|> getRouter($$)
|> getDispatcher($$, $request)
|> dispatchBusinessLogic($$, $request, new Response())
|> renderResponse($$)
|> buildPsr7Response($$)
|> emit($$);
```

## Hurdles to overcome

### PHP programmers are far too used to Object Orientated programming

Even just seeing a list of functions being called in a row without any `->`'s is going to make people feel odd, which isn't a good start for an RFC.

### RFC needs better examples

I don't think the examples used in the RFC were great. In particular, the names of the variables __really__ help a reader understand what the code is doing. An example where the numbers are more obviously super-fluous, would help people see why pipe operators are useful.

It's quite likely that maths based examples might be better, and maybe steal some from R.

## Forecast

Right now, it's hard to see an updated RFC passing, though it might do better than previously.

However after function auto-loading becomes a feature of the languge, and people start using 'just functions' more, a pipe-operator would probably have a higher chance of succeeding.

## Notes

Previous RFCs:

* https://wiki.php.net/rfc/pipe-operator - didn't go to vote.
* https://wiki.php.net/rfc/pipe-operator-v2 - rejected 11-17 against.