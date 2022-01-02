# Consistent callables

## Summary 

~~Make callables be less insane in PHP https://wiki.php.net/rfc/consistent_callables~~

Most of the behaviour has been cleaned up in the [Deprecate partially supported callables](https://wiki.php.net/rfc/deprecate_partially_supported_callables) RFC. However there is still some stuff left:

> if we want to make callables a proper type we need to forbid specifying
> non-public methods through them, and require those to use
> Callable::fromCallable() / first class callable syntax instead

## Forecast

While the work to implement the RFC in PHP core will be pretty straight-foward there is a non-trivial chance that some of the changes needed in the SPL might be very tricky to do in ways that are full backwards compatible.

The problem is that doing the work to cleanup the bad parts of callable just doesn't provide enough value to be worth doing.

It would provide a lot more value to introduce the ability to [define callable signatures](https://github.com/Danack/RfcCodex/blob/master/typedef_callables.md), and then figure out what to do about the existing code after that.

