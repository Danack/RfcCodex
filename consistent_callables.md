# Consistent callables

## Summary 

Make callables be less insane in PHP https://wiki.php.net/rfc/consistent_callables


## Forecast

While the work to implement the RFC in PHP core will be pretty straight-foward there is a non-trivial chance that some of the changes needed in the SPL might be very tricky to do in ways that are full backwards compatible.

The problem is that doing the work to cleanup the bad parts of callable just doesn't provide enough value to be worth doing.

It would provide a lot more value to introduce the ability to [define callable signatures](https://github.com/Danack/RfcCodex/blob/master/typedef_callables.md), and then figure out what to do about the existing code after that.

