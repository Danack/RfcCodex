# Better web SAPI 

## General idea

Although it functions, the FPM SAPI is not fantastic, and has a couple of major limitations, that make using PHP much more difficult than it needs to be.

## Details 

### Per project ini files and extensions

Even with containers being a thing, the way that PHP requires management of ini files in a system directory makes PHP harder to use than other languages.

One of the main problems with the Pickle idea was that currently PHP requires libraries to be installed into system directories, which means that www-data user cannot install them.

A new web SAPI that prefers to (or maybe only) loads ini files and extensions from the project directory it is in, would be easier to manage.

### Process management cleanup

Allegedly some of the code inside the FPM SAPI that manages processes is written with some unsafe assumptions in it, which can lead to race-conditions.

https://bugs.php.net/bug.php?id=65398

### ini file code cleanup

The code for handling ini files inside the FPM SAPI is definitely not good. That should probably be re-written from scratch. 

### function and behaviour cleanup

There are a reasonable number of things that were done in PHP which were good at the time, but are less good now.

Some of them could be cleaned up just for the sake of having the SAPI be simpler. Others should be cleaned up to remove hacks/magic that are contained within them.

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

### Request field mangling

For reasons, post fields are mangled in PHP.
 
```
"a.b" => $_REQUEST["a_b"]
"a b" => $_REQUEST["a_b"]
"a[b" => $_REQUEST["a_b"]
"a]b" => $_REQUEST["a]b"]
"a-b" => $_REQUEST["a-b"]
"a/b" => $_REQUEST["a/b"]
"a\b" => $_REQUEST["a\b"]
"a,b" => $_REQUEST["a,b"]
```

Let's not do that.

#### urlencode vs rawurlencode

This might not be an issue given the refactoring of the magic globals.

https://www.gyrocode.com/articles/php-urlencode-vs-rawurlencode/



#### Ini settings that can have error conditions

Currently all the error conditions for things like "post content-length exceeded", "file upload size exceeded", "max input time" have bad developer experience.

https://bugs.php.net/bug.php?id=54948
https://bugs.php.net/bug.php?id=41977
https://bugs.php.net/bug.php?id=63875

On of the bugs suggests doing something like:

```
get_startup_errors();
```
that returns something like this:  
```
[
    [
        'message' => 'Post content data limit exceeded'
        'errType' => STARTUP_ERR_PARTIAL_POST
    ],   
    [
        'message' => "Module 'ssh2' blah blah blah",
        'startupErrType' => STARTUP_ERR_SERVER
    ]
]
```

Also "post_max_size exceeded. post_max_size just clears all data when overflowing"


### Better pool management

Currently the pools can only be managed through config files. It would be quite convenient to be able to set things like pool sizes dynamically, either internally through PHP code, or externally through an API.

TODO - think through details.


### Better failing

There are a couple of places where PHP-FPM has bad behaviour around crashes. Although that might sound weird, it is better to have easy to figure out problems than to have hard to figure out problems, even if the problem is still there.

Currently in PHP-FPM, there are scenarios where an extension fails to be loaded correctly, which results in the pool not coming up correctly. This spams the error log with megabytes of data per minute, but otherwise provides no other info about what is happening.


### Don't tie to SPL.

It looks like SPL, Date, Session etc. are coupled with the Standard - I'd love to loose those dependencies and have a naked interpreter able to interpret the language and provide a replacement for Standard build around vendor SDK like for eg. the SDK for ESP microchips.


### Other ini settings

There are a reasonable number of ini settings that could be removed.

* user_dir
* variables_order
* request_order
* auto_append_file
* auto_prepend_file

There needs to be a reason to keep them, other than 'why not'.

### Windows + opcache + IIS oh my.

I don't really understand the issue here, but apparently IIS + opcache is very special.

> If you run FCGI with IIS, everything may work fine, until the temp folder gets purged. Afterwards FCGI appears to run fine, but it never can start new worker processes...
>
> There is a file with the base address of the mapping (and execute_ex). If that file is missing, OPcache bails out if it already has opened the existing file mapping. It might be possible to improve that by moving the info in that file into SHM, but that would require mapping at arbitrary address first, reading the info, closing, and then trying to map at the specified address.
>
> Also, execute_ex address doesn't catch different base addresses of extension DLLs.
>
> Possibly php-fpm could be made to work on windows with a thread instead of fork model...but that would be a lot of difficult work. 


## Hurdles to overcome

### Huge amount of work to be done 

This would be a big task to implement.

### Reticience to take on another SAPI

There would naturally be some reluctance to bring another SAPI into core.


# Why not copy Python’s WSGI

https://www.python.org/dev/peps/pep-3333/

aka do we want to redefine our own stuff yet again?


no proper dictionary of request headers, have to access through $_SERVER["HTTP_FOO_BAR"], or through getallheaders() which, unfortunately, 1) is not available in all SAPIs (IIRC), 2) in some SAPIs is a horrible hack which does not preserve the case of the headers. Likewise header() is nasty btw.




## Forecast

¯\\\_(ツ)\_/¯

Could possibly be done with Golang as the process manager. Although that would raise interesting questions about where opcache would live, and how code that is already in opcache would be passed to the spawned worker processes.

## Notes


Pools



