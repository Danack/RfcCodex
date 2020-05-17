# Better web sapi 

## General idea

Although it functions, the FPM sapi is not fantastic, and has a couple of major limitations, that make using PHP much more difficult than it needs to be.


## Details 

### Per project ini files and extensions

Even with containers being a thing, the way that PHP requires management of ini files in a system directory makes PHP harder to use than other languages.

One of the main problems with the Pickle idea was that currently PHP requires libraries to be installed into system directories, which means that www-data user cannot install them.

A new web sapi that prefers to (or maybe only) loads ini files and extensions from the project directory it is in, would be easier to manage.

### Process management cleanup

Allegedly some of the code inside the FPM sapi that manages processes is written with some unsafe assumptions in it, which can lead to race-conditions.

https://bugs.php.net/bug.php?id=65398

### ini file code cleanup

The code for handling ini files inside the FPM sapi is definitely not good. That should probably be re-written from scratch. 

### function and behaviour cleanup

There are a reasonable number of things that were done in PHP which were good at the time, but are less good now

#### Remove request super-globals

The $GLOBALS variable that holds global variables is fine and does an appropriate job for allowing access to global variables.

The other ones are not fine:

* $_SERVER - replaced with functions to get the cgi headers.
* $_GET - removed and replaced by a userland function that parses query string params from the headers.
* $_POST - removed and replaced by a function getBody()
* $_FILES - removed and replaced by a function getFiles()
* $_COOKIE - removed. This can be done in userland.
* $_SESSION - removed. This can be done in userland.
* $_REQUEST - removed. Can be done in userland
* $_ENV - removed, probably. The interplay between env variables and their lack of thread safety should be thought about a bit more.

#### max_input_vars limit and detection

https://externals.io/message/110062

For those not familiar with this ini setting, it defines a maximum number of input vars in either $_GET, $_POST or $_COOKIE. Additional variables are discarded. This is a good idea to avoid attacks sending lots of data, but the program has no way of knowing it’s working with a truncated $_POST, $_GET or $_COOKIE.


```php
$max = ini_get("max_input_vars") - 1;
$check = count($_REQUEST);
if ($check > $max) {
     throw new RequestException("Request is too large, only {$max} input
variables are permitted");
}
```

#### urlencode vs rawurlencode

This might not be an issue given the refactoring of the magic globals.

https://www.gyrocode.com/articles/php-urlencode-vs-rawurlencode/


### Better pool management

Currently the pools can only be managed through config files. It would be quite convenient to be able to set things like pool sizes dynamically, either internally through PHP code, or externally through an API.

TODO - think through details.


### Better failing

There are a couple of places where PHP-FPM has bad behaviour around crashes. Although that might sound weird, it is better to have easy to figure out problems than to have hard to figure out problems, even if the problem is still there.

Currently in PHP-FPM, there are scenarios where an extension fails to be loaded correctly, which results in the pool not coming up correctly. This spams the error log with megabytes of data per minute, but otherwise provides no other info about what is happening.


## Hurdles to overcome

### Huge amount of work to be done 

This would be a big task to implement.

### Reticience to take on another sapi

There would naturally be some reluctance to bring another SAPI into core.

## Forecast

¯\\\_(ツ)\_/¯

Could possibly be done with Golang as the process manager. Though that would raise interesting questions about where opcache would live, and how code that is already in opcache would be passed to the spawned worker processes.

## Notes



